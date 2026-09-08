## 1. 接口描述

查询某条 DLP 日志内容，私有化调用path为：capi/DLPOpenApi/DescribeDLPLog，从8.6P1版本开始支持

## 2. 输入参数

| 参数名称 | 必选 | 类型 | 描述 |
|---------|---------|---------|---------|
| LogId | 否 | String | 日志ID<br/>DLPAlarmLog-DLP审计/拦截日志、UserLogin-用户登录日志、IAMLogin-IAM登录日志、NGNAccess-终端访问日志、Access-代理访问日志、NGNTicket-NGN小票日志、DynamicAccess-动态访问日志<br/>示例值：DLPAlarmLog |
| Filters.N | 否 | Array of [LogFilter](/开放API/云规范接口/版本：2022-06-01/数据结构.md#LogFilter) | 过滤条件；<li>Field：过滤字段（如 `Body.Guid`、`AuditUUID`）</li><li>Operator：`eq` 等于 / `like` 模糊等于</li><li>Values：过滤值列表</li> |

## 3. 输出参数

| 参数名称 | 类型 | 描述 |
|---------|---------|---------|
| Data | [DescribeDLPLogData](/开放API/云规范接口/版本：2022-06-01/数据结构.md#DescribeDLPLogData) | 业务响应数据<br/>注意：此字段可能返回 null，表示取不到有效值。|
| RequestId | String | 唯一请求 ID，由服务端生成，每次请求都会返回（若请求因其他原因未能抵达服务端，则该次请求不会获得 RequestId）。定位问题时需要提供该次请求的 RequestId。|

## 4. 示例

### 示例1 通过 AuditUUID 查询单条 DLP 日志

#### 输入示例

```
POST / HTTP/1.1
Host: ioa.tencentcloudapi.com
Content-Type: application/json
X-TC-Action: DescribeDLPLog
<公共请求参数>

{
  "LogId": "DLPAlarmLog",
  "Filters": [
    {
      "Field": "AuditUUID",
      "Operator": "eq",
      "Values": ["8366a0d3-a1cf-412a-8201-b88739f93a39"],
      "Describe": "审计UUID"
    }
  ]
}
```

#### 输出示例

```json
{
    "Response": {
        "Data": {
            "Content": "{\"@timestamp\":\"2023-11-23T20:10:22.000+08:00\",\"Body\":{\"Action\":\"FileSend\",\"DataType\":\"DataAudit\",\"FileName\":\"企业微信截图.png\",\"FileMd5\":\"f0cf0a3b458ea57c8bf0cbb9e2a3ac96\"},\"Client\":{\"Account\":\"Bone\"}}"
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
