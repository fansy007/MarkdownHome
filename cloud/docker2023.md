#cloud [[docker & k8s]]
# 家组网方式
主wifi Lan 192.168.31.1
DHCP 设 110-254
副wifi bedroom wan 192.168.31.101
副wifi qjgeng wan 192.168.31.103

---
三网桥接
虚拟机分配
桥接模式 mac_centeros manual set:
192.168.31.88

---
# reboost
```sh
systemctl restart networkManager #centeros8
shutdown -r now

```
# Install redis
prepare a folder
```sh
/home/hg26502/redis
/home/hg26502/redis/data
```

add config file

```sh
vi redis.conf
appendonly yes


docker run -v /home/hg26502/redis/redis.conf:/etc/redis/redis.conf \
-v /home/hg26502/redis/data:/data \
-d --name redis --restart always \
-p 6379:6379 \
redis:latest redis-server /etc/redis/redis.conf
```



# Install by docker compose

要启动这些服务，你需要在包含 `docker-compose.yml` 文件的目录下运行 `docker-compose up` 命令

```sh
docker compose -f docker-compose.yml up -d
```

建立/prod目录， vi 以下两个yml

docker-compose.yml

```yml
version: '3.9'

services:
  redis:
    image: redis:latest
    container_name: redis
    restart: always
    ports:
      - "6379:6379"
    networks:
      - backend

  zookeeper:
    image: bitnami/zookeeper:latest
    container_name: zookeeper
    restart: always
    environment:
      ZOOKEEPER_CLIENT_PORT: 2181
      ZOOKEEPER_TICK_TIME: 2000
      ALLOW_ANONYMOUS_LOGIN: yes
    networks:
      - backend

  kafka:
    image: bitnami/kafka:3.4.0
    container_name: kafka
    restart: always
    depends_on:
      - zookeeper
    ports:
      - "9092:9092"
    environment:
      ALLOW_PLAINTEXT_LISTENER: yes
      KAFKA_CFG_ZOOKEEPER_CONNECT: zookeeper:2181
      KAFKA_OFFSETS_TOPIC_REPLICATION_FACTOR: 1
    networks:
      - backend
  
  kafka-ui:
    image: provectuslabs/kafka-ui:latest
    container_name:  kafka-ui
    restart: always
    depends_on:
      - kafka
    ports:
      - "8080:8080"
    environment:
      KAFKA_CLUSTERS_0_NAME: dev
      KAFKA_CLUSTERS_0_BOOTSTRAPSERVERS: kafka:9092
    networks:
      - backend

  prometheus:
    image: prom/prometheus:latest
    container_name: prometheus
    restart: always
    volumes:
      - ./prometheus.yml:/etc/prometheus/prometheus.yml
    ports:
      - "9090:9090"
    networks:
      - backend

  grafana:
    image: grafana/grafana:latest
    container_name: grafana
    restart: always
    depends_on:
      - prometheus
    ports:
      - "3000:3000"
    networks:
      - backend

networks:
  backend:
    name: backend
```



prometheus.yml

```sh
global:
  scrape_interval: 15s
  evaluation_interval: 15s

scrape_configs:
  - job_name: 'prometheus'
    static_configs:
      - targets: ['localhost:9090']

  - job_name: 'redis'
    static_configs:
      - targets: ['redis:6379']

  - job_name: 'kafka'
    static_configs:
      - targets: ['kafka:9092']
```


# pull image and use proxy
set proxy
![[Pasted image 20240801195402.png|825]]
```sh
{
  "builder": {
    "gc": {
      "defaultKeepStorage": "20GB",
      "enabled": true
    }
  },
  "experimental": false,
  "registry-mirrors": [
    "https://01uinh3k.mirror.aliyuncs.com"
  ]
}
```


```sh
docker pull nicolaka/netshoot
```

# running net shoot 
```sh
docker run --rm nicolaka/netshoot ping -c 4 www.baidu.com
docker run --rm -it nicolaka/netshoot bash. (ctrl+D退出)
```

# install minikube
set mirrow first
```sh
/etc/docker/daemon.json

  "registry-mirrors": [
    "https://01uinh3k.mirror.aliyuncs.com"
  ]
```

安装
```sh
brew install minikube
minikube start （minikube delete， minikube stop）
```

使用
```sh
kubectl apply -f test.yaml (kubectl delete -f test.yaml) 
```


# Kubectl 实际操作

```sh
k exec -it my-nginx-fc567748-vnw6b --/bin/sh
k get svc
k get deployment
k get pods
k logs XXXX
k describle pod XXXX 
```

deployment
```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: my-nginx
spec:
  selector:
    matchLabels:
      app: my-web
      tier: front-end
  replicas: 3
  strategy:
      # indicate which strategy we want for rolling update
      type: RollingUpdate
      rollingUpdate:
        maxSurge: 1
        maxUnavailable: 0
  template:
    metadata:
      labels:
        app: my-web
        tier: front-end
        svc: my-svc
    spec:
      containers:
      - name: my-nginx
        image: nginx:1.20-alpine-perl
        ports:
        - containerPort: 80

```

service
```yaml
apiVersion: v1
kind: Service
metadata:
  name: my-svc  # Service 的名称
spec:
  selector:
    app: my-web       # 选择有这个标签的 Pods
    tier: front-end   # 选择有这个标签的 Pods
  ports:
  - port: 80
    targetPort: 80
  type: NodePort
```
等价于 k expose my-nginx --port=80 --type=NodePort

查看
```sh
(base) hg26502@192 deploy-service % minikube service my-svc
|-----------|--------|-------------|---------------------------|
| NAMESPACE |  NAME  | TARGET PORT |            URL            |
|-----------|--------|-------------|---------------------------|
| default   | my-svc |          80 | http://192.168.49.2:32608 |
|-----------|--------|-------------|---------------------------|
🏃  为服务 my-svc 启动隧道。
|-----------|--------|-------------|------------------------|
| NAMESPACE |  NAME  | TARGET PORT |          URL           |
|-----------|--------|-------------|------------------------|
| default   | my-svc |             | http://127.0.0.1:62160 |
|-----------|--------|-------------|------------------------|
```