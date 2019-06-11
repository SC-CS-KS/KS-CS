
```md
	last
		 一旦被当前规则匹配并重写后，立即停止检查后续的其他rewrite的规则
			而后通过重写后的url重新发起请求（如果有多个rewrite规则时，可能会造成死循环）
	break
		一旦被当前规则匹配并重写后，立即停止检查后续的其他rewrite的规则
			而后继续由nginx进行后续的操作（不需要再通过其它的rewrite规则检查 ）
	redirect
		返回302临时重定向代码
	permanent
		返回301永久重定向
	 last 和 break
		last一般写在server和if中，而break一般使用在location中
		last不终止重写后的url匹配，即新的url会再从server走一遍匹配流程，而break终止重写后的匹配
		break和last都能组织继续执行后面的rewrite指令
	注意
		nginx最多循环10次，超出之后返回500错误
		一般将rewrite写在location中时都使用break标志，或者将rewrite写在if上下文中

```