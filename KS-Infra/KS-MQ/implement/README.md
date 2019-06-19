# MQ 实现

## 开源实现
* [Apache Kafka](../kafka/README.md)
* [Apache Pulsar] - 由Yahoo开发并开源的下一代发布订阅消息系统
* [Apache DistributedLog] - 被称为“共享日志基础设施”
* [Apache RocketMQ] - 阿里开源的消息中间件
```md
是由Java语言开发的，具备高吞吐量、高可用性、适合大规模分布式系统应用等特点，经历过双11的洗礼，实力不容小觑。
```
* [RabbitMQ] - 基采用 Erlang 语言实现的AMQP协议的消息中间件
```md
最初起源于金融系统，用于在分布式系统中存储转发消息。
RabbitMQ发展到今天，被越来越多的人认可，这和它在可靠性、可用性、扩展性、功能丰富等方面的卓越表现是分不开的。
```
* [ActiveMQ] - 介于 ZeroMQ 和 RabbitMQ 之间,被誉为消息中间件的“瑞士军刀”
```md
Apache出品的、采用 Java 语言编写的完全基于 JMS1.1规范的面向消息的中间件，
为应用程序提供高效的、可扩展的、稳定的和安全的企业级消息通信。
不过由于历史原因包袱太重，目前市场份额没有后面三种消息中间件多，
其最新架构被命名为Apollo，号称下一代ActiveMQ。
```
* [ZeroMQ] - 是一个异步消息库，在套接字的基础上提供了类似于消息代理的机制
```md
号称史上最快的消息队列，基于C语言开发。
是一个消息处理队列库，可在多线程、多内核和主机之间弹性伸缩，虽然大多数时候我们习惯将其归入消息队列家族之中，
但是其和前面的几款有着本质的区别，ZeroMQ本身就不是一个消息队列服务器，
更像是一组底层网络通讯库，对原有的Socket API上加上一层封装而已。
```
* [MetaQ](https://github.com/killme2008/Metamorphosis) - 淘宝开源的一个Java消息中间件，类似apache-kafka
* [NSQ - A realtime distributed messaging platform] - 基于Go语言
* [Apollo] - Apache 称 Apollo 为最快、最强健的STOMP服务器
* [nanomsg] - 构建在ZeroMQ的可靠性能之上，同时又提供了若干重要的改进

## [技术选型](choice.md)

## Compare
* [NSQ vs Kafka](http://bridgeforyou.cn/2018/10/02/Nsq-5-Nsq-vs-Kafka/)

* 协议
```md
RabbitMQ 支持 AMQP（二进制），STOMP（文本），MQTT（二进制），HTTP（里面包装其他协议）等协议。
Kafka 使用自定义协议。
```
* 性能
```md
RabbitMQ 在有大量消息堆积的情况下性能会下降，Kafka不会。
毕竟AMQP设计的初衷不是用来持久化海量消息的，而Kafka一开始是用来处理海量日志的。
```
* 总体
```md
ZeroMQ小而美，RabbitMQ大而稳，Kakfa和RocketMQ快而强劲。
```