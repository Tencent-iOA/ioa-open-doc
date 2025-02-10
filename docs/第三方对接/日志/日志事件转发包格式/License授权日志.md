### License终端授权日志

对应控制台页面：事件中心->日志审计->License授权日志->License终端授权日志

对应命令字：7252

支持版本：8.2+

#### 格式

| 字段名 | 字段类型 | 字段说明 | 取值说明 |
| --- | --- | --- | --- |
| Mid | string | 设备唯一标识码 | 示例：6B854AB1C430826AECFD44CF0148BD6F67A97320 |
| AuthType | string | 授权类型 | 授权激活、授权回收 |
| AuthMode | string | 授权方式 | 自动激活、验证激活、审核激活、自动回收、手动回收 |
| Reason | string | 原因 | 暂无需关注 |
| AuthTime | string | 触发时间 | 示例：2025-02-10 12:12:55 |
| Modules | json list | 表具体哪些模块发生了授权变更 | ModuleKey是产品内置不会被修改，ModuleName是方便人识别，名称可能会被调整。取值的所有可能映射关系为：<br/>ModuleKey：MODULE_NGN，ModuleName：无边界接入(NGN)<br/>ModuleKey：MODULE_INAC，ModuleName：安全准入<br/>ModuleKey：MODULE_SECURITY，ModuleName：终端安全<br/>ModuleKey：MODULE_CONTROL，ModuleName：终端管控<br/>ModuleKey：MODULE_SECURITY_REINFORCEMENT，ModuleName：Win7遁甲<br/>ModuleKey：MODULE_SOFTWARE_MANAGEMENT，ModuleName：企业版软件管家<br/>ModuleKey：MODULE_WATERMARK，ModuleName：水印保护<br/>ModuleKey：MODULE_EDR，ModuleName：终端检测与响应(EDR)<br/>ModuleKey：MODULE_REMOTE_DESKTOP，ModuleName：远程桌面<br/>ModuleKey：MODULE_SAAS_QYWX_DLP，ModuleName：SaaS企微数据安全（DLP）<br/>ModuleKey：MODULE_EDLP，ModuleName：终端数据安全(DLP)<br/> |

#### 示例

```json
{
    "_type": "Event_7252",
    "recvTime": "2025-02-10T12:12:57+08:00",
    "sender": {
        "_type": "",
        "mid": "",
        "publicIP": "",
        "clientVersion": "",
        "client": null,
        "src": null
    },
    "args": {
        "AuthMode": "验证激活",
        "AuthTime": "2025-02-10 12:12:55",
        "AuthType": "授权激活",
        "Mid": "6B854AB1C430826AECFD44CF0148BD6F67A97320",
        "Modules": [
            {
                "ModuleKey": "MODULE_NGN",
                "ModuleName": "无边界接入(NGN)"
            }
        ],
        "Reason": ""
    }
}
```

### License并发授权日志

对应控制台页面：事件中心->日志审计->License授权日志->License并发授权日志

对应命令字：7257

支持版本：8.2

#### 格式
| 字段名 | 字段类型 | 字段说明 | 取值说明 |
| --- | --- | --- | --- |
| AccountId | int | 账号唯一ID，在iOA账号体系里，唯一标识一个账号，控制台不可见，对应的是底层数据库表的自增ID | 示例：1 |
| LoginTime | string | 废弃无用 | 暂无需关注 |
| Mid | string | 设备唯一标识码 | 示例：6B854AB1C430826AECFD44CF0148BD6F67A97320 |
| AuthType | string | 授权类型 | 授权激活、授权回收 |
| AuthMode | string | 授权方式 | 自动激活、验证激活、审核激活、自动回收、手动回收 |
| Reason | string | 原因 | 暂无需关注 |
| AuthTime | string | 触发时间 | 示例：2025-02-10 12:12:55 |
| Modules | json list | 表具体哪些模块发生了授权变更 | ModuleKey是产品内置不会被修改，ModuleName是方便人识别，名称可能会被调整。取值的所有可能映射关系为：<br/>ModuleKey：MODULE_NGN，ModuleName：无边界接入(NGN)<br/>ModuleKey：MODULE_INAC，ModuleName：安全准入<br/>ModuleKey：MODULE_SECURITY，ModuleName：终端安全<br/>ModuleKey：MODULE_CONTROL，ModuleName：终端管控<br/>ModuleKey：MODULE_SECURITY_REINFORCEMENT，ModuleName：Win7遁甲<br/>ModuleKey：MODULE_SOFTWARE_MANAGEMENT，ModuleName：企业版软件管家<br/>ModuleKey：MODULE_WATERMARK，ModuleName：水印保护<br/>ModuleKey：MODULE_EDR，ModuleName：终端检测与响应(EDR)<br/>ModuleKey：MODULE_REMOTE_DESKTOP，ModuleName：远程桌面<br/>ModuleKey：MODULE_SAAS_QYWX_DLP，ModuleName：SaaS企微数据安全（DLP）<br/>ModuleKey：MODULE_EDLP，ModuleName：终端数据安全(DLP)<br/> |

#### 示例

```json
{
    "_type": "Event_7257",
    "recvTime": "2023-09-22T15:01:02+08:00",
    "sender": {
        "_type": "",
        "mid": "",
        "publicIP": "",
        "clientVersion": "",
        "client": null,
        "src": null
    },
    "args": {
		"AccountId": 1,
        "AuthMode": "验证激活",
        "AuthTime": "2023-09-22 15:01:02",
        "AuthType": "授权激活",
        "Mid": "6B854AB1C430826AECFD44CF0148BD6F67A97320",
        "Modules": [
            {
                "ModuleKey": "MODULE_NGN",
                "ModuleName": "无边界接入(NGN)"
            }
        ],
        "Reason": ""
    }
}
```

### License账号授权日志

对应控制台页面：事件中心->日志审计->License授权日志->License账号授权日志

对应命令字：7268

支持版本：8.5+

#### 格式
| 字段名 | 字段类型 | 字段说明 | 取值说明 |
| --- | --- | --- | --- |
| Uid | int | 账号唯一ID，在iOA账号体系里，唯一标识一个账号，控制台不可见，对应的是底层数据库表的自增ID | 示例：1 |
| AuthType | string | 授权类型 | 授权激活、授权回收 |
| AuthMode | string | 授权方式 | 自动激活、验证激活、审核激活、自动回收、手动回收 |
| AuthTime | string | 触发时间 | 示例：2025-02-10 12:12:55 |
| Modules | json list | 表具体哪些模块发生了授权变更 | ModuleKey是产品内置不会被修改，ModuleName是方便人识别，名称可能会被调整。取值的所有可能映射关系为：<br/>ModuleKey：MODULE_NGN，ModuleName：无边界接入(NGN)<br/>ModuleKey：MODULE_INAC，ModuleName：安全准入<br/>ModuleKey：MODULE_SECURITY，ModuleName：终端安全<br/>ModuleKey：MODULE_CONTROL，ModuleName：终端管控<br/>ModuleKey：MODULE_SECURITY_REINFORCEMENT，ModuleName：Win7遁甲<br/>ModuleKey：MODULE_SOFTWARE_MANAGEMENT，ModuleName：企业版软件管家<br/>ModuleKey：MODULE_WATERMARK，ModuleName：水印保护<br/>ModuleKey：MODULE_EDR，ModuleName：终端检测与响应(EDR)<br/>ModuleKey：MODULE_REMOTE_DESKTOP，ModuleName：远程桌面<br/>ModuleKey：MODULE_SAAS_QYWX_DLP，ModuleName：SaaS企微数据安全（DLP）<br/>ModuleKey：MODULE_EDLP，ModuleName：终端数据安全(DLP)<br/> |

#### 示例

```json
{
    "_type": "Event_7268",
    "recvTime": "2023-09-22T15:01:02+08:00",
    "sender": {
        "_type": "",
        "mid": "",
        "publicIP": "",
        "clientVersion": "",
        "client": null,
        "src": null
    },
    "args": {
		"Uid": 1,
		"AuthType": "授权激活",
		"AuthMode": "手动回收",
		"AuthTime": "2023-09-22 15:01:02",
		"Modules": [{"ModuleKey": "NGN", "ModuleName": "无边界办公"}]
	}
}
```
