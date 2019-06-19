# MQ Theory

## MQ Model
* 点对点消息队列模型
> * 角色
```md
消息队列（Queue）
发送者(Sender)
接收者(Receiver)
```
* 发布订阅消息模型
> * 角色
```md
主题（Topic）
发布者（Publisher）
订阅者（Subscriber）
```
```md
生产者发送一条消息到队列queue，只有一个消费者能收到。
发布者发送到topic的消息，只有订阅了topic的订阅者才会收到消息。
```
## 消息的顺序性

## 消息的ACK机制

## 最终一致性的设计

## 消息的事务支持
