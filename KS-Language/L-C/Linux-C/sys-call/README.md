# 系统调用


## [What Is](WhatIs.md)

## Why
```md
1. 系统调用可以为用户空间提供访问硬件资源的统一接口，应用程序不必去关注具体的硬件访问操作。
2. 系统调用可以对系统进行保护，保证系统的稳定和安全。
    有了进入内核的统一访问路径限制才能保证内核的安全。
```

## [Linux系统调用列表](https://blog.csdn.net/wwwdc1012/article/details/78759326)

## Design
* 系统调用表
* 系统调用号
* 系统调用服务例程


## Utils
```md
# 查询系统调用
$ cat  /proc/kallsyms | grep getpid
```
* 如何使用系统调用


## Reference
* [Linux 内核系统调用和标准 C库函数的关系分析](https://blog.csdn.net/skyflying2012/article/details/10044343)
