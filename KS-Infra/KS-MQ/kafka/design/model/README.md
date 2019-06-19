# Kafka Model
* [Broker](Broker.md)
```md
Kafka 集群包含一个或多个服务器，这种服务器被称为 broker。
```
* [Topic](Topic.md)
```md
每条发布到 Kafka 集群的消息都有一个类别，这个类别被称为 Topic。
（物理上不同 Topic 的消息分开存储，逻辑上一个 Topic 的消息虽然保存于一个或多个 broker 上，
但用户只需指定消息的 Topic 即可生产或消费数据而不必关心数据存于何处）。
```
* Partition 
```md
物理上的概念，每个 Topic 包含一个或多个 Partition。
```
* [Producer](Producer.md)
```md
负责发布消息到 Kafka broker。
```
* [Consumer](Consumer.md)
```md
消息消费者，向 Kafka broker 读取消息的客户端。

可以认为一个group是一个“订阅者”，一个topic 中的每个 partitions 只会被一个“订阅者”中的一个consumer消费，
不过一个 consumer 可以消费多个partitions中的消息。

Kafka的设计原理决定，对于一个topic，同一个group不能多于 partition 个数的 consumer 同时消费，
否则将意味着某些consumer无法得到消息。
```
* Consumer Group
```md
每个 Consumer 属于一个特定的 Consumer Group
（可为每个 Consumer 指定 group name，若不指定 group name 则属于默认的 group）。
```
* [Message](Message.md)