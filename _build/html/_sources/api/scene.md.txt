# 情景模式

## 执行情景模式

<!-- tabs:start -->

#### ** 请求 **

```json
{
    "nodeid": 1,
    "opcode": "SWITCH",
    "arg": "ON",
    "requester": "HJ_Profile"
}
```

`arg` 固定取 `ON`

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

## 新建情景模式

<!-- tabs:start -->

#### ** 请求 **

```json
{
    "arg": {
        "scene_type": "1",
        "name": "聚会模式",
        "room_id": 0
    },
    "nodeid": "*",
    "opcode": "ADD_SCENE",
    "requester": "HJ_Config"
}
```

`arg` 内字段说明：

* scene_type：情景模式类型，详情请见附录，可以随意设置一个值
* name：情景模式名称
* room_id：房间 id，如果没有房间业务，则可以设置为 0

#### ** 响应 **

```json
{
    "nodeid": "*",
    "opcode": "ADD_SCENE",
    "arg": 1,
    "status": "success"
}
```

`arg` 为新建的情景模式的 id

<!-- tabs:end -->

## 修改情景模式

<!-- tabs:start -->

#### ** 请求 **

```json
{
    "arg": {
        "scene_type": "1",
        "name": "回家模式",
        "room_id": 0
    },
    "nodeid": 1,
    "opcode": "UPDATE_SCENE",
    "requester": "HJ_Config"
}
```

`arg` 参数与新建情景模式相同

#### ** 响应 **

```json
{
    "nodeid": 1,
    "opcode": "UPDATE_SCENE",
    "arg": "*",
    "status": "success"
}
```

<!-- tabs:end -->

## 删除情景模式

<!-- tabs:start -->

#### ** 请求 **

```json
{
    "nodeid": 1,
    "opcode": "DELETE_SCENE",
    "arg": "*",
    "requester": "HJ_Config"
}
```

#### ** 响应 **

```json
{
    "nodeid": 1,
    "opcode": "DELETE_SCENE",
    "arg": "*",
    "status": "success"
}
```

<!-- tabs:end -->

## 修改情景模式的动作

情景模式的动作是与设备强关联的，每个动作的执行者都是设备，所以动作内的参数都是从对应的设备中获得的。

<!-- tabs:start -->

#### ** 请求 **

```json
{
    "nodeid": 1,
    "opcode": "SET_SCENE_ACTIONS",
    "arg": {
        "actions": []
    },
    "requester": "HJ_Config"
}
```

actions 格式请见附录：同步和新设备数据

#### ** 响应 **

```json
{
    "nodeid": 1,
    "opcode": "SET_SCENE_ACTIONS",
    "arg": "*",
    "status": "success"
}
```

<!-- tabs:end -->

## 设置情景模式定时器

<!-- tabs:start -->

#### ** 请求 **

```json
{
    "nodeid": 1,
    "opcode": "SET_TIMER",
    "arg": [
        {
            "enable": 1,
            "week": "1,2,3",
            "time": "10:23:00"
        }
    ],
    "requester": "HJ_Profile"
}
```

* enable：使用标记。1：启用。0：禁用。
* time：执行时间。格式：`hh:mm:ss`。
* week：周重复周期。格式采用 `,` 分割。例如：`1,2,3,4`。

#### ** 响应 **

```json
{
    "nodeid": 1,
    "opcode": "SET_TIMER",
    "arg": "*",
    "status": 2
}
```

<!-- tabs:end -->