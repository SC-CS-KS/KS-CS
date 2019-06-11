# Nignx 限流

## Config
```md
ngx_http_limit_req_module
	//每个配置指令主要包含两个字段：名称，解析配置的处理方法
static ngx_command_t  ngx_http_limit_req_commands[] = {
    { ngx_string("limit_req_zone"),
      ngx_http_limit_req_zone,
     },
 
    { ngx_string("limit_req"),
      ngx_http_limit_req,
     },
 
    { ngx_string("limit_req_log_level"),
      ngx_conf_set_enum_slot,
     },
 
    { ngx_string("limit_req_status"),
      ngx_conf_set_num_slot,
    },
};
	
		limit_req_zone
			一般用法：limit_req_zone $binary_remote_addr zone=one:10m rate=1r/s;
			
				$binary_remote_addr
					表示远程客户端IP
					是nginx提供的变量，用户在配置文件中可以直接使用
				zone配置一个存储空间
					需要分配空间记录每个客户端的访问速率，超时空间限制使用lru算法淘汰
					注意此空间是在共享内存分配的，所有worker进程都能访问
				rate表示限制速率，此例为1qps
		limit_req
			用法：limit_req zone=one burst=5 nodelay;
			
				zone指定使用哪一个共享空间
				burst配置用于处理突发流量，表示最大排队请求数目
					当客户端请求速率超过限流速率时，请求会排队等待
					而超出burst的才会被直接拒绝
				nodelay必须与burst一起使用
					此时排队等待的请求会被优先处理
					否则假如这些请求依然按照限流速度处理，可能等到服务器处理完成后，客户端早已超时
		limit_req_log_level
			当请求被限流时，日志记录级别
			用法：limit_req_log_level info | notice | warn | error;
		limit_req_status
			当请求被限流时，给客户端返回的状态码
			用法：limit_req_status 503
```
## Design
* ngx_http_limit_conn_module 连接数限流模块
```md
用来对某个 KEY 对应的 总的网络连接数 进行限流
	可以按照如 IP、域名维度 进行限流
```
* ngx_http_limit_req_module 请求限流模块 漏桶算法
* lua-resty-limit-traffic OpenResty 提供的 Lua 限流模块，更复杂的 限流场景

***[源码](https://github.com/SunnnyChan/sc.drill-code/blob/master/nginx/modules/ngx_http_limit_req_module.md)***


## Reference
* [应用接入层限流（ Nginx / OpenResty ）](https://www.toutiao.com/i6684055284526088717/)
