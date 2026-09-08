## 1. 接口描述

DLP 日志导出任务（大数据量异步），超过最大下载日志数据限制时走异步任务下载；与 data-mgr/log-center 老接口请求参数保持一致；当前 LogId 仅支持 `DLPAlarmLog`（DLP 审计/拦截日志）。私有化调用path为：`capi/DlpOpenApi/CreateDLPLogDownloadTask`，从 2026-06-22 版本开始支持。

任务成功创建后由服务端异步处理并生成下载文件，请前往日志中心「日志下载任务列表」查看进度并获取下载链接。若数据量较小，可使用同步接口 [DLP日志导出URL](/开放API/云规范接口/版本：2022-06-01/数据安全中心相关接口/DLP日志导出URL.md)。

## 2. 输入参数

| 参数名称 | 必选 | 类型 | 描述 |
|---------|---------|---------|---------|
| LogId | 是 | String | 日志ID，当前仅支持 `DLPAlarmLog`<br/>示例值：DLPAlarmLog |
| StartTime | 是 | Integer | 开始时间（Unix 时间戳，秒）<br/>示例值：1700668800 |
| EndTime | 是 | Integer | 结束时间（Unix 时间戳，秒；必须大于 StartTime）<br/>示例值：1700755199 |
| Department | 否 | Integer | 用户分组ID<br/>示例值：0 |
| EndpointGroup | 否 | Integer | 终端分组ID<br/>示例值：0 |
| Sort | 否 | [LogSort](/开放API/云规范接口/版本：2022-06-01/数据结构.md#LogSort) | 排序参数；<li>Field：排序字段（如 `@timestamp`）</li><li>Order：`desc` / `asc`</li> |
| Filters.N | 否 | Array of [DLPLogDownloadFilterItem](/开放API/云规范接口/版本：2022-06-01/数据结构.md#DLPLogDownloadFilterItem) | 过滤条件；<li>Field：过滤字段（如 `Body.DataType`、`Body.InterceptStatus`、`Client.Account`）</li><li>Operator：`eq` 等于 / `like` 模糊等于 / `not` 不等于</li><li>Values：过滤值列表</li> |
| Fields | 否 | Map of String→String | 导出字段映射，`key` 为英文字段名，`value` 为中文表头。<br/>示例值：{"Body.FileName":"文件名","Body.FileMd5":"文件MD5","Body.DataLevel":"数据级别"} |
| LogDownloadFields.N | 否 | Array of String | 导出字段列表，元素格式支持 `field` 或 `field:label`（形如 `field:label` 时自动写入 Fields）<br/>示例值：["Body.FileName:文件名","Body.FileMd5:文件MD5"] |
| OsType | 否 | Integer | 终端类型（0: win，1：linux，2: mac，3: win_srv，4：android，5：ios）<br/>示例值：0 |
| UserName | 否 | String | 用户名（私有化场景作为 Owner 使用，SAAS 场景留空走 SubAccountUin）<br/>示例值：admin |

## 3. 输出参数

| 参数名称 | 类型 | 描述 |
|---------|---------|---------|
| Data | [CreateDLPLogDownloadTaskData](/开放API/云规范接口/版本：2022-06-01/数据结构.md#CreateDLPLogDownloadTaskData) | 业务响应数据<br/>注意：此字段可能返回 null，表示取不到有效值。|
| RequestId | String | 唯一请求 ID，由服务端生成，每次请求都会返回（若请求因其他原因未能抵达服务端，则该次请求不会获得 RequestId）。定位问题时需要提供该次请求的 RequestId。|

## 4. 示例

### 示例1 创建DLP审计日志异步导出任务

#### 输入示例

```
POST / HTTP/1.1
Host: ioa.tencentcloudapi.com
Content-Type: application/json
X-TC-Action: CreateDLPLogDownloadTask
<公共请求参数>

{
  "LogId": "DLPAlarmLog",
  "StartTime": 1700668800,
  "EndTime": 1700755199,
  "Filters": [
    {
      "Field": "Body.InterceptLog",  // 0: 拦截日志，1: 审计日志
      "Operator": "eq",
      "Values": ["0"],
      "Describe": "审计类型"
    }
  ],
  "Sort": {
    "Field": "@timestamp",
    "Order": "desc"
  },
  "LogDownloadFields": [
    "Body.FileName:文件名",
    "Body.FileMd5:文件MD5",
    "Body.DataLevel:数据级别",
    "Body.RiskChan:风险通道",
    "Client.Account:账号",
    "Client.Ip:终端IP"
  ],
  "UserName": "admin"
}
```

#### 输出示例

```json
{
    "Response": {
        "Data": {
            "Message": "任务已创建，可到日志下载任务列表查看进度"
        },
        "RequestId": "b8f67971-f7dd-41a8-a42f-caee1df373d9"
    }
}
```

### 示例2 创建DLP拦截日志异步导出任务

#### 输入示例

```
POST / HTTP/1.1
Host: ioa.tencentcloudapi.com
Content-Type: application/json
X-TC-Action: CreateDLPLogDownloadTask
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
  "Fields": {
    "Body.FileName": "文件名",
    "Body.RiskChan": "风险通道",
    "Client.Account": "账号"
  },
  "UserName": "admin"
}
```

#### 输出示例

```json
{
    "Response": {
        "Data": {
            "Message": "任务已创建，可到日志下载任务列表查看进度"
        },
        "RequestId": "b8f67971-f7dd-41a8-a42f-caee1df373d9"
    }
}
```


## 5. 错误码

| 错误码 | 描述 |
|---------|---------|
| FailedOperation.DataTooLarge | 数据量过大，请缩小查询范围。 |
| FailedOperation.QueryData | 查询数据失败。 |
| InternalError.DatabaseException | 内部错误，数据库异常。 |
| InternalError.Unknown | 内部未知错误。 |
| InvalidParameter.InvalidParameter | 参数无效。 |
| InvalidParameter.ParameterValidationFailed | 参数校验失败。 |
| InvalidParameter.RequestParam | 请求参数错误。 |
| MissingParameter.CommonParam | 缺少公共参数。 |
| ResourceNotFound.NotFound | 资源不存在。 |
| UnauthorizedOperation.PermissionDenied | 未授权的操作。 |
