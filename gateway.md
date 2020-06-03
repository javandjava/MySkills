## gateway

### 依赖
```
<dependency>
    <groupId>org.springframework.cloud</groupId>
    <artifactId>spring-cloud-starter-gateway</artifactId>
</dependency>
```

### 配置
```
spring:
  application:
    name: spring-cloud-gateway-sample
  cloud:
    gateway:
      routes:
        - id: blog
          uri: http://
          predicates:
            		# 匹配路径转发
            		- Path=/
         - id: combox
          	uri: 
          	predicates:
	            - Query=
	            - Query=
	            - Method=GET
	            - Cookie=
	            - Header=
	            - RemoteAddr=
```
- id：路由的ID
- uri：匹配路由的转发地址
- predicates：配置该路由的断言，通过PredicateDefinition类进行接收配置。

### filter
#### 类型
1. pre：参数校验、权限校验、流量监控、日志输出、协议转换
2. post：响应内容、响应头的修改，日志的输出，流量监控
3. 单个路由: gateway 需要配置在具体路由下
4. 所有路由: global 不需要配置，作用在所有路由上

#### 内置过滤器
##### 单路由过滤器
1. AddRequestHeader
2. AddRequestParameter
3. AddResponseHeader
4. Hystrix
5. PrefixPath
6. PreserveHostHeader
7. RequstRateLimiter
8. RedirectTo
9. RemoveNonProxyHeaders
10. RemoveRequestHeader
11. RemoveResponseHeader
12. RewritePath
13. SaveSession
14. SecureHeaders
15. SetPath
16. SetResponseHeader
17. SetStatus
18. StripPrefix
19. Retry
##### 全局过滤器
1. LoadBalancer：
2. HttpClient：
3. Websocket：
4. ForwardPath：解析路径并转发
5. RouteToRequestUrl:转换路由中的URI
6. WebClient：

#### 自定义过滤器
##### 单个路由
1. 实现GatewayFilter,Order 这2个接口
2. filter方法：

##### 全局路由
1. 实现GlobalFiiter,Order
2. 注入 

##### default过滤器
1. 必须继承GatewayFilter
2. 必须有GatewayFilterFactory

```
@Override
public GatewayFilter apply(Object config) {
    return new LoggerFilter();
}
```

3. 必须

```
@Bean
public LoggerGatewayFilterFactory loggerGatewayFilterFactory(){
    return new LoggerGatewayFilterFactory();
}
``` 

4. 配置

```
gateway:
      default-filters:
        - name: LoggerFilter
```

5. 注意
*  如果没有路由被选中，filter也不会起作用

#### 自定义过滤器工厂
1. GatewayFilterFactory 接口
2. 2个抽象类 AbstractGatewayFilterFactory

### route: RouteLocator

### predicate 路由转发断言
1. After
2. Before
3. Between
4. Cookie
5. Header
6. Host
7. Method
8. Path
9. Query
10. Readbody
11. RemoteAddr
12. Weight
13. CloudFoundry