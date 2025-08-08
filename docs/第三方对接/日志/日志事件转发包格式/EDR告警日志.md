### 高级威胁防护告警日志上报

对应命令字：7510

支持版本：8.2

#### 格式

| 字段名 | 字段类型 | 字段说明 | 取值说明 |
| --- | --- | --- | --- |
|EventId |int64 |告警ID（7日内重复告警使用相同的ID） | |
|EventName |string |告警名称 | |
|EventNameEN |string |告警名称英文 | |
|IOAAccount |string |企业账号 | |
|AttackSummary |string |告警攻击摘要 | |
|OccurTime |int64 |发生时间戳（毫秒） | |
|EngineName |string |引擎名称 |CloudEngine:云引擎 <br>GraphEngine:关联图引擎<br>IocEngine:威胁情报<br>TavEngine:TAV引擎 |
|PolicyName |string |触发策略名称 | |
|PolicyDescription |string |触发策略描述 | |
|PolicyNameEN |string |触发策略名称英文 | |
|PolicyDescriptionEN |string |触发策略描述英文 | |
|RiskLevel |int32 |风险等级 |1:低危<br>2:中危<br>3:高危 |
|AttackTech |[]string |ATT&CK战技术编号 |参见：https://attack.mitre.org/ |
|Mid |string |终端mid | |
|TerminalName |string |终端名称 | |
|OnlineStatus |int32 |在线状态 |1:离线<br>2:在线<br>3:未授权 |
|Ostype |int32 |终端系统类型 |0:windows<br>1:linux<br>2:macOS<br>3:windows server<br>4:android<br>5:iOS |
|Source |string |告警源节点 | |
|Target |string |告警目标节点 | |
|ActionType |string |动作类型 |见7520采集日志动作类型取值范围 |
|ActionName |string |动作名称 |见7520采集日志子动作名称取值范围 |
|IncidentUuid |string |事件聚合的唯一ID | |
|OriginLog |map |原始上报日志（详见7520高级威胁防护采集日志上报） | |

#### 示例

```json
{
    "_type": "Event_7510",
    "recvTime": "2023-12-18T23:26:11+08:00",
    "sender": {
        "_type": "Terminal",
        "mid": "",
        "publicIP": "",
        "clientVersion": "0.0.0.0",
        "client": {
            "IpPort": "",
            "Mid": "",
            "Guid": "",
            "Mac": "",
            "Name": "",
            "User": "",
            "OSType": 0,
            "OS": "",
            "GroupIDPath": "",
            "GroupNamePath": "",
            "Account": "",
            "Version": 0,
            "GroupId": 0,
            "GroupName": "",
            "AccountGroupId": 0,
            "AccountName": "",
            "AccountGroupName": "",
            "AccountGroupIdPath": "",
            "AccountGroupNamePath": "",
            "AccountVirtualGroupId": 0,
            "AccountVirtualGroupName": ""
        },
        "src": null
    },
    "args": {
        "ActionName": "ProcessCreate",
        "ActionType": "Proc",
        "AttackSummary": "\"kylinssoclient (deleted)\"进程 创建 \"ping\"进程",
        "AttackTech": [
            "TA0007",
            "TA0006"
        ],
        "EngineName": "GraphEngine",
        "EventId": 1367,
        "EventName": "测试linux告警ping",
        "IOAAccount": "testing",
        "Mid": "0000000000000000000000000000000000000000",
        "OccurTime": 1702913084087,
        "OnlineStatus": 2,
        "OriginLog": {
            "@collection": "2023-12-18T23:24:44.087+08:00",
            "@timestamp": "2023-12-18T23:24:59.982462743+08:00",
            "Action": {
                "Name": "ProcessCreate",
                "NodeMergeId": "/usr/sbin/kylinssoclient (deleted)_aaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaa_processcreate_/usr/bin/ping_0aef4d6aec3105d4461445da130adc47",
                "Type": "Proc"
            },
            "Alert": {
                "ActionShow": "ProcessCreate",
                "AlertSource": "",
                "BlockType": "",
                "ChildShow": "ping",
                "CloudEngineName": "",
                "CloudRuleId": 0,
                "CloudTitle": "",
                "EngineName": "GraphEngine",
                "EventUuid": "",
                "FixResult": "",
                "ParentShow": "kylinssoclient (deleted)",
                "RuleId": 0,
                "RuleName": "",
                "RuleNature": ""
            },
            "Child": {
                "CallStack": "",
                "CloudAttr": "Unknown",
                "FileAccessTime": 0,
                "FileCompany": "",
                "FileCopyright": "",
                "FileCreateTime": 0,
                "FileDesc": "",
                "FileDriverType": "",
                "FileFormat": "SO",
                "FileIssuer": "",
                "FileLegalMark": "",
                "FileMd5": "0aef4d6aec3105d4461445da130adc47",
                "FileMd5Type": "FullMd5",
                "FileModifyTime": 1580425883,
                "FileName": "ping",
                "FileOriginalName": "",
                "FilePath": "/usr/bin/ping",
                "FileProductName": "",
                "FileProductVer": "",
                "FileSign": "",
                "FileSignStatus": "",
                "FileSignWhite": 0,
                "FileSize": 72776,
                "FileStream": "",
                "FileTags": "",
                "FileVersion": "",
                "ProcArch": "",
                "ProcChainInfo": "kylinssoclient (deleted)_Trust_1814",
                "ProcChainTrust": "Trust",
                "ProcCmdline": "/usr/bin/ping 8.8.8.8 -c1",
                "ProcCmdline-raw": "",
                "ProcCpuArch": "amd64",
                "ProcCurDir": "",
                "ProcDesktop": "",
                "ProcDomainName": "",
                "ProcElevationType": 0,
                "ProcExited": false,
                "ProcGuid": "9045350895302169775",
                "ProcIntegrity": 0,
                "ProcPid": 2970799,
                "ProcTrust": "Trust",
                "ProcUserName": "",
                "ScanAttr": "Unknown",
                "ScriptContent": "",
                "ThreadId": 0,
                "TrojanName": "",
                "Type": "Proc"
            },
            "Common": {
                "AuthId": 0,
                "ClientVer": "",
                "DeviceGroup": "全网终端.未分组终端",
                "EventId": 28246,
                "EventTime": 1702913084087,
                "EventUUId": "bf81027b-82a3-4b6b-9bea-6ef96b2fb65c",
                "Guid": "",
                "KernelId": 0,
                "LoginStatus": 2,
                "Mid": "0000000000000000000000000000000000000000",
                "MonitorName": "",
                "ReportId": 5058,
                "SessionId": 15,
                "Source": "",
                "Uid": 0,
                "UserName": "testing"
            },
            "Environment": {
                "DomainName": "",
                "ExportIp": "",
                "HostName": "testing-VMware-Virtual-Platform",
                "MacAddr": "00-0c-29-7e-9c-ee",
                "OsBit": "64",
                "OsBuild": 0,
                "OsProduectDesc": "",
                "OsType": "Linux",
                "OsUserName": "testing",
                "OsVersion": "Kylin V10 SP1",
                "SysStartTimes": 1702348874000
            },
            "Event": {
                "AttackTech": "TA0007,TA0006",
                "EngineName": "GraphEngine",
                "EventId": 1367,
                "EventName": "测试linux告警ping",
                "RiskLevel": 2
            },
            "OS": "1",
            "Parent": {
                "CloudAttr": "",
                "FileAccessTime": 0,
                "FileCompany": "",
                "FileCopyright": "",
                "FileCreateTime": 0,
                "FileDesc": "",
                "FileDriverType": "",
                "FileFormat": "",
                "FileIssuer": "",
                "FileLegalMark": "",
                "FileMd5": "AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA",
                "FileMd5Type": "FullMd5",
                "FileModifyTime": 0,
                "FileName": "kylinssoclient (deleted)",
                "FileOriginalName": "",
                "FilePath": "/usr/sbin/kylinssoclient (deleted)",
                "FileProductName": "",
                "FileProductVer": "",
                "FileSign": "",
                "FileSignStatus": "",
                "FileSignWhite": 0,
                "FileSize": 0,
                "FileTags": "",
                "FileVersion": "",
                "ProcArch": "",
                "ProcChainGuid": "8930008985805848577,6622091318409560065",
                "ProcChainInfo": "",
                "ProcChainTrust": "Trust",
                "ProcCmdline": "/usr/sbin/kylinssoclient",
                "ProcCmdline-raw": "",
                "ProcCpuArch": "amd64",
                "ProcDomainName": "",
                "ProcElevationType": 0,
                "ProcExited": false,
                "ProcGuid": "8930009183374346006",
                "ProcIntegrity": 0,
                "ProcPid": 1814,
                "ProcTrust": "Trust",
                "ProcUserName": "",
                "ScanAttr": "Unknown",
                "ThreadId": 0,
                "TrojanName": "",
                "Type": "Proc"
            },
            "Uuid": "33078ed407575b8490fee13bafc1c923_28246",
            "Version": 1,
            "_id": "uTeHfYwBTDbys-ncyP_P"
        },
        "Ostype": 0,
        "PolicyDescription": "testing配置的",
        "PolicyName": "测试linux告警ping",
        "RiskLevel": 2,
        "Source": "\"kylinssoclient (deleted)\"",
        "Target": "\"ping\"",
        "TerminalName": "testing-VMware-Virtual-Platform"
    }
}
```

### 高级威胁防护聚合事件日志上报

对应命令字：7511

支持版本：8.7

#### 格式

| 字段名 | 字段类型 | 字段说明 | 取值说明 |
| --- | --- | --- | --- |
|Uuid |string |事件唯一ID | |
|IsNew |bool |是否新事件 | |
|MergeUuids |[]string |聚合子事件的唯一ID | |
|IncidentName |string |事件名称 | |
|IncidentNameEN |string |事件名称英文 | |
|RiskLevel |int32 |风险等级 |1:低危<br>2:中危<br>3:高危 |
|AttackTech |[]string |ATT&CK战术编号 |参见：https://attack.mitre.org/ |
|AttckSubTech |[]string |ATT&CK技术编号 |参见：https://attack.mitre.org/ |
|FirstTime |datetime |首次发生时间 | |
|LastTime |datetime |末次发生时间戳 | |
|EventTotal |int64 |包含告警数量 | |
|TerminalTotal |int64 |包含终端数量 | |
|EvidenceTotal |int64 |包含证据数量 | |
|UserTotal |int64 |包含用户数量 | |
|IncidentNature |int32 |事件性质 |0:ATT&CK基础事件<br>1:精准事件 |
|Ostype |[]int32 |系统类型 |0:windows<br>1:linux<br>2:macOS<br>3:windows server<br>4:android<br>5:iOS |

#### 示例

```json
{
    "_type": "Event_7511",
    "recvTime": "2025-01-01T23:26:11+08:00",
    "sender": {
        "_type": "Terminal",
        "mid": "",
        "publicIP": "",
        "clientVersion": "0.0.0.0",
        "client": {
            "IpPort": "",
            "Mid": "",
            "Guid": "",
            "Mac": "",
            "Name": "",
            "User": "",
            "OSType": 0,
            "OS": "",
            "GroupIDPath": "",
            "GroupNamePath": "",
            "Account": "",
            "Version": 0,
            "GroupId": 0,
            "GroupName": "",
            "AccountGroupId": 0,
            "AccountName": "",
            "AccountGroupName": "",
            "AccountGroupIdPath": "",
            "AccountGroupNamePath": "",
            "AccountVirtualGroupId": 0,
            "AccountVirtualGroupName": ""
        },
        "src": null
    },
    "args": {
        "Uuid": "f846c3ba-c9b2-4744-bcb4-cabd0a7a80ef",
        "IsNew": true,
        "MergeUuids": [
            "053e8688-a510-452d-b397-ffbf49222090",
            "94ed3113-5df0-40ba-8f03-514d036754e5"
        ],
        "IncidentName": "PC-0001 '权限提升'攻击",
        "IncidentNameEN": "PC-0001 'Privilege Escalation' Attack",
        "RiskLevel": 1,
        "AttckTech": [
            "TA0004"
        ],
        "AttckSubTech": [
            "TA0004.001"
        ],
        "FirstTime": "2025-08-08T11:20:22.579711+08:00",
        "LastTime": "2025-08-08T11:20:22.579711+08:00",
        "EventTotal": 4,
        "TerminalTotal": 2,
        "UserTotal": 2,
        "EvidenceTotal": 10,
        "IncidentNature": 0,
        "Ostype": [
            0
        ]
    }
}
```


### 高级威胁防护采集日志上报

对应命令字：7520

支持版本：7.5

#### 格式

| id | 名称 | 类型 | 字段说明 | 取值说明 |
| :--- | :--- | :--- | :--- | :--- |
| 1 | OS | int | 系统平台 | 0: Windows<br/>1: Linux<br/>2: macOS |
| 2 | Uuid | string | 唯一ID |  |
| 3 | @collection | datetime | 采集时间 |  |
| 4 | @timestamp | datetime | 入库时间 |  |
| 5 | Action | object | 动作信息 |  |
| 6 | Action.Type | string | 事件动作类型 | :  |
| 7 | Action.Name | string | 事件动作名称 | :  |
| 8 | Action.EventLogId | int | Windows日志ID |  |
| 9 | PParent | object | 操作者父信息 |  |
| 10 | PParent.CloudAttr | string | 云查属性 | Black: 黑\(Black\)<br/>Gray: 灰\(Gray\)<br/>Unknown: 未知\(Unknown\)<br/>White: 安全\(White\) |
| 11 | PParent.FilePath | string | 文件路径 |  |
| 12 | PParent.FileMd5 | string | 文件md5 |  |
| 13 | PParent.FileMd5Type | string | 文件md5类型 | FullMd5: 全文<br/>HalfMd5: 半文 |
| 14 | PParent.FileSign | string | 文件签名 |  |
| 15 | PParent.FileSignStatus | string | 文件签名状态 | Expired: 签名过期<br/>Invalid: 验证不通过<br/>Valid: 验证通过 |
| 16 | PParent.FileSignWhite | int | 是否白签名 | 0: 不是<br/>1: 是 |
| 17 | PParent.FileTags | string | 文件标签 | Browser: 浏览器渠道<br/>Browser:114高速浏览器: 114高速浏览器下载<br/>Browser:115极速浏览器: 115极速浏览器下载<br/>Browser:115浏览器: 115浏览器下载<br/>Browser:2345加速浏览器: 2345加速浏览器下载<br/>Browser:2345智能浏览器: 2345智能浏览器下载<br/>Browser:360安全浏览器: 360安全浏览器下载<br/>Browser:360极速浏览器: 360极速浏览器下载<br/>Browser:Edge浏览器: Edge浏览器下载<br/>Browser:GreenBrowser: GreenBrowser下载<br/>Browser:GT游戏浏览器: GT游戏浏览器下载<br/>Browser:hao123桔子浏览器: hao123桔子浏览器下载<br/>Browser:IE浏览器: IE浏览器下载<br/>Browser:iQ浏览器: iQ浏览器下载<br/>Browser:KR浏览器: KR浏览器下载<br/>Browser:MyIE浏览器: MyIE浏览器下载<br/>Browser:Opera: Opera下载<br/>Browser:QQ浏览器: QQ浏览器下载<br/>Browser:Safari浏览器: Safari浏览器下载<br/>BrowserSoft: 浏览器软件<br/>Browser:Spartan浏览器: Spartan浏览器下载<br/>Browser:TT浏览器: TT浏览器下载<br/>Browser:UC浏览器: UC浏览器下载<br/>Browser:YY浏览器: YY浏览器下载<br/>Browser:世界之窗浏览器: 世界之窗浏览器下载<br/>Browser:世界之窗浏览器极速版: 世界之窗浏览器极速版下载<br/>Browser:傲游浏览器: 傲游浏览器下载<br/>Browser:搜狗浏览器: 搜狗浏览器下载<br/>Browser:淘宝浏览器: 淘宝浏览器下载<br/>Browser:火狐浏览器: 火狐浏览器下载<br/>Browser:猎豹浏览器: 猎豹浏览器下载<br/>Browser:瑞影浏览器: 瑞影浏览器下载<br/>Browser:百度浏览器: 百度浏览器下载<br/>Browser:百度浏览器hao123专版: 百度浏览器hao123专版下载<br/>Browser:糖果浏览器: 糖果浏览器下载<br/>Browser:花儿世界浏览器: 花儿世界浏览器下载<br/>Browser:谷歌浏览器: 谷歌浏览器下载<br/>Browser:超速浏览器: 超速浏览器下载<br/>Browser:闪游浏览器: 闪游浏览器下载<br/>Browser:随E浏览器: 随E浏览器下载<br/>Browser:青猴浏览器: 青猴浏览器下载<br/>ChildNode: 操作目标<br/>DllHijack: DLL劫持<br/>Downloader: 下载器渠道<br/>Downloader:BitComet: BitComet下载<br/>Downloader:IDMan: IDMan下载<br/>Downloader:QQ旋风: QQ旋风下载<br/>Downloader:QQ旋风下载助手: QQ旋风下载助手下载<br/>Downloader:RaySource: RaySource下载<br/>DownloaderSoft: 下载软件<br/>Downloader:旋风高速下载引擎: 旋风高速下载<br/>Downloader:比特彗星: 比特彗星下载<br/>Downloader:电驴: 电驴下载<br/>Downloader:百度下载助手: 百度下载助手下载<br/>Downloader:百度云管家: 百度云管家下载<br/>Downloader:网际快车: 网际快车下载<br/>Downloader:网页迅雷: 网页迅雷下载<br/>Downloader:迅雷: 迅雷下载<br/>Downloader:迅雷云加速: 迅雷云加速下载<br/>Downloader:迅雷精简版: 迅雷精简版下载<br/>Downloader:迅雷迷你版: 迅雷迷你版下载<br/>Downloader:迷你快车: 迷你快车下载<br/>Downloader:迷你电驴: 迷你电驴下载<br/>Downloader:飞鸟下载器: 飞鸟下载器下载<br/>IM: IM渠道<br/>IM:FSLink: FSLink下载<br/>IM:MSN: MSN下载<br/>IM:Skype: Skype下载<br/>IMSoft: IM软件<br/>IM:YY语音: YY语音下载<br/>IM:京东咚咚: 京东咚咚下载<br/>IM:企业微信: 企业微信下载<br/>IM:微信: 微信下载<br/>IM:易信: 易信下载<br/>IM:润工作: 润工作下载<br/>IM:环信: 环信下载<br/>IM:百度Hi: 百度Hi下载<br/>IM:百度Hi: 百度Hi下载<br/>IM:网易CC语音: 网易CC语音下载<br/>IM:网易云信: 网易云信下载<br/>IM:腾讯QQ: 腾讯QQ下载<br/>IM:腾讯TM: 腾讯TM下载<br/>IM:腾讯通\(RTX\): 腾讯通\(RTX\)下载<br/>IM:钉钉: 钉钉下载<br/>IM:阿里旺旺: 阿里旺旺下载<br/>IM:飞书: 飞书下载<br/>IM:飞信: 飞信下载<br/>InjectProc: 进程注入<br/>Mail: 邮箱渠道<br/>Mail:139邮箱: 139邮箱下载<br/>Mail:Foxmail: Foxmail下载<br/>Mail:PP助手: OutLook下载<br/>MailSoft: 邮箱软件<br/>Mail:新浪邮箱: 新浪邮箱下载<br/>Mail:网易邮箱: 网易邮箱下载<br/>Mail:阿里邮箱: 阿里邮箱下载<br/>NetDisk: 网盘渠道<br/>NetDisk:115网盘: 115网盘下载<br/>NetDisk:360云盘: 360云盘下载<br/>NetDisk:360网盘: 360网盘下载<br/>NetDiskSoft: 网盘软件<br/>NetDisk:优蛋: 优蛋下载<br/>NetDisk:华为网盘: 华为网盘下载<br/>NetDisk:坚果云: 坚果云下载<br/>NetDisk:城通网盘: 城通网盘下载<br/>NetDisk:天翼云盘: 天翼云盘下载<br/>NetDisk:夸克网盘: 夸克网盘下载<br/>NetDisk:微云: 微云下载<br/>NetDisk:微盘: 微盘下载<br/>NetDisk:百度网盘: 百度网盘下载<br/>NetDisk:纳米盘: 纳米盘下载<br/>NetDisk:酷盘: 酷盘下载<br/>NetDisk:金山快盘: 金山快盘下载<br/>NetDisk:阿里云盘: 阿里云盘下载<br/>NetShare: 网络共享渠道<br/>NewFile: 新入文件<br/>NewFileExec: 新入执行<br/>NewFileInject: 新入注入<br/>NewSuspicious: 新入可疑<br/>ParentNode: 操作者<br/>SoftMgr: 软件管理渠道<br/>SoftMgr:2345软件管家: 2345软件管家下载<br/>SoftMgr:360安全卫士: 360安全卫士下载<br/>SoftMgr:360驱动大师: 360驱动大师下载<br/>SoftMgr:91手机助手: 91手机助手下载<br/>SoftMgr:PP助手: PP助手下载<br/>SoftMgrSoft: 软件管理软件<br/>SoftMgr:天极软件管家: 天极软件管家下载<br/>SoftMgr:微软电脑管家: 微软电脑管家下载<br/>SoftMgr:搜狗手机助手: 搜狗手机助手下载<br/>SoftMgr:爱思助手: 爱思助手下载<br/>SoftMgr:联想电脑管家: 联想电脑管家下载<br/>SoftMgr:腾讯电脑管家: 腾讯电脑管家下载<br/>SoftMgr:豌豆荚2: 豌豆荚2下载<br/>SoftMgr:软媒魔方软件管理: 软媒魔方软件管理下载<br/>SoftMgr:金山手机助手: 金山手机助手下载<br/>SoftMgr:金山毒霸: 金山毒霸下载<br/>SoftMgr:风灵软件管家: 风灵软件管家下载<br/>SoftMgr:驱动人生: 驱动人生下载<br/>SoftMgr:驱动人生软件管理: 驱动人生软件管理下载<br/>SoftMgr:驱动精灵: 驱动精灵下载<br/>TrustSource: 可信进程释放<br/>UnknownSource: 未知进程释放 |
| 18 | PParent.ProcPid | int | 进程Pid |  |
| 19 | PParent.ProcCmdline | string | 进程命令行 |  |
| 20 | PParent.ProcGuid | string | 进程唯一ID |  |
| 21 | Parent | object | 操作者信息 |  |
| 22 | Parent.ProcPid | int | 进程Pid |  |
| 23 | Parent.ProcCmdline | string | 进程命令行 |  |
| 24 | Parent.FileName | string | 文件名 |  |
| 25 | Parent.FilePath | string | 文件路径 |  |
| 26 | Parent.FileDriverType | string | 驱动器类型 | CDRom: CD光盘<br/>Fixed: 硬盘<br/>NoRootDir: 非驱动<br/>Ramdisk: 内存磁盘<br/>Remote: 网络驱动器<br/>Removeable: 可移动介质<br/>Unknown: 未知 |
| 27 | Parent.FileMd5 | string | 文件md5 |  |
| 28 | Parent.CloudAttr | string | 云查属性 | Black: 黑\(Black\)<br/>Gray: 灰\(Gray\)<br/>Unknown: 未知\(Unknown\)<br/>White: 安全\(White\) |
| 29 | Parent.Type | string | 节点类型 | ApiCall: 系統API<br/>File: 文件<br/>FileStatics: 文件统计<br/>Log: 日志<br/>Network: 网络<br/>Pipe: 管道<br/>Pipe: 管道<br/>Proc: 进程<br/>Reg: 注册表<br/>Script: 脚本 |
| 30 | Parent.NodeName | string | 节点名称 |  |
| 31 | Parent.ProcGuid | string | 进程唯一ID |  |
| 32 | Parent.ProcIntegrity | int | 进程完整性级别 | 1: 不可信<br/>2: 低<br/>3: 中<br/>4: 中+<br/>5: 高<br/>6: 系统<br/>7: 保护进程 |
| 33 | Parent.ProcElevationType | int | 进程提权类型 | 1: UAC关闭<br/>2: UAC提权<br/>3: UAC限制权限 |
| 34 | Parent.ProcUserName | string | 进程用户名 |  |
| 35 | Parent.ProcDomainName | string | 进程用户域名 |  |
| 36 | Parent.ProcArch | string | 进程架构 | x64: x64<br/>x86: x86 |
| 37 | Parent.ProcTrust | string | 进程可信 | NoTrust: 不可信<br/>Trust: 可信 |
| 38 | Parent.ProcChainTrust | string | 进程链可信 | NoTrust: 不可信<br/>Trust: 可信 |
| 39 | Parent.ProcChainInfo | string | 进程链详情 |  |
| 40 | Parent.FileFormat | string | 文件类型 | DLL: 动态链接库<br/>EXE: 可执行EXE<br/>NPE: 非PE<br/>SYS: 驱动<br/>Unknown: 未知格式 |
| 41 | Parent.FileMd5Type | string | 文件md5类型 | FullMd5: 全文<br/>HalfMd5: 半文 |
| 42 | Parent.FileSize | int | 文件大小 |  |
| 43 | Parent.FileSign | string | 文件签名 |  |
| 44 | Parent.FileSignStatus | string | 文件签名状态 | Expired: 签名过期<br/>Invalid: 验证不通过<br/>Valid: 验证通过 |
| 45 | Parent.FileSignWhite | int | 是否白签名 | 0: 不是<br/>1: 是 |
| 46 | Parent.FileIssuer | string | 签名颁发机构 |  |
| 47 | Parent.FileCompany | string | 文件公司名 |  |
| 48 | Parent.FileDesc | string | 文件描述 |  |
| 49 | Parent.FileVersion | string | 文件版本 |  |
| 50 | Parent.FileOriginalName | string | 原始文件名 |  |
| 51 | Parent.FileProductName | string | 文件产品名 |  |
| 52 | Parent.FileProductVer | string | 文件产品版本号 |  |
| 53 | Parent.FileLegalMark | string | 文件产品商标 |  |
| 54 | Parent.FileCopyright | string | 文件版权 |  |
| 55 | Parent.FileModifyTime | int | 文件修改时间 |  |
| 56 | Parent.FileAccessTime | int | 文件访问时间 |  |
| 57 | Parent.FileCreateTime | int | 文件创建时间 |  |
| 58 | Parent.FileTags | string | 文件标签 | Browser: 浏览器渠道<br/>Browser:114高速浏览器: 114高速浏览器下载<br/>Browser:115极速浏览器: 115极速浏览器下载<br/>Browser:115浏览器: 115浏览器下载<br/>Browser:2345加速浏览器: 2345加速浏览器下载<br/>Browser:2345智能浏览器: 2345智能浏览器下载<br/>Browser:360安全浏览器: 360安全浏览器下载<br/>Browser:360极速浏览器: 360极速浏览器下载<br/>Browser:Edge浏览器: Edge浏览器下载<br/>Browser:GreenBrowser: GreenBrowser下载<br/>Browser:GT游戏浏览器: GT游戏浏览器下载<br/>Browser:hao123桔子浏览器: hao123桔子浏览器下载<br/>Browser:IE浏览器: IE浏览器下载<br/>Browser:iQ浏览器: iQ浏览器下载<br/>Browser:KR浏览器: KR浏览器下载<br/>Browser:MyIE浏览器: MyIE浏览器下载<br/>Browser:Opera: Opera下载<br/>Browser:QQ浏览器: QQ浏览器下载<br/>Browser:Safari浏览器: Safari浏览器下载<br/>BrowserSoft: 浏览器软件<br/>Browser:Spartan浏览器: Spartan浏览器下载<br/>Browser:TT浏览器: TT浏览器下载<br/>Browser:UC浏览器: UC浏览器下载<br/>Browser:YY浏览器: YY浏览器下载<br/>Browser:世界之窗浏览器: 世界之窗浏览器下载<br/>Browser:世界之窗浏览器极速版: 世界之窗浏览器极速版下载<br/>Browser:傲游浏览器: 傲游浏览器下载<br/>Browser:搜狗浏览器: 搜狗浏览器下载<br/>Browser:淘宝浏览器: 淘宝浏览器下载<br/>Browser:火狐浏览器: 火狐浏览器下载<br/>Browser:猎豹浏览器: 猎豹浏览器下载<br/>Browser:瑞影浏览器: 瑞影浏览器下载<br/>Browser:百度浏览器: 百度浏览器下载<br/>Browser:百度浏览器hao123专版: 百度浏览器hao123专版下载<br/>Browser:糖果浏览器: 糖果浏览器下载<br/>Browser:花儿世界浏览器: 花儿世界浏览器下载<br/>Browser:谷歌浏览器: 谷歌浏览器下载<br/>Browser:超速浏览器: 超速浏览器下载<br/>Browser:闪游浏览器: 闪游浏览器下载<br/>Browser:随E浏览器: 随E浏览器下载<br/>Browser:青猴浏览器: 青猴浏览器下载<br/>ChildNode: 操作目标<br/>DllHijack: DLL劫持<br/>Downloader: 下载器渠道<br/>Downloader:BitComet: BitComet下载<br/>Downloader:IDMan: IDMan下载<br/>Downloader:QQ旋风: QQ旋风下载<br/>Downloader:QQ旋风下载助手: QQ旋风下载助手下载<br/>Downloader:RaySource: RaySource下载<br/>DownloaderSoft: 下载软件<br/>Downloader:旋风高速下载引擎: 旋风高速下载<br/>Downloader:比特彗星: 比特彗星下载<br/>Downloader:电驴: 电驴下载<br/>Downloader:百度下载助手: 百度下载助手下载<br/>Downloader:百度云管家: 百度云管家下载<br/>Downloader:网际快车: 网际快车下载<br/>Downloader:网页迅雷: 网页迅雷下载<br/>Downloader:迅雷: 迅雷下载<br/>Downloader:迅雷云加速: 迅雷云加速下载<br/>Downloader:迅雷精简版: 迅雷精简版下载<br/>Downloader:迅雷迷你版: 迅雷迷你版下载<br/>Downloader:迷你快车: 迷你快车下载<br/>Downloader:迷你电驴: 迷你电驴下载<br/>Downloader:飞鸟下载器: 飞鸟下载器下载<br/>IM: IM渠道<br/>IM:FSLink: FSLink下载<br/>IM:MSN: MSN下载<br/>IM:Skype: Skype下载<br/>IMSoft: IM软件<br/>IM:YY语音: YY语音下载<br/>IM:京东咚咚: 京东咚咚下载<br/>IM:企业微信: 企业微信下载<br/>IM:微信: 微信下载<br/>IM:易信: 易信下载<br/>IM:润工作: 润工作下载<br/>IM:环信: 环信下载<br/>IM:百度Hi: 百度Hi下载<br/>IM:百度Hi: 百度Hi下载<br/>IM:网易CC语音: 网易CC语音下载<br/>IM:网易云信: 网易云信下载<br/>IM:腾讯QQ: 腾讯QQ下载<br/>IM:腾讯TM: 腾讯TM下载<br/>IM:腾讯通\(RTX\): 腾讯通\(RTX\)下载<br/>IM:钉钉: 钉钉下载<br/>IM:阿里旺旺: 阿里旺旺下载<br/>IM:飞书: 飞书下载<br/>IM:飞信: 飞信下载<br/>InjectProc: 进程注入<br/>Mail: 邮箱渠道<br/>Mail:139邮箱: 139邮箱下载<br/>Mail:Foxmail: Foxmail下载<br/>Mail:PP助手: OutLook下载<br/>MailSoft: 邮箱软件<br/>Mail:新浪邮箱: 新浪邮箱下载<br/>Mail:网易邮箱: 网易邮箱下载<br/>Mail:阿里邮箱: 阿里邮箱下载<br/>NetDisk: 网盘渠道<br/>NetDisk:115网盘: 115网盘下载<br/>NetDisk:360云盘: 360云盘下载<br/>NetDisk:360网盘: 360网盘下载<br/>NetDiskSoft: 网盘软件<br/>NetDisk:优蛋: 优蛋下载<br/>NetDisk:华为网盘: 华为网盘下载<br/>NetDisk:坚果云: 坚果云下载<br/>NetDisk:城通网盘: 城通网盘下载<br/>NetDisk:天翼云盘: 天翼云盘下载<br/>NetDisk:夸克网盘: 夸克网盘下载<br/>NetDisk:微云: 微云下载<br/>NetDisk:微盘: 微盘下载<br/>NetDisk:百度网盘: 百度网盘下载<br/>NetDisk:纳米盘: 纳米盘下载<br/>NetDisk:酷盘: 酷盘下载<br/>NetDisk:金山快盘: 金山快盘下载<br/>NetDisk:阿里云盘: 阿里云盘下载<br/>NetShare: 网络共享渠道<br/>NewFile: 新入文件<br/>NewFileExec: 新入执行<br/>NewFileInject: 新入注入<br/>NewSuspicious: 新入可疑<br/>ParentNode: 操作者<br/>SoftMgr: 软件管理渠道<br/>SoftMgr:2345软件管家: 2345软件管家下载<br/>SoftMgr:360安全卫士: 360安全卫士下载<br/>SoftMgr:360驱动大师: 360驱动大师下载<br/>SoftMgr:91手机助手: 91手机助手下载<br/>SoftMgr:PP助手: PP助手下载<br/>SoftMgrSoft: 软件管理软件<br/>SoftMgr:天极软件管家: 天极软件管家下载<br/>SoftMgr:微软电脑管家: 微软电脑管家下载<br/>SoftMgr:搜狗手机助手: 搜狗手机助手下载<br/>SoftMgr:爱思助手: 爱思助手下载<br/>SoftMgr:联想电脑管家: 联想电脑管家下载<br/>SoftMgr:腾讯电脑管家: 腾讯电脑管家下载<br/>SoftMgr:豌豆荚2: 豌豆荚2下载<br/>SoftMgr:软媒魔方软件管理: 软媒魔方软件管理下载<br/>SoftMgr:金山手机助手: 金山手机助手下载<br/>SoftMgr:金山毒霸: 金山毒霸下载<br/>SoftMgr:风灵软件管家: 风灵软件管家下载<br/>SoftMgr:驱动人生: 驱动人生下载<br/>SoftMgr:驱动人生软件管理: 驱动人生软件管理下载<br/>SoftMgr:驱动精灵: 驱动精灵下载<br/>TrustSource: 可信进程释放<br/>UnknownSource: 未知进程释放 |
| 59 | Parent.FileEncrypted | bool | 加密文件 |  |
| 60 | Parent.FileContentType | string | 文件内容格式 | application/atom+xml: atom文件<br/>application/dicom: dcm文件<br/>application/epub+zip: 电子书\(epub\)<br/>application/fits: fits文件<br/>application/geo+json: json文件本\(geo\)<br/>application/gml+xml: gml文件<br/>application/gpx+xml: gpx文件<br/>application/gzip: 压缩包\(gzip\)<br/>application/jar: jar文件<br/>application/javascript: 代码\(javascript\)<br/>application/json: json文件<br/>application/lzip: 压缩包\(lz\)<br/>application/marc: mrc文件<br/>application/msword: 微软Word\(doc\)<br/>application/octet-stream: aaf文件<br/>application/ogg: 音视频\(ogg\)<br/>application/owl+xml: owl文件<br/>application/pdf: Adobe PDF\(pdf\)<br/>application/pkcs7-signature: p7s文件<br/>application/postscript: 代码\(postscript\)<br/>application/rss+xml: rss文件<br/>application/tzif: tzif文件<br/>application/vnd.adobe.xfdf: Adobe PDF\(xfdf\)<br/>application/vnd.apple.mpegurl: 音视频\(m3u\)<br/>application/vnd.debian.binary-package: deb安装包<br/>application/vnd.fdf: Adobe PDF\(fdf\)<br/>application/vnd.garmin.tcx+xml: tcx文件<br/>application/vnd.google-earth.kml+xml: kml文件<br/>application/vnd.ms-cab-compressed: 压缩包\(cab\)<br/>application/vnd.ms-excel: 微软Excel\(xls\)<br/>application/vnd.ms-fontobject: 字体文件\(eot\)<br/>application/vnd.ms-outlook: 微软Outlook邮件<br/>application/vnd.ms-package.3dmanufacturing-3dmodel+xml: 3mf文件<br/>application/vnd.ms-powerpoint: 微软PPT\(ppt\)<br/>application/vnd.ms-publisher: 微软Publisher<br/>application/vnd.nintendo.snes.rom: 游戏\(nes\)<br/>application/vnd.oasis.opendocument.chart: OpenOffice图表\(odc\)<br/>application/vnd.oasis.opendocument.formula: OpenOffice公式\(odf\)<br/>application/vnd.oasis.opendocument.graphics: OpenOffice画图\(odg\)<br/>application/vnd.oasis.opendocument.graphics-template: OpenOffice画图\(otg\)<br/>application/vnd.oasis.opendocument.presentation: OpenOffice PPT\(odp\)<br/>application/vnd.oasis.opendocument.presentation-template: OpenOffice PPT\(otp\)<br/>application/vnd.oasis.opendocument.spreadsheet: OpenOffice表格\(ods\)<br/>application/vnd.oasis.opendocument.spreadsheet-template: OpenOffice表格\(ots\)<br/>application/vnd.oasis.opendocument.text: OpenOffice文档\(odt\)<br/>application/vnd.oasis.opendocument.text-template: OpenOffice文档\(ott\)<br/>application/vnd.openxmlformats-officedocument.presentationml.presentation: 微软PPT\(pptx\)<br/>application/vnd.openxmlformats-officedocument.spreadsheetml.sheet: 微软Excel\(xlsx\)<br/>application/vnd.openxmlformats-officedocument.wordprocessingml.document: 微软Word\(docx\)<br/>application/vnd.rn-realmedia-vbr: 音视频\(rmvb\)<br/>application/vnd.shp: shp文件<br/>application/vnd.shx: shx文件<br/>application/vnd.sqlite3: 数据库\(sqlite\)<br/>application/vnd.sun.xml.calc: OpenOffice表格\(sxc\)<br/>application/warc: warc文件<br/>application/wasm: wasm文件<br/>application/x-7z-compressed: 压缩包\(7z\)<br/>application/x-amf: amf文件<br/>application/x-archive: 压缩包\(a\)<br/>application/x-bittorrent: 种子文件\(bt\)<br/>application/x-bzip2: 压缩包\(bz2\)<br/>application/x-chrome-extension: 谷歌扩展<br/>application/x-coredump: coredump文件<br/>application/x-cpio: cpio文件<br/>application/x-dbf: dbf文件<br/>application/x-java-applet: 代码\(class\)<br/>application/x-mobipocket-ebook: 电子书\(mobi\)<br/>application/x-msaccess: 数据库\(access\)<br/>application/x-ms-reader: 电子书\(lit\)<br/>application/x-ms-shortcut: 快捷方式<br/>application/x-ndjson: ndjson文件<br/>application/x-ole-storage: x-ole-storage<br/>application/x-rar-compressed: 压缩包\(rar\)<br/>application/x-rpm: rpm安装包<br/>application/x-shockwave-flash: 音视频\(swf\)<br/>application/x-subrip: 字幕\(srt\)<br/>application/x-tar: 压缩包\(tar\)<br/>application/x-xar: 压缩包\(xar\)<br/>application/x-xliff+xml: xlf文件<br/>application/x-xz: 压缩包\(xz\)<br/>application/zip: 压缩包\(zip\)<br/>application/zstd: 压缩包\(zst\)<br/>audio/aac: 音视频\(aac\)<br/>audio/aiff: 音视频\(aiff\)<br/>audio/amr: 音视频\(amr\)<br/>audio/ape: 音视频\(ape\)<br/>audio/basic: 音视频\(au\)<br/>audio/flac: 音视频\(flac\)<br/>audio/midi: 音视频\(midi\)<br/>audio/mp4: 音视频\(mp4\)<br/>audio/mpeg: 音视频\(mp3\)<br/>audio/musepack: 音视频\(mpc\)<br/>audio/ogg: 音视频\(oga\)<br/>audio/qcelp: 音视频\(qcp\)<br/>audio/wav: 音视频\(wav\)<br/>audio/x-m4a: 音视频\(m4a\)<br/>audio/x-unknown: 音视频\(voc\)<br/>font/collection: 字体文件\(ttc\)<br/>font/otf: 字体文件\(otf\)<br/>font/ttf: 字体文件\(ttf\)<br/>font/woff: 字体文件\(woff\)<br/>font/woff2: 字体文件\(woff2\)<br/>image/avif: 图片\(avif\)<br/>image/bmp: 图片\(bmp\)<br/>image/bpg: 图片\(bpg\)<br/>image/gif: 图片\(gif\)<br/>image/heic: 图片\(heic\)<br/>image/heic-sequence: 图片\(heic-sequence\)<br/>image/heif: 图片\(heif\)<br/>image/heif-sequence: 图片\(heif-sequence\)<br/>image/jp2: 图片\(jp2\)<br/>image/jpeg: 图片\(jpeg\)<br/>image/jpm: 图片\(jpm\)<br/>image/jpx: 图片\(jpx\)<br/>image/jxl: 图片\(jxl\)<br/>image/jxr: 图片\(jxr\)<br/>image/jxs: 图片\(jxs\)<br/>image/png: 图片\(png\)<br/>image/svg+xml: 图片\(svg\)<br/>image/tiff: 图片\(tiff\)<br/>image/vnd.adobe.photoshop: psd文件<br/>image/vnd.djvu: 图片\(djvu\)<br/>image/vnd.dwg: 图片\(dwg\)<br/>image/vnd.mozilla.apng: 图片\(apng\)<br/>image/vnd.radiance: 图片\(hdr\)<br/>image/webp: 图片\(webp\)<br/>image/x-gimp-gbr: 图片\(gbr\)<br/>image/x-gimp-pat: 图片\(pat\)<br/>image/x-icns: 图标\(icns\)<br/>image/x-icon: 图标\(ico\)<br/>image/x-xcf: 图片\(xcf\)<br/>image/x-xpixmap: 图片\(xpm\)<br/>model/gltf-binary: glb文件<br/>model/vnd.collada+xml: dae文件<br/>model/x3d+xml: x3d文件<br/>SFX\_7Z: 自解压安装包（7Z）<br/>SFX\_NSIS: NSIS安装包<br/>SFX\_ZIP: 自解压安装包（ZIP）<br/>text/calendar: ics文件<br/>text/csv: csv文件<br/>text/html: html文件<br/>text/plain: txt文件<br/>text/rtf: 富文本<br/>text/tab-separated-values: tsv文件<br/>text/vcard: vcf文件<br/>text/vtt: vtt文件<br/>text/x-lua: 代码\(lua\)<br/>text/xml: xml文件<br/>text/x-perl: 代码\(perl\)<br/>text/x-php: 代码\(php\)<br/>text/x-python: 代码\(python\)<br/>text/x-tcl: 代码\(tcl\)<br/>unknown: 未知格式<br/>video/3gpp: 音视频\(3gpp\)<br/>video/3gpp2: 音视频\(3g2\)<br/>video/mp4: 音视频\(mp4\)<br/>video/mpeg: 音视频\(mpeg\)<br/>video/ogg: 音视频\(ogv\)<br/>video/quicktime: 音视频\(mov/mqv\)<br/>video/webm: 音视频\(webm\)<br/>video/x-flv: 音视频\(flv\)<br/>video/x-m4v: 音视频\(m4v\)<br/>video/x-matroska: 音视频\(mkv\)<br/>video/x-ms-asf: 音视频\(asf\)<br/>video/x-msvideo: 音视频\(avi\) |
| 61 | Parent.ThreadId | int | 线程ID |  |
| 62 | Parent.TrojanName | string | 病毒名 |  |
| 63 | Parent.ProcReplacePid | int | 替换前Pid |  |
| 64 | Parent.ProcChainGuid | string | 进程链唯一ID |  |
| 65 | Parent.ProcGId | int | 进程组ID |  |
| 66 | Parent.ProcCpuArch | string | 进程CPU架构 | amd64: AMD64架构<br/>arm64: ARM64架构<br/>loongarch64: 龙芯64架构 |
| 67 | Parent.CallStack | string | 调用堆栈 |  |
| 68 | Parent.FileSourceUrl | string | 文件来源URL |  |
| 69 | Child | object | 目标信息 |  |
| 70 | Child.SubjectUserSid | string | 用户安全ID |  |
| 71 | Child.SubjectUserName | string | 账户名称 |  |
| 72 | Child.SubjectDomainName | string | 账户域 |  |
| 73 | Child.SubjectLogonId | string | 登录ID |  |
| 74 | Child.PreviousTime | string | 上一时间 |  |
| 75 | Child.NewTime | string | 新时间 |  |
| 76 | Child.ElevatedToken | string | 提升的令牌 | 否: 否<br/>是: 是 |
| 77 | Child.ImpersonationLevel | string | 模拟级别 | 委派: 委派<br/>标识: 标识<br/>模拟: 模拟 |
| 78 | Child.RestrictedAdminMode | string | 受限管理员模式 | 否: 否<br/>是: 是 |
| 79 | Child.TargetUserSid | string | 目标安全ID |  |
| 80 | Child.TargetUserName | string | 目标账户名称 |  |
| 81 | Child.TargetDomainName | string | 目标账户域 |  |
| 82 | Child.TargetLogonId | string | 目标登录ID |  |
| 83 | Child.TargetLinkedLogonId | string | 目标链接登录ID |  |
| 84 | Child.TargetOutboundUserName | string | 网络账户名称 |  |
| 85 | Child.TargetOutboundDomainName | string | 网络账户域 |  |
| 86 | Child.TransmittedServices | string | 传输服务 |  |
| 87 | Child.VirtualAccount | string | 虚拟账户 | 否: 否<br/>是: 是 |
| 88 | Child.WorkstationName | string | 工作站名称 |  |
| 89 | Child.AccessList | string | 访问列表 |  |
| 90 | Child.AccessMask | string | 访问掩码 |  |
| 91 | Child.AccessReason | string | 访问检查结果 |  |
| 92 | Child.AccountExpires | string | 账户过期 |  |
| 93 | Child.AllowedToDelegateTo | string | 委派凭据的SPN 列表 |  |
| 94 | Child.AuditSourceName | string | 源名称 |  |
| 95 | Child.AuthenticationPackageName | string | 身份验证包 | Kerberos: Kerberos<br/>LM: LM<br/>Negotiate: Negotiate<br/>NTLM V1: NTLM V1<br/>NTLM V2: NTLM V2 |
| 96 | Child.ConfiguredNames | string | 配置名称 |  |
| 97 | Child.ClassId | string | 类ID |  |
| 98 | Child.ClassName | string | 类名 |  |
| 99 | Child.CompatibleIds | string | 兼容ID |  |
| 100 | Child.ClientMachine | string | 主机名 |  |
| 101 | Child.ClientMachineFQDN | string | 域名 |  |
| 102 | Child.ClientProcessCreationTime | string | 进程启动时间 |  |
| 103 | Child.CorrelationId | string | 绑定ID |  |
| 104 | Child.Commandline | string | 创建命令行 |  |
| 105 | Child.CreatedProcessCreationTime | string | 创建进程时间 |  |
| 106 | Child.DeviceClaims | string | 设备声明 |  |
| 107 | Child.DisabledPrivilegeList | string | 禁用权限列表 |  |
| 108 | Child.DisplayName | string | 显示名称 |  |
| 109 | Child.DeviceId | string | 设备ID |  |
| 110 | Child.DeviceDescription | string | 设备名称 |  |
| 111 | Child.EnabledPrivilegeList | string | 启用权限列表 |  |
| 112 | Child.EventSourceId | string | 事件源ID |  |
| 113 | Child.ErrorCode | string | 错误代码 |  |
| 114 | Child.FailureReason | string | 失败原因 |  |
| 115 | Child.GroupOperationId | string | 组操作ID |  |
| 116 | Child.HandleId | string | 句柄ID |  |
| 117 | Child.HomeDirectory | string | 主目录 |  |
| 118 | Child.HomePath | string | 主路径 |  |
| 119 | Child.IsLocal | bool | 是否本地 |  |
| 120 | Child.IpAddress | string | 源网络地址 |  |
| 121 | Child.IpPort | string | 源端口 |  |
| 122 | Child.KeyLength | string | 密钥长度 |  |
| 123 | Child.LogonGuid | string | 登录GUID |  |
| 124 | Child.LogonProcessName | string | 登录进程名称 |  |
| 125 | Child.LogonType | string | 登录类型 | 0: 系统启动<br/>10: 远程登录<br/>2: 交互式<br/>3: 网络<br/>4: 计划任务<br/>5: 服务 |
| 126 | Child.LogonHours | string | 登录限制时长 |  |
| 127 | Child.LocationInformation | string | 位置信息 |  |
| 128 | Child.NewSd | string | 新的安全描述符 |  |
| 129 | Child.MasterKeyId | string | 密钥标识符 |  |
| 130 | Child.NewUacValue | string | 新UAC值 |  |
| 131 | Child.NewRemark | string | 新注释值 |  |
| 132 | Child.NewMaxUsers | string | 新的用户数限制值 |  |
| 133 | Child.NewShareFlags | string | 新的脱机设置值 |  |
| 134 | Child.NamespaceName | string | 命名空间名称 |  |
| 135 | Child.ObjectServer | string | 对象服务器 |  |
| 136 | Child.ObjectType | string | 对象类型 |  |
| 137 | Child.ObjectName | string | 对象名称 |  |
| 138 | Child.OldSd | string | 原始安全描述 |  |
| 139 | Child.OldUacValue | string | 旧UAC值 |  |
| 140 | Child.OldRemark | string | 旧注释值 |  |
| 141 | Child.OldMaxUsers | string | 旧的用户数限制值 |  |
| 142 | Child.OldShareFlags | string | 旧的脱机设置值 |  |
| 143 | Child.Operation | string | 操作 |  |
| 144 | Child.OperationId | string | 操作ID |  |
| 145 | Child.PrivilegeList | string | 权限列表 |  |
| 146 | Child.Properties | string | 属性 |  |
| 147 | Child.ProfilePath | string | 配置文件路径 |  |
| 148 | Child.PasswordLastSet | string | 密码最后一个集 |  |
| 149 | Child.PrimaryGroupId | string | 主组ID |  |
| 150 | Child.ProfileChanged | string | 已更改配置文件 |  |
| 151 | Child.RestrictedSidCount | string | 受限SID 计数 |  |
| 152 | Child.RecoveryServer | string | 恢复服务器 |  |
| 153 | Child.RecoveryKeyId | string | 恢复密钥 ID |  |
| 154 | Child.RelativeTargetName | string | 相对目标名称 |  |
| 155 | Child.Status | string | 状态 |  |
| 156 | Child.SubStatus | string | 子状态 |  |
| 157 | Child.Service | string | 服务名称 |  |
| 158 | Child.SamAccountName | string | SAM账户名称 |  |
| 159 | Child.ScriptPath | string | 脚本路径 |  |
| 160 | Child.SidHistory | string | SID历史记录 |  |
| 161 | Child.SettingType | string | 设置类型 |  |
| 162 | Child.SettingValue | string | 设置类型 |  |
| 163 | Child.SidList | string | 特殊组SID列表 |  |
| 164 | Child.ShareName | string | 共享名称 |  |
| 165 | Child.ShareLocalPath | string | 共享路径 |  |
| 166 | Child.SpnName | string | SPN名称 |  |
| 167 | Child.ServerNames | string | 服务器名称 |  |
| 168 | Child.TargetLogonGuid | string | 目标登录GUID |  |
| 169 | Child.TargetServerName | string | 目标服务器名称 |  |
| 170 | Child.TargetInfo | string | 目标信息 |  |
| 171 | Child.TransactionId | string | 事务ID |  |
| 172 | Child.TaskName | string | 任务名称 |  |
| 173 | Child.TaskContent | string | 任务内容 |  |
| 174 | Child.TaskContentNew | string | 任务新内容 |  |
| 175 | Child.TargetSid | string | 目标登录ID |  |
| 176 | Child.UserClaims | string | 用户声明 |  |
| 177 | Child.UserPrincipalName | string | 用户主体名称 |  |
| 178 | Child.UserWorkstations | string | 用户工作站 |  |
| 179 | Child.UserAccountControl | string | 用户账户控件 |  |
| 180 | Child.UserParameters | string | 用户参数 |  |
| 181 | Child.User | string | 用户名 |  |
| 182 | Child.VendorIds | string | 供应商ID |  |
| 183 | Child.FilterType | string | Hook类型 |  |
| 184 | Child.ReturnValue | string | 注册结果 |  |
| 185 | Child.hmod | string | DLL句柄 |  |
| 186 | Child.pfnFilterProc | string | 过滤函数 |  |
| 187 | Child.pstrLib | string | 模块路径 |  |
| 188 | Child.ContentName | string | 脚本名称 |  |
| 189 | Child.ContentData | string | 脚本数据 |  |
| 190 | Child.ScriptRiskName | string | 脚本风险名称 |  |
| 191 | Child.ScriptRiskType | string | 脚本风险类型 | Black: 黑\(Black\)<br/>Gray: 灰\(Gray\)<br/>Unknown: 未知\(Unknown\) |
| 192 | Child.ApiRet | int | 返回值 |  |
| 193 | Child.Privileges | string | 特权列表 |  |
| 194 | Child.Addr | int | 起始地址 |  |
| 195 | Child.Param1 | int | 参数1 |  |
| 196 | Child.Size | int | 地址大小 |  |
| 197 | Child.NewProtect | int | 新权限 | 0x1: 无权限<br/>0x10: 可执行<br/>0x100: 保护页面<br/>0x2: 只读<br/>0x20: 执行读<br/>0x200: 无缓存<br/>0x4: 只写<br/>0x40: 执行读写<br/>0x8: 只拷贝<br/>0x80: 执行写拷贝 |
| 198 | Child.OldProtect | int | 旧权限 | 0x1: 无权限<br/>0x10: 可执行<br/>0x100: 保护页面<br/>0x2: 只读<br/>0x20: 执行读<br/>0x200: 无缓存<br/>0x4: 只写<br/>0x40: 执行读写<br/>0x8: 只拷贝<br/>0x80: 执行写拷贝 |
| 199 | Child.Method | string | 请求方法 | CONNECT: CONNECT<br/>DELETE: DELETE<br/>GET: GET<br/>HEAD: HEAD<br/>OPTIONS: OPTIONS<br/>PATCH: PATCH<br/>POST: POST<br/>PUT: PUT<br/>TRACE: TRACE |
| 200 | Child.ProtoVersion | string | 协议版本 |  |
| 201 | Child.Referer | string | 来源 |  |
| 202 | Child.AcceptTypes | string | 接受类型 |  |
| 203 | Child.Flags | int | 选项标志 |  |
| 204 | Child.UserName | string | 用户名 |  |
| 205 | Child.Password | string | 密码 |  |
| 206 | Child.ProtoService | int | 访问类型 | 1: FTP<br/>2: GOPHER<br/>3: HTTP |
| 207 | Child.Header | string | 请求头 |  |
| 208 | Child.Agent | string | User-Agent |  |
| 209 | Child.AccessTypes | int | 接受类型 | 0: 注册表配置<br/>1: 直连网络<br/>2: 通过代理<br/>3: 无自动代理 |
| 210 | Child.Proxy | string | 代理服务 |  |
| 211 | Child.ProxyByPass | string | 免代理域名 |  |
| 212 | Child.EventBegin | int | 事件起始 |  |
| 213 | Child.EventEnd | int | 事件结束 |  |
| 214 | Child.Handle | int | 句柄 |  |
| 215 | Child.ContextFlags | int | 上下文类型 |  |
| 216 | Child.Eip | int | EIP寄存器 |  |
| 217 | Child.OldEip | int | 旧EIP寄存器 |  |
| 218 | Child.BlobData | string | 二进制数据 |  |
| 219 | Child.FuncName | string | 函数名 |  |
| 220 | Child.ProtectType | int | 内存权限 | 0x1: 无权限<br/>0x10: 可执行<br/>0x100: 保护页面<br/>0x2: 只读<br/>0x20: 执行读<br/>0x200: 无缓存<br/>0x4: 只写<br/>0x40: 执行读写<br/>0x8: 只拷贝<br/>0x80: 执行写拷贝 |
| 221 | Child.AllocType | int | 分配类型 | 0x1000: 提交内存<br/>0x2000: 保留内存<br/>0x40000: 映射内存<br/>0x400000: 物理内存 |
| 222 | Child.Protocol | string | 协议类型 | tcp: tcp<br/>udp: udp |
| 223 | Child.SrcIp | string | 本地IP |  |
| 224 | Child.SrcPort | int | 本地端口 |  |
| 225 | Child.DstIp | string | 远程IP |  |
| 226 | Child.DstPort | int | 远程端口 |  |
| 227 | Child.Direct | int | 流量方向 | 1: 出站<br/>2: 入站 |
| 228 | Child.SendTotal | int | 发送总的字节数 |  |
| 229 | Child.RecvTotal | int | 收到总的字节数 |  |
| 230 | Child.Host | string | 域名 |  |
| 231 | Child.Url | string | URL |  |
| 232 | Child.FlowTags | string | 流数据标签 |  |
| 233 | Child.DnsAnswers | string | DNS应答IP |  |
| 234 | Child.IpIoc | string | IP威胁情报 | Black: 黑\(Black\)<br/>Gray: 灰\(Gray\)<br/>Unknown: 未知\(Unknown\)<br/>White: 安全\(White\) |
| 235 | Child.HostIoc | string | 域名威胁情报 | Black: 黑\(Black\)<br/>Gray: 灰\(Gray\)<br/>Unknown: 未知\(Unknown\)<br/>White: 安全\(White\) |
| 236 | Child.LuaScanAttr | string | 社工引擎扫描结果 | Black: 黑\(Black\)<br/>Gray: 灰\(Gray\)<br/>Unknown: 未知\(Unknown\)<br/>White: 安全\(White\) |
| 237 | Child.LuaScanScore | int | 社工引擎扫描分值 |  |
| 238 | Child.LuaScanInfo | string | 社工引擎扫描详情 |  |
| 239 | Child.PacketType | int | 流量包类型 | 1: Syn洪水攻击 |
| 240 | Child.DDosInfo | string | DDos详情 |  |
| 241 | Child.DDosTotal | int | DDos攻击次数 |  |
| 242 | Child.DDosInterval | int | DDos统计时长（秒） |  |
| 243 | Child.ServiceName | string | 服务名称 |  |
| 244 | Child.StartType | int | 启动类型 | 0: Boot启动<br/>1: System启动<br/>2: 自动启动<br/>3: 手动启动<br/>4: 禁止启动 |
| 245 | Child.TaskName | string | 任务名称 |  |
| 246 | Child.TaskArg | string | 任务参数 |  |
| 247 | Child.RemoteCallType | int | 远程调用类型 | 0x1: MMC20Application<br/>0x10: WMI<br/>0x2: InternetExplorer<br/>0x4: ShellWindows<br/>0x8: ShellBrowserWindows |
| 248 | Child.PrintType | int | 打印机类型 | 1: RpcAsyncAddPrinterDriver<br/>2: RpcAddPrinterDriverEx |
| 249 | Child.DocFileOpt | int | 勒索诱饵操作 | 0x10: 删除文件<br/>0x4: 重命名<br/>0x40: 文件大小改变<br/>0x8: 写文件<br/>0x80: 设置文件信息 |
| 250 | Child.HoneypotUrl | string | 蜜罐链接 |  |
| 251 | Child.PhishChain | string | 钓鱼链 |  |
| 252 | Child.ProcPid | int | 进程Pid |  |
| 253 | Child.ProcCmdline | string | 进程命令行 |  |
| 254 | Child.FileName | string | 文件名 |  |
| 255 | Child.FilePath | string | 文件路径 |  |
| 256 | Child.FileDriverType | string | 驱动器类型 | CDRom: CD光盘<br/>Fixed: 硬盘<br/>NoRootDir: 非驱动<br/>Ramdisk: 内存磁盘<br/>Remote: 网络驱动器<br/>Removeable: 可移动介质<br/>Unknown: 未知 |
| 257 | Child.FileMd5 | string | 文件md5 |  |
| 258 | Child.CloudAttr | string | 云查属性 | Black: 黑\(Black\)<br/>Gray: 灰\(Gray\)<br/>Unknown: 未知\(Unknown\)<br/>White: 安全\(White\) |
| 259 | Child.FileSign | string | 文件签名 |  |
| 260 | Child.FileSignStatus | string | 文件签名状态 | Expired: 签名过期<br/>Invalid: 验证不通过<br/>Valid: 验证通过 |
| 261 | Child.FileSignWhite | int | 是否白签名 | 0: 不是<br/>1: 是 |
| 262 | Child.FileEncrypted | bool | 加密文件 |  |
| 263 | Child.FileContentType | string | 文件内容格式 | application/atom+xml: atom文件<br/>application/dicom: dcm文件<br/>application/epub+zip: 电子书\(epub\)<br/>application/fits: fits文件<br/>application/geo+json: json文件本\(geo\)<br/>application/gml+xml: gml文件<br/>application/gpx+xml: gpx文件<br/>application/gzip: 压缩包\(gzip\)<br/>application/jar: jar文件<br/>application/javascript: 代码\(javascript\)<br/>application/json: json文件<br/>application/lzip: 压缩包\(lz\)<br/>application/marc: mrc文件<br/>application/msword: 微软Word\(doc\)<br/>application/octet-stream: aaf文件<br/>application/ogg: 音视频\(ogg\)<br/>application/owl+xml: owl文件<br/>application/pdf: Adobe PDF\(pdf\)<br/>application/pkcs7-signature: p7s文件<br/>application/postscript: 代码\(postscript\)<br/>application/rss+xml: rss文件<br/>application/tzif: tzif文件<br/>application/vnd.adobe.xfdf: Adobe PDF\(xfdf\)<br/>application/vnd.apple.mpegurl: 音视频\(m3u\)<br/>application/vnd.debian.binary-package: deb安装包<br/>application/vnd.fdf: Adobe PDF\(fdf\)<br/>application/vnd.garmin.tcx+xml: tcx文件<br/>application/vnd.google-earth.kml+xml: kml文件<br/>application/vnd.ms-cab-compressed: 压缩包\(cab\)<br/>application/vnd.ms-excel: 微软Excel\(xls\)<br/>application/vnd.ms-fontobject: 字体文件\(eot\)<br/>application/vnd.ms-outlook: 微软Outlook邮件<br/>application/vnd.ms-package.3dmanufacturing-3dmodel+xml: 3mf文件<br/>application/vnd.ms-powerpoint: 微软PPT\(ppt\)<br/>application/vnd.ms-publisher: 微软Publisher<br/>application/vnd.nintendo.snes.rom: 游戏\(nes\)<br/>application/vnd.oasis.opendocument.chart: OpenOffice图表\(odc\)<br/>application/vnd.oasis.opendocument.formula: OpenOffice公式\(odf\)<br/>application/vnd.oasis.opendocument.graphics: OpenOffice画图\(odg\)<br/>application/vnd.oasis.opendocument.graphics-template: OpenOffice画图\(otg\)<br/>application/vnd.oasis.opendocument.presentation: OpenOffice PPT\(odp\)<br/>application/vnd.oasis.opendocument.presentation-template: OpenOffice PPT\(otp\)<br/>application/vnd.oasis.opendocument.spreadsheet: OpenOffice表格\(ods\)<br/>application/vnd.oasis.opendocument.spreadsheet-template: OpenOffice表格\(ots\)<br/>application/vnd.oasis.opendocument.text: OpenOffice文档\(odt\)<br/>application/vnd.oasis.opendocument.text-template: OpenOffice文档\(ott\)<br/>application/vnd.openxmlformats-officedocument.presentationml.presentation: 微软PPT\(pptx\)<br/>application/vnd.openxmlformats-officedocument.spreadsheetml.sheet: 微软Excel\(xlsx\)<br/>application/vnd.openxmlformats-officedocument.wordprocessingml.document: 微软Word\(docx\)<br/>application/vnd.rn-realmedia-vbr: 音视频\(rmvb\)<br/>application/vnd.shp: shp文件<br/>application/vnd.shx: shx文件<br/>application/vnd.sqlite3: 数据库\(sqlite\)<br/>application/vnd.sun.xml.calc: OpenOffice表格\(sxc\)<br/>application/warc: warc文件<br/>application/wasm: wasm文件<br/>application/x-7z-compressed: 压缩包\(7z\)<br/>application/x-amf: amf文件<br/>application/x-archive: 压缩包\(a\)<br/>application/x-bittorrent: 种子文件\(bt\)<br/>application/x-bzip2: 压缩包\(bz2\)<br/>application/x-chrome-extension: 谷歌扩展<br/>application/x-coredump: coredump文件<br/>application/x-cpio: cpio文件<br/>application/x-dbf: dbf文件<br/>application/x-java-applet: 代码\(class\)<br/>application/x-mobipocket-ebook: 电子书\(mobi\)<br/>application/x-msaccess: 数据库\(access\)<br/>application/x-ms-reader: 电子书\(lit\)<br/>application/x-ms-shortcut: 快捷方式<br/>application/x-ndjson: ndjson文件<br/>application/x-ole-storage: x-ole-storage<br/>application/x-rar-compressed: 压缩包\(rar\)<br/>application/x-rpm: rpm安装包<br/>application/x-shockwave-flash: 音视频\(swf\)<br/>application/x-subrip: 字幕\(srt\)<br/>application/x-tar: 压缩包\(tar\)<br/>application/x-xar: 压缩包\(xar\)<br/>application/x-xliff+xml: xlf文件<br/>application/x-xz: 压缩包\(xz\)<br/>application/zip: 压缩包\(zip\)<br/>application/zstd: 压缩包\(zst\)<br/>audio/aac: 音视频\(aac\)<br/>audio/aiff: 音视频\(aiff\)<br/>audio/amr: 音视频\(amr\)<br/>audio/ape: 音视频\(ape\)<br/>audio/basic: 音视频\(au\)<br/>audio/flac: 音视频\(flac\)<br/>audio/midi: 音视频\(midi\)<br/>audio/mp4: 音视频\(mp4\)<br/>audio/mpeg: 音视频\(mp3\)<br/>audio/musepack: 音视频\(mpc\)<br/>audio/ogg: 音视频\(oga\)<br/>audio/qcelp: 音视频\(qcp\)<br/>audio/wav: 音视频\(wav\)<br/>audio/x-m4a: 音视频\(m4a\)<br/>audio/x-unknown: 音视频\(voc\)<br/>font/collection: 字体文件\(ttc\)<br/>font/otf: 字体文件\(otf\)<br/>font/ttf: 字体文件\(ttf\)<br/>font/woff: 字体文件\(woff\)<br/>font/woff2: 字体文件\(woff2\)<br/>image/avif: 图片\(avif\)<br/>image/bmp: 图片\(bmp\)<br/>image/bpg: 图片\(bpg\)<br/>image/gif: 图片\(gif\)<br/>image/heic: 图片\(heic\)<br/>image/heic-sequence: 图片\(heic-sequence\)<br/>image/heif: 图片\(heif\)<br/>image/heif-sequence: 图片\(heif-sequence\)<br/>image/jp2: 图片\(jp2\)<br/>image/jpeg: 图片\(jpeg\)<br/>image/jpm: 图片\(jpm\)<br/>image/jpx: 图片\(jpx\)<br/>image/jxl: 图片\(jxl\)<br/>image/jxr: 图片\(jxr\)<br/>image/jxs: 图片\(jxs\)<br/>image/png: 图片\(png\)<br/>image/svg+xml: 图片\(svg\)<br/>image/tiff: 图片\(tiff\)<br/>image/vnd.adobe.photoshop: psd文件<br/>image/vnd.djvu: 图片\(djvu\)<br/>image/vnd.dwg: 图片\(dwg\)<br/>image/vnd.mozilla.apng: 图片\(apng\)<br/>image/vnd.radiance: 图片\(hdr\)<br/>image/webp: 图片\(webp\)<br/>image/x-gimp-gbr: 图片\(gbr\)<br/>image/x-gimp-pat: 图片\(pat\)<br/>image/x-icns: 图标\(icns\)<br/>image/x-icon: 图标\(ico\)<br/>image/x-xcf: 图片\(xcf\)<br/>image/x-xpixmap: 图片\(xpm\)<br/>model/gltf-binary: glb文件<br/>model/vnd.collada+xml: dae文件<br/>model/x3d+xml: x3d文件<br/>SFX\_7Z: 自解压安装包（7Z）<br/>SFX\_NSIS: NSIS安装包<br/>SFX\_ZIP: 自解压安装包（ZIP）<br/>text/calendar: ics文件<br/>text/csv: csv文件<br/>text/html: html文件<br/>text/plain: txt文件<br/>text/rtf: 富文本<br/>text/tab-separated-values: tsv文件<br/>text/vcard: vcf文件<br/>text/vtt: vtt文件<br/>text/x-lua: 代码\(lua\)<br/>text/xml: xml文件<br/>text/x-perl: 代码\(perl\)<br/>text/x-php: 代码\(php\)<br/>text/x-python: 代码\(python\)<br/>text/x-tcl: 代码\(tcl\)<br/>unknown: 未知格式<br/>video/3gpp: 音视频\(3gpp\)<br/>video/3gpp2: 音视频\(3g2\)<br/>video/mp4: 音视频\(mp4\)<br/>video/mpeg: 音视频\(mpeg\)<br/>video/ogg: 音视频\(ogv\)<br/>video/quicktime: 音视频\(mov/mqv\)<br/>video/webm: 音视频\(webm\)<br/>video/x-flv: 音视频\(flv\)<br/>video/x-m4v: 音视频\(m4v\)<br/>video/x-matroska: 音视频\(mkv\)<br/>video/x-ms-asf: 音视频\(asf\)<br/>video/x-msvideo: 音视频\(avi\) |
| 264 | Child.RegKeyPath | string | 注册表路径 |  |
| 265 | Child.RegValName | string | 注册表值名 |  |
| 266 | Child.RegValType | int | 注册表值类型 | 1: 字符串<br/>11: QWORD（64位整数）<br/>2: 可扩展字符串<br/>3: 二进制<br/>4: DWORD（32位整数）<br/>7: 多字符串 |
| 267 | Child.RegValData | string | 注册表值数据 |  |
| 268 | Child.RegOldValType | int | 注册表旧值类型 | 1: 字符串<br/>11: QWORD（64位整数）<br/>2: 可扩展字符串<br/>3: 二进制<br/>4: DWORD（32位整数）<br/>7: 多字符串 |
| 269 | Child.RegOldValData | string | 注册表旧值数据 |  |
| 270 | Child.RegGroupName | string | 注册表分组名称 | DOS虚拟机程序: DOS虚拟机程序<br/>IE临时文件夹: IE临时文件夹<br/>IE安全性设置: IE安全性设置<br/>IE插件扩展: IE插件扩展<br/>IE浏览器路径: IE浏览器路径<br/>IE源码查看器: IE源码查看器<br/>INI文件劫持: INI文件劫持<br/>IPSec策略设置: IPSec策略设置<br/>IP安全组策略: IP安全组策略<br/>SHELL名字空间: SHELL名字空间<br/>TCPIP网络设置: TCPIP网络设置<br/>URL前缀: URL前缀<br/>URL协议关联: URL协议关联<br/>Windows防火墙: Windows防火墙<br/>分层网络协议: 分层网络协议<br/>协议关联图标: 协议关联图标<br/>右键菜单: 右键菜单<br/>启动文件夹: 启动文件夹<br/>启动项: 启动项<br/>启动项登录脚本: 启动项登录脚本<br/>命令行劫持: 命令行劫持<br/>命令行工具: 命令行工具<br/>安全模式配置: 安全模式配置<br/>应用卸载设置: 应用卸载设置<br/>打印机支持程序: 打印机支持程序<br/>控制面板设置: 控制面板设置<br/>敏感启动项: 敏感启动项<br/>文件关联: 文件关联<br/>映像劫持: 映像劫持<br/>服务支持程序: 服务支持程序<br/>本地安全策略: 本地安全策略<br/>本地账户凭证: 本地账户凭证<br/>浏览器侧边栏: 浏览器侧边栏<br/>浏览器工具条: 浏览器工具条<br/>浏览器工具栏按钮: 浏览器工具栏按钮<br/>浏览器插件: 浏览器插件<br/>浏览器插件: 浏览器插件<br/>浏览器通信协议: 浏览器通信协议<br/>浏览器首页设置: 浏览器首页设置<br/>浏览器默认下载工具: 浏览器默认下载工具<br/>浏览器默认搜索引擎: 浏览器默认搜索引擎<br/>漏洞CLSID: 漏洞CLSID<br/>系统动态组件: 系统动态组件<br/>系统启动校验程序: 系统启动校验程序<br/>系统常用文件夹: 系统常用文件夹<br/>系统服务: 系统服务<br/>系统环境变量: 系统环境变量<br/>系统登录初始化程序: 系统登录初始化程序<br/>系统登录界面: 系统登录界面<br/>系统登录管理: 系统登录管理<br/>系统登录脚本: 系统登录脚本<br/>系统登陆管理项: 系统登陆管理项<br/>系统证书: 系统证书<br/>系统配置策略: 系统配置策略<br/>组策略启动项: 组策略启动项<br/>组策略脚本启动项: 组策略脚本启动项<br/>网络远程调用协议: 网络远程调用协议<br/>老版操作系统启动项: 老版操作系统启动项<br/>输入法设置: 输入法设置<br/>进程预加载项: 进程预加载项<br/>远程桌面服务: 远程桌面服务<br/>隐藏文件夹选项: 隐藏文件夹选项<br/>隐藏桌面图标设置: 隐藏桌面图标设置<br/>默认任务管理器: 默认任务管理器<br/>默认加载库: 默认加载库<br/>默认字库设置: 默认字库设置<br/>默认屏保程序: 默认屏保程序<br/>默认浏览器设置: 默认浏览器设置<br/>默认输入法设置: 默认输入法设置 |
| 271 | Child.Type | string | 节点类型 | ApiCall: 系統API<br/>File: 文件<br/>FileStatics: 文件统计<br/>Log: 日志<br/>Network: 网络<br/>Pipe: 管道<br/>Pipe: 管道<br/>Proc: 进程<br/>Reg: 注册表<br/>Script: 脚本 |
| 272 | Child.NodeName | string | 节点名称 |  |
| 273 | Child.ThreadId | int | 线程ID |  |
| 274 | Child.ProcGuid | string | 进程唯一ID |  |
| 275 | Child.ProcIntegrity | int | 进程完整性级别 | 1: 不可信<br/>2: 低<br/>3: 中<br/>4: 中+<br/>5: 高<br/>6: 系统<br/>7: 保护进程 |
| 276 | Child.ProcElevationType | int | 进程提权类型 | 1: UAC关闭<br/>2: UAC提权<br/>3: UAC限制权限 |
| 277 | Child.ProcExited | bool | 进程退出标志 |  |
| 278 | Child.ProcArch | string | 进程架构 | x64: x64<br/>x86: x86 |
| 279 | Child.ProcCpuArch | string | 进程CPU架构 | amd64: AMD64架构<br/>arm64: ARM64架构<br/>loongarch64: 龙芯64架构 |
| 280 | Child.ProcUserName | string | 进程用户名 |  |
| 281 | Child.ProcDomainName | string | 进程用户域名 |  |
| 282 | Child.ProcCurDir | string | 进程当前目录 |  |
| 283 | Child.ProcDesktop | string | 进程桌面名称 |  |
| 284 | Child.ProcTrust | string | 进程可信 | NoTrust: 不可信<br/>Trust: 可信 |
| 285 | Child.ProcChainTrust | string | 进程链可信 | NoTrust: 不可信<br/>Trust: 可信 |
| 286 | Child.ProcChainInfo | string | 进程链详情 |  |
| 287 | Child.ProcChainGuid | string | 进程链唯一ID |  |
| 288 | Child.FileStream | string | 文件流名称 |  |
| 289 | Child.FileFormat | string | 文件类型 | DLL: 动态链接库<br/>EXE: 可执行EXE<br/>NPE: 非PE<br/>SYS: 驱动<br/>Unknown: 未知格式 |
| 290 | Child.FileMd5Type | string | 文件md5类型 | FullMd5: 全文<br/>HalfMd5: 半文 |
| 291 | Child.FileSize | int | 文件大小 |  |
| 292 | Child.FileIssuer | string | 签名颁发机构 |  |
| 293 | Child.FileCompany | string | 文件公司名 |  |
| 294 | Child.FileDesc | string | 文件描述 |  |
| 295 | Child.FileVersion | string | 文件版本 |  |
| 296 | Child.FileOriginalName | string | 原始文件名 |  |
| 297 | Child.FileProductName | string | 文件产品名 |  |
| 298 | Child.FileProductVer | string | 文件产品版本号 |  |
| 299 | Child.FileLegalMark | string | 文件产品商标 |  |
| 300 | Child.FileCopyright | string | 文件版权 |  |
| 301 | Child.FileModifyTime | int | 文件修改时间 |  |
| 302 | Child.FileAccessTime | int | 文件访问时间 |  |
| 303 | Child.FileCreateTime | int | 文件创建时间 |  |
| 304 | Child.FileTags | string | 文件标签 | Browser: 浏览器渠道<br/>Browser:114高速浏览器: 114高速浏览器下载<br/>Browser:115极速浏览器: 115极速浏览器下载<br/>Browser:115浏览器: 115浏览器下载<br/>Browser:2345加速浏览器: 2345加速浏览器下载<br/>Browser:2345智能浏览器: 2345智能浏览器下载<br/>Browser:360安全浏览器: 360安全浏览器下载<br/>Browser:360极速浏览器: 360极速浏览器下载<br/>Browser:Edge浏览器: Edge浏览器下载<br/>Browser:GreenBrowser: GreenBrowser下载<br/>Browser:GT游戏浏览器: GT游戏浏览器下载<br/>Browser:hao123桔子浏览器: hao123桔子浏览器下载<br/>Browser:IE浏览器: IE浏览器下载<br/>Browser:iQ浏览器: iQ浏览器下载<br/>Browser:KR浏览器: KR浏览器下载<br/>Browser:MyIE浏览器: MyIE浏览器下载<br/>Browser:Opera: Opera下载<br/>Browser:QQ浏览器: QQ浏览器下载<br/>Browser:Safari浏览器: Safari浏览器下载<br/>BrowserSoft: 浏览器软件<br/>Browser:Spartan浏览器: Spartan浏览器下载<br/>Browser:TT浏览器: TT浏览器下载<br/>Browser:UC浏览器: UC浏览器下载<br/>Browser:YY浏览器: YY浏览器下载<br/>Browser:世界之窗浏览器: 世界之窗浏览器下载<br/>Browser:世界之窗浏览器极速版: 世界之窗浏览器极速版下载<br/>Browser:傲游浏览器: 傲游浏览器下载<br/>Browser:搜狗浏览器: 搜狗浏览器下载<br/>Browser:淘宝浏览器: 淘宝浏览器下载<br/>Browser:火狐浏览器: 火狐浏览器下载<br/>Browser:猎豹浏览器: 猎豹浏览器下载<br/>Browser:瑞影浏览器: 瑞影浏览器下载<br/>Browser:百度浏览器: 百度浏览器下载<br/>Browser:百度浏览器hao123专版: 百度浏览器hao123专版下载<br/>Browser:糖果浏览器: 糖果浏览器下载<br/>Browser:花儿世界浏览器: 花儿世界浏览器下载<br/>Browser:谷歌浏览器: 谷歌浏览器下载<br/>Browser:超速浏览器: 超速浏览器下载<br/>Browser:闪游浏览器: 闪游浏览器下载<br/>Browser:随E浏览器: 随E浏览器下载<br/>Browser:青猴浏览器: 青猴浏览器下载<br/>ChildNode: 操作目标<br/>DllHijack: DLL劫持<br/>Downloader: 下载器渠道<br/>Downloader:BitComet: BitComet下载<br/>Downloader:IDMan: IDMan下载<br/>Downloader:QQ旋风: QQ旋风下载<br/>Downloader:QQ旋风下载助手: QQ旋风下载助手下载<br/>Downloader:RaySource: RaySource下载<br/>DownloaderSoft: 下载软件<br/>Downloader:旋风高速下载引擎: 旋风高速下载<br/>Downloader:比特彗星: 比特彗星下载<br/>Downloader:电驴: 电驴下载<br/>Downloader:百度下载助手: 百度下载助手下载<br/>Downloader:百度云管家: 百度云管家下载<br/>Downloader:网际快车: 网际快车下载<br/>Downloader:网页迅雷: 网页迅雷下载<br/>Downloader:迅雷: 迅雷下载<br/>Downloader:迅雷云加速: 迅雷云加速下载<br/>Downloader:迅雷精简版: 迅雷精简版下载<br/>Downloader:迅雷迷你版: 迅雷迷你版下载<br/>Downloader:迷你快车: 迷你快车下载<br/>Downloader:迷你电驴: 迷你电驴下载<br/>Downloader:飞鸟下载器: 飞鸟下载器下载<br/>IM: IM渠道<br/>IM:FSLink: FSLink下载<br/>IM:MSN: MSN下载<br/>IM:Skype: Skype下载<br/>IMSoft: IM软件<br/>IM:YY语音: YY语音下载<br/>IM:京东咚咚: 京东咚咚下载<br/>IM:企业微信: 企业微信下载<br/>IM:微信: 微信下载<br/>IM:易信: 易信下载<br/>IM:润工作: 润工作下载<br/>IM:环信: 环信下载<br/>IM:百度Hi: 百度Hi下载<br/>IM:百度Hi: 百度Hi下载<br/>IM:网易CC语音: 网易CC语音下载<br/>IM:网易云信: 网易云信下载<br/>IM:腾讯QQ: 腾讯QQ下载<br/>IM:腾讯TM: 腾讯TM下载<br/>IM:腾讯通\(RTX\): 腾讯通\(RTX\)下载<br/>IM:钉钉: 钉钉下载<br/>IM:阿里旺旺: 阿里旺旺下载<br/>IM:飞书: 飞书下载<br/>IM:飞信: 飞信下载<br/>InjectProc: 进程注入<br/>Mail: 邮箱渠道<br/>Mail:139邮箱: 139邮箱下载<br/>Mail:Foxmail: Foxmail下载<br/>Mail:PP助手: OutLook下载<br/>MailSoft: 邮箱软件<br/>Mail:新浪邮箱: 新浪邮箱下载<br/>Mail:网易邮箱: 网易邮箱下载<br/>Mail:阿里邮箱: 阿里邮箱下载<br/>NetDisk: 网盘渠道<br/>NetDisk:115网盘: 115网盘下载<br/>NetDisk:360云盘: 360云盘下载<br/>NetDisk:360网盘: 360网盘下载<br/>NetDiskSoft: 网盘软件<br/>NetDisk:优蛋: 优蛋下载<br/>NetDisk:华为网盘: 华为网盘下载<br/>NetDisk:坚果云: 坚果云下载<br/>NetDisk:城通网盘: 城通网盘下载<br/>NetDisk:天翼云盘: 天翼云盘下载<br/>NetDisk:夸克网盘: 夸克网盘下载<br/>NetDisk:微云: 微云下载<br/>NetDisk:微盘: 微盘下载<br/>NetDisk:百度网盘: 百度网盘下载<br/>NetDisk:纳米盘: 纳米盘下载<br/>NetDisk:酷盘: 酷盘下载<br/>NetDisk:金山快盘: 金山快盘下载<br/>NetDisk:阿里云盘: 阿里云盘下载<br/>NetShare: 网络共享渠道<br/>NewFile: 新入文件<br/>NewFileExec: 新入执行<br/>NewFileInject: 新入注入<br/>NewSuspicious: 新入可疑<br/>ParentNode: 操作者<br/>SoftMgr: 软件管理渠道<br/>SoftMgr:2345软件管家: 2345软件管家下载<br/>SoftMgr:360安全卫士: 360安全卫士下载<br/>SoftMgr:360驱动大师: 360驱动大师下载<br/>SoftMgr:91手机助手: 91手机助手下载<br/>SoftMgr:PP助手: PP助手下载<br/>SoftMgrSoft: 软件管理软件<br/>SoftMgr:天极软件管家: 天极软件管家下载<br/>SoftMgr:微软电脑管家: 微软电脑管家下载<br/>SoftMgr:搜狗手机助手: 搜狗手机助手下载<br/>SoftMgr:爱思助手: 爱思助手下载<br/>SoftMgr:联想电脑管家: 联想电脑管家下载<br/>SoftMgr:腾讯电脑管家: 腾讯电脑管家下载<br/>SoftMgr:豌豆荚2: 豌豆荚2下载<br/>SoftMgr:软媒魔方软件管理: 软媒魔方软件管理下载<br/>SoftMgr:金山手机助手: 金山手机助手下载<br/>SoftMgr:金山毒霸: 金山毒霸下载<br/>SoftMgr:风灵软件管家: 风灵软件管家下载<br/>SoftMgr:驱动人生: 驱动人生下载<br/>SoftMgr:驱动人生软件管理: 驱动人生软件管理下载<br/>SoftMgr:驱动精灵: 驱动精灵下载<br/>TrustSource: 可信进程释放<br/>UnknownSource: 未知进程释放 |
| 305 | Child.FileMappingType | mask | 映射方式 | 0x04: 读写<br/>0x08: 写复制<br/>0x10: 执行<br/>0x20: 执行读<br/>0x40: 执行读写<br/>0x80: 执行写复制 |
| 306 | Child.FileCreateOpName | string | 打开方式 | CREATE: 新建文件<br/>OPEN: 打开文件<br/>OVERWRITE: 覆盖写文件 |
| 307 | Child.FileCreateDisposition | int | 打开位置 | 1: 新建<br/>2: 新建覆盖<br/>3: 打开新建<br/>4: 打开存在<br/>5: 打开清空 |
| 308 | Child.FileCreateDesiredAccess | mask | 打开权限 | 0x10000000: 所有权限<br/>0x20000000: 执行权限<br/>0x40000000: 写权限<br/>0x80000000: 读权限 |
| 309 | Child.FileCreateShareAccess | mask | 共享权限 | 0x1: 共享读<br/>0x2: 共享写<br/>0x4: 共享删除 |
| 310 | Child.FileCreateFileAttributes | mask | 设置属性 | 0x1: 只读\(0x1\)<br/>0x100: 临时\(0x100\)<br/>0x2: 隐藏\(0x2\)<br/>0x4: 系统\(0x4\)<br/>0x40: 设备\(0x40\)<br/>0x80: 常规\(0x80\) |
| 311 | Child.FileTotalWrite | int | 文件写入大小 |  |
| 312 | Child.FileTotalRead | int | 文件读取大小 |  |
| 313 | Child.OldFilePath | string | 源文件路径 |  |
| 314 | Child.OldFileTags | string | 源文件标签 | Browser: 浏览器渠道<br/>Browser:114高速浏览器: 114高速浏览器下载<br/>Browser:115极速浏览器: 115极速浏览器下载<br/>Browser:115浏览器: 115浏览器下载<br/>Browser:2345加速浏览器: 2345加速浏览器下载<br/>Browser:2345智能浏览器: 2345智能浏览器下载<br/>Browser:360安全浏览器: 360安全浏览器下载<br/>Browser:360极速浏览器: 360极速浏览器下载<br/>Browser:Edge浏览器: Edge浏览器下载<br/>Browser:GreenBrowser: GreenBrowser下载<br/>Browser:GT游戏浏览器: GT游戏浏览器下载<br/>Browser:hao123桔子浏览器: hao123桔子浏览器下载<br/>Browser:IE浏览器: IE浏览器下载<br/>Browser:iQ浏览器: iQ浏览器下载<br/>Browser:KR浏览器: KR浏览器下载<br/>Browser:MyIE浏览器: MyIE浏览器下载<br/>Browser:Opera: Opera下载<br/>Browser:QQ浏览器: QQ浏览器下载<br/>Browser:Safari浏览器: Safari浏览器下载<br/>BrowserSoft: 浏览器软件<br/>Browser:Spartan浏览器: Spartan浏览器下载<br/>Browser:TT浏览器: TT浏览器下载<br/>Browser:UC浏览器: UC浏览器下载<br/>Browser:YY浏览器: YY浏览器下载<br/>Browser:世界之窗浏览器: 世界之窗浏览器下载<br/>Browser:世界之窗浏览器极速版: 世界之窗浏览器极速版下载<br/>Browser:傲游浏览器: 傲游浏览器下载<br/>Browser:搜狗浏览器: 搜狗浏览器下载<br/>Browser:淘宝浏览器: 淘宝浏览器下载<br/>Browser:火狐浏览器: 火狐浏览器下载<br/>Browser:猎豹浏览器: 猎豹浏览器下载<br/>Browser:瑞影浏览器: 瑞影浏览器下载<br/>Browser:百度浏览器: 百度浏览器下载<br/>Browser:百度浏览器hao123专版: 百度浏览器hao123专版下载<br/>Browser:糖果浏览器: 糖果浏览器下载<br/>Browser:花儿世界浏览器: 花儿世界浏览器下载<br/>Browser:谷歌浏览器: 谷歌浏览器下载<br/>Browser:超速浏览器: 超速浏览器下载<br/>Browser:闪游浏览器: 闪游浏览器下载<br/>Browser:随E浏览器: 随E浏览器下载<br/>Browser:青猴浏览器: 青猴浏览器下载<br/>ChildNode: 操作目标<br/>DllHijack: DLL劫持<br/>Downloader: 下载器渠道<br/>Downloader:BitComet: BitComet下载<br/>Downloader:IDMan: IDMan下载<br/>Downloader:QQ旋风: QQ旋风下载<br/>Downloader:QQ旋风下载助手: QQ旋风下载助手下载<br/>Downloader:RaySource: RaySource下载<br/>DownloaderSoft: 下载软件<br/>Downloader:旋风高速下载引擎: 旋风高速下载<br/>Downloader:比特彗星: 比特彗星下载<br/>Downloader:电驴: 电驴下载<br/>Downloader:百度下载助手: 百度下载助手下载<br/>Downloader:百度云管家: 百度云管家下载<br/>Downloader:网际快车: 网际快车下载<br/>Downloader:网页迅雷: 网页迅雷下载<br/>Downloader:迅雷: 迅雷下载<br/>Downloader:迅雷云加速: 迅雷云加速下载<br/>Downloader:迅雷精简版: 迅雷精简版下载<br/>Downloader:迅雷迷你版: 迅雷迷你版下载<br/>Downloader:迷你快车: 迷你快车下载<br/>Downloader:迷你电驴: 迷你电驴下载<br/>Downloader:飞鸟下载器: 飞鸟下载器下载<br/>IM: IM渠道<br/>IM:FSLink: FSLink下载<br/>IM:MSN: MSN下载<br/>IM:Skype: Skype下载<br/>IMSoft: IM软件<br/>IM:YY语音: YY语音下载<br/>IM:京东咚咚: 京东咚咚下载<br/>IM:企业微信: 企业微信下载<br/>IM:微信: 微信下载<br/>IM:易信: 易信下载<br/>IM:润工作: 润工作下载<br/>IM:环信: 环信下载<br/>IM:百度Hi: 百度Hi下载<br/>IM:百度Hi: 百度Hi下载<br/>IM:网易CC语音: 网易CC语音下载<br/>IM:网易云信: 网易云信下载<br/>IM:腾讯QQ: 腾讯QQ下载<br/>IM:腾讯TM: 腾讯TM下载<br/>IM:腾讯通\(RTX\): 腾讯通\(RTX\)下载<br/>IM:钉钉: 钉钉下载<br/>IM:阿里旺旺: 阿里旺旺下载<br/>IM:飞书: 飞书下载<br/>IM:飞信: 飞信下载<br/>InjectProc: 进程注入<br/>Mail: 邮箱渠道<br/>Mail:139邮箱: 139邮箱下载<br/>Mail:Foxmail: Foxmail下载<br/>Mail:PP助手: OutLook下载<br/>MailSoft: 邮箱软件<br/>Mail:新浪邮箱: 新浪邮箱下载<br/>Mail:网易邮箱: 网易邮箱下载<br/>Mail:阿里邮箱: 阿里邮箱下载<br/>NetDisk: 网盘渠道<br/>NetDisk:115网盘: 115网盘下载<br/>NetDisk:360云盘: 360云盘下载<br/>NetDisk:360网盘: 360网盘下载<br/>NetDiskSoft: 网盘软件<br/>NetDisk:优蛋: 优蛋下载<br/>NetDisk:华为网盘: 华为网盘下载<br/>NetDisk:坚果云: 坚果云下载<br/>NetDisk:城通网盘: 城通网盘下载<br/>NetDisk:天翼云盘: 天翼云盘下载<br/>NetDisk:夸克网盘: 夸克网盘下载<br/>NetDisk:微云: 微云下载<br/>NetDisk:微盘: 微盘下载<br/>NetDisk:百度网盘: 百度网盘下载<br/>NetDisk:纳米盘: 纳米盘下载<br/>NetDisk:酷盘: 酷盘下载<br/>NetDisk:金山快盘: 金山快盘下载<br/>NetDisk:阿里云盘: 阿里云盘下载<br/>NetShare: 网络共享渠道<br/>NewFile: 新入文件<br/>NewFileExec: 新入执行<br/>NewFileInject: 新入注入<br/>NewSuspicious: 新入可疑<br/>ParentNode: 操作者<br/>SoftMgr: 软件管理渠道<br/>SoftMgr:2345软件管家: 2345软件管家下载<br/>SoftMgr:360安全卫士: 360安全卫士下载<br/>SoftMgr:360驱动大师: 360驱动大师下载<br/>SoftMgr:91手机助手: 91手机助手下载<br/>SoftMgr:PP助手: PP助手下载<br/>SoftMgrSoft: 软件管理软件<br/>SoftMgr:天极软件管家: 天极软件管家下载<br/>SoftMgr:微软电脑管家: 微软电脑管家下载<br/>SoftMgr:搜狗手机助手: 搜狗手机助手下载<br/>SoftMgr:爱思助手: 爱思助手下载<br/>SoftMgr:联想电脑管家: 联想电脑管家下载<br/>SoftMgr:腾讯电脑管家: 腾讯电脑管家下载<br/>SoftMgr:豌豆荚2: 豌豆荚2下载<br/>SoftMgr:软媒魔方软件管理: 软媒魔方软件管理下载<br/>SoftMgr:金山手机助手: 金山手机助手下载<br/>SoftMgr:金山毒霸: 金山毒霸下载<br/>SoftMgr:风灵软件管家: 风灵软件管家下载<br/>SoftMgr:驱动人生: 驱动人生下载<br/>SoftMgr:驱动人生软件管理: 驱动人生软件管理下载<br/>SoftMgr:驱动精灵: 驱动精灵下载<br/>TrustSource: 可信进程释放<br/>UnknownSource: 未知进程释放 |
| 315 | Child.FileSecurityAttr | mask | 文件安全属性 | 0x1: 拥有者安全信息<br/>0x10: LABEL安全信息<br/>0x100: 备份安全信息<br/>0x10000000: 未保护的SACL安全信息<br/>0x2: 组安全信息<br/>0x20: 属性安全信息<br/>0x20000000: 未保护的DACL安全信息<br/>0x4: DACL安全信息<br/>0x40: 范围安全信息<br/>0x40000000: 保护的SACL安全信息<br/>0x8: SACL安全信息<br/>0x80: 进程信任LABEL安全信息<br/>0x80000000: 保护的DACL安全信息 |
| 316 | Child.FileAttr | mask | 文件属性 | 0x1: 只读\(0x1\)<br/>0x100: 临时\(0x100\)<br/>0x2: 隐藏\(0x2\)<br/>0x4: 系统\(0x4\)<br/>0x40: 设备\(0x40\)<br/>0x80: 常规\(0x80\) |
| 317 | Child.ModifyCreateTime | mask | 修改创建时间 |  |
| 318 | Child.SetBasicOp | mask | 设置类型 | 0x1: 设置属性<br/>0x2: 修改创建时间 |
| 319 | Child.TrojanName | string | 病毒名 |  |
| 320 | Child.ModuleSize | int | 模块大小 |  |
| 321 | Child.ModuleBase | int | 模块起始地址 |  |
| 322 | Child.Cx | int | 坐标X |  |
| 323 | Child.Cy | int | 坐标Y |  |
| 324 | Child.WindowName | string | 窗口名 |  |
| 325 | Child.ClassName | string | 类名 |  |
| 326 | Child.AppVersion | int | 应用版本号 |  |
| 327 | Child.OpName | string | 操作方式 | COPY: 拷贝<br/>DELETE: 删除<br/>MOVE: 移动<br/>RENAME: 重命名 |
| 328 | Child.PipeOpName | string | 管道操作名称 | CREATE: 创建管道<br/>OPEN: 打开管道 |
| 329 | Child.PipeName | string | 管道名 |  |
| 330 | Child.RemoteThreadOpName | string | 线程操作名 |  |
| 331 | Child.ThreadStartAddr | int | 线程起始地址 |  |
| 332 | Child.HandleObjectOpName | string | 句柄操作名称 |  |
| 333 | Child.HandleAccessMask | int | 句柄访问权限 | 0x1: 结束进程<br/>0x10: 虚拟内存读<br/>0x100: 设置配额<br/>0x2: 创建线程<br/>0x20: 虚拟内存写<br/>0x4: 设置会话ID<br/>0x8: 虚拟内存操作<br/>0x80: 创建进程 |
| 334 | Child.DirPath | string | 目录路径 |  |
| 335 | Child.QueryClass | int | 信息类别 | 1: 目录信息<br/>2: 完整目录信息<br/>3: 额外目录信息<br/>4: 基础信息<br/>5: 标准信息 |
| 336 | Child.LnkName | string | 快捷方式名称 |  |
| 337 | Child.LnkPath | string | 快捷方式路径 |  |
| 338 | Child.LnkArgs | string | 快捷方式参数 |  |
| 339 | Child.ScriptFileName | string | 脚本名 |  |
| 340 | Child.ScriptFilePath | string | 脚本路径 |  |
| 341 | Child.ScriptFileMd5 | string | 脚本MD5 |  |
| 342 | Child.ScriptFileMd5Type | string | 脚本md5类型 | FullMd5: 全文<br/>HalfMd5: 半文 |
| 343 | Child.ScriptContent | string | 脚本内容 |  |
| 344 | Child.Sender | string | 邮件发件人 |  |
| 345 | Child.Subject | string | 邮件标题 |  |
| 346 | Child.Links | string | 邮件链接 |  |
| 347 | Child.Attachment | string | 邮件附件 |  |
| 348 | Child.FileStElapsedTime | int | 统计时长 |  |
| 349 | Child.FileStEnumDirCnt | int | 枚举目录数 |  |
| 350 | Child.FileStWriteDirCnt | int | 写入包含目录数 |  |
| 351 | Child.FileStWriteFileCnt | int | 写入文件数 |  |
| 352 | Child.FileStWriteExtCnt | int | 写入文件后缀数 |  |
| 353 | Child.FileSWriteSize | int | 写入大小 |  |
| 354 | Child.FileSWriteSpeed | int | 写入速度 |  |
| 355 | Child.FileStRenameDirCnt | int | 重命名包含目录数 |  |
| 356 | Child.FileStRenameFileCnt | int | 重命名文件数 |  |
| 357 | Child.FileStRenameExtCnt | int | 重命名文件后缀数 |  |
| 358 | Child.FileStRenameSrcExtCnt | int | 重命名文件源后缀数 |  |
| 359 | Child.FileStDeleteDirCnt | int | 删除包含目录数 |  |
| 360 | Child.FileStDeleteFileCnt | int | 删除文件数 |  |
| 361 | Child.FileStDeleteExtCnt | int | 删除文件后缀数 |  |
| 362 | Child.FileStExtWriteDirCnt | int | 后缀包含写入目录数 |  |
| 363 | Child.FileStExtWriteFileCnt | int | 后缀包含写入文件数 |  |
| 364 | Child.FileStExtWriteSize | int | 后缀包含写入文件大小 |  |
| 365 | Child.FileStExtDeleteDirCnt | int | 后缀包含删除目录数 |  |
| 366 | Child.FileStExtDeleteFileCnt | int | 后缀包含删除文件数 |  |
| 367 | Child.FileStExtRenameDirCnt | int | 后缀包含重命名目录数 |  |
| 368 | Child.FileStExtRenameFileCnt | int | 后缀包含重命名文件数 |  |
| 369 | Child.FileStExtRenameSrcExtCnt | int | 后缀包含重命名源后缀数 |  |
| 370 | Child.FileStExtName | string | 统计后缀名 |  |
| 371 | Child.VulId | int | 漏洞Id |  |
| 372 | Child.RemoteInjectEvent | string | 注入事件名称 |  |
| 373 | Child.RemoteProcPid | int | 远程进程Pid |  |
| 374 | Child.RemoteProcGuid | string | 远程进程唯一ID |  |
| 375 | Child.RemoteProcCmdline | string | 远程进程命令行 |  |
| 376 | Child.RemoteProcPid | int | 远程线程ID |  |
| 377 | Child.RemoteFileName | string | 远程进程名 |  |
| 378 | Child.RemoteFilePath | string | 远程进程路径 |  |
| 379 | Child.RemoteFileMd5 | string | 远程进程md5 |  |
| 380 | Child.RemoteFileMd5Type | string | 远程进程md5类型 | FullMd5: 全文<br/>HalfMd5: 半文 |
| 381 | Child.RemoteThreadId | int | 注入线程ID |  |
| 382 | Child.RemoteModuleName | string | 注入模块名 |  |
| 383 | Child.RemoteModulePath | string | 注入模块路径 |  |
| 384 | Child.RemoteModuleMd5 | string | 注入模块md5 |  |
| 385 | Child.RemoteModuleMd5Type | string | 注入模块md5类型 | FullMd5: 全文<br/>HalfMd5: 半文 |
| 386 | Child.RemoteModuleSize | int | 注入模块大小 |  |
| 387 | Child.RemoteModuleBase | int | 注入模块起始地址 |  |
| 388 | Child.FileSourceUrl | string | 文件来源URL |  |
| 389 | Common | object | 基础信息 |  |
| 390 | Common.Mid | string | 唯一标识码 |  |
| 391 | Common.ClientVer | string | 客户端版本号 |  |
| 392 | Common.EventId | int | 事件自增ID |  |
| 393 | Common.EventUUId | string | 事件唯一ID |  |
| 394 | Common.SessionId | int | 客户端启动号 |  |
| 395 | Common.KernelId | int | 内核事件ID |  |
| 396 | Common.Source | string | 事件来源 |  |
| 397 | Common.EventTime | int | 事件采集时间 |  |
| 398 | Common.AuthId | int | iOA授权ID |  |
| 399 | Common.Uid | int | iOA登录用户ID |  |
| 400 | Common.UserName | string | 企业账户 |  |
| 401 | Common.LoginStatus | int | 登录状态 | 1: 登录<br/>2: 未登录 |
| 402 | Common.Guid | string | GuidEx |  |
| 403 | Common.DeviceGroup | string | 终端分组信息 |  |
| 404 | Common.ReportId | int | 数据上报ID |  |
| 405 | Common.AgentMode | int | Agent模式 | 0: 全功能版本<br/>1: miniEDR版本 |
| 406 | Common.MonitorId | int | 监控点ID |  |
| 407 | Common.MonitorGroupId | int | 监控点组ID |  |
| 408 | Environment | object | 系统环境信息 |  |
| 409 | Environment.OsBit | string | 系统位数 | 32: 32位<br/>64: 64位 |
| 410 | Environment.OsVersion | string | 系统版本 | Win10: Win10<br/>Win11: Win11<br/>Win2000: Win2000<br/>Win2003: Win2003<br/>Win7: Win7<br/>Win8: Win8<br/>WinFuture: WinFuture<br/>WinVista: WinVista<br/>WinXP: WinXP |
| 411 | Environment.OsBuild | int | 系统build号 |  |
| 412 | Environment.OsProduectDesc | string | 系统版本描述 |  |
| 413 | Environment.OsUserName | string | 系统登录用户名 |  |
| 414 | Environment.SysStartTimes | int | 系统启动时间 |  |
| 415 | Environment.HostName | string | 主机名称 |  |
| 416 | Environment.ExportIp | string | 出口IP |  |
| 417 | Environment.MacAddr | string | MAC地址 |  |
| 418 | Environment.DomainName | string | 域 |  |
| 419 | Environment.OsType | string | 系统类型 | Linux: Linux<br/>macOS: macOS<br/>Windows: Windows |
| 420 | Alert | object | 告警字段 |  |
| 421 | Alert.RuleId | int | 命中的规则ID |  |
| 422 | Alert.RuleName | string | 命中规则名称 |  |
| 423 | Alert.RuleNameEN | string | 命中规则名称\(英文\) |  |
| 424 | Alert.RuleNature | int | 命中规则特性 | 0: 探针<br/>1: 告警<br/>100: 白名单 |
| 425 | Alert.EventUuid | string | 告警去重ID |  |
| 426 | Alert.FixResult | string | 处置结果 |  |
| 427 | Alert.FixAction | string | 处置动作 |  |
| 428 | Alert.FixType | string | 处置方式 |  |
| 429 | Alert.UserOpt | string | 用户选择 |  |
| 430 | Alert.AlertSource | string | 告警来源 |  |
| 431 | Alert.BlockType | string | 拦截方式 |  |
| 432 | Alert.CloudRuleId | int | 云规则Id |  |
| 433 | Alert.CloudTitle | string | 云规则标题 |  |
| 434 | Alert.CloudEngineName | string | 云判定引擎 |  |
| 435 | Alert.ExplainTags | string | 家族信息 |  |
| 436 | Alert.Whois | string | 域名信息 |  |
| 437 | Alert.YaraRuleId | string | Yara规则ID |  |
| 438 | Alert.YaraRuleTag | string | Yara规则标签 |  |

##### 采集日志动作类型取值范围

| 唯一key | 说明 |
| :--- | :--- |
| Proc | 进程 |
| File | 文件 |
| Module | 加载模块 |
| Reg | 注册表 |
| Network | 网络 |
| WinEventLog | 系统日志 |
| InjectHook | 系统API |
| Script | 脚本文档 |
| LeftMove | 横向移动 |
| Ransomware | 终端欺骗 |
| Phishing | 钓鱼攻击 |
| MemScan | 内存扫描 |
| StopChain | 断链攻击 |
| Assoc | 动作关联 |

##### 采集日志子动作名称取值范围

| 所属动作 | 唯一key | 说明 |
| :--- | :--- | :--- |
| Assoc | FileToProc | 文件关联进程 |
| Assoc | InjectPayloadToFile | 注入模块文件关联 |
| Assoc | DefRemoteInject | 未知注入动作关联 |
| Assoc | RemoteThreadInject | 远程线程注入动作关联 |
| Assoc | ApcInject | APC注入动作关联 |
| Assoc | LnkToTarget | 快捷方式关联 |
| Assoc | FileToExplorerCopy | 桌面拷贝关联 |
| Assoc | FileRenameSource | 重命名源文件关联 |
| Assoc | SrcToMove | 文件移动关联 |
| Assoc | SrcToCopy | 文件拷贝关联 |
| Assoc | SrcToRename | 文件重命名关联 |
| Assoc | RegToFile | 注册表值解析关联 |
| File | FileDelete | 文件删除 |
| File | NamedPipe | 命名管道事件 |
| File | FileStatics | 文件操作统计 |
| File | FileSetBasicInfo | 文件设置基本信息 |
| File | FileSetSecurity | 文件设置安全属性 |
| File | WriteMbr | 修改主引导记录\(MBR\) |
| File | WriteVbr | 修改卷引导记录\(VBR\) |
| File | DiskRawReadWrte | 直接读写磁盘 |
| File | FileWriteClose | 文件写关闭 |
| File | FileRename | 文件重命名 |
| File | FileRead | 文件读 |
| File | FileWrite | 文件写 |
| File | FileReadDir | 枚举目录 |
| File | FileMapping | 文件映射 |
| File | FileClose | 文件关闭句柄 |
| File | FileCreate | 文件打开 |
| InjectHook | GetRawInputData | 获取原始输入数据 |
| InjectHook | NtCreateThreadEx | 创建线程（NTDLL） |
| InjectHook | NtMapViewOfSection | 映射内存视图（NTDLL） |
| InjectHook | RtlCreateUserThread | 创建用户线程（NTDLL） |
| InjectHook | SetThreadContext | 设置线程上下文 |
| InjectHook | NtQueryInformationProcess | 获取指定进程信息 |
| InjectHook | AdjustTokenPrivileges | 调整令牌特权 |
| InjectHook | DuplicateTokenEx | 复制令牌 |
| InjectHook | ImpersonateLoggedOnUser | 线程模拟登录用户 |
| InjectHook | LookupPrivilegeValueW | 查询特权LUID |
| InjectHook | CredBackupCredentials | 备份账户凭据 |
| InjectHook | CredEnumerateW | 枚举账户凭据 |
| InjectHook | CredReadW | 读取账户凭据 |
| InjectHook | CredUnPackAuthenticationBufferW | 解析身份验证缓冲区 |
| InjectHook | SspiPrepareForCredRead | 准备加密凭据读取 |
| InjectHook | VaultEnumerateItems | 枚举账号凭据（未公开） |
| InjectHook | SpGetCredentials | 获取账户凭据（未公开） |
| InjectHook | AcquireCredentialsHandleW | 获取加密组件句柄 |
| InjectHook | NetUserEnum | 枚举服务器账号 |
| InjectHook | NetUserGetGroups | 获取账户全局组 |
| InjectHook | NetUserGetLocalGroups | 获取账号本地组 |
| InjectHook | LsaEnumerateLogonSessions | 枚举登录会话 |
| InjectHook | LsaGetLogonSessionData | 获取登录会话信息 |
| InjectHook | LsaQueryForestTrustInformation | 获取林信任信息 |
| InjectHook | WNetAddConnection2W | 本地设备映射网络资源2 |
| InjectHook | WNetAddConnectionW | 本地设备映射到网络资源 |
| InjectHook | DsEnumerateDomainTrustsW | 枚举信任域信息 |
| InjectHook | DsGetDcNameW | 获取域控制器名称 |
| InjectHook | NetGroupEnum | 枚举服务器账户组 |
| InjectHook | NetLocalGroupEnum | 枚举服务器本地组账户组 |
| InjectHook | NetShareCheck | 检查服务器共享资源 |
| InjectHook | NetShareEnum | 枚举服务器共享资源 |
| InjectHook | NetShareGetInfo | 获取服务器指定资源 |
| InjectHook | HttpOpenRequestW | 打开Http请求 |
| InjectHook | InternetConnectW | WinINet连接 |
| InjectHook | InternetOpenUrlW | WinINet打开Url |
| InjectHook | InternetOpenW | 初始化WinINet |
| InjectHook | CreateToolhelp32Snapshot | 创建进程快照 |
| InjectHook | Process32FirstW | 遍历进程快照 |
| InjectHook | EnumProcess | 枚举进程Pid |
| InjectHook | OpenFileMappingW | 打开文件映射 |
| InjectHook | FindFirstFileW | 遍历文件 |
| InjectHook | FindFirstVolumeMountPointW | 枚举指定卷挂载目录 |
| InjectHook | FindFirstVolumeW | 枚举计算机卷 |
| InjectHook | SHFileOperationW | 文件操作 |
| InjectHook | IFileOperation\_RenameItem | 重命名文件 |
| InjectHook | IFileOperation\_RenameItems | 批量重命名文件 |
| InjectHook | IFileOperation\_MoveItems | 批量移动文件 |
| InjectHook | IFileOperation\_CopyItems | 批量拷贝文件 |
| InjectHook | IFileOperation\_DeleteItems | 批量删除文件 |
| InjectHook | CopyFileExW | 拷贝文件 |
| InjectHook | MoveFileExW | 移动文件 |
| InjectHook | NetWkstaGetInfo | 获取工作站配置 |
| InjectHook | GetCurrentHwProfileW | 检索硬件配置 |
| InjectHook | GetIpNetTable | 获取IPv4映射表 |
| InjectHook | GetIpNetTable2 | 获取IPv4映射表2 |
| InjectHook | GetComputerNameExW | 获取计算机名Ex |
| InjectHook | GetComputerNameW | 获取计算机名 |
| InjectHook | GetDiskFreeSpaceExW | 获取磁盘剩余空间Ex |
| InjectHook | GetDiskFreeSpaceW | 获取磁盘剩余空间 |
| InjectHook | GetLogicalProcessorInformationEx | 获取逻辑处理器Ex |
| InjectHook | GetLogicalProcessorInformation | 获取逻辑处理器 |
| InjectHook | GetNativeSystemInfo | 获取系统信息 |
| InjectHook | RtlGetNtProductType | 获取系统产品版本（未公开） |
| InjectHook | RtlGetVersion | 获取系统版本 |
| InjectHook | GetProcAddress | 获取函数地址 |
| InjectHook | GetUserNameExW | 获取本机用户名 |
| InjectHook | ConvertSidToStringSidW | Sid转换为字符串 |
| InjectHook | ConvertStringSidToSidW | 字符串转换为Sid |
| InjectHook | FindFirstUrlCacheEntryW | 枚举浏览器缓存 |
| InjectHook | AttachThreadInput | 附加线程输入 |
| InjectHook | GetAsyncKeyState | 获取物理按键状态 |
| InjectHook | GetClipboardData | 获取剪切板数据 |
| InjectHook | GetKeyboardState | 获取键盘虚拟状态 |
| InjectHook | GetKeyState | 获取虚拟按键状态 |
| InjectHook | RegisterHotKey | 注册热键 |
| InjectHook | SetWindowsHookEx | 设置消息钩子Ex |
| InjectHook | SetWinEventHook | 设置消息钩子 |
| InjectHook | GetDC | 获取显示设备 |
| InjectHook | BitBlt | 位块传输 |
| InjectHook | CreateCompatibleBitmap | 创建兼容位图 |
| InjectHook | NtUserFindWindowEx | 查找窗口（NTAPI） |
| InjectHook | GetWindowLongPtr | 获取指定窗口信息 |
| InjectHook | GetForegroundWindow | 获取前台窗口 |
| InjectHook | SetThreadToken | 设置线程令牌 |
| InjectHook | CreateService | 创建服务 |
| InjectHook | StartService | 启动服务 |
| InjectHook | ModifyService | 修改服务 |
| InjectHook | DeleteService | 删除服务 |
| InjectHook | StopService | 停止服务 |
| InjectHook | RpcSchedTaskCreate | 计划任务创建 |
| InjectHook | ReadConsoleW | Cmd命令执行 |
| InjectHook | ComCall | Com调用 |
| InjectHook | ClearEventLogW | 清除事件日志 |
| InjectHook | DeregisterEventSource | 关闭事件日志写入 |
| InjectHook | CheckRemoteDebuggerPresent | 检查远程调试状态 |
| InjectHook | IsDebuggerPresent | 检查调试状态 |
| InjectHook | CryptAcquireContextW | 获取密钥容器句柄 |
| InjectHook | CryptDeriveKey | 创建加密密钥 |
| InjectHook | CryptUnprotectData | 解密敏感数据 |
| InjectHook | EncryptFileW | 加密文件 |
| InjectHook | CreateRemoteThread | 创建远程线程 |
| InjectHook | QueueUserAPC | APC注入 |
| InjectHook | NtQueueApcThreadEx | APC注入（NTDLL） |
| InjectHook | ReadProcessMemory | 读进程内存 |
| InjectHook | VirtualProtectEx | 修改进程内存保护 |
| InjectHook | VirtualAllocEx | 分配进程内存 |
| InjectHook | WriteProcessMemory | 写进程内存 |
| InjectHook | UuidFromStringW | 转换UUID |
| InjectHook | NtProtectVirtualMemory | 修改虚拟内存保护（NTDLL） |
| InjectHook | NtUnmapViewOfSection | 卸载映射视图（NTDLL） |
| InjectHook | NtOpenProcess | 打开进程（NTDLL） |
| InjectHook | NtWriteVirtualMemory | 写虚拟内存（NTDLL） |
| LeftMove | RemoteRegQueryValue | 远程注册表查询值 |
| LeftMove | RemoteRegRenameKey | 远程注册表修改键 |
| LeftMove | RemoteRegDeleteKey | 远程注册表删除键 |
| LeftMove | RemoteRegCreateKey | 远程注册表创建键 |
| LeftMove | RemoteSheduleTask | 远程计划任务 |
| LeftMove | RemoteAt | 远程计划任务（AT） |
| LeftMove | RemoteStopService | 远程停止服务 |
| LeftMove | RemoteDeleteService | 远程删除服务 |
| LeftMove | RemoteModifyService | 远程修改服务 |
| LeftMove | RemoteStartService | 远程启动服务 |
| LeftMove | RemoteCreateService | 远程创建服务 |
| LeftMove | RemoteWinRM | 远程WinRM访问 |
| LeftMove | FileWriteShareDir | 修改共享文件 |
| LeftMove | RemoteRegCreateValue | 远程注册表创建值 |
| LeftMove | RemotePrint | 远程打印机漏洞 |
| LeftMove | RemoteDCOM-WMI | 远程执行WMI/DCOM |
| LeftMove | RemoteRegSetValue | 远程注册表修改值 |
| MemScan | YaraMemScan | Yara内存扫描 |
| Module | LoadDriver | 加载驱动 |
| Module | LoadDll | 加载DLL |
| Network | NetConnect | 网络连接 |
| Network | SocketRequest | Socket请求 |
| Network | KerberosRequest | Kerberos请求 |
| Network | NetPing | Ping请求 |
| Network | NetBind | 网络监听 |
| Network | VulAttack | 漏洞攻击 |
| Network | SynDDos | DDos攻击 |
| Network | NetScanPort | 端口扫描 |
| Network | NetFlowStart | 网络会话流开始 |
| Network | NetFlowFinish | 网络会话流结束 |
| Network | NetFlowData | 网络会话数据 |
| Network | NetDnsQuery | DNS查询 |
| Network | HttpRequest | Http请求 |
| Network | HttpsRequest | Https请求 |
| Phishing | PhishingNet | 钓鱼外联 |
| Proc | ProcessHandleObject | 打开进程句柄 |
| Proc | RemoteThread | 远程线程注入 |
| Proc | ProcessExit | 进程退出 |
| Proc | ProcessCreate | 进程创建 |
| Ransomware | AccessUrlTrap | 访问域名 |
| Ransomware | DocTrap | 修改诱饵文件 |
| Ransomware | LoginTrap | 登录账号 |
| Reg | RegQueryValue | 注册表读取值 |
| Reg | RegDeleteValue | 注册表删除值 |
| Reg | RegSetValue | 注册表设置值 |
| Reg | RegRenameKey | 注册表重命名键 |
| Reg | RegDeleteKey | 注册表删除键 |
| Reg | RegCreateKey | 注册表创建键 |
| Script | ScriptScan | 脚本执行 |
| Script | DocumentOpen | 打开文档 |
| Script | MailOpen | 打开邮件 |
| StopChain | LnkAssoc | 快捷方式启动关联 |
| StopChain | ArchiveDecompress | 压缩包释放关联 |
| StopChain | Rundll32Exec | Rundll执行关联 |
| StopChain | CmdLineAssoc | 命令行关联 |
| WinEventLog | AccountPwdReset | 用户密码重置 |
| WinEventLog | AccountPwdChange | 用户密码更改 |
| WinEventLog | AccountCreate | 用户账户创建 |
| WinEventLog | SACLPolicyChange | SACL审核策略更改 |
| WinEventLog | UserRightAssign | 用户权限分配 |
| WinEventLog | UserTokenAdjust | 调整用户权限 |
| WinEventLog | SchedTaskUpdate | 更新计划任务 |
| WinEventLog | SchedTaskDelete | 删除计划任务 |
| WinEventLog | SystemTimeChange | 系统时间已更改 |
| WinEventLog | SchedTaskCreate | 创建计划任务 |
| WinEventLog | AuditLogClear | 安全日志清除记录 |
| WinEventLog | LogShutdown | 事件日志记录服务已关闭 |
| WinEventLog | WmiCreateProcess | WMI创建进程 |
| WinEventLog | WmiOperation | WMI操作 |
| WinEventLog | BackupDPMasterKey | 备份数据保护主密钥 |
| WinEventLog | PrivilegedOperation | 执行特权对象 |
| WinEventLog | PrivilegedCall | 调用特权服务 |
| WinEventLog | LogonAssignPrivilege | 新登录分配特权 |
| WinEventLog | ObjectPrivilegeChange | 更改对象权限 |
| WinEventLog | OpenSAMObject | 打开SAM对象句柄 |
| WinEventLog | LoginExplicitCredentials | 显式凭据登录 |
| WinEventLog | LoginClaimsInfo | 登录用户声明 |
| WinEventLog | LoginFailed | 登录失败 |
| WinEventLog | LoginSuccess | 登录成功 |
| WinEventLog | NetShareObjAdd | 添加网络共享对象 |
| WinEventLog | NetShareObjModify | 修改网络共享对象 |
| WinEventLog | NetShareObjCheck | 检查网络共享对象的权限 |
| WinEventLog | SMBCheckSpnFail | SMB SPN 检查失败 |
| WinEventLog | ExtDeviceRecognized | 识别新的外部设备 |
| WinEventLog | CMCredentialBackup | 用户成功备份凭据管理器 |
| WinEventLog | SetWindowsHookExLog | 设置消息钩子日志 |
| WinEventLog | NetShareObjAccess | 访问网络共享对象 |
| WinEventLog | SpGroupAssignLogon | 已将特殊组分配给新登录 |
| WinEventLog | FirewallSettingChange | 更改 Windows 防火墙本地设置 |
| WinEventLog | RegisterSecurityEvent | 注册新的安全事件源 |
| WinEventLog | UserLocalGroupEnum | 用户本地组成员枚举 |

#### 示例

```json
{
    "_type": "Event_7520",
    "recvTime": "2023-12-18T23:25:36+08:00",
    "sender": {
        "_type": "Terminal",
        "mid": "0000000000000000000000000000000000000000",
        "publicIP": "192.168.1.1",
        "clientVersion": "108.3.18764.64011",
        "client": {
            "IpPort": "192.168.1.1",
            "Mid": "0000000000000000000000000000000000000000",
            "Guid": "00000000000000000000000000000000",
            "Mac": "C8:5A:CF:00:E8:14",
            "Name": "testing-PC3",
            "User": "testing",
            "OSType": 0,
            "OS": "Microsoft Windows 10 专业版",
            "GroupIDPath": "1.2",
            "GroupNamePath": "全网终端.未分组终端",
            "Account": "",
            "Version": 30399311599434251,
            "GroupId": 2,
            "GroupName": "未分组终端",
            "AccountGroupId": 0,
            "AccountName": "",
            "AccountGroupName": "",
            "AccountGroupIdPath": "",
            "AccountGroupNamePath": "",
            "AccountVirtualGroupId": 0,
            "AccountVirtualGroupName": ""
        },
        "src": null
    },
    "args": {
        "Data": {
            "Action": {
                "KernelName": "NetFlowData",
                "Name": "HttpRequest",
                "Type": "Network"
            },
            "Alert": {},
            "Child": {
                "Direct": 1,
                "DstIp": "58.222.30.69",
                "DstPort": 80,
                "FlowTags": "HttpGet",
                "Host": "archive.kylinos.cn",
                "HostIoc": "WHITE",
                "IpIoc": "UNKNOWN",
                "Protocol": "tcp",
                "SrcIp": "192.168.255.10",
                "SrcPort": 52134,
                "Type": "Network",
                "Url": "http://tencent.com"
            },
            "Common": {
                "AuthId": 28779,
                "ClientVer": "108.3.18764.64011",
                "DeviceGroup": "全网终端.未分组终端",
                "EventId": 67799712,
                "EventTime": 1702913126832,
                "EventUUId": "a4278f52-78db-4270-876a-142fc62ce437",
                "Guid": "00000000000000000000000000000000",
                "KernelId": 86682097,
                "LoginStatus": 2,
                "Mid": "00000000000000000000000000000000",
                "MonitorName": "网络请求",
                "ReportId": 217470,
                "SessionId": 158,
                "Source": "KernelMon",
                "Uid": 0,
                "UserName": ""
            },
            "Environment": {
                "DomainName": "TENCENT",
                "ExportIp": "192.168.1.1",
                "HostName": "testing-PC3",
                "MacAddr": "00-00-00-00-00-00",
                "OsBit": "64",
                "OsBuild": 19045,
                "OsProduectDesc": "Windows 10 Enterprise 22H2",
                "OsType": "Windows",
                "OsUserName": "testing",
                "OsVersion": "Win10",
                "SysStartTimes": 1700474927500
            },
            "Parent": {
                "CallStack": "[]",
                "CloudAttr": "Unknown",
                "FileAccessTime": 1670572121,
                "FileCompany": "VMware, Inc.",
                "FileCopyright": "Copyright © 1998-2022 VMware, Inc.",
                "FileCreateTime": 1701829307,
                "FileDesc": "VMware NAT Service",
                "FileDriverType": "Fixed",
                "FileFormat": "EXE",
                "FileIssuer": "DigiCert Assured ID Code Signing CA-1",
                "FileLegalMark": "",
                "FileMd5": "6ee023f00cd791995a88ec3fac5c7dee",
                "FileMd5Type": "FullMd5",
                "FileModifyTime": 1668532542,
                "FileName": "vmnat.exe",
                "FileOriginalName": "vmnat.exe",
                "FilePath": "C:\\windows\\SysWOW64\\vmnat.exe",
                "FileProductName": "VMware Workstation",
                "FileProductVer": "17.0.0 build-20800274",
                "FileSign": "VMware, Inc.",
                "FileSignStatus": "Valid",
                "FileSignWhite": 1,
                "FileSize": 428184,
                "FileTags": "",
                "FileVersion": "17.0.0 build-20800274",
                "ProcArch": "x86",
                "ProcChainGuid": "13564637203494864296,13561953501747873116,13467929752712774668,13400554540571558492,13400554540571295748,13400554540571295744",
                "ProcChainInfo": "",
                "ProcChainTrust": "Trust",
                "ProcCmdline": "C:\\windows\\SysWOW64\\vmnat.exe",
                "ProcDomainName": "NT AUTHORITY",
                "ProcElevationType": 1,
                "ProcGuid": "13636445328657356468",
                "ProcIntegrity": 6,
                "ProcPid": 5812,
                "ProcTrust": "Trust",
                "ProcUserName": "SYSTEM",
                "SolutionId": 0,
                "ThreadId": 5576,
                "Type": "Proc"
            }
        },
        "Version": 1
    }
}
```

