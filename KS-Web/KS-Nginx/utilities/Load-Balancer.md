# Nginx Load Balancer
## 协议支持
```md
支持七层HTTP、HTTPS协议的负载均衡。
对四层协议的支持需要第三方插件 - yaoweibin 的 ngx_tcp_proxy_module 实现了 tcp upstream。
```
```md
nginx本身也逐渐在完善对其他协议的支持：
nginx 1.4.0对Websocket和SPDY都做了正式的支持。
nginx 1.6.0对SPDY 3.1的正式支持 nginx
1.10.0正式支持HTTP/2
```

## 策略
* RR（默认）
```md
每个请求按时间顺序逐一分配到不同的后端服务器，如果后端服务器down掉，能自动剔除。
```
```json
	upstream test {
        server localhost:8080;
        server localhost:8081;
    }
			    server {
        listen       81;                                                        
        server_name  localhost;                                              
        client_max_body_size 1024M;
 
        location / {
            proxy_pass http://test;
            proxy_set_header Host $host:$server_port;
        }
    }
```
* 加权轮询（weighted round robin）
```md
指定轮询几率，weight和访问比率成正比，用于后端服务器性能不均的情况。
```
```json
    upstream test {
        server localhost:8080 weight=9;
        server localhost:8081 weight=1;
    }
```	
* ip_hash
```md
iphash的每个请求按访问ip的hash结果分配，这样每个访客固定访问一个后端服务器，可以解决session的问题。
```
```json
	upstream test {
        ip_hash;
        server localhost:8080;
        server localhost:8081;
    }
```
* fair（第三方）
```md
按后端服务器的响应时间来分配请求，响应时间短的优先分配
```
```json
	upstream backend {
        fair;
        server localhost:8080;
        server localhost:8081;
    }
```
* url_hash（第三方）
```md
按访问url的hash结果来分配请求，使每个url定向到同一个后端服务器，后端服务器为缓存时比较有效。
在upstream中加入hash语句，server语句中不能写入weight等其他的参数，hash_method是使用的hash算法。
```
```json
	upstream backend {
        hash $request_uri;
        hash_method crc32;
        server localhost:8080;
        server localhost:8081;
    }
```
* 通用hash
```md
通用hash比较简单，可以以nginx内置的变量为key进行hash
```
* 一致性hash
```md
一致性hash采用了nginx内置的一致性hash环。
```
* session_sticky
```md
一次会话内的请求都会落到同一个结点上。
```
* 动态负载均衡
> * 自身监控
```md
内置了对后端服务器的健康检查功能。
如果Nginx proxy后端的某台服务器宕机了，会把返回错误的请求重新提交到另一个节点，不会影响前端访问。

它没有独立的健康检查模块，而是使用业务请求作为健康检查，这省去了独立健康检查线程，这是好处。
坏处是，当业务复杂时，可能出现误判，
例如后端响应超时，这可能是后端宕机，也可能是某个业务请求自身出现问题，跟后端无关。
```
## Tengine
* 对比原生Nginx的优势
```md
支持一致性Hash模块
会话保持模块
对后端服务器的主动健康检查
增加了请求体不缓存到磁盘的机制
```
