# Nginx
## 工作模式
```md
	单工作进程模式（默认）
		除主进程外，还有一个工作进程，且工作进程是单线程的
	多工作进程模式
		每个工作进程包含多工作线程
```
## [Config](config/README.md)
## [Nginx Variables](variables/README.md)
## [Modules](https://www.nginx.com/resources/wiki/modules/)
* [ngx_http_limit_req_module](modules/ngx_http_limit_req_module.md)
```md
	模块的类型
		event module
			搭建 独立于操作系统的事件处理机制的框架，以及 提供各种具体事件的处理。
				包括ngx_events_module,ngx_event_core_module,ngx_epoll_module等
			ngx_events_module
			ngx_event_core_module
			ngx_epoll_module
		phase handler
			此类型模块也被直接称为handler模块，主要负责处理客户端请求并产生待响应的内容
			ngx_http_static_moduler
				负责客户端的静态页面请求处理并将对应的磁盘 文件准备为响应内容输出。
			ngx_headers_more
				增加、删除出站、入站的 Header 信息。
					要想使用相关功能需要在编译 Nginx 时加入该模块。
				more_clear_headers
					语法：more_clear_headers [-t <content-type list>]... [-s <status-code list>]... <new-header>...
					默认值：no
					配置段：http, server, location, location if
					阶段：输出报头过滤器
					清除指定的输出头。
				more_set_headers -s 404 -t 'text/html' 'X-Foo: Bar';
					语法：more_set_headers [-t <content-type list>]... [-s <status-code list>]... <new-header>...
					默认值：no
					配置段：http, server, location, location if
					阶段：输出报头过滤器
					替换（如有）或增加（如果不是所有）指定的输出头时响应状态代码与-s选项相匹配和响应的内容类型的-t选项指定的类型相匹配的。
					如果没有指定-s或-t，或有一个空表值，无需匹配。因此，对于下面的指定，任何状态码和任何内容类型都讲设置。
				more_set_input_headers
					非常类似more_set_headers，不同的是它工作在输入头（或请求头），它仅支持-t选项。
				more_clear_input_headers
				局限性
					1. 不同于标准头模块，该模块不会对下面头有效： Expires, Cache-Control, 和Last-Modified。
					2. 使用此模块无法删除Connection的响应报头。唯一方法是更改src/ HTTP/ ngx_http_header_filter_module.c文件。
			ngx_http_headers_module
				add_header
					语法: add_header name value;
					默认值: —
					配置段: http, server, location, if in location
					对响应代码为200，201，204，206，301，302，303，304，或307的响应报文头字段添加任意域。如：
						add_header From jb51.net
				expires
					语法: expires [modified] time;
					expires epoch | max | off;
					默认值: expires off;
					配置段: http, server, location, if in location
					在对响应代码为200，201，204，206，301，302，303，304，或307头部中是否开启对“Expires”和“Cache-Control”的增加和修改操作。
					可以指定一个正或负的时间值，Expires头中的时间根据目前时间和指令中指定的时间的和来获得。
					epoch表示自1970年一月一日00:00:01 GMT的绝对时间，max指定Expires的值为2037年12月31日23:59:59，Cache-Control的值为10 years。
					Cache-Control头的内容随预设的时间标识指定：
						·设置为负数的时间值:Cache-Control: no-cache。
						·设置为正数或0的时间值：Cache-Control: max-age = #，这里#的单位为秒，在指令中指定。
					参数off禁止修改应答头中的"Expires"和"Cache-Control"。
		output filter
			也称为filter模块，主要 负责处理输出的内容，包括修改输出内容，可以实现对输出的所有的 html的 页面添加 预定义的footbar一类的工作，或者对输出的 图片的URL进行替换的 工作。
		upstream
			pstream模块实现反向代理，将真正的请求 转发到服务器上，并 从后端服务器上读取响应，发回客户端。
				upstream模块 是一种特殊的handler,只不过响应内容也不是真正由自己产生的，而是从后端服务器上读取的。
		load-balancer
			负载均衡模块，实现特定的 算法，在 众多的后端 服务器中，选择一个服务器出来作为某个请求的转发服务器。
	基础模块
		HTTP Access模块
			ngx_http_access_module
		HTTP FastCGI模块
		HTTP Proxy模块
		HTTP Rewrite模块
	第三方模块
		HTTP Upstream Hash模块
			ngx_http_upstream_consistent_hash
		Notice模块
		HTTP Access Key模块
		HTTP Access Log 模块
		Request模块
	机制
		组织和管理
			在Nginx中，使用全局数组ngx_modules保存和管理所有Nginx的模块。
			Nginx的众多模块被分成两类：必须安装的模块和可以安装的模块。
				必须安装的模块是保证Nginx正常功能的模块，没得选择，这些模块会出现在ngx_modules里。比如ngx_core_module
				可以安装的模块通过configure的配置和系统环境，被有选择的安装，这些模块里，被选择安装的模块会出现在ngx_modules数组中。
				当configure执行结束后，会生成一个objs\ngx_modules.c的源代码文件
					文件内容随configure配置不同而不同
					ngx_module_t *ngx_modules[] 
					ngx_modules数组里存放的是ngx_module_t *类型指针，并且，最后一个一定是空指针NULL
					将最后一个元素置为空指针NULL，是为了遍历数组的时候，标记数组结束，这样不必在使用时记录数组大小。
		配置模块的设计
			配置模块是所有 模块的基础
				它实现了最基本的配置项 的解析功能（也就是解析 nginx.conf） 
				核心模块的类型是ngx_core_module
			ngx_conf_module
			核心模块
				ngx_http_module
				ngx_mail_module
				ngx_event_module
				ngx_stream_module
				ngx_core_module
		模块的加载
		模块的主要轮廓
			客户请求
				配置模块
核心模块
					选择对应的处理模块
						处理模块或负载均衡模块
							过滤模块 1 ... n
								响应客户

```

## nginx事件处理
```md
		nginx需要将所有关心的fd注册到epoll
		static ngx_int_t ngx_epoll_add_event(ngx_event_t *ev, ngx_int_t event, ngx_uint_t flags);
	ngx_event_t
		结构体指针，代表关心的一个读或者写事件
		nginx为事件可能会设置一个超时定时器，从而能够处理事件超时情况
		struct ngx_event_s {
    ngx_event_handler_pt  handler; //函数指针：事件的处理函数
    ngx_rbtree_node_t   timer;     //超时定时器，存储在红黑树中（节点的key即为事件的超时时间）
    unsigned         timedout:1;   //记录事件是否超时
};
	epoll_wait
		监听所有fd，处理发生的读写事件
		epoll_wait是阻塞调用
			最后一个参数timeout是超时时间，即最多阻塞timeout时间如果还是没有事件发生，方法会返回
	timeout
		从上面说的记录超时定时器的红黑树中查找最近要到时的节点
		以此作为epoll_wait的超时时间
			ngx_msec_t ngx_event_find_timer(void)
{
    node = ngx_rbtree_min(root, sentinel);
    timer = (ngx_msec_int_t) (node->key - ngx_current_msec);
 
    return (ngx_msec_t) (timer > 0 ? timer : 0);
}
		同时nginx在每次循环的最后
			会从红黑树中查看是否有事件已经过期
			如果过期，标记timeout=1，并调用事件的handler
			void ngx_event_expire_timers(void)
{
    for ( ;; ) {
        node = ngx_rbtree_min(root, sentinel);
 
        if ((ngx_msec_int_t) (node->key - ngx_current_msec) <= 0) {  //当前事件已经超时
            ev = (ngx_event_t *) ((char *) node - offsetof(ngx_event_t, timer));
 
            ev->timedout = 1;
 
            ev->handler(ev);
 
            continue;
        }
 
        break;
    }
}
	nginx就是通过上面的方法实现了socket事件的处理，定时事件的处理
```