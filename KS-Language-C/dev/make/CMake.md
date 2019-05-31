# CMake
```md
不同 Make (例如 GNU Make ，QT 的 qmake ，微软的 MS nmake，BSD Make（pmake），Makepp) 工具
遵循不同的规范和标准，所执行的 Makefile 格式也千差万别。
使用上面的 Make 工具无法做到跨平台编译。
```
```md
允许开发者编写一种平台无关的 CMakeList.txt 文件来定制整个编译流程，
然后再根据目标用户的平台进一步生成所需的本地化 Makefile 和工程文件，
如 Unix 的 Makefile 或 Windows 的 Visual Studio 工程。
从而做到“Write once, run everywhere”。
```

## 流程
```md
1. 编写 CMake 配置文件 CMakeLists.txt 。
2. 执行命令 cmake PATH 或者 ccmake PATH 生成 Makefile。其中， PATH 是 CMakeLists.txt 所在的目录。
3. 使用 make 命令进行编译。
```
## 常用变量
* CMAKE_MODULE_PATH
```md
定义自己的 cmake 模块所在的路径。
FIND_PACKAGE( libdb_cxx REQUIRED)命令执行后，
CMake 会到变量 CMAKE_MODULE_PATH 指示的目录中查找文件 Findlibdb_cxx.cmake 并执行。
```

## [CMakeLists.txt](CMakeLists.md)

## Resources
* [CMake 入门实战](https://www.hahack.com/codes/cmake/)
* [CMake 常用变量和常用环境变量查表手册](https://www.cnblogs.com/xianghang123/p/3556425.html)

* [Quick CMake Tutorial](http://www.jetbrains.com/help/clion/quick-cmake-tutorial.html)
