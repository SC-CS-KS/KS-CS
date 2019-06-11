# Nginx Virtual Host
```md
	把一台物理服务器划分成多个“虚拟”的服务器，每一个虚拟主机都可以有独立的域名和独立的目录
	nginx的虚拟主机就是通过nginx.conf中server节点指定的，想要设置多个虚拟主机，配置多个server节点即可
	虚拟机功能是ngx_http_core_module（http核心模块）实现
	server_name a.test.com;
		指定这个虚拟主机名为a.test.com，当用户访问a.test.com时，就有这个虚机主机进行处理
		虚拟主机名可以有4种格式：
			（1）准确的名字，例如此例中的a.test.com
			（2）*号开头的，例如 *.test.com
			（3）*号结尾的，例如 mail.*
			（4）正则表达式形式，例如 
				server_name ~^www\d+\.test\.com$; 
				注意，使用正则表达式形式时，必须以'~'开头
		server_name也可以同时指定多个
			server_name test.com www.test.com *.test.com;
		优先级为：
			（1）确切的名字
			（2）最长的以*起始的通配符名字
			（3）最长的以*结束的通配符名字
			（4）第一个匹配的正则表达式名字
```