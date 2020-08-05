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
- [参考]( https://www.throwable.club/2019/05/18/spring-cloud-gateway-modify-request-response/)

#### 类型
1. pre：参数校验、权限校验、流量监控、日志输出、协议转换
2. post：响应内容、响应头的修改，日志的输出，流量监控
3. 单个路由: gateway 需要配置在具体路由下
4. 所有路由: global 不需要配置，作用在所有路由上
5. filter 如何处理request和response

#### filter处理exchange,request和response
1. ServerWebExchange：上下文。包含request和response，exchange.getRequest()获取request，这个rexchange不能修改，必须通过exchange.mutate().生产一个可变的exchange，将这个exchange设置新的数值，然后build(),既生成一个新的ServerWebExchange，通过chain.filter()传递

```
public Mono<Void> filter(ServerWebExchange exchange, GatewayFilterChain chain) {
        ServerHttpRequest request = exchange.getRequest();
        // 这里可以修改ServerHttpRequest实例
        ServerHttpRequest newRequest = ...
        ServerHttpResponse response = exchange.getResponse();
        // 这里可以修改ServerHttpResponse实例
        ServerHttpResponse newResponse = ...
        // 构建新的ServerWebExchange实例
        ServerWebExchange newExchange = exchange.mutate().request(newRequest).response(newResponse).build();
        return chain.filter(newExchange);
    }
```
2. 修改request, exchange.getRequest().mutate().header().build()
3.  修改respnose,
4. GatewayFilterChain

#### 重点使用
##### 负载均衡
路由器通过服务名进行查找转发，实现负载均衡，在uri中配置服务名；官方建议：
LoadBalancerClientFilter uses a blocking ribbon LoadBalancerClient under the hood. We suggest you use ReactiveLoadBalancerClientFilter instead. You can switch to it by setting the value of the spring.cloud.loadbalancer.ribbon.enabled to false.

```
routes:
    - id: core-account
      uri: lb://account
      order: 0
      predicates:
        - Host=core.xdf.cn
        - Path=/account/**
```

##### 限流
1. 配置
2. 令牌桶参数的计算

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

### 使用
#### 拦截

#### 修改request
exchange获取resqust，产生一个新的request，修改新的request（通过新的修饰器），然后chain.filter传递
#### 修改respone
exchange产生一个新的respone修改，chain.filter传递,通过定义新的修饰器修改内容

```
exchange.getResponse().writeWith(Flux.just(DataBufferFactory.warp(byte[])))
```