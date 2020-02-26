# 多控

## 添加/编辑多控

<!-- tabs:start -->

#### ** 请求 **

```json
{
    "nodeid": "*",
    "opcode": "SET_GROUP",
    "arg": {
        "id": 1,
        "nodes": [
            {
                "nodeid": 1
            }
        ]
    },
    "requester": "HJ_Config"
}
```

如果中控内不存在 id 为 1 的多控，则创建一个新的多控，如果存在，则编辑这个多控。

客户端在新建之前需要先查询中控内所有的多控，将 id+1 后调用该接口。

* nodes: 多控内设备 id 列表，目前仅支持：灯光面板、调光灯、窗帘三种设备，不同类型的设备不要混用。

#### ** 响应 **

```json
{
    "nodeid": "*",
    "opcode": "SET_GROUP",
    "arg": {
        "id": 1,
        "nodes": [
            {
                "nodeid": 1
            }
        ]
    },
    "status": "success"
}
```

<!-- tabs:end -->

## 删除多控

<!-- tabs:start -->

#### ** 请求 **

```json
{
    "nodeid": "*",
    "opcode": "DELETE_GROUP",
    "arg": "1",
    "requester": "HJ_Config"
}
```

arg 为要删除的多控的 id

#### ** 响应 **

```json
{
    "nodeid": "*",
    "opcode": "DELETE _GROUP",
    "arg": 1,
    "status": "success"
}
```

<!-- tabs:end -->