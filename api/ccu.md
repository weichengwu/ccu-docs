# 操作主机

## 发现主机

用于客户端发现所在局域网内已联网的中控主机，获取中控主机的基本信息。

客户端采用中控发现链路发送发现报文。

<!-- tabs:start -->

#### ** 请求 **

```json
{
    "nodeid": "*",
    "opcode": "FIND_CCU",
    "arg": "*",
    "requester": "HJ_CCU"
}
```

#### ** 响应 **

```json
{
    "nodeid": "*",
    "opcode": "FIND_CCU",
    "arg": {
        "zkid": "00162",
        "zk": "162主机",
        "ip": "192.168.0.5",
        "ssl": true
    },
    "status": "success"
}
```

arg 内参数说明：

* zkid：主机 ID
* zk：主机名称
* ip：主机在局域网内的 IP 地址
* ssl：是否支持 SSL 连接

<!-- tabs:end -->

## 登录主机

客户端和中控主机建立 TCP 连接后发送登录报文。

<!-- tabs:start -->

#### ** 请求 **

```json
{
    "arg": {
        "device": "iOS-xxxxxxx",
        "seq": "1",
        "zkid": "00018",
        "version": "1.0",
        "username": "admin",
        "password": "admin"
    },
    "nodeid": "*",
    "opcode": "LOGIN",
    "requester": "HJ_Server"
}
```

* device: 客户端型号
* seq: 登录序列号，可以用随机数
* zkid: 主机id
* version: 客户端版本号
* username: 固定 "admin"
* password: 固定 "admin"

#### ** 响应 **

```json
{
    "arg": {
        "error_code": 0,
        "seq": "1"
    },
    "nodeid": "*",
    "opcode": "LOGIN",
    "status": "success"
}
```

* error_code: 登录错误码，详情请见附录。

<!-- tabs:end -->

## 同步数据

客户端通过认证后，需主机进行同步数据。

同步信息包含，设备信息，区域信息，情景模式信息，规则信息，主机基本信息，状态信息等所有相关信息。

<!-- tabs:start -->

#### ** 请求 **

```json
{
    "nodeid": "*",
    "opcode": "SYNC_INFO",
    "arg": "*",
    "requester": "HJ_Config"
}
```

#### ** 响应 **

```json
{
    "arg": {
        "guard": {
            "arming_status": "1",
            "guard_sensors": [
                {
                    "nodeid": "1",
                    "sensor_type": "2"
                }
            ]
        },
        "scenes": [
            {
                "id": "4",
                "name": "离家",
                "time": "19:00:00",
                "timer_enable": "0",
                "week": "1,2,3",
                "actions": [
                    {
                        "name": "客厅灯",
                        "nodeid": 1,
                        "operate_type": 1,
                        "delay": 0,
                        "operation": "开"
                    }
                ]
            }
        ],
        "group": [
            {
                "id": 1,
                "name": 2,
                "nodes": [
                    {
                        "nodeid": 3
                    }
                ]
            }
        ]
    },
    "nodeid": "*",
    "opcode": "SYNC_INFO",
    "status": " success"
}
```

* guard：主机安防信息
  * arming_status：安防状态 (1)离家布防 (2)撤防 (3)在家布防
  * guard_sensors：安防类传感器列表，数组类型
    * nodeid：传感器的设备 id
    * sensor_type：传感器类型，(1)在家安防传感器 (2)室外安防传感器 (3)24小时安防传感器 (4)24小时不告警传感器
* scenes：情景模式列表
  * time：定时执行时间，格式 `HH:mm:ss`
  * timer_enable：定时器开关
  * week：重复周期，使用半角逗号分割，`1` 代表星期一，以此类推
  * actions：动作列表
    * name：关联设备的名称
    * nodeid：关联设备的 id
    * operate_type：关联设备的类型
    * delay：延时执行，相对于情景模式开始执行，单位：秒
    * operation：动作，全部设备支持的动作见附录
* group：多控列表
  * nodes：多控关联动作列表
    * nodeid：关联设备的 id

<!-- tabs:end -->

## 主机心跳

客户端定期发送心跳请求报文到中控，识别维护 TCP 链路状态。

<!-- tabs:start -->

#### ** 请求 **

```json
{
    "nodeid": "*",
    "opcode": "CCU_HB",
    "arg": "*",
    "requester": "HJ_Server"
}
```

#### ** 响应 **

```json
{
    "nodeid": "*",
    "opcode": "CCU_HB",
    "arg": "*",
    "status": "success"
}
```

<!-- tabs:end -->

## 查询主机内 ZigBee 设备的硬件信息

<!-- tabs:start -->

#### ** 请求 **

```json
{
    "nodeid": "*",
    "opcode": "GET_ZIGBEE_DEVS_HW_INFO",
    "arg": {
        "conditions": [
            {
                "condition_type": "dev_list",
                "condition_arg": [
                    "00:12:4B:00:04:3F:AD:91"
                ]
            }
        ]
    },
    "requester": "HJ_Config"
}
```

arg 内字段说明：

* conditions：查询过滤条件，如果为 `[]`，则表示查询主机内所有 ZigBee 设备的硬件信息。

conditions 内字段说明：

* 当 `condition_type` == `dev_list` 时，`condition_arg` 表示要查询的所有 ZigBee 设备的 Mac 地址
* 目前 `condition_type` 仅支持 `dev_list` 一种情况
* 注意 `conditions` 是一个数组

#### ** 响应 **

```json
{
    "nodeid": "*",
    "opcode": "GET_ZIGBEE_DEVS_HW_INFO",
    "arg": [
        {
            "mac": "00:12:4B:00:04:3F:AD:91",
            "version": "",
            "product_id": -1,
            "online_status": 0
        }
    ],
    "status": "success"
}
```

arg 内字段说明（arg 为数组）：

* mac：设备 Mac 地址
* version：设备版本信息，空表示未获取到
* product_id：设备产品 ID
* online_status：设备在线状态。0：未知，1：在线，2：离线

<!-- tabs:end -->

## 新设备数据

<!-- tabs:start -->

#### ** 推送 **

```json
{
    "arg": {
        "new_device_count": 0,
        "new_devices": [],
        "new_hue_lights_count": 0,
        "new_hue_lights": [],
        "new_ipc_count": 0,
        "new_ipcs": [],
        "new_konke_count": 0,
        "new_konke_sockets": [],
        "new_konke_lights_count": 0,
        "new_konke_lights": [],
        "new_cnwise_music_controllers_count": 0,
        "new_cnwise_music_controllers": [],
        "new_modbus_devs_count": 0,
        "new_modbus_devs": [],
        "new_modbus_daikin_indoorunits_count": 0,
        "new_modbus_daikin_indoorunits": [],
        "new_konke_humidifiers_count": 0,
        "new_konke_humidifiers": [],
        "new_konke_aircleaners_count": 0,
        "new_konke_aircleaners": [],
        "new_central_ac_gws_count": 0,
        "new_central_ac_gws": [],
        "new_central_ac_indoorunits_count": 0,
        "new_central_ac_indoorunits": [],
        "new_youzhuan_music_controllers_count": 0,
        "new_youzhuan_music_controllers": []
    },
    "nodeid": "*",
    "opcode": "NEW_DEVICES",
    "status": "success"
}
```

字段详细说明请参考附录：同步和新设备数据说明

<!-- tabs:end -->

## 获取中控主机基本信息

<!-- tabs:start -->

#### ** 请求 **

```json
{
    "nodeid": "*",
    "opcode": "GET_CCU_INFO",
    "arg": "*",
    "requester": "HJ_Server"
}
```

#### ** 响应 **

```json
{
    "arg": {
        "local_ip": "192.168.0.5",
        "wan_status": 1,
        "cloud_status": 1,
        "gw_list": [
            {
                "gw_nodeid": "1",
                "gw_name": "内置网关",
                "gw_mac": "00:FF",
                "gw_ip": "127.0.0.1",
                "gw_link": 1,
                "gw_type": "1",
                "run_version": "1.1.2",
                "download_version": "1.1.3"
            }
        ]
    },
    "nodeid": "*",
    "opcode": "GET_CCU_INFO",
    "status": "success"
}
```

* local_ip：主机 ip
* wan_status：(0)不能访问外网 (1)能访问外网
* cloud_status：(0)与云平台断开连接 (1)与云平台连接正常
* gw_list：网关列表
  * gw_nodeid：网关 id
  * gw_name：网关名称
  * gw_mac：网关 mac
  * gw_ip：网关 ip
  * gw_link：(0)网关离线 (1)网关在线
  * gw_type：网关类型，(0)udp 网关 (1)tcp 网关 (2)串口一体化网关 (3)POE 网关 (4)9531 网关
  * run_version：当前运行的版本
  * download_version：已下载到本地的版本

<!-- tabs:end -->