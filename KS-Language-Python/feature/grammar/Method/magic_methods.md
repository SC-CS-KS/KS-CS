# Magic Methods
* 什么是魔术方法?
```md
他们是面向对象的Python的一切。
他们是可以给你的类增加”magic”的特殊方法。
他们总是被双下划线所包围。
```
## 构造和初始化

* __new__()
```md
是在一个对象实例化的时候所调用的第一个方法。
第一个参数是这个类，其他的参数是用来直接传递给 __init__ 方法。
```
* __init__()
```md
类的初始化方法，当构造函数被调用的时候的任何参数都将会传给它。
x = SomeClass(10, 'foo')，__init__ 将会得到两个参数10和foo。
```
* __del__()
```md
如果 __new__ 和 __init__ 是对象的构造器的话，那么 __del__ 就是析构器。
它定义的是当一个对象进行垃圾回收时候的行为。
```
### 示例
```python
from os.path import join

class FileObject:
    '''给文件对象进行包装从而确认在删除时文件流关闭'''

    def __init__(self, filepath='~', filename='sample.txt'):
        #读写模式打开一个文件
        self.file = open(join(filepath, filename), 'r+')

    def __del__(self):
        self.file.close()
        del self.file
```



## 用于比较
* __eq__(self, other) 定义了等号的行为, == 。

* __ne__(self, other) 定义了不等号的行为, != 。

* __lt__(self, other) 定义了小于号的行为， < 。

* __gt__(self, other) 定义了大于等于号的行为， >= 。


## 数值处理

## 普通算术操作符

## 反运算

## 增量赋值

## 类型转换

## 打印
* __str__()
```md
如果要把一个类的实例变成 str，就需要实现特殊方法__str__()。
```

* __repr__()
```md
__str__()用于显示给用户，而__repr__()用于显示给开发人员。
```

## Utils
* __len__()
* __reversed__()
* __contains__()
