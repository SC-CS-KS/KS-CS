Table of Contents
=================

   * [安装](#安装)
   * [打包发布](#打包发布)
   * [导入 import](#导入-import)
   * [Module](#module)

# 包安装
```sh
pip3 install image
pip3 install pyautogui
```

# 打包发布

# 导入 import
* Regular imports
* Using from
* Relative imports
* Optional imports
* Local imports

[Python 101: All about imports](http://www.blog.pythonlibrary.org/2016/03/01/python-101-all-about-imports/)

# Module
```md
一个文件算一个模块，一个带__init__.py的目录算一个包。
```

# pip -  The Python Package Installer
```md
通用的 Python 包管理工具。提供了对 Python 包的查找、下载、安装、卸载的功能。
```
```bash
easy_install pip //安装 pip
pip install Markdown //安装package
pip freeze //列出安装的packages
pip install ‘Markdown<2.0’ //安装特定版本的package，通过使用 ==, >=, <=, >, < 指定一个版
pip install -U Markdown //升级到当前最新的版本
pip uninstall Markdown //卸载
pip search “Markdown” //查询
```




