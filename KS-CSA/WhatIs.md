# Computer Architecture


## Flynn分类法
```md
1966年，Michael J.Flynn提出根据指令流、数据流的并行度对计算机系统进行分类。
```
* SISD 单指令流单数据流（Single Instruction Stream Single DataStream)
```md
传统的顺序执行的单处理器计算机。
指令部件每次只对一条指令进行译码，并只对一个操作部件分配数据。
```
* SIMD 单指令流多数据流（Single Instruction Stream Multiple Data Stream)
```md
以并行处理机为代表，并行处理机包括多个重复的处理单元PU1～PUn，
由单一指令部件控制，按照同一指令流的要求为它们分配各自所需的不同的数据。
```
* MISD 多指令流单数据流（Multiple Instruction Stream Single Data Stream)
```md
具有n个处理单元，按n条不同指令的要求对同一数据流及其中间结果进行不同的处理。
一个处理单元的输出又作为另一个处理单元的输入。
```
* MIMD 多指令流多数据流（Multiple Instruction Stream Multiple Data Stream)
```md
是指能实现作业、任务、指令等各级全面并行的多机系统，多处理机就属于MIMD。
```