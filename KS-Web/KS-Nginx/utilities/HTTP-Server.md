# Nginx HTTP Server
```md
	Nginx本身也是一个静态资源的服务器，当只有静态资源的时候，就可以使用Nginx来做服务器。
	静态
	动静分离
		        # 所有动态请求都转发给tomcat处理  
        location ~ .(jsp|do)$ {  
            proxy_pass  http://test;  
        } 
	访问控制
		基于来源地址访问控制
			ngx_http_access_module模块实现
			location / {
    deny  192.168.1.1;
    allow 192.168.1.0/24;
    allow 10.1.1.0/16;
    allow 2001:0db8::/32;
    deny  all;
}
			至上而下依次检查，默认为通过(被上面的匹配到了就直接允许或拒绝，下面的规则就不会检查了)
		基于用户认证 
			ngx_http_auth_baisc_module模块实现
			location /admin {                       # /admin对哪些路径进行用户认证
       
    auth_basic   "closed site";        # 提示语
    auth_basic_user_file conf/htpasswd;     # 密码的存放位置
}
	建立下载站点
		gx_http_autoindex_module模块实现
	URL rewrite
		ngx_http_rewrite_module实现
		“内部跳转”
			就是在处理请求的过程中，于服务器内部，从一个 location 跳转到另一个 location 的过程。
			内部跳转和 Bourne Shell（或 Bash）中的 exec 命令很像，都是“有去无回”。
			echo_exec
			 rewrite
				效果和使用 echo_exec 是完全相同的
		“外部跳转”
			利用 HTTP 状态码 301 和 302 进行重写
	防盗链
		ngx_http_referer_module实现
		valid_referers none blocked server_names
               *.example.com example.* www.example.org/galleries/
               ~\.google\.;

if ($invalid_referer) {
    return 403;
}
		定义合规引用
			valid_referers none |block |server_names|string ...   
			none：“-”，空，通过浏览器直接访问
			blocked：请求报文中有referers字段但被清空
				 such values are strings that do not start with “http://” or “https://”;
			server_names
				  the “Referer” request header field contains one of the server names;
				   请求报文中"Referer"字段包含以下服务器名称；
		判断不合规的引用
			ngx_http_referer_module引入了$invalid_referer变量，$valid_referer是一个布尔值，表示不被valid_referer匹配到都是不合规的引用$invalid_referer
			if ($invaild_referer) {
   rewrite ^/.*$ http://www.a.com/403.html   
}
	状态页
		由status模块实现
		location /status{
        stub_status on;
        access_log off;
        allow 192.168.10.0/24 
        deny all;
}
	压缩
		 gzip模块实现
		gzip            on;
gzip_min_length 1000;
gzip_proxied    expired no-cache no-store private auth;
gzip_types      text/plain application/xml;
```