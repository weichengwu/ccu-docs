# ZigBee 设备通用

## 设备入网推送

<!-- tabs:start -->

#### ** 推送 **

```json
{
    "arg": {
        "mac": "00:15:8D:00:01:17:48:97",
        "productId": "-1"
    },
    "opcode": "ZIGBEE_DEV_JOIN_NOTIFY",
    "nodeid": "*",
    "status": "success"
}
```

arg 内字段解释：

* mac: 设备 mac 地址
* productId：产品 ID

<!-- tabs:end -->