# Utils

## 消费偏移量
* 查看有那些 group ID 正在进行消费
```sh
sh ./bin/kafka-consumer-groups.sh --new-consumer --bootstrap-server 127.0.0.1:9092 --list
```
* 查看指定group.id 的消费者消费情况 
```sh
$ sh bin/kafka-consumer-groups.sh --new-consumer --bootstrap-server 127.0.0.1:9092 --group console-consumer-56967 --describe
TOPIC                          PARTITION  CURRENT-OFFSET  LOG-END-OFFSET  LAG        CONSUMER-ID                                       HOST            CLIENT-ID
sunny_test                     0          8               8               0          consumer-1-342656ca-2d8b-43c9-acbf-001fd0ed821c   /127.0.0.1      consumer-1
```
## zookeeper 维护  消费偏移量的 情况
```sh
sh ./bin/kafka-consumer-groups.sh --zookeeper localhost:2181 --list
```
```sh
$ sh bin/kafka-consumer-groups.sh --zookeeper localhost:2181 --group console-consumer-45357 --describe
```