Table of Contents
=================

   * [Variable](#variable)
   * [<a href="magic-variable.md">Magic Variable</a>](#magic-variable)
   * [<a href="https://www.python.org/dev/peps/pep-0318/" rel="nofollow">@ Modifier</a>](#-modifier)
      * [@ Decorators](#-decorators)
   * [Methods](#methods)
      * [Magic Methods](#magic-methods)
         * [构造和初始化](#构造和初始化)
         * [示例](#示例)
         * [用于比较](#用于比较)
         * [数值处理](#数值处理)
         * [普通算术操作符](#普通算术操作符)
         * [反运算](#反运算)
         * [增量赋值](#增量赋值)
         * [类型转换](#类型转换)
         * [打印](#打印)
         * [Utils](#utils)
   * [OOP](#oop)

# Variable
# [Magic Variable](magic-variable.md)
* __name__
```md
获取导入文件的路径加文件名称，路径以点分割。
注意:获取当前文件返回 __main__ 
```
* __file__
```md
获取 python 脚本的“路径+脚本名称”。
可能是一个相对路径也可能是一个绝对路径，取决按照什么路径来执行的脚本。

一般配合os模块的os.path.dirname()，os.path.basename() ，os.path.join() 模块函数来使用
一般来说__file__变量和os.path配合，可以用来获取python脚本的绝对路径。
```
```python
#a.py
import os
print os.path.realpath(__file__)

out>>E:\Eclipse_workspace\python_learn\a.py
```
* __doc__ —— 获取文件的注释

* __package__ 
```md
获取导入文件的路径，多层目录以点分割，注意：对当前文件返回None
```
* __cached__ —— 获取导入文件的缓存路径

* __builtins__ —— 内置函数

# [@ Modifier](https://www.python.org/dev/peps/pep-0318/)
## @ Decorators
```md
An @ symbol at the beginning of a line is used for class, function and method decorators.
```
* @property
```md
是一种特殊的属性，访问它时会执行一段功能（函数）然后返回值。
将一个类的函数定义成特性以后，obj.name 调用方式遵循了统一访问的原则。
```
* @classmethod
```md
类方法是给类用的，类在使用时会将类本身当做参数传给类方法的第一个参数。
```
* @staticmethod
```md
是一种普通函数，位于类定义的命名空间中，不会对任何实例类型进行操作。
```
* @functionName

# Methods
## Magic Methods
* 什么是魔术方法?
```md
他们是面向对象的Python的一切。
他们是可以给你的类增加”magic”的特殊方法。
他们总是被双下划线所包围。
```
### 构造和初始化
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

### 用于比较
* __eq__(self, other) 定义了等号的行为, == 。
* __ne__(self, other) 定义了不等号的行为, != 。
* __lt__(self, other) 定义了小于号的行为， < 。
* __gt__(self, other) 定义了大于等于号的行为， >= 。

### 数值处理

### 普通算术操作符

### 反运算

### 增量赋值

### 类型转换

### 打印
* __str__()
```md
如果要把一个类的实例变成 str，就需要实现特殊方法__str__()。
```
* __repr__()
```md
__str__()用于显示给用户，而__repr__()用于显示给开发人员。
```
### Utils
* __len__()
* __reversed__()
* __contains__()

# OOP