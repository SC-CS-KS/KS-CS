# Var-Type
```md
	“预定义变量”
		“内建变量”（builtin variables）
			最常见的用途就是获取关于请求或响应的各种信息
		 ngx_http_core 模块
			 $uri
				获取当前请求的 URI（经过解码，并且不含请求参数）
			 $request_uri
				用来获取请求最原始的 URI （未经解码，并且包含请求参数）。
			    $ curl 'http://localhost:8080/test/hello%20world?a=3&b=4'
    uri = /test/hello world
    request_uri = /test/hello%20world?a=3&b=
		有无限多变种的一群变量
			 $arg_XXX 变量群
				一个例子是 $arg_name
					当前请求名为 name 的 URI 参数的值
					而且还是未解码的原始形式的值。
				    location /test {
        echo "name: $arg_name";
        echo "class: $arg_class";
    }
					    $ curl 'http://localhost:8080/test?name=hello%20world&class=9'
    name: hello%20world
    class: 9
				其实 $arg_name 不仅可以匹配 name 参数，也可以匹配 NAME 参数，抑或是 Name，等等
				有一些局限
					 $arg_XXX 变量在请求 URL 中有多个同名 XXX 参数时，就只会返回最先出现的那个 XXX 参数的值，而默默忽略掉其他实例
					$ curl 'http://localhost:8080/test?name'
    name: missing
						此时，$arg_name 变量仍然读出“找不到”这个特殊值，这就明显有些违反常识。
					要解决这些局限，可以直接在 Lua 代码中使用 ngx_lua 模块提供的 ngx.req.get_uri_args 函数。
			 $sent_http_XXX 变量群
				取响应头
			 $http_XXX 变量群
				取请求头
			 $cookie_XXX 变量群
				取 cookie 值
			像 $arg_XXX 这种类型的变量拥有无穷无尽种可能的名字，所以它们并不对应任何存放值的容器
				而且这种变量在 Nginx 核心中是经过特别处理的，第三方 Nginx 模块是不能提供这样充满魔法的内建变量的。
		如果你想对 URI 参数值中的 %XX 这样的编码序列进行解码
			可以使用第三方 ngx_set_misc 模块提供的 set_unescape_uri 配置指令
				        set_unescape_uri $name $arg_name;
			 set_unescape_uri 
				也像 set 指令那样，拥有自动创建 Nginx 变量的功能
		需要指出的是，许多内建变量都是只读的
			比如我们刚才介绍的 $uri 和 $request_uri. 
				对只读变量进行赋值是应当绝对避免的，因为会有意想不到的后果
					 [emerg] the duplicate "uri" variable in ...
			如果你尝试改写另外一些只读的内建变量
				比如 $arg_XXX 变量，在某些 Nginx 的版本中甚至可能导致进程崩溃。
		也有一些内建变量是支持改写的
			 $args
				在读取时返回当前请求的 URL 参数串（即请求 URL 中问号后面的部分，如果有的话），而在赋值时可以直接修改参数串。
				这里的 $args 变量和 $arg_XXX 一样，也不再使用属于自己的存放值的容器。
					当我们读取 $args 时，Nginx 会执行一小段代码，从 Nginx 核心中专门存放当前 URL 参数串的位置去读取数据；
					当我们改写 $args 时，Nginx 会执行另一小段代码，对相同位置进行改写。
						Nginx 的其他部分在需要当前 URL 参数串的时候，都会从那个位置去读数据，所以我们对 $args 的修改会影响到所有部分的功能。
	“用户和自定义变量”
		“用户变量“
```