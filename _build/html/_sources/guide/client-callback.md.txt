# 回调处理

回调是指客户端上层的业务逻辑，用户执行一个操作，发送请求报文之后，等待对应的响应报文到达时，上层该做什么逻辑。最好的做法是将客户端上层传递进来的回调，以某种形式缓存起来。

与 HTTP 请求不同，TCP 的读写是分开在不同的方法里的。

* 请求：TCP Socket 写数据
* 响应：TCP Socket 读数据

这里还用打开组网通道的报文举例：

<!-- tabs:start -->

#### ** 请求 **

```json
{
    "reqId": "xxx",
    "nodeid": 1,
    "opcode": "OPEN_NET_CHANNEL",
    "arg": "*",
    "requester": "HJ_Server"
}
```

#### ** 响应 **

```json
{
    "reqId": "xxx",
    "nodeid": 1,
    "opcode": "OPEN_NET_CHANNEL",
    "arg": "*",
    "status": "success"
}
```

<!-- tabs:end -->

观察报文结构得知：

* 请求和反馈的 `reqId` 为相同的，但并不是所有的协议均支持 `reqId`，所有场景覆盖不全
* 请求和反馈的 `nodeid` 和 `opcode` 是相同的，除登录主机报文之外，其他所有的协议均是如此

于是可以封装一个指纹对象，构造方法接收 `reqId`、`nodeid`、`opcode` 三个参数，再根据语言特性，重写指纹对象的相关方法，使其可以作为 Map 的键，这样即可将请求和响应对应上了。下面是伪代码：

```
// 声明
Map map; // 用于缓存回调
Request req; // 请求，根据中控协议和对应的请求参数进行构造
Response resp; // 响应，根据中控协议和响应报文进行构造
Callback callback; // 回调，上层传入

// 缓存
map[req.fingerprint] = callback; // req.fingerprint 为 Request 的快捷方法，生成一个指纹对象

// 提取
Callback callback = map[resp.fingerprint];

// 执行
callback();
```