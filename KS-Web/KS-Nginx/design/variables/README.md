# Nginx Variables
* [变量类型](Var-Type.md)
* [全局变量](Global-Var.md)
* [值类型](Value-Type.md)
* 生命期
```md
		一个请求在其处理过程中，即使经历多个不同的 location 配置块
			它使用的还是同一套 Nginx 变量的副本
			如 通过 echo_exec 指令发起内部跳转
```
* [操作](Var-Operation.md)
* [机制](Var-Handle.md)
* 概念
```md
		“变量插值”
			variable interpolation
			"foo: $foo"
			并非所有的配置指令都支持“变量插值”。事实上，指令参数是否允许“变量插值”，取决于该指令的实现模块。
			在“变量插值”的上下文中，还有一种特殊情况，即当引用的变量名之后紧跟着变量名的构成字符时（比如后跟字母、数字以及下划线），我们就需要使用特别的记法来消除歧义
				echo "${first}world";
		“惰性求值”（lazy evaluation）
			只在实际使用对象时才计算对象值的技术
			提供“惰性求值” 语义的编程语言并不多见，最经典的例子便是 Haskell.
			与之相对的便是“主动求值” （eager evaluation）
```