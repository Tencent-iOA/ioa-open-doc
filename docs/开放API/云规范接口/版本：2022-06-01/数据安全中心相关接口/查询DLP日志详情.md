## 1. 接口描述

DLP 日志详情查询（支持审计日志、拦截日志等），私有化调用path为：capi/DLPOpenApi/DescribeDLPLogDetail，从8.6P1版本开始支持。

审计日志、拦截日志均通过 `LogId=DLPAlarmLog` 查询，并可通过 `Filters` 中 `Body.InterceptStatus` 或 `Body.DataType` 字段区分审计（`DataAudit`）与拦截（`DataIntercept`）。

## 2. 输入参数

| 参数名称 | 必选 | 类型 | 描述 |
|---------|---------|---------|---------|
| LogId | 是 | String | 日志ID<br/>DLPAlarmLog-DLP审计/拦截日志、UserLogin-用户登录日志、IAMLogin-IAM登录日志、NGNAccess-终端访问日志、Access-代理访问日志、NGNTicket-NGN小票日志、DynamicAccess-动态访问日志<br/>示例值：DLPAlarmLog |
| StartTime | 是 | Integer | 开始时间（Unix时间戳，秒）<br/>示例值：1700668800 |
| EndTime | 是 | Integer | 结束时间（Unix时间戳，秒；必须大于 StartTime）<br/>示例值：1700755199 |
| Filters.N | 否 | Array of [LogFilter](/开放API/云规范接口/版本：2022-06-01/数据结构.md#LogFilter) | 过滤条件；<li>Field：过滤字段（如 `Body.DataType`、`Body.InterceptStatus`、`Client.Account`）</li><li>Operator：`eq` 等于 / `like` 模糊等于</li><li>Values：过滤值列表</li> |
| OsType | 否 | Integer | 终端类型（0: win，1：linux，2: mac，3: win_srv，4：android，5：ios）<br/>示例值：0 |
| Department | 否 | Integer | 用户分组ID<br/>示例值：0 |
| EndpointGroup | 否 | Integer | 终端分组ID<br/>示例值：0 |
| Sort | 否 | [LogSort](/开放API/云规范接口/版本：2022-06-01/数据结构.md#LogSort) | 排序参数；<li>Field：排序字段（如 `@timestamp`）</li><li>Order：`desc` / `asc`</li> |
| PageNumber | 是 | Integer | 页码（从0开始）<br/>示例值：0 |
| PageSize | 是 | Integer | 每页数目<br/>示例值：10 |

## 3. 输出参数

| 参数名称 | 类型 | 描述 |
|---------|---------|---------|
| Data | [DescribeDLPLogDetailData](/开放API/云规范接口/版本：2022-06-01/数据结构.md#DescribeDLPLogDetailData) | 业务响应数据<br/>注意：此字段可能返回 null，表示取不到有效值。|
| RequestId | String | 唯一请求 ID，由服务端生成，每次请求都会返回（若请求因其他原因未能抵达服务端，则该次请求不会获得 RequestId）。定位问题时需要提供该次请求的 RequestId。|

## 4. 示例

### 示例1 查询审计日志列表

#### 输入示例

```
POST / HTTP/1.1
Host: ioa.tencentcloudapi.com
Content-Type: application/json
X-TC-Action: DescribeDLPLogDetail
<公共请求参数>

{
  "LogId": "DLPAlarmLog",
  "StartTime": 1700668800,
  "EndTime": 1700755199,
  "Filters": [
    {
      "Field": "Body.DataType",
      "Operator": "eq",
      "Values": ["DataAudit"],
      "Describe": "审计类型"
    }
  ],
  "Sort": {
    "Field": "@timestamp",
    "Order": "desc"
  },
  "PageNumber": 0,
  "PageSize": 1
}
```

#### 输出示例

```json
{
    "Response": {
        "Data": {
            "Total": 1469,
            "Data": [
                "{\"@timestamp\":\"2023-11-23T20:10:22.000+08:00\",\"Body\":{\"Action\":\"FileSend\",\"DataLevel\":\"S6\",\"DataType\":\"DataAudit\",\"FileName\":\"企业微信截图_17007034431454.png\",\"FileMd5\":\"f0cf0a3b458ea57c8bf0cbb9e2a3ac96\",\"FileSize\":3047,\"FileType\":\".png\",\"Intercept\":0,\"InterceptStatus\":0,\"OperateTime\":\"2023-11-23 20:10:22\",\"RiskChan\":\"wxwork\",\"RiskType\":\"FileLeak\"},\"Client\":{\"Account\":\"Bone\",\"Ip\":\"119.147.10.191\",\"Mac\":\"80:E8:2C:E3:E4:73\",\"Name\":\"LEIFHUANG-PC\",\"OSType\":0},\"TenantId\":\"1300056258\"}"
            ]
        },
        "RequestId": "b8f67971-f7dd-41a8-a42f-caee1df373d9"
    }
}
```

### 示例2 查询拦截日志列表

#### 输入示例

```
POST / HTTP/1.1
Host: ioa.tencentcloudapi.com
Content-Type: application/json
X-TC-Action: DescribeDLPLogDetail
<公共请求参数>

{
  "LogId": "DLPAlarmLog",
  "StartTime": 1700668800,
  "EndTime": 1700755199,
  "Filters": [
    {
      "Field": "Body.InterceptStatus",
      "Operator": "eq",
      "Values": ["1"],
      "Describe": "拦截状态"
    }
  ],
  "Sort": {
    "Field": "@timestamp",
    "Order": "desc"
  },
  "PageNumber": 0,
  "PageSize": 10
}
```

#### 输出示例

```json
{
    "Response": {
        "Data": {
            "Total": 25,
            "Data": [
                "{\"@timestamp\":\"2023-11-23T21:05:11.000+08:00\",\"Body\":{\"Action\":\"FileSend\",\"DataType\":\"DataIntercept\",\"Intercept\":1,\"InterceptStatus\":1}}"
            ]
        },
        "RequestId": "b8f67971-f7dd-41a8-a42f-caee1df373d9"
    }
}
```


## 5. 错误码

| 错误码 | 描述 |
|---------|---------|
| FailedOperation.QueryData | 查询数据失败。 |
| InternalError.DatabaseException | 内部错误，数据库异常。 |
| InternalError.Unknown | 内部未知错误。 |
| InvalidParameter.InvalidParameter | 参数无效。 |
| InvalidParameter.ParameterValidationFailed | 参数校验失败。 |
| InvalidParameter.RequestParam | 请求参数错误。 |
| MissingParameter.CommonParam | 缺少公共参数。 |
| ResourceNotFound.NotFound | 资源不存在。 |
| UnauthorizedOperation.PermissionDenied | 未授权的操作。 |
