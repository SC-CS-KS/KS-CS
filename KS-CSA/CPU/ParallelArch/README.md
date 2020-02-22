# 并行计算机体系结构

* [Parallel Computer System Architecture](parallel-arch.md)
> * [MPP](MPP.md)

* [Parallel Computing](parallel-computing.md)

## 并行计算机的访存模型
* UMA(uniform memory access) 均匀存储访问模型
* NUMA（nonuniform memory access）非均匀存储模型
* COMA(Cache-Only memory access)  全高速缓存存储模型
* CC-NUMA(coherent-cache nonuniform menory access) 高速缓存一致性非均匀存储访问
* NORMA(No-Remote Memory Access) 非远程存储模型

## 并行算法
### 并行算法设计策略
```md
串行算法直接并行化
从问题描述开始设计并行算法
借用已有算法求解新问题
```
## 并行程序
### 体系结构
```md
共享内存（PVP、SMP、DSM）
数据并行（SIMD）
消息传递（MPP、Clusters）
```
### 编程模型
```md
隐式并行、数据并行、共享并行、消息并行

编程模型渐渐汇聚于三类标准模型：
数据并行（如HPF）、消息传递（如MPI和PVM）和 共享变量（如OpenMP）
```
### 编程语言
```md
KAP、Fortran90、HPF、X3H5、OpenMP、PVM、MPI
```
### 并行程序设计方法


## 参考
* [并行计算](http://www.voidcn.com/article/p-zqnakxlm-sg.html)

