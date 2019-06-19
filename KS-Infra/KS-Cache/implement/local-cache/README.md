# 本地缓存

## 缓存介质
* 缓存在磁盘
```md
直接读取本机文件，减少了网络传输消耗，比通过网络读取数据库快速。
针对对缓存速度要求不高，但需要缓存大量数据的场景。
```
* 缓存在内存

## 缓存策略
* 本地缓存的重要等级
* 本地缓存的加载顺序
* 本地缓存更新频率和保护机制
* 本地缓存的失败重试策略
* 本地缓存启动时间
* 本地缓存增量更新

## 本地缓存标准
* [Jcache]()

## 实现
## 编程直接实现
```md
主要满足单机场景下的小数据量缓存需求，同时对数据的更新无需太铭感感知。
如 配置管理、基础静态数据等。
```
* 基于ConcurrentHashMap
```md
基于此实现的LocalCache在多线程并发环境的操作是安全的。
```
* 基于LinkedHashMap
```md
通过LinkedHashMap的按照访问顺序的特性来实现LRU策略。
LinkedHashMap并不是线程安全，所以在LRUMap中引入了ReentrantReadWriteLock读写锁，来控制并发问题。
```
### 开源实现
* [Caffeine Cache](https://github.com/ben-manes/caffeine)
* Guava Cache