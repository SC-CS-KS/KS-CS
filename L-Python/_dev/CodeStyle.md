# Code Style


## 变量
### 命名
```md
单下划线开头：弱内部使用标识，无法被from M import * 所引用
单下划线结尾：避免和 python 关键字冲突，可以加个后置下划线
双下划线开头：类成员变量中的私有变量
双下划线开头，双下划线结尾：magic对象或属性的名字，永远不要将这样的命名方式应用于自己的变量和函数
```

## Reference
* [PEP 8 -- Style Guide for Python Code](https://www.python.org/dev/peps/pep-0008/)