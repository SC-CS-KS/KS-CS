# [gflags](https://github.com/gflags/gflags)
```md
Google 开源的处理命令行参数的库，使用C++开发，具备python接口，可以替代 getopt。
```

## Practice
* 1.首先要定义变量
```md
DEFINE_xxxxx(变量名，默认值，help-string)
参数依次是: 变量名， 默认值，说明

DEFINE_bool(test_bool, false, “tests bool-ness”);
```
* 2.访问变量
```md
FLAGS_test_bool = true;
```
* 3. 如何在命令行传入非默认值
```md
a. 首先在程序内解析命令行参数
google::ParseCommandLineFlags(&argc, &argv, false);

b.运行程序时要传入定义的参数
./ext –test_bool=true

```

