### License账号授权日志

对应日志报表：License授权日志->License账号授权日志

对应命令字：7257

支持版本：8.2

#### 格式

| 字段名 | 字段类型 | 字段说明 | 取值说明 |
| --- | --- | --- | --- |
| AccountId | int | 用户id | |
| AuthTime | string | 授权时间 | |
| LoginTime | string | 登录时间 | |
| AuthType | string | 授权类型 | |
| AuthMode | string | 授权方式 | |
| Reason | string | 原因 | |
| Modules | other | 授权功能 | |

#### 示例

```json
{
    "AccountId": 1,
    "AuthTime": "2023-09-22 15:01:02",
    "LoginTime": "2023-09-22 15:01:02",
    "AuthType": "授权激活",
    "AuthMode": "手动回收",
    "Reason": "原因",
    "Modules": [{"ModuleKey": "NGN", "ModuleName": "无边界办公"}]
}
```

### License授权日志

对应日志报表：License授权日志->License授权日志

对应命令字：7252

支持版本：8.2+

#### 格式

| 字段名 | 字段类型 | 字段说明 | 取值说明 |
| --- | --- | --- | --- |
| Mid | string | Mid | |
| AuthType | string | 授权类型 | |
| AuthMode | string | 授权方式 | |
| Reason | string | 原因 | |
| AuthTime | string | 授权时间 | |
| Modules | other | 授权功能 | |

#### 示例

```json
{
    "Mid": "abc",
    "AuthType": "授权激活",
    "AuthMode": "手动回收",
    "Reason": "原因",
    "AuthTime": "2023-09-22 15:01:02",
    "Modules": [{"ModuleKey": "NGN", "ModuleName": "无边界办公"}]
}
```


### 终端安全管控授权日志上报

对应日志报表：License授权日志->终端安全管控授权日志

对应命令字：7243

支持版本：SAAS

#### 格式

| 字段名 | 字段类型 | 字段说明 | 取值说明 |
| --- | --- | --- | --- |
| Operation | string | 授权操作 | 激活授权: <br /> 回收授权: <br /> |
| ActivationStatus | string | 激活状态 | 自动激活: <br /> 手动激活: <br /> 自动回收: <br /> 手动回收: <br /> |
| Timestamp | int | 上报时间戳 | |
| Duration | int | 占用时长（s) | |
| Mid | string | 设备ID | |
| DomainID | string | 组织域 ID | |
| UserID | string | 用户账号 | |

#### 示例

```json
{
    "Operation": "激活授权",
    "ActivationStatus": "自动激活",
    "Timestamp": 1654745421,
    "Duration": 100,
    "Mid": "89E2C7642432F54838D25C38D57314F25E2133FA",
    "DomainID": "8",
    "UserID": "用户账号"
}
```

### NGN并发授权日志上报

对应日志报表：License授权日志->NGN并发授权日志

对应命令字：7242

支持版本：SAAS

#### 格式

| 字段名 | 字段类型 | 字段说明 | 取值说明 |
| --- | --- | --- | --- |
| Operation | int | 授权操作 | 1: 激活授权<br /> 2: 更新活跃时间<br /> 3: 回收授权<br /> |
| Result | int | 执行结果 | 1: 成功<br /> 2: 失败<br /> |
| Os | int | 系统平台类型 | 0: win<br /> 1: linux<br /> 2: mac<br /> 4: android<br /> 5: ios<br /> 6: web<br /> |
| Timestamp | int | 上报时间戳 | |
| Mid | string | 设备ID | |
| GroupId | int | 用户分组ID | |
| UserId | string | 用户账号 | |
| Uid | int | 用户唯一ID | |
| TenantId | string | 租户 ID | |

#### 示例

```json
{
    "Operation": 1,
    "Result": 1,
    "Os": 0,
    "Timestamp": 1654745421,
    "Mid": "89E2C7642432F54838D25C38D57314F25E2133FA",
    "GroupId": 999,
    "UserId": "用户账号",
    "Uid": 999,
    "TenantId": ""
}
```