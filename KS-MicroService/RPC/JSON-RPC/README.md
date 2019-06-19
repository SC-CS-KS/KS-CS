# [JSON-RPC](http://wiki.geekdream.com/Specification/json-rpc_2.0.html)
```md
是一个无状态且轻量级的远程过程调用(RPC)协议

通信协议采用二进制方式
序列化采用JSON的形式
```

## Implement

* [toa-net](https://github.com/toajs/toa-net)
```md
JSON-RPC 2.0 client/server over TCP net.

特征
使用JSON-RPC 2.0规范作为RPC协议。
使用RESP（Redis序列化协议）或MsgP（字节消息协议）作为消息协议。
使用JSON Web签名作为身份验证协议。
实施ES6 Iterable协议。
```
