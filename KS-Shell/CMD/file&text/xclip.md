# [xclip](https://github.com/astrand/xclip)

```md
xclip 用命令行实现直接从文件中复制内容到桌面剪贴板，或者从桌面剪贴板中提取内容到命令行文件。
```

## 桌面剪贴板
```md
Linux 中有三个x-selection:
* XA_PIRMARY
    存储了你当前用鼠标选中的内容，当选中内容之后，你可以点击鼠标中键来粘贴当前选中的内容。
* XA_SECONDARY

* XA_CLIPBOARD 常说的剪贴板
    通过ctrl-c（或者复制）操作的内容都存储在这个区域中。
```

## 参数
```md
-i 从标准输入或者一个文件中读入内容到指定的x-selection。

-o 从指定的x-selection中输出内容到标准输出。

-sel / -selection 
    选择特定的x-selection，
    primary、secondary、clipboard 分别对应 XA_PRIMARY、XA_SECONDARY、XA_CLIPBOARD。
```

## Utils
```md
从文件复制内容到剪贴板：
xclip -i -sel clipboard myfile.txt

从剪贴板输出内容到制定文件：
xclip -o -sel clipboard > myfile.txt
```

## 安装

```sh
autoreconf		# create configuration files
./configure		# create the Makefile
make			# build the binary
su			# su to root to install
make install		# install xclip
make install.man	# install man page
```

* configure: error: *** X11/Xmu/Atoms.h is missing ***
```md
yum install  -y libXmu-devel.x86_64
```
