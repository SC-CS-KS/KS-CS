# TCC (Try-Confirm-Cancel)

## 执行阶段
* Try
```md
Try 操作一般都是锁定资源，设置预备类的状态，冻结部分数据等等此类操作。
```
* Confirm
```md
如果 Try 操作都成功，则进入 Confirm 操作阶段，完成各个服务的所有业务逻辑的执行。
```
* Cancel
```md
如果 Try 操作存在失败的情况，则进入 Cancel 操作阶段，对整个TCC分布式事务进行回滚。
```

## 可用性
* 分布式事务日志

## 应用方法
* TCC分布式事务框架
* 原本的一个接口，要改造为3个逻辑，Try-Confirm-Cancel
```md
1. 服务调用链路依次执行Try逻辑
2. 如果都正常的话，TCC分布式事务框架推进执行Confirm逻辑，完成整个事务
3. 如果某个服务的Try逻辑有问题，TCC分布式事务框架感知到之后就会推进执行各个服务的Cancel逻辑
```

## 参考
* [TCC分布式事务的实现原理](https://www.codercto.com/a/39752.html)

