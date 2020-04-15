### nacos-config

#### 部署
1. pom
2. 
```
<dependency>
            <groupId>com.alibaba.cloud</groupId>
            <artifactId>spring-cloud-starter-alibaba-nacos-config</artifactId>
            <version>2.0.1.RELEASE</version>
</dependency>
如果使用springcloud的config-center需要去掉
<dependency>
         <groupId>org.springframework.cloud</groupId>
         <artifactId>spring-cloud-config-client</artifactId>
</dependency>
```

2. 配置 bootstrap

```
spring:
  application:
    name: account
  cloud:
    nacos:
      config:
        server-addr: 127.0.0.1:8848
        group: seal
        file-extension: yaml
```

3. nacos服务

- 启动nacos
- 配置；dataid需要application-{}.文件类型,注意需要有文件类型

4. 启动

-   
 
