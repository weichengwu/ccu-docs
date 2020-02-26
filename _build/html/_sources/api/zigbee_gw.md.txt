# ZigBee 网关

## 打开组网通道

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

> [!TIP]
> 网关列表通过 `GET_CCU_INFO` 获得。