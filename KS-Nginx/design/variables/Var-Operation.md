# Var-Operation
***读取输出***
```md
Nginx 会在匹配参数名之前，自动把原始请求中的参数名调整为全部小写的形式。
```
* echo [ngx_echo 模块](https://github.com/openresty/echo-nginx-module#readme)
```md
			    server {
        listen 8080;

        location /test {
            set $foo hello;
            echo "foo: $foo";
        }
    }
				    $ curl 'http://localhost:8080/test'
    foo: hello
			如果我们想通过 echo 指令直接输出含有“美元符”（$）的字符串
				那么有没有办法把特殊的 $ 字符给转义掉呢？
					答案是否定的（至少到目前最新的 Nginx 稳定版 1.0.10）
				不过幸运的是，我们可以绕过这个限制，
					比如通过不支持“变量插值”的模块配置指令专门构造出取值为 $ 的 Nginx 变量，然后再在 echo 中使用这个变量。
				    geo $dollar {
        default "$";
    }
			用户变量未赋值就输出的话，得到的便是空字符串。
```
***创建和赋值***
* [set](http://nginx.org/en/docs/http/ngx_http_rewrite_module.html#set) [ngx_rewrite 模块](http://nginx.org/en/docs/http/ngx_http_rewrite_module.html)
```md
			 
			Syntax:	set $variable value;
			Default:	—
			Context:	server, location, if
			Sets a value for the specified variable. The value can contain text, variables, and their combination.
			不仅有赋值的功能，它还有创建 Nginx 变量的副作用
				即当作为赋值对象的变量尚不存在时，它会自动创建该变量。
```
```md
		创建
			Nginx 变量的创建只能发生在 Nginx 配置加载的时候，或者说 Nginx 启动的时候
				这意味着不创建而直接使用变量会导致启动失败，
					此时 Nginx 服务器会拒绝加载配置:
					[emerg] unknown "foo" variable
			Nginx 变量一旦创建，其变量名的可见范围就是整个 Nginx 配置，甚至可以跨越不同虚拟主机的 server 配置块。
		赋值
			赋值操作则只会发生在请求实际处理的时候。
				意味着我们无法在请求处理时动态地创建新的 Nginx 变量。
		    server {
        listen 8080;

        location /foo {
            echo "foo = [$foo]";
        }

        location /bar {
            set $foo 32;
            echo "foo = [$foo]";
        }
    }
			    $ curl 'http://localhost:8080/foo'
    foo = []

    $ curl 'http://localhost:8080/bar'
    foo = [32]

    $ curl 'http://localhost:8080/foo'
    foo = []

				在 location /bar 中用 set 指令创建了变量 $foo，于是在整个配置文件中这个变量都是可见的，因此我们可以在 location /foo 中直接引用这个变量而不用担心 Nginx 会报错。
				set 指令因为是在 location /bar 中使用的，所以赋值操作只会在访问 /bar 的请求中执行。
				而请求 /foo 接口时，我们总是得到空的 $foo 值，因为用户变量未赋值就输出的话，得到的便是空字符串。
		Nginx 变量名的可见范围虽然是整个配置，但每个请求都有所有变量的独立副本，或者说都有各变量用来存放值的容器的独立副本，彼此互不干扰。
			事实上，Nginx 变量的生命期是不可能跨越请求边界的。
```