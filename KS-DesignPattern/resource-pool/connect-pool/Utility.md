
* 端上的连接池
```md
		由于互联网尤其是广域网中的速度非可控性
		特别是移动互联网（基于3G／4G）的速度的不确定性
			在端上的应用也将连接池作为一种重要的技术手段
	
		以Chrome浏览器为例
			其网络库采取连接池的方式管理连接的建立、分配以及释放
			当请求可以直接从连接池中获取复用连接时，可以减少建立连接的时间消耗
			打开chrome://net-internals/#sockets 可以看到浏览器当前的连接状态。
		在app中，连接池同样被广泛采用
			流的网络通信库都支持连接池，例如Okhttp
		平台层也是如此，例如Android 平台中的binder 连接池
```
```md
类型
		websoket连接池
		TransportClientSocketPool
		SSLClientSocketPool
		SOCKSClientSocketPool
```