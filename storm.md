## 基础概念
### 拓扑(topologies)
计算任务
### 流(stream)
由元组(tuple)构成，需要一个id
### 数据源(spouts)
数据来源

* 可靠，处理失败时重新发送
* 不可靠  

#### 方法
1. nextTuple，发送新元组，或者在没有可发送元组时直接返回
2. ack 元组被成功处理后的进一步处理
3. fail 元组被失败处理后的进一步处理

### 数据流处理组件(bolts)
1. filtering
2. functions
3. aggregations
4. jions
5. 数据库交互

#### 方法
* 订阅数据流
* execute

### 数据流分组(stream groupings)
#### 分组方式
1. 随机分组：元组随机分到bolts中
2. 域分组：根据定义的域分组
3. 部分关键字分组：
4. 完全分组：
5. 全局分组：
6. 非分组：
7. 直接分组：
8. 本地随机分组

### 可靠性(reliability)
* emit
* ack

### 任务(task)
每个spout和bolt都由若干task执行
### 工作进程(workers)
* 拓扑在一个或者多个工作进程(worker processes)中运行
* 每个工作进程都是一个实际的jvm

### 集群结构
1. nimbus
2. supervisor

## 使用流程
1. 安装部署

* 本地模式：开发测试
* 集群模式：生产模式

### 配置
1. 配置文件storm.yaml

#### 配置项 
1. zookeeper
```
storm.zookeeper.servers:
 - "172.26.130.39"
```

2.   storm.local.dir
3.   nimbus.host
```
nimbus.host:
 "172.26.130.39"
```

4.   supervisor.slots.ports
5.   ui.host
6.   ui.port
7.  命令

*  storm nimbus
*  storm supervisor
*  storm ui 

### 编写代码
2. 编写代码
3. 提交到storm

