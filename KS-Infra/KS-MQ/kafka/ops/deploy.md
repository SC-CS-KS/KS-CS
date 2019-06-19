# Kafka 部署

## 单节点单Broker部署
```sh
$ wget wget https://archive.apache.org/dist/kafka/1.0.0/kafka_2.12-1.0.0.tgz
```
### 配置
* config/server.properties
```md
# broker的全局唯一编号，不能重复
broker.id=0
# 监听
listeners=PLAINTEXT://:9092
# 日志目录
log.dirs=/home/kafka/logs
# 配置zookeeper的连接（如果不是本机，需要该为ip或主机名）
zookeeper.connect=localhost:2181
```
### 管理
* 启动 内置 zookeeper
```sh
$ nohup sh  bin/zookeeper-server-start.sh config/zookeeper.properties &
```
> [ZK可以单独部署]((https://github.com/SunnnyChan/sc.drill-code/blob/master/infra/apache-zookeeper/dev/Deploy.md))
* 启动 kafka
```sh
$ nohup bin/kafka-server-start.sh config/server.properties &
```
```sh
$ cat nohup.out 
打印：
[2019-04-26 09:35:16,628] INFO [KafkaServer id=0] started (kafka.server.KafkaServer)
```
* 创建 topic
```sh
$ bin/kafka-topics.sh --create --zookeeper localhost:2181 --replication-factor 1 --partitions 1 --topic sunny_test
$ bin/kafka-topics.sh --list --zookeeper localhost:2181
```
```sh
sh bin/zkCli.sh
ls  /consumers/console-consumer-45357/offsets/sunny_test
```
### test
* 发送消息
```sh
$ bin/kafka-console-producer.sh --broker-list localhost:9092 --topic sunny_test
This is a message
This is another message
```
* 消费消息
```sh
$ bin/kafka-console-consumer.sh --bootstrap-server localhost:9092 --topic sunny_test --from-beginning
This is a message
This is another message
```
* * –from-beginning参数
```md
如果有表示从最开始消费数据，旧的和新的数据都会被消费，而没有该参数表示只会消费新产生的数据
```

## 单节点多Broker部署 

## 集群搭建(多节点多Broker)

## Reference
* [Kafka 安装部署及使用(单节点/集群)](https://blog.csdn.net/hg_harvey/article/details/79174104)