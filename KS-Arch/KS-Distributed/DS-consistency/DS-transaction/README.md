# 分布式事务

* [Distributed Transaction](distributed-transaction.md)

## 实现形态
* 基于消息实现的分布式事务
  > * [基于可靠消息的分布式事务实现如何保证高可用](https://juejin.im/post/5bf2c6b6e51d456693549af4)
* 基于补偿实现的分布式事务
* 基于TCC实现的分布式事务
* 基于SAGA实现的分布式事务
* 基于2PC实现的分布式事务

> [《各种形态的分布式事务》](https://www.cnblogs.com/skyesx/p/9697817.html)

## 以「CAP」为基础的强一致性解决方案 -（Distributed Transaction Service）
```md
都会引入一个类似“协调器”的东西来作为全局事务的掌控者。
```
### 协议
* [2PC Two Phase Commit(](2PC.md)
* [3PC](3PC.md)
* [TCC](TCC.md)

### 问题
* [幂等性问题]()

### 框架
#### TCC 框架
* [tcc-transaction](https://github.com/changmingxie/tcc-transaction)
* [Hmily](https://github.com/yu199195/hmily)
* [ByteTCC](https://github.com/liuyangming/ByteTCC)
* [EasyTransaction](https://github.com/QNJR-GROUP/EasyTransaction)

> [《TCC 实现框架的压力测试记录》](https://blog.csdn.net/yongyou890410/article/details/82719062)

#### 2PC 框架
* [Raincat](https://github.com/yu199195/Raincat)

## 以「BASE」理论为基础最终一致性解决方案
### 协议
* 异步消息——本地消息表
* 异步消息——不支持事务的MQ
* 异步消息——支持事务的MQ
> * RocketMQ

* [Saga 模式 - 可以看做一个异步的、利用队列实现的补偿事务]()
* [Gossip 协议 - 是一个具体的、运用BASE理论实现的协议]()

### 框架
* [Lottor - 基于可靠消息的柔性分布式事务实现方案](https://github.com/keets2012/Lottor)

### 其他
* [事务补偿机制]()

