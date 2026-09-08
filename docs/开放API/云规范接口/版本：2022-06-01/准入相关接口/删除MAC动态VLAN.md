## 1. 接口描述

删除MAC动态VLAN，私有化调用path为：capi/inac/DeleteINacMacDynamicVLAN, 从8.7P6版本开始支持

## 2. 输入参数

| 参数名称 | 必选 | 类型 | 描述 |
|---------|--------|---------|---------|
| Ids.N | 否 | Array of Integer | <p>记录ID列表</p><br/>示例值：[1] |
| MacAddresses.N | 否 | Array of String | <p>Mac地址列表</p><br/>示例值：["AA:BB:CC:DD:EE:FF"] |

## 3. 输出参数

| 参数名称 | 类型 | 描述 |
|---------|---------|---------|
| RequestId | String | 唯一请求 ID，由服务端生成，每次请求都会返回（若请求因其他原因未能抵达服务端，则该次请求不会获得 RequestId）。定位问题时需要提供该次请求的 RequestId。|

## 4. 示例

### 示例1 基于Mac地址列表删除

#### 输入示例

```
POST / HTTP/1.1
Host: ioa.tencentcloudapi.com
Content-Type: application/json
X-TC-Action: DeleteINacMacDynamicVLAN
<公共请求参数>

{
  "MacAddresses": [
    "AA:BB:CC:DD:EE:FF"
  ]
}
```

#### 输出示例

```json
{
    "Response": {
        "RequestId": "built-in-1786414640"
    }
}
```

### 示例2 基于Mac绑定VLAN记录ID删除

#### 输入示例

```
POST / HTTP/1.1
Host: ioa.tencentcloudapi.com
Content-Type: application/json
X-TC-Action: DeleteINacMacDynamicVLAN
<公共请求参数>

{
  "Ids": [
    1
  ]
}
```

#### 输出示例

```json
{
  "Response": {
    "RequestId": "built-in-1786414640"
  }
}
```


## 5. 错误码

| 错误码 | 描述 |
|---------|---------|
| InternalError.DatabaseException | 内部错误，数据库异常。 |
| InvalidParameter.RequestParam | 请求参数错误。 |