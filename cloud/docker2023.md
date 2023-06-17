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

