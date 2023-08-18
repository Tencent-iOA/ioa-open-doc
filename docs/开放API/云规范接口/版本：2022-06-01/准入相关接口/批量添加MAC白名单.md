## 1. 接口描述




添加多个准入MAC白名单，私有化调用path为：capi/inac/CreateBatchMacWhite

## 2. 输入参数


| 参数名称 | 必选 | 类型 | 描述 |
|---------|---------|---------|---------|
| MacWhites.N | 否 | Array of [MacWhites](/开放API/云规范接口/版本：2022-06-01/数据结构.md#MacWhites) | <strong><font color="blue"></font></strong>白名单列表<br/>示例值：{“Mac”:"AA:AA:AA:CC:CC:CC"} |

## 3. 输出参数

| 参数名称 | 类型 | 描述 |
|---------|---------|---------|
| RequestId | String | 唯一请求 ID，每次请求都会返回。定位问题时需要提供该次请求的 RequestId。|

## 4. 示例












## 5. 错误码


| 错误码 | 描述 |
|---------|---------|
| InternalError.DatabaseException | 内部错误，数据库异常。 |
| InvalidParameter.InvalidDateFormat | 日期格式无效。 |
| InvalidParameter.InvalidMacAddress | 无效的MAC地址。 |
| InvalidParameter.RequestParam | 请求参数错误。 |
