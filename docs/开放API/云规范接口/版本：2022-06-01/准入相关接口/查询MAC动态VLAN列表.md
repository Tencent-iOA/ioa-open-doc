## 1. 接口描述

查询MAC动态VLAN列表，私有化调用path为：capi/inac/DescribeINacMacDynamicVLANs, 从8.7P6版本开始支持

## 2. 输入参数

| 参数名称 | 必选 | 类型 | 描述 |
|---------|---------|---------|---------|
| Condition | 否 | [Condition](/开放API/云规范接口/版本：2022-06-01/数据结构.md#Condition) | <p>条件过滤</p> |

## 3. 输出参数

| 参数名称 | 类型 | 描述 |
|---------|---------|---------|
| Data | [INacMacDynamicVLANsPageData](/开放API/云规范接口/版本：2022-06-01/数据结构.md#INacMacDynamicVLANsPageData) | <p>Mac绑定VLAN分页数据</p>|
| RequestId | String | 唯一请求 ID，由服务端生成，每次请求都会返回（若请求因其他原因未能抵达服务端，则该次请求不会获得 RequestId）。定位问题时需要提供该次请求的 RequestId。|

## 4. 示例

### 示例1 查询所有

#### 输入示例

```
POST / HTTP/1.1
Host: ioa.tencentcloudapi.com
Content-Type: application/json
X-TC-Action: DescribeINacMacDynamicVLANs
<公共请求参数>

{}
```

#### 输出示例

```json
{
    "Response": {
        "RequestId": "built-in-1786412739",
        "Data": {
            "Page": {
                "PageCount": 0,
                "PageSize": 1000,
                "PageNum": 1,
                "Total": 3
            },
            "Items": [
                {
                    "NetType": "办公网",
                    "MachineName": "test",
                    "UpdateDate": "2026-08-11 09:28:57",
                    "CreateDate": "2026-08-07 17:22:54",
                    "Mac": "AA:BB:CC:DD:EE:AG",
                    "UserName": "",
                    "Id": 3
                },
                {
                    "NetType": "办公网",
                    "MachineName": "",
                    "UpdateDate": "2026-08-07 17:22:26",
                    "CreateDate": "2026-08-07 17:22:16",
                    "Mac": "AA:BB:CC:DD:EE:AA",
                    "UserName": "",
                    "Id": 2
                },
                {
                    "NetType": "办公网",
                    "MachineName": "11",
                    "UpdateDate": "2026-08-07 17:14:35",
                    "CreateDate": "2026-08-07 17:14:35",
                    "Mac": "DD:DD:DD:DD:DD:DD",
                    "UserName": "11",
                    "Id": 1
                }
            ]
        }
    }
}
```

### 示例2 查询指定Mac地址

#### 输入示例

```
POST / HTTP/1.1
Host: ioa.tencentcloudapi.com
Content-Type: application/json
X-TC-Action: DescribeINacMacDynamicVLANs
<公共请求参数>

{
  "Condition": {
    "PageNum": 1,
    "PageSize": 10,
    "Filters": [
      {
        "Field": "Mac",
        "Values": [
          "AA:BB:CC:DD:EE:AA"
        ],
        "Operator": "eq"
      }
    ],
    "Sort": {
      "Field": "Mac",
      "Order": "desc"
    }
  }
}
```

#### 输出示例

```json
{
    "Response": {
        "RequestId": "built-in-1786414389",
        "Data": {
            "Items": [
                {
                    "UserName": "",
                    "Mac": "AA:BB:CC:DD:EE:AA",
                    "NetType": "办公网",
                    "CreateDate": "2026-08-07 17:22:16",
                    "MachineName": "",
                    "UpdateDate": "2026-08-07 17:22:26",
                    "Id": 2
                }
            ],
            "Page": {
                "PageCount": 0,
                "PageSize": 10,
                "PageNum": 1,
                "Total": 1
            }
        }
    }
}
```


## 5. 错误码

| 错误码 | 描述 |
|---------|---------|
| InternalError.DatabaseException | 内部错误，数据库异常。 |
| InvalidParameter.RequestParam | 请求参数错误。 |