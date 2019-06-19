# [Kafka Manager](https://github.com/yahoo/kafka-manager)
```md
A tool for managing Apache Kafka.

可以很容易地发现分布在集群中的哪些topic分布不均匀，或者是分区在整个集群分布不均匀的的情况。
它支持管理多个集群、选择副本、副本重新分配以及创建Topic。
同时，这个管理工具也是一个非常好的可以快速浏览这个集群的工具。
```



# [Deploy](https://github.com/yahoo/kafka-manager#deployment)
```sh
./sbt clean dist
产生部署文件 target/universal/kafka-manager-2.0.0.2.zip
```
```sh 
nohup ./bin/kafka-manager &
```
