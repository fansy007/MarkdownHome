# basic concept

| Key    |                            |
| ------ | -------------------------- |
| Cache  | Single instance in cluster |
| Region | HashMap                    |



# Quick start

```xml
<dependencies>
    <!-- Other dependencies -->
    
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-data-gemfire</artifactId>
    </dependency>
</dependencies>

```



```java
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.data.gemfire.GemfireTemplate;
import org.springframework.stereotype.Service;

@Service
public class ExampleService {

    private final GemfireTemplate gemfireTemplate;

    @Autowired
    public ExampleService(GemfireTemplate gemfireTemplate) {
        this.gemfireTemplate = gemfireTemplate;
    }

    public String readValueFromRegion() {
        ExampleEntity entity = gemfireTemplate.get("exampleKey", ExampleEntity.class);
        if (entity != null) {
            return entity.getValue();
        }
        return null;
    }
}

```



```java
import org.springframework.data.annotation.Id;
import org.springframework.data.gemfire.mapping.annotation.Region;

@Region("exampleRegion")
public class ExampleEntity {

    @Id
    private Long id;
    private String value;

    // getters and setters
}

```



```properties
# GemFire Locator 配置
spring.data.gemfire.pool.locators=localhost[10334]

# SSL 配置
spring.data.gemfire.ssl.key-store=/path/to/keystore.p12
spring.data.gemfire.ssl.key-store-password=yourKeystorePassword
spring.data.gemfire.ssl.trust-store=/path/to/truststore.p12
spring.data.gemfire.ssl.trust-store-password=yourTruststorePassword

```



```java
import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;
import org.springframework.context.annotation.Bean;
import org.springframework.data.gemfire.config.annotation.ClientCacheApplication;
import org.springframework.data.gemfire.config.annotation.EnableEntityDefinedRegions;
import org.springframework.data.gemfire.config.annotation.EnableGemFireProperties;
import org.springframework.data.gemfire.config.annotation.EnablePdx;

@SpringBootApplication
@ClientCacheApplication(locators = {
    @Locator(host = "boombox" port = 11235),
    @Locator(host = "skullbox", port = 12480)
})
@EnableEntityDefinedRegions(basePackageClasses = ExampleEntity.class)
@EnableGemFireProperties(useSsl = true)
@EnablePdx
public class GemFireClientApplication {

    public static void main(String[] args) {
        SpringApplication.run(GemFireClientApplication.class, args);
    }

    // Other beans and configurations can be added here
}

```

