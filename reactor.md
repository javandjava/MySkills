### Reactor

#### 概念
1. 响应式，事件驱动
2.  数据流 Flux，Mono
3.  订阅 subscribe() 
4. Publisher，Subscriber，Subcription

#### 构成
1. Flux:0~n元素
2. Mono  0-1个元素


#### 使用
1. jdk8

```
<dependency>
        <groupId>io.projectreactor</groupId>
        <artifactId>reactor-core</artifactId>
        <version>3.1.4.RELEASE</version>
 </dependency>

```

#### Mono,Flux
1. 生成
2. 处理，fliter,map,flatMap,then,zip,reduce
3. 消费 subscribe


#### 参考文档
- [参考文档 1] (https://blog.csdn.net/get_set/article/details/79480172)
- [参考文档 2] (https://juejin.im/post/5b3a22a16fb9a024db5ff13e)
