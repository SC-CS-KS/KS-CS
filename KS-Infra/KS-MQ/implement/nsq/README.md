# [NSQ - A realtime distributed messaging platform](https://github.com/nsqio/nsq)

```md
基于Go语言的分布式实时消息平台

* 设计目标
在分布式环境下运行的去中心化服务提供一个强大的基础架构。
```
## Features
* Distributed
```md
NSQ具有分布式、去中心化的拓扑结构。
具有无单点故障、故障容错、高可用性以及能够保证消息的可靠传递的特征。
```
* Scalable易于扩展
```md
NSQ支持水平扩展，没有中心化的brokers。
内置的发现服务简化了在集群中增加节点。
同时支持pub-sub和load-balanced 的消息分发。
```
* Ops Friendly
```md
NSQ非常容易配置和部署，生来就绑定了一个管理界面。
二进制包没有运行时依赖。官方有Docker image。
```
*  Integrated 高度集成
```md
官方的 Go 和 Python库都有提供。而且为大多数语言提供了库。
```
## 组件
* Topic
* Channels
* Messages
* nsqd
* nsqlookupd
* nsqadmin

## 扩展
* [youzan/nsq](https://github.com/youzan/nsq)

## 参考
* [消息中间件NSQ深入与实践](https://mp.weixin.qq.com/s/lrbIx88Z1HwWNTO_5aABJQ)
* [MQ](http://bridgeforyou.cn/2018/10/02/Nsq-1-From-Queue-To-MQ/)

