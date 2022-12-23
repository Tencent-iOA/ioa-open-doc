## 1. 接口描述




添加多个准入MAC白名单

<div class="rno-api-explorer">
    <div class="rno-api-explorer-inner">
        <div class="rno-api-explorer-hd">
            <div class="rno-api-explorer-title">
            </div>
        </div>
        <div class="rno-api-explorer-body">
            <div class="rno-api-explorer-cont">
            </div>
        </div>
    </div>
</div>

## 2. 输入参数


| 参数名称 | 必选 | 类型 | 描述 |
|---------|---------|---------|---------|
| MacWhites.N | 否 | Array of [MacWhite](/开放API/云规范接口/版本：2022-06-01/数据结构.md#MacWhite) | 白名单列表 |

## 3. 输出参数

| 参数名称 | 类型 | 描述 |
|---------|---------|---------|
| RequestId | String | 唯一请求 ID，每次请求都会返回。定位问题时需要提供该次请求的 RequestId。|

## 4. 示例












## 5. 错误码


| 错误码 | 描述 |
|---------|---------|
| InternalError.DatabaseException | InternalError.DatabaseException |
| InvalidParameter.InvalidDateFormat | InvalidParameter.InvalidDateFormat |
| InvalidParameter.InvalidMacAddress | InvalidParameter.InvalidMacAddress |
| InvalidParameter.RequestParam | 缺少请求参数。 |
