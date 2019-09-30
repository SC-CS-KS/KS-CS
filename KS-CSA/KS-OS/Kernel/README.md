# Kernel
```md
是操作系统的基础模块，用于管理系统资源。
例如 提供对软件层面的抽象（例如对进程、文件系统、同步、内存、网络协议等对象的操作和权限控制），
和对硬件访问的抽象（例如磁盘，显示，网络接口卡（NIC））；
操作系统，在内核的基础上有延伸，包括了提供基础服务的系统组件。

是计算机学科意义上的操作系统，直接与硬件交互，提供CPU时间片管理、中断、内存管理、IO管理等等；
一般意义上的操作系统包含的东西要更多一些，至少要有用户交互的基本程序，
比如一个命令行界面和基本的指令（文件遍历、进程管理等等），或者图形界面的桌面和文件浏览器。
```
```md
一个内核不是一套完整的操作系统，拿Linux来说，Linux 这个词本身只表示 Linux内核，
但现在大家已经默认的把 Linux理解成整个 Linux系统，这是由于历史原因造成的。

也就是说人们已经习惯了用 Linux来形容整个基于 Linux内核，
并且使用GNU 工程各种工具和应用程序的操作系统（也被称为GNU/Linux），而基于这些组件的 Linux软件被称为 Linux发行版。
```
```md
一般来讲，一个 Linux发行版本出来包括 Linux内核之外，还包含大量的软件（套件），
比如软件开发工具，数据库，Web服务器（例如Apache），X Window，桌面环境（比如 GNOME和 KDE），办公套件（比如OpenOffice、org）等等。
```