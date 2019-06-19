# Linux Command Line

## File
```sh
grep "XXX" . -rl  //查询符合包含 “XXX”字符串的文件，输出多行文件名
```
```sh
find . -type f //输出多行文件名
find . -type f -print0 //输出文件列表
```
```md
readlink -f [file path] //获取文件绝对路径
```
## Text
```sh
rsync -av --exclude "logs/"  /data/dc star@10.3.111.111:/home/deploy
```
## Network
```sh
lsof -i:[port] //通过网络端口号，查找运行进程
```
## Software Management

## OS
```sh
whereis eclipse // 查找软件安装
```
