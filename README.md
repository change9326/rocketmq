# Apache RocketMQ 
## 1.NameServer
### 1.1 NameServer 架构设计
### 1.2 NameServer 启动流程分析
### 1.3 路由注册、故障剔除
#### 路由元数据
#### 路由注册
#### 路由删除
NameServer 集群中那个节点执行路由删除，还是NameServer 集群 中所有的节点都执行删除操作？

## 2.消息发送
RocketMQ 发送普通消息有三种实现方式：
- 可靠同步发送(sync):同步等待
- 可靠异步发送(async):异步、回调
- 单向发送(oneway):只管发送
### 重点
- RocketMQ消息结构
- 消息生产者启动流程
- 消息发送过程
- 批量消息发送
## 4.消息消费
## 4.1 消息消费的两种模式
### 1.推模式-MQPushConsumer
### 2.拉模式-MQPullConsumer
## 4.2 MQPushConsumer 核心属性&方法
## 4.3 消费者启动流程分析
## 4.4 消息消费过程



## Q
### 1.在集群消费模式下，我们的消息只能被消费一次，rocketmq是怎么实现的呢?

在默认情况下，rocketmq会为每个topic在Broker节点上分配若干个队列，默认的队列数量是4 （defaultTopicQueueNums: 4），
客户端使用长轮询发起请求，和服务端连接上，主动从broker上拉取消息，而`每个队列只能由一个消费者监听消费`，这样就做到了消息的实时性得到保障，同时保证了消息只有由一个消费者监听消费.
rocketmq可以横向扩展消费者数量来提高集群的消费能力，但由于一条队列只能由一个消费者监听消费，多余的消费者将不能消费，所以我们扩展消费者数量的时候，需要注意队列的数量是否大于消费者数量。
### 2.Rocket如何保证每个队列只能由一个消费者监听消费
### 3.NameServer 集群，节点间无通信，当集群中任意节点宕机，路由信息如何保证不丢失？
Broker 在启动的时候会向所有的NameServer注册，单个Broker节点与所有的NameServer节点保持长连接及心跳，
并会定时将Topic信息注册到NameServer
#### 3.1  NameServer宕机 Broker 如何感知
### 4. Topic创建流程

## 源码分析篇
- [深度解析RocketMQ Topic的创建机制](http://objcoding.com/2019/03/31/rocketmq-topic/)
