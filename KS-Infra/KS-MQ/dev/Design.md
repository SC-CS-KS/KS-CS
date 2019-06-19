# MQ 设计开发

## 需要解决的问题
* 如何让一个topic的消息，能够被多个消费者实例消费？
* 如何让MQ、生产者、消费者能够自动发现对方？
* 如何实现集群？

## 模型 设计
* 消息投递策略
```md
* 消息投递语义(Message Delivery Semantics)
最多一次(At most once)
至少一次(At least once)
准确一次(Exactly once)
```

* 消息时序性
* 消息幂等性
* push or pull
```md
* push
优点：延时小，几乎可以做到实时
缺点：消费者端不好做流控 很难做批量推送，不知道要推送多少合适
解决思路: nsq的流控策略
* pull
优点：消费者可以自己把握节奏
缺点：
  延时大
  消费者可能经常有空pull，即pull不到消息，造成浪费
解决思路：Kafka采用的是阻塞式pull
```
> 参考 [Kafka: Push vs Pull](https://kafka.apache.org/documentation/#design_pull)
* 流量控制
* 失败重试

## 协议

## 高可用 设计
* 可扩展
* 多租户
* 持久化

## API 设计
