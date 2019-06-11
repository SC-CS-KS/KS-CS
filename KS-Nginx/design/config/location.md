
```md
	匹配模式
		location = /uri 　
			=开头表示精确匹配，只有完全匹配上才能生效
		location ^~ /uri 
			^~ 开头对URL路径进行前缀匹配，并且在正则之前
		location ~ pattern 
			~开头表示区分大小写的正则匹配
		location ~* pattern 
			~*开头表示不区分大小写的正则匹配
		location /uri
			不带任何修饰符，也表示前缀匹配，但是在正则匹配之后
		location / 
			通用匹配，任何未匹配到其它location的请求都会匹配到，相当于switch中的default
	匹配顺序
		
			"="前缀指令匹配，如果匹配成功，则停止其他匹配
			普通字符串指令匹配，顺序是从长到短，匹配成功的location如果使用^~，则停止其他匹配（正则匹配）
			正则表达式指令匹配，按照配置文件里的顺序，成功就停止其他匹配
			如果第三步中有匹配成功，则使用该结果，否则使用第二步结果
		(location =) > (location 完整路径) > (location ^~ 路径) > (location ~,~* 正则顺序) > (location 部分起始路径) > (/)
		注意
			匹配的顺序是先匹配普通字符串，然后再匹配正则表达式
			普通字符串匹配顺序是根据配置中字符长度从长到短
			正则表达式按照配置文件里的顺序测试。找到第一个比配的正则表达式将停止搜索。
			一般情况下
				匹配成功了普通字符串location后还会进行正则表达式location匹配
				有两种方法改变这种行为
					其一就是使用“=”前缀，这时执行的是严格匹配，并且匹配成功后立即停止其他匹配，同时处理这个请求
					另外一种就是使用“^~”前缀
						如果把这个前缀用于一个常规字符串那么告诉nginx 如果路径匹配那么不测试正则表达式。
	示例
		location  = / {
  # 精确匹配 / ，主机名后面不能带任何字符串
  [ configuration A ] 
}
		location  / {
  # 因为所有的地址都以 / 开头，所以这条规则将匹配到所有请求
  # 但是正则和最长字符串会优先匹配
  [ configuration B ] 
}
		location /documents/ {
  # 匹配任何以 /documents/ 开头的地址，匹配符合以后，还要继续往下搜索
  # 只有后面的正则表达式没有匹配到时，这一条才会采用这一条
  [ configuration C ] 
}
		location ~ /documents/Abc {
  # 匹配任何以 /documents/ 开头的地址，匹配符合以后，还要继续往下搜索
  # 只有后面的正则表达式没有匹配到时，这一条才会采用这一条
  [ configuration CC ] 
}
		location ^~ /images/ {
  # 匹配任何以 /images/ 开头的地址，匹配符合以后，停止往下搜索正则，采用这一条。
  [ configuration D ] 
}
		location ~* \.(gif|jpg|jpeg)$ {
  # 匹配所有以 gif,jpg或jpeg 结尾的请求
  # 然而，所有请求 /images/ 下的图片会被 config D 处理，因为 ^~ 到达不了这一条正则
  [ configuration E ] 
}
		location /images/ {
  # 字符匹配到 /images/，继续往下，会发现 ^~ 存在
  [ configuration F ] 
}
		location /images/abc {
  # 最长字符匹配到 /images/abc，继续往下，会发现 ^~ 存在
  # F与G的放置顺序是没有关系的
  [ configuration G ] 
}
		location ~ /images/abc/ {
  # 只有去掉 config D 才有效：先最长匹配 config G 开头的地址，继续往下搜索，匹配到这一条正则，采用
    [ configuration H ] 
}
	实践
		实际使用中，建议至少有三个匹配规则定义
		# 第一个必选规则
			location = / {
    proxy_pass http://tomcat:8080/index
}
				#直接匹配网站根，通过域名访问网站首页比较频繁，使用这个会加速处理，官网如是说。
				#这里是直接转发给后端应用服务器了，也可以是一个静态首页
		# 第二个必选规则是处理静态文件请求
			location ^~ /static/ {
    root /webroot/static/;
}
location ~* \.(gif|jpg|jpeg|png|css|js|ico)$ {
    root /webroot/res/;
}
				这是nginx作为http服务器的强项
				# 有两种配置模式，目录匹配或后缀匹配,任选其一或搭配使用
		#第三个规则就是通用规则
			location / {
    proxy_pass http://tomcat:8080/
}
			用来转发动态请求到后端应用服务器
				#非静态文件请求就默认是动态请求，自己根据实际把握
				#毕竟目前的一些框架的流行，带.php,.jsp后缀的情况很少了
```