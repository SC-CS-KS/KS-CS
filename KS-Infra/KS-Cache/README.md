# 缓存
```md
将数据写入速度更快的存储设备中，或者读出。
将数据缓存到里应用最近的位置。
将数据缓存到离用户最近的位置。
```

## [What Is?](WhatIs.md)

## Design

* [缓存更新](design/Update.md)

* [缓存失效（Evict Policy）](design/EvictPolicy.md)

* [Multi-Level Cache](Multi-Level/README.md)
* 内存数据网格(In Memory Data Grid，IMDG)

## Utility
* CDN 缓存
* 反向代理缓存
* 本地应用缓存(Local Cache)
* 分布式缓存 Distributed Cache （Remote Cache）

## Implement
* [Local Cache](local-cache/README.md)
* [Distributed Cache （Remote Cache）](ds-cache/README.md)
* 弹性缓存平台
* 弹性应用平台 - 代表了云环境下分布式缓存系统未来的发展方向

### 缓存组件
* Ehcache
* JetCache - 由阿里巴巴开源的 通用缓存访问框架

## [Cache HA](HA/README.md)

## Develop
* 迁移
```md
		平滑迁移
			第1步，双写
			第2步，迁移历史数据
			第3步，切读
			第4步，下线双写
		停机迁移
			停止应用
			迁移历史数据
			更改应用的数据源
			启动应用
		一致性哈希
			Redis的客户端Jedis本身实现了基于一致性哈希的客户端路由框架
				这种框架的好处是便于动态扩容
```
