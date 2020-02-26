# 同步和新设备数据

以下所有数据都在同步报文和新设备报文两个协议中。

## 设备信息

所处位置：

* 同步：`devices`
* 新设备：`new_devices`

格式：

```json
{
    "device_field": "灯光",
    "device_field_index": "",
    "device_icon": "",
    "device_pos": "",
    "mac": "",
    "name": "",
    "nodeid": "1",
    "operate_type": "1",
    "room_id": "-1",
    "gw_mac": "",
    "channel": "1"
}
```

* device_field：设备类别。格式为字符串
* device_field_index：弃用，格式为字符串
* device_icon：设备图标，格式为字符串
* device_pos：弃用，格式为字符串
* mac：设备节点 MAC 地址，格式为字符串
* gw_mac：设备节点归属网关 MAC 地址，格式为字符串
* channel：设备通道，格式字符串
* name：设备名称，格式为字符串
* nodeid：设备 ID，格式为字符串
* operate_type：设备类型，格式为字符串
* room_id：设备归属房间，格式字符串

`device_field` 目前支持的取值范围：

* 灯光
* 遥控器
* 窗帘
* 插座
* 情景
* 空调面板
* 传感器
* 智能门锁
* 安防设备

## 设备状态

所处位置：

* 同步：`device_status`
* 新设备：无

格式：

```json
{
    "arg": "ON",
    "nodeid": 1,
    "opcode": "SWITCH"
}
```

nodeid 对应的设备的 operate_type 不同，即设备类型不同，那么对应的 arg 和 opcode 也是不同的，详细格式参考附录：设备状态信息。

## 情景模式

所处位置：

* 同步：`scenes`
* 新设备：无

```json
{
    "actions": [
        {
            "area": "",
            "name": "",
            "room_id": -1,
            "nodeid": 1,
            "operate_type": 1,
            "delay": 0,
            "operation": "开"
        }
    ],
    "id": "4",
    "name": "离家",
    "pannel_id": "*",
    "room_id": "0",
    "scene_image": "scene_leave",
    "scene_type": "6",
    "time": "",
    "timer_enable": "0",
    "week": ""
}
```

* area: 设备位置，一般用空字符串
* name: 设备名称
* room_id: 设备所在房间
* nodeid: 设备id
* operate_type: 设备类型
* delay: 动作延时，单位：秒
* operation: 动作，所有支持的动作请参考附录
* timer_enable：是否启用定时器。1：启用。0：禁用。
* time：执行时间。格式：`hh:mm:ss`。
* week：周重复周期。格式采用 `,` 分割。例如：`1,2,3,4`。

