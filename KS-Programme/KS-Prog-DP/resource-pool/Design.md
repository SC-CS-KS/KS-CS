# Design

## 指标
```md
资源池模式有通用的几个指标，这也是资源池的通用设计模式。
```

* setMaxActive
```md
设置能被池（能检出给客户使用或者空闲等待检出）创建的对象的最大个数。
使用负值就是不限制。
```
* setMaxWait
```md
当池消耗殆尽且消耗的动作是 WHEN_EXHAUSTED_BLOCK。
borrowobject函数在抛出异常前被阻止，可以设置的最大等待时间，
如果小于0，borrowobject函数可能会无限期阻止。 
```
* setMaxIdle - 设置池中的空闲实例阀值
```md
如果在负载严重的系统上最大空闲设置的太小，你可能会看到对象刚被销毁立即就被创建，
这是由于活跃线程瞬间产生对象的速度远大于他们需要对象，会造成大量空闲对象远超最大空闲值。
对于负载严重的系统最佳值采用默认的开始值直到它发生变化。
```
* setMinIdle
```md
在线程产生新对象被释放之前设置池中允许的最小对象，
注意当numactive + numidle > = maxactive，将不会建立任何对象，
如果空闲对象释放被禁止设置是没有效果的。
```

```md
WHEN_EXHAUSTED_FAIL 到达pool的阀值，失败的处理
WHEN_EXHAUSTED_BLOCK 到达pool的阀值，阻止再次借用对象的处理 
WHEN_EXHAUSTED_GROW 到达pool的阀值，生成新的对象提供给外部调用者 
DEFAULT_LIFO 默认是对象后进先出，也可以改成是先进先出
```