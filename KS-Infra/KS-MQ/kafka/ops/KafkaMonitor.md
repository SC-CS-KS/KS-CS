# [Kafka Monitor](https://github.com/linkedin/kafka-monitor)

![](../pic/Kafka-OP-Arch.jpeg)

```md
Kafka Monitor是一个在真实集群中实现和执行长期运行的 kafka 系统测试的框架。
它通过捕获仅在长时间或低概率后可能发生的潜在错误或回归来补充Kafka现有的系统测试。
此外，它允许您使用端到端管道监控Kafka集群，以获取许多派生的重要统计数据，
例如端到端延迟，服务可用性和消息丢失率。
(在生产的消息中包含了时间戳、序列号，Kafka Monitor可以依据这些数据对消息的延迟、丢失率和重复率进行统计。)
```

## Design
![](../pic/kafka-monitor.jpeg)

## Model
* Jetty Service：提供用于Web UI 展示的HTTP服务
* Jolokia Service：提供 JMX 的 HTTP 接口
* Produce Service: 生产者服务，汇报生产速率和生产可用性
* Consumer Service: 消费者服务，汇报消费速率和可用性、消息的延迟、丢失率和重复率
* Metrics Service：接受 Produce Service 和 Consumer Service汇报的监控指标

## Deploy
* build
```sh
git clone https://github.com/linkedin/kafka-monitor.git
cd kafka-monitor
./gradlew jar
```
* Config
```md
repo 中的默认 kafka-monitor.properties 提供了一个如何监视单个集群的简单示例。
需要更改 zookeeper.connect 和 bootstrap.servers 的值以指向您的群集。

完整的配置列表及其文档可以在Config类的代码中找到，用于各自的服务，例如：
ProduceServiceConfig.java 和 ConsumeServiceConfig.java。

可以在kafka-monitor.properties 中指定多个 SingleClusterMonitor，
以在一个Kafka Monitor 进程中监视多个 Kafka群集。

作为另一个高级用例，您可以将 ProduceService 和 ConsumeService 
指向两个由 MirrorMaker 连接的不同 Kafka 集群，以监控其端到端延迟。

默认情况下，Kafka Monitor会根据配置中指定的 topic-management.replicationFactor
和 topic-management.partitionsToBrokersRatio 自动创建监视器主题。
ReplicationFactor默认为1，您可能希望将其更改为与现有主题相同的复制因子。
您可以通过将produce.topic.topicCreationEnabled 设置为 false 来禁用自动主题创建。

Kafka Monitor可以自动增加监视器主题的分区数，以确保分区＃> = broker＃。
它还可以重新分配分区并触发首选领导者选举，以确保每个代理充当监视器主题的至少一个分区的领导者。
要使用此功能，请在属性文件中使用 EndToEndTest 或 TopicManagementService。
```
* start
```sh
./bin/kafka-monitor-start.sh config/kafka-monitor.properties
```


## Resources
* [LinkedIn 开源 Kafka Monitor](https://www.jianshu.com/p/d4cf65aecdce)