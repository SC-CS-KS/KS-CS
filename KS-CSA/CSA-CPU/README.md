# CPU
```md
独立的中央处理单元，体现在主板上是有多个CPU的槽位。
```
* CPU cores
```md
在每一个CPU上，都可能有多个核（core）
	每一个核中都有独立的一套ALU、FPU、Cache等组件
		所以这个概念也被称作物理核
算术逻辑运算单元ALU
	（Arithmetic and Logic Unit） 
		主要完成对二进制数据的定点算术运算（加减乘除）、逻辑运算（与或非异或）以及移位操作
	在某些CPU中还有专门用于处理移位操作的移位器
	整数单元有时也称为IEU（Integer Execution Unit）
	通常所说的“CPU是XX位的”就是指ALU所能处理的数据的位数
浮点运算单元FPU
	（Floating Point Unit） 
		主要负责浮点运算和高精度整数运算
		有些FPU还具有向量运算的功能，另外一些则有专门的向量处理单元。 
```
* processor
```md
得益于超线程技术
	让一个物理核模拟出多个逻辑核，即processor
简单来说就是
	当有多个计算任务时，可以让其中一个计算任务使用ALU的时候，另一个则去使用FPU。
	这样就可以充分利用物理核中的各个部件，使得同一个物理核中，也可以并行处理多个计算任务。  
```

## [并行计算机体系结构](ParallelArch/README.md)

## [CPU 缓存](Cache/README.md)

## [CPU 上下文 （Context）](Context.md)



