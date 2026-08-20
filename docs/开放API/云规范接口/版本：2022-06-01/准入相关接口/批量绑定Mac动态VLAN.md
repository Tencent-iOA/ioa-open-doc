## 1. 接口描述

绑定MAC动态VLAN，私有化调用path为：capi/inac/BindINacMacDynamicVLANs, 从8.7P6版本开始支持

## 2. 输入参数

| 参数名称 | 必选 | 类型 | 描述 |
|---------|---------|---------|---------|
| Items.N | 是 | Array of [MacDynamicVLANData](/开放API/云规范接口/版本：2022-06-01/数据结构.md#MacDynamicVLANData) | <p>MAC动态VLAN数据列表</p> |

## 3. 输出参数

| 参数名称 | 类型 | 描述 |
|---------|---------|---------|
| RequestId | String | 唯一请求 ID，由服务端生成，每次请求都会返回（若请求因其他原因未能抵达服务端，则该次请求不会获得 RequestId）。定位问题时需要提供该次请求的 RequestId。|

## 4. 示例

### 示例1 批量Mac绑定VLAN

绑定成功

#### 输入示例

```
POST / HTTP/1.1
Host: ioa.tencentcloudapi.com
Content-Type: application/json
X-TC-Action: BindINacMacDynamicVLANs
<公共请求参数>

{
  "Items": [
    {
      "Mac": "aa:bb:cc:dd:ee:ag",
      "NetType": "办公网",
      "MachineName": "test"
    },
    {
      "Mac": "AA:CC:cc:dd:ee:ag",
      "NetType": "研发网",
      "MachineName": "test"
    }
  ]
}
```

#### 输出示例

```json
{
    "Response": {
        "RequestId": "built-in-1786411737"
    }
}
```

### 示例2 绑定失败

#### 输入示例

```
POST / HTTP/1.1
Host: ioa.tencentcloudapi.com
Content-Type: application/json
X-TC-Action: BindINacMacDynamicVLANs
<公共请求参数>

{
  "Items": [
    {
      "Mac": "aa:bb:cc:dd",
      "NetType": "办公网",
      "MachineName": "test"
    }
  ]
}
```

#### 输出示例

```json
{
    "Response": {
        "Error": {
            "Message": "无效的MAC地址。",
            "Code": "InvalidParameter.InvalidMacAddress"
        },
        "RequestId": "built-in-1786411154024"
    }
}
```


## 5. 错误码

| 错误码 | 描述 |
|---------|---------|
| InternalError.DatabaseException | 内部错误，数据库异常。 |
| InvalidParameter.InvalidMacAddress | 无效的MAC地址。 |
| InvalidParameter.NetTypeNotExist | 网络类型不存在。 |
| InvalidParameter.RequestParam | 请求参数错误。 |