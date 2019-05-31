# Magic Variable

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