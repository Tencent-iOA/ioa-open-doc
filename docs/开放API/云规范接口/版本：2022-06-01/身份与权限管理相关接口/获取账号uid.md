## 1. 接口描述

获取账号uid：/capi/Assets/Account/DescribeUid

注意：参数Data最长为5000个，超过5000被抛出参数错误

## 2. 输入参数


| 参数名称 | 必选 | 类型           | 描述                           |
|------|----|--------------|------------------------------|
| Data | 是  | Object Array | 要查询的账号userId、分组id的集合,详细字段见示例 |

## 3. 输出参数

| 参数名称      | 类型            | 描述                 |
|-----------|---------------|--------------------|
| Items     | Object Array  | 查询到的账号信息集合,详细字段见示例 | 

## 4. 示例

### 示例1 normal

#### 输入示例

POST / HTTP/1.1
Host: ioa.tencentcloudapi.com
Content-Type: application/json
X-TC-Action: DescribeLocalAccounts
```json
{
  "Data":[
      {"UserId":"huangfan1","GroupId":2},
      {"UserId":"huangfan11","GroupId":3}
    ]
}
```

#### 输出示例

```json
{
  "Response": {
    "RequestId": "billfhuang-postman-test",
    "Data": [
      {
        "GroupId": 2,
        "UserId": "huangfan1",
        "Uid": 1
      },
      {
        "GroupId": 3,
        "UserId": "huangfan11",
        "Uid": 2
      }
    ]
  }
}
```

## 5. 错误码


| 错误码 | 描述 |
|---------|---------|
| InternalError.DatabaseException | 内部错误，数据库异常。 |
| InvalidParameter.RequestParam | 请求参数错误。 |
