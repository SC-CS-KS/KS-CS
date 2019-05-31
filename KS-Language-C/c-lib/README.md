# Library

* [#include](#include.md)

## libc
```md
libc 是 Linux 下的 ANSI C 函数库。glibc 是 Linux 下的 GUN C 函数库。
实际上有多种 libc 的实现，所以 libc 也可以是一个泛指。
glibc 是 GNU 组织对 libc 的一种实现。它是 Unix/Linux 的根基之一。

GNU C 库主要设计成一个可移植的高性能C库。
它遵循所有相关标准，包括ISO C11和 POSIX.1-2008。
它也是国际化的，并且拥有已知的最完整的国际化接口之一。
```
### [ANSI C(ANSI-C/README.md)
```md
<ctype.h>：包含用来测试某个特征字符的函数的函数原型，以及用来转换大小写字母的函数原型；
<errno.h>：定义用来报告错误条件的宏；
<float.h>：包含系统的浮点数大小限制；
<math.h>：包含数学库函数的函数原型；
<stddef.h>：包含执行某些计算 C 所用的常见的函数定义；
<stdio.h>：包含标准输入输出库函数的函数原型，以及他们所用的信息；
<stdlib.h>：包含数字转换到文本，以及文本转换到数字的函数原型，还有内存分配、随机数字以及其他实用函数的函数原型；
<string.h>：包含字符串处理函数的函数原型；
<time.h>：包含时间和日期操作的函数原型和类型；
<stdarg.h>：包含函数原型和宏，用于处理未知数值和类型的函数的参数列表；
<signal.h>：包含函数原型和宏，用于处理程序执行期间可能出现的各种条件；
<setjmp.h>：包含可以绕过一般函数调用并返回序列的函数的原型，即非局部跳转；
<locale.h>：包含函数原型和其他信息，使程序可以针对所运行的地区进行修改。
            地区的表示方法可以使计算机系统处理不同的数据表达约定，如全世界的日期、时间、美元数和大数字；
<assert.h>：包含宏和信息，用于进行诊断，帮助程序调试。
```

* 文件操作标准I/O库函数：
```md
fopen、fread、fwrite、fclose、fflush、fseek、fgetc、getc、getchar、fputc、putc、
putchar、fgets、gets、printf、fprintf、sprintf、scanf、fscanf、sscanf、fgetops、
fsetops、ftell、rewind、freopen、setvbuf、remove、fileno、fdopen
```
* 目录操作标准I/O库函数：
```md
opendir、readdir、telldir、seekdir、closedir
```

### [GNU C](GNU-C/README.md)

##
* [boost](boost/README.md)

* ICU(International Component for Unicode)
```md
是基于"IBM公共许可证"的，与开源组织合作研究的, 用于支持软件国际化的开源项目。
ICU4C 提供了 C/C++平台强大的国际化开发能力，软件开发者几乎可以使用ICU4C解决任何国际化的问题，
根据各地的风俗和语言习惯，实现对数字、货币、时间、日期、和消息的格式化、解析，
对字符串进行大小写转换、整理、搜索和排序等功能，
必须一提的是，ICU4C 提供了强大的 BIDI 算法，对阿拉伯语等 BIDI 语言提供了完善的支持。
```
* [gflags](gflags/README.md)

* [gtest]()
```md
是一个跨平台的(Liunx、Mac OS X、Windows、Cygwin、Windows CE and Symbian)C++单元测试框架，由google公司发布。
gtest 是为在不同平台上为编写 C++ 测试而生成的。
它提供了丰富的断言、致命和非致命判断、参数化、”死亡测试”等等。
```
##
* arpa/inet.h
* unistd.h
```md
是 C 和 C++ 程序设计语言中提供对 POSIX 操作系统 API 的访问功能的头文件的名称。
该头文件由 POSIX.1 标准（单一UNIX规范的基础）提出，
故所有遵循该标准的操作系统和编译器均应提供该头文件（如 Unix 的所有官方版本，包括 Mac OS X、Linux 等）。
```
