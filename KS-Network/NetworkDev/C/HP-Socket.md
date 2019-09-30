# [HP-Socket](https://github.com/ldcsaa/HP-Socket)
```md
High Performance Network Framework
是一套通用的高性能 TCP/UDP/HTTP 通信框架
	包含服务端组件、客户端组件和Agent组件
广泛适用于各种不同应用场景的 TCP/UDP/HTTP 通信系统
```
```md
提供 C/C++、C#、Delphi、E（易语言）、Java、Python 等编程语言接口
HP-Socket 对通信层实现完全封装，应用程序不必关注通信层的任何细节
HP-Socket 提供基于事件通知模型的 API 接口，能非常简单高效地整合到新旧应用程序中
```
* 特性
```md
通用性
	唯一职责就是接收和发送字节流，不参与应用程序的协议解析等工作
	与应用程序通过接口进行交互，并完全解耦
易用性
	接口设计得非常简单和统一
	完全封装了所有底层通信细节，应用程序不必也不能干预底层通信操作
	提供 PUSH / PULL / PACK 等接收模型
高性能
	
		Server
			Based on IOCP/EPOLL communication model
		Agent
			Agent组件实质上是Multi-Client组件，与Server组件采用相同的技术架构
		Client
			Based on Event-Select/POLL communication model
伸缩性
	应用程序能够根据不同的容量要求、通信规模和资源状况等现实场景
	调整 HP-Socket 的各项性能参数（如：工作线程的数量、缓存池的大小、发送模式和接收模式等）
	优化资源配置，在满足应用需求的同时不必过度浪费资源
```
* 工作流程
```md
创建监听器对象
创建组件对象（并绑定监听器）
启动组件
连接远程主机（仅用于Agent组件）
处理通信事件（OnConnect/OnReceive/OnClose ......）
停止组件（可选，第7步销毁组件对象前会先停止组件）
销毁组件对象
销毁监听器对象
```
