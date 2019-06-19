# Value-Type
```md
	变量的值只有一种类型，那就是字符串
	没有值的变量也有两种特殊的值
		一种是“不合法”（invalid）
			当 Nginx 用户变量 $foo 创建了却未被赋值时，$foo 的值便是“不合法”
		另一种是“没找到”（not found）
			如果当前请求的 URL 参数串中并没有提及 XXX 这个参数，则 $arg_XXX 内建变量的值便是“没找到”。
			遗憾的是在 Nginx 原生配置语言（我们估且这么称呼它）中是不能很方便地把它和空字符串区分开来的
				Nginx 的“变量插值”引擎自动把“找不到”给忽略了。
			应当如何把它和空字符串给区分开来呢？
				通过第三方模块 ngx_lua，我们可以轻松地在 Lua 代码中做到这一点。
					    location /test {
        content_by_lua '
            if ngx.var.arg_name == nil then
                ngx.say("name: missing")
            else
                ngx.say("name: [", ngx.var.arg_name, "]")
            end
        ';
    }
	无论是“不合法”也好，还是“没找到”也罢，这两种 Nginx 变量所拥有的特殊值，和空字符串（""）这种取值是完全不同的
		由 set 指令创建的变量未初始化就用在“变量插值”中时，效果等同于空字符串，但那是因为 set 指令为它创建的变量自动注册了一个“取处理程序”，将“不合法”的变量值转换为空字符串
			Nginx 的错误日志文件（一般文件名叫做 error.log）中多出一行类似下面这样的警告：
			[warn] 5765#0: *1 using uninitialized "foo" variable, ...
			上面这样的警告一般会指示出我们的 Nginx 配置中存在变量名拼写错误，抑或是在错误的场合使用了尚未初始化的变量。
			因为值缓存的存在，这条警告在一个请求的生命期中也不会打印多次。
			 ngx_rewrite 模块专门提供了一条 uninitialized_variable_warn 配置指令可用于禁止这条警告日志。
		set 指令在这里借用
			那些支持值缓存的内建变量的工作原理
				来处理未正确初始化的 Nginx 变量。
			只有“不合法”这个特殊值才会触发 Nginx 调用变量的“取处理程序”，而特殊值“没找到”却不会。
	 $cookie_XXX 变量
		不存在以及取值为空字符串这两种情况被很好地区分开了
	在 Lua 里访问未创建的 Nginx 用户变量时，在 Lua 里也会得到 nil 值，而不会像先前的例子那样直接让 Nginx 拒绝加载配置
		因为 Nginx 在加载配置时只会编译 content_by_lua 配置指令指定的 Lua 代码而不会实际执行它
	ngx_array_var 
		第三方模块让 Nginx 变量也能存放数组类型的值
		array_split、 array_map 和 array_join 这三条配置指令
			其含义很接近 Perl 语言中的内建函数 split、map 和 join
		可以很方便地处理这样具有不定个数的组成元素的输入数据
			例如此例中的 names URL 参数值就是由不定个数的逗号分隔的名字所组成。不过，这种类型的复杂任务通过 ngx_lua 来做通常会更灵活而且更容易维护。
```