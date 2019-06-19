# [Kafka APIs](https://kafka.apache.org/10/documentation.html#api)

* Producer API
* Consumer API 
* Streams API 
```md
允许应用程序充当流处理器，消耗来自一个或多个主题的输入流并产生到一个或多个输出主题的输出流，从而有效地将输入流转换为输出流。
```
* Connector API
```md
允许构建和运行将Kafka主题连接到现有应用程序或数据系统的可重用生产者或使用者。
例如，关系数据库的连接器可能捕获对表的每个更改。
```
* AdminClient API
```md
有些时候需要将某些管理查看的功能集成到系统（比如Kafka Manager）中，那么就需要调用一些 API来 直接操作Kafka。
```
