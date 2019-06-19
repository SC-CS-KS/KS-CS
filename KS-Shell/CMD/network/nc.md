# [The GNU Netcat - nc](http://netcat.sourceforge.net/)

## Usage

## Utils
* 调试基于HTTP协议的服务调用
```sh
# while true; do nc -l 8888; done

# curl "http://localhost:8888?abc=def"

* 打印
GET /?abc=def HTTP/1.1
User-Agent: curl/7.35.0
Host: localhost:8888
Accept: */*

```
* 端口扫描
```sh
# nc -nvz 127.0.0.1 8000-8118
```
* 远程拷贝文件
```md
scp 命令基于SSH协议，nc 可以绕过该协议传输文件。
```
```sh
[server2]# nc -l 1234 > 1234.txt
[server1]# nc -w 1 192.168.200.27 1234 < abc.txt
```
* 通信
```md
* Server1
# nc -l 8118 
* Server2
# nc  192.168.200.27 8118 
```





