# 灯光类设备

## 开关

<!-- tabs:start -->

#### ** 请求 **

```json
{
    "nodeid": 1,
    "opcode": "SWITCH",
    "arg": "ON",
    "requester": "HJ_Server"
}
```

`arg` 说明：

* `ON`：开
* `OFF`：关

#### ** 响应 **

```json
{
    "nodeid": 1,
    "opcode": "SWITCH",
    "arg": "ON",
    "status": "success"
}
```

`arg` 与请求相同

<!-- tabs:end -->