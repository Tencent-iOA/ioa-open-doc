### 高级威胁防护告警日志上报

对应命令字：7510

支持版本：8.2

#### 格式

| 字段名 | 字段类型 | 字段说明 | 取值说明 |
| --- | --- | --- | --- |
|EventId |int64 |告警ID（7日内重复告警使用相同的ID） | |
|EventName |string |告警名称 | |
|IOAAccount |string |企业账号 | |
|AttackSummary |string |告警攻击摘要 | |
|OccurTime |int64 |发生时间戳（毫秒） | |
|EngineName |string |引擎名称 |CloudEngine:云引擎 <br>GraphEngine:关联图引擎<br>IocEngine:威胁情报<br>TavEngine:TAV引擎 |
|PolicyName |string |触发策略名称 | |
|PolicyDescription |string |触发策略描述 | |
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

### 高级威胁防护采集日志上报

对应命令字：7520

支持版本：7.5

#### 格式

| 字段名 | 字段类型 | 字段说明 | 取值说明 |
| :--- | :--- | :--- | :--- |
| OS | int | 系统平台 |  |
| Uuid | string | 唯一ID |  |
| @collection | datetime | 采集时间 |  |
| @timestamp | datetime | 入库时间 |  |
| Cmd | string | 命令字 |  |
| Version | int | 数据版本 |  |
| Action | object | 动作 |  |
| Action.Type | string | 事件动作类型 | 见采集日志动作类型取值范围 |
| Action.Name | string | 事件动作名称 | 见采集日志子动作名称取值范围 |
| Action.EventLogId | int | Windows日志ID |  |
| Parent | object | 操作者节点 |  |
| Parent.ProcPid | int | 进程Pid |  |
| Parent.ProcCmdline | string | 进程命令行 |  |
| Parent.FileName | string | 文件名 |  |
| Parent.FilePath | string | 文件路径 |  |
| Parent.FileDriverType | string | 驱动器类型 | CDRom: CD光盘<br/>Fixed: 硬盘<br/>NoRootDir: 非驱动<br/>Ramdisk: 内存磁盘<br/>Remote: 网络驱动器<br/>Removeable: 可移动介质<br/>Unknown: 未知 |
| Parent.FileMd5 | string | 文件md5 |  |
| Parent.CloudAttr | string | 云查属性 | Black: 黑\(Black\)<br/>Gray: 灰\(Gray\)<br/>Unknown: 未知\(Unknown\)<br/>White: 安全\(White\) |
| Parent.Type | string | 节点类型 | ApiCall: 系統API<br/>File: 文件<br/>FileStatics: 文件统计<br/>Log: 日志<br/>Network: 网络<br/>Pipe: 管道<br/>Pipe: 管道<br/>Proc: 进程<br/>Reg: 注册表<br/>Script: 脚本 |
| Parent.ProcGuid | string | 进程唯一ID |  |
| Parent.ProcIntegrity | int | 进程完整性级别 | 1: 不可信<br/>2: 低<br/>3: 中<br/>4: 中+<br/>5: 高<br/>6: 系统<br/>7: 保护进程 |
| Parent.ProcElevationType | int | 进程提权类型 | 1: UAC关闭<br/>2: UAC提权<br/>3: UAC限制权限 |
| Parent.ProcUserName | string | 进程用户名 |  |
| Parent.ProcDomainName | string | 进程用户域名 |  |
| Parent.ProcArch | string | 进程架构 | x64: x64<br/>x86: x86 |
| Parent.ProcTrust | string | 进程可信 | NoTrust: 不可信<br/>Trust: 可信 |
| Parent.ProcChainTrust | string | 进程链可信 | NoTrust: 不可信<br/>Trust: 可信 |
| Parent.ProcChainInfo | string | 进程链详情 |  |
| Parent.FileFormat | string | 文件类型 | DLL: 动态链接库<br/>EXE: 可执行EXE<br/>NPE: 非PE<br/>SYS: 驱动 |
| Parent.FileMd5Type | string | 文件md5类型 | FullMd5: 全文<br/>HalfMd5: 半文 |
| Parent.FileSize | int | 文件大小 |  |
| Parent.FileSign | string | 文件签名 |  |
| Parent.FileSignStatus | string | 文件签名状态 | Expired: 签名过期<br/>Invalid: 验证不通过<br/>Valid: 验证通过 |
| Parent.FileSignWhite | int | 是否白签名 | 0: 不是<br/>1: 是 |
| Parent.FileIssuer | string | 签名颁发机构 |  |
| Parent.FileCompany | string | 文件公司名 |  |
| Parent.FileDesc | string | 文件描述 |  |
| Parent.FileVersion | string | 文件版本 |  |
| Parent.FileOriginalName | string | 原始文件名 |  |
| Parent.FileProductName | string | 文件产品名 |  |
| Parent.FileProductVer | string | 文件产品版本号 |  |
| Parent.FileLegalMark | string | 文件产品商标 |  |
| Parent.FileCopyright | string | 文件版权 |  |
| Parent.FileModifyTime | int | 文件修改时间 |  |
| Parent.FileAccessTime | int | 文件访问时间 |  |
| Parent.FileCreateTime | int | 文件创建时间 |  |
| Parent.FileTags | string | 文件标签 | Browser: 浏览器渠道<br/>Browser:114高速浏览器: 114高速浏览器下载<br/>Browser:115极速浏览器: 115极速浏览器下载<br/>Browser:115浏览器: 115浏览器下载<br/>Browser:2345加速浏览器: 2345加速浏览器下载<br/>Browser:2345智能浏览器: 2345智能浏览器下载<br/>Browser:360安全浏览器: 360安全浏览器下载<br/>Browser:360极速浏览器: 360极速浏览器下载<br/>Browser:Edge浏览器: Edge浏览器下载<br/>Browser:GreenBrowser: GreenBrowser下载<br/>Browser:GT游戏浏览器: GT游戏浏览器下载<br/>Browser:hao123桔子浏览器: hao123桔子浏览器下载<br/>Browser:IE浏览器: IE浏览器下载<br/>Browser:iQ浏览器: iQ浏览器下载<br/>Browser:KR浏览器: KR浏览器下载<br/>Browser:MyIE浏览器: MyIE浏览器下载<br/>Browser:Opera: Opera下载<br/>Browser:QQ浏览器: QQ浏览器下载<br/>Browser:Safari浏览器: Safari浏览器下载<br/>Browser:Spartan浏览器: Spartan浏览器下载<br/>Browser:TT浏览器: TT浏览器下载<br/>Browser:UC浏览器: UC浏览器下载<br/>Browser:YY浏览器: YY浏览器下载<br/>Browser:世界之窗浏览器: 世界之窗浏览器下载<br/>Browser:世界之窗浏览器极速版: 世界之窗浏览器极速版下载<br/>Browser:傲游浏览器: 傲游浏览器下载<br/>Browser:搜狗浏览器: 搜狗浏览器下载<br/>Browser:淘宝浏览器: 淘宝浏览器下载<br/>Browser:火狐浏览器: 火狐浏览器下载<br/>Browser:猎豹浏览器: 猎豹浏览器下载<br/>Browser:瑞影浏览器: 瑞影浏览器下载<br/>Browser:百度浏览器: 百度浏览器下载<br/>Browser:百度浏览器hao123专版: 百度浏览器hao123专版下载<br/>Browser:糖果浏览器: 糖果浏览器下载<br/>Browser:花儿世界浏览器: 花儿世界浏览器下载<br/>Browser:谷歌浏览器: 谷歌浏览器下载<br/>Browser:超速浏览器: 超速浏览器下载<br/>Browser:闪游浏览器: 闪游浏览器下载<br/>Browser:随E浏览器: 随E浏览器下载<br/>Browser:青猴浏览器: 青猴浏览器下载<br/>Downloader: 下载器渠道<br/>Downloader:BitComet: BitComet下载<br/>Downloader:IDMan: IDMan下载<br/>Downloader:QQ旋风: QQ旋风下载<br/>Downloader:QQ旋风下载助手: QQ旋风下载助手下载<br/>Downloader:RaySource: RaySource下载<br/>Downloader:旋风高速下载引擎: 旋风高速下载<br/>Downloader:比特彗星: 比特彗星下载<br/>Downloader:电驴: 电驴下载<br/>Downloader:百度下载助手: 百度下载助手下载<br/>Downloader:百度云管家: 百度云管家下载<br/>Downloader:网际快车: 网际快车下载<br/>Downloader:网页迅雷: 网页迅雷下载<br/>Downloader:迅雷: 迅雷下载<br/>Downloader:迅雷云加速: 迅雷云加速下载<br/>Downloader:迅雷精简版: 迅雷精简版下载<br/>Downloader:迅雷迷你版: 迅雷迷你版下载<br/>Downloader:迷你快车: 迷你快车下载<br/>Downloader:迷你电驴: 迷你电驴下载<br/>Downloader:飞鸟下载器: 飞鸟下载器下载<br/>IM: IM渠道<br/>IM:FSLink: FSLink下载<br/>IM:MSN: MSN下载<br/>IM:Skype: Skype下载<br/>IM:YY语音: YY语音下载<br/>IM:京东咚咚: 京东咚咚下载<br/>IM:企业微信: 企业微信下载<br/>IM:微信: 微信下载<br/>IM:易信: 易信下载<br/>IM:润工作: 润工作下载<br/>IM:环信: 环信下载<br/>IM:百度Hi: 百度Hi下载<br/>IM:百度Hi: 百度Hi下载<br/>IM:网易CC语音: 网易CC语音下载<br/>IM:网易云信: 网易云信下载<br/>IM:腾讯QQ: 腾讯QQ下载<br/>IM:腾讯TM: 腾讯TM下载<br/>IM:腾讯通\(RTX\): 腾讯通\(RTX\)下载<br/>IM:钉钉: 钉钉下载<br/>IM:阿里旺旺: 阿里旺旺下载<br/>IM:飞书: 飞书下载<br/>IM:飞信: 飞信下载<br/>Mail: 邮箱渠道<br/>Mail:139邮箱: 139邮箱下载<br/>Mail:Foxmail: Foxmail下载<br/>Mail:PP助手: OutLook下载<br/>Mail:新浪邮箱: 新浪邮箱下载<br/>Mail:网易邮箱: 网易邮箱下载<br/>Mail:阿里邮箱: 阿里邮箱下载<br/>NetDisk: 网盘渠道<br/>NetDisk:115网盘: 115网盘下载<br/>NetDisk:360云盘: 360云盘下载<br/>NetDisk:360网盘: 360网盘下载<br/>NetDisk:优蛋: 优蛋下载<br/>NetDisk:华为网盘: 华为网盘下载<br/>NetDisk:坚果云: 坚果云下载<br/>NetDisk:城通网盘: 城通网盘下载<br/>NetDisk:天翼云盘: 天翼云盘下载<br/>NetDisk:夸克网盘: 夸克网盘下载<br/>NetDisk:微云: 微云下载<br/>NetDisk:微盘: 微盘下载<br/>NetDisk:百度网盘: 百度网盘下载<br/>NetDisk:纳米盘: 纳米盘下载<br/>NetDisk:酷盘: 酷盘下载<br/>NetDisk:金山快盘: 金山快盘下载<br/>NetDisk:阿里云盘: 阿里云盘下载<br/>NetShare: 网络共享渠道<br/>NewFile: 新入文件<br/>SoftMgr: 软件管理渠道<br/>SoftMgr:2345软件管家: 2345软件管家下载<br/>SoftMgr:360安全卫士: 360安全卫士下载<br/>SoftMgr:360驱动大师: 360驱动大师下载<br/>SoftMgr:91手机助手: 91手机助手下载<br/>SoftMgr:PP助手: PP助手下载<br/>SoftMgr:天极软件管家: 天极软件管家下载<br/>SoftMgr:微软电脑管家: 微软电脑管家下载<br/>SoftMgr:搜狗手机助手: 搜狗手机助手下载<br/>SoftMgr:爱思助手: 爱思助手下载<br/>SoftMgr:联想电脑管家: 联想电脑管家下载<br/>SoftMgr:腾讯电脑管家: 腾讯电脑管家下载<br/>SoftMgr:豌豆荚2: 豌豆荚2下载<br/>SoftMgr:软媒魔方软件管理: 软媒魔方软件管理下载<br/>SoftMgr:金山手机助手: 金山手机助手下载<br/>SoftMgr:金山毒霸: 金山毒霸下载<br/>SoftMgr:风灵软件管家: 风灵软件管家下载<br/>SoftMgr:驱动人生: 驱动人生下载<br/>SoftMgr:驱动人生软件管理: 驱动人生软件管理下载<br/>SoftMgr:驱动精灵: 驱动精灵下载<br/>TrustSource: 可信进程释放<br/>UnknownSource: 未知进程释放 |
| Parent.ScanAttr | string | 威胁鉴定 | Black: 恶意<br/>Safe: 安全<br/>Unknown: 未知<br/>Virus: 恶意<br/>White: 安全 |
| Parent.ThreadId | int | 线程ID |  |
| Parent.TrojanName | string | 病毒名 |  |
| Child | object | 目标节点 |  |
| Child.SubjectUserSid | string | 用户安全ID |  |
| Child.SubjectUserName | string | 帐户名称 |  |
| Child.SubjectDomainName | string | 账户域 |  |
| Child.SubjectLogonId | string | 登录ID |  |
| Child.PreviousTime | string | 上一时间 |  |
| Child.NewTime | string | 新时间 |  |
| Child.ElevatedToken | string | 提升的令牌 | 否: 否<br/>是: 是 |
| Child.ImpersonationLevel | string | 模拟级别 | 委派: 委派<br/>标识: 标识<br/>模拟: 模拟 |
| Child.RestrictedAdminMode | string | 受限管理员模式 | 否: 否<br/>是: 是 |
| Child.TargetUserSid | string | 目标安全ID |  |
| Child.TargetUserName | string | 目标帐户名称 |  |
| Child.TargetDomainName | string | 目标账户域 |  |
| Child.TargetLogonId | string | 目标登录ID |  |
| Child.TargetLinkedLogonId | string | 目标链接登录ID |  |
| Child.TargetOutboundUserName | string | 网络帐户名称 |  |
| Child.TargetOutboundDomainName | string | 网络帐户域 |  |
| Child.TransmittedServices | string | 传输服务 |  |
| Child.VirtualAccount | string | 虚拟帐户 | 否: 否<br/>是: 是 |
| Child.WorkstationName | string | 工作站名称 |  |
| Child.AccessList | string | 访问列表 |  |
| Child.AccessMask | string | 访问掩码 |  |
| Child.AccessReason | string | 访问检查结果 |  |
| Child.AccountExpires | string | 账户过期 |  |
| Child.AllowedToDelegateTo | string | 委派凭据的SPN 列表 |  |
| Child.AuditSourceName | string | 源名称 |  |
| Child.AuthenticationPackageName | string | 身份验证包 | Kerberos: Kerberos<br/>LM: LM<br/>Negotiate: Negotiate<br/>NTLM V1: NTLM V1<br/>NTLM V2: NTLM V2 |
| Child.ConfiguredNames | string | 配置名称 |  |
| Child.ClassId | string | 类ID |  |
| Child.ClassName | string | 类名 |  |
| Child.CompatibleIds | string | 兼容ID |  |
| Child.ClientMachine | string | 主机名 |  |
| Child.ClientMachineFQDN | string | 域名 |  |
| Child.ClientProcessCreationTime | string | 进程启动时间 |  |
| Child.CorrelationId | string | 绑定ID |  |
| Child.Commandline | string | 创建命令行 |  |
| Child.CreatedProcessCreationTime | string | 创建进程时间 |  |
| Child.DeviceClaims | string | 设备声明 |  |
| Child.DisabledPrivilegeList | string | 禁用权限列表 |  |
| Child.DisplayName | string | 显示名称 |  |
| Child.DeviceId | string | 设备ID |  |
| Child.DeviceDescription | string | 设备名称 |  |
| Child.EnabledPrivilegeList | string | 启用权限列表 |  |
| Child.EventSourceId | string | 事件源ID |  |
| Child.ErrorCode | string | 错误代码 |  |
| Child.FailureReason | string | 失败原因 |  |
| Child.GroupOperationId | string | 组操作ID |  |
| Child.HandleId | string | 句柄ID |  |
| Child.HomeDirectory | string | 主目录 |  |
| Child.HomePath | string | 主路径 |  |
| Child.IsLocal | bool | 是否本地 |  |
| Child.IpAddress | string | 源网络地址 |  |
| Child.IpPort | string | 源端口 |  |
| Child.KeyLength | string | 密钥长度 |  |
| Child.LogonGuid | string | 登录GUID |  |
| Child.LogonProcessName | string | 登录进程名称 |  |
| Child.LogonType | string | 登录类型 | 0: 系统启动<br/>10: 远程登录<br/>2: 交互式<br/>3: 网络<br/>4: 计划任务<br/>5: 服务 |
| Child.LogonHours | string | 登录限制时长 |  |
| Child.LocationInformation | string | 位置信息 |  |
| Child.NewSd | string | 新的安全描述符 |  |
| Child.MasterKeyId | string | 密钥标识符 |  |
| Child.NewUacValue | string | 新UAC值 |  |
| Child.NewRemark | string | 新注释值 |  |
| Child.NewMaxUsers | string | 新的用户数限制值 |  |
| Child.NewShareFlags | string | 新的脱机设置值 |  |
| Child.NamespaceName | string | 命名空间名称 |  |
| Child.ObjectServer | string | 对象服务器 |  |
| Child.ObjectType | string | 对象类型 |  |
| Child.ObjectName | string | 对象名称 |  |
| Child.OldSd | string | 原始安全描述 |  |
| Child.OldUacValue | string | 旧UAC值 |  |
| Child.OldRemark | string | 旧注释值 |  |
| Child.OldMaxUsers | string | 旧的用户数限制值 |  |
| Child.OldShareFlags | string | 旧的脱机设置值 |  |
| Child.Operation | string | 操作 |  |
| Child.OperationId | string | 操作ID |  |
| Child.PrivilegeList | string | 权限列表 |  |
| Child.Properties | string | 属性 |  |
| Child.ProfilePath | string | 配置文件路径 |  |
| Child.PasswordLastSet | string | 密码最后一个集 |  |
| Child.PrimaryGroupId | string | 主组ID |  |
| Child.ProfileChanged | string | 已更改配置文件 |  |
| Child.RestrictedSidCount | string | 受限SID 计数 |  |
| Child.RecoveryServer | string | 恢复服务器 |  |
| Child.RecoveryKeyId | string | 恢复密钥 ID |  |
| Child.RelativeTargetName | string | 相对目标名称 |  |
| Child.Status | string | 状态 |  |
| Child.SubStatus | string | 子状态 |  |
| Child.Service | string | 服务名称 |  |
| Child.SamAccountName | string | SAM帐户名称 |  |
| Child.ScriptPath | string | 脚本路径 |  |
| Child.SidHistory | string | SID历史记录 |  |
| Child.SettingType | string | 设置类型 |  |
| Child.SettingValue | string | 设置类型 |  |
| Child.SidList | string | 特殊组SID列表 |  |
| Child.ShareName | string | 共享名称 |  |
| Child.ShareLocalPath | string | 共享路径 |  |
| Child.SpnName | string | SPN名称 |  |
| Child.ServerNames | string | 服务器名称 |  |
| Child.TargetLogonGuid | string | 目标登录GUID |  |
| Child.TargetServerName | string | 目标服务器名称 |  |
| Child.TargetInfo | string | 目标信息 |  |
| Child.TransactionId | string | 事务ID |  |
| Child.TaskName | string | 任务名称 |  |
| Child.TaskContent | string | 任务内容 |  |
| Child.TaskContentNew | string | 任务新内容 |  |
| Child.TargetSid | string | 目标登录ID |  |
| Child.UserClaims | string | 用户声明 |  |
| Child.UserPrincipalName | string | 用户主体名称 |  |
| Child.UserWorkstations | string | 用户工作站 |  |
| Child.UserAccountControl | string | 用户帐户控件 |  |
| Child.UserParameters | string | 用户参数 |  |
| Child.User | string | 用户名 |  |
| Child.VendorIds | string | 供应商ID |  |
| Child.FilterType | string | Hook类型 |  |
| Child.ReturnValue | string | 注册结果 |  |
| Child.hmod | string | DLL句柄 |  |
| Child.pfnFilterProc | string | 过滤函数 |  |
| Child.pstrLib | string | 模块路径 |  |
| Child.ContentName | string | 脚本名称 |  |
| Child.ContentData | string | 脚本数据 |  |
| Child.ApiRet | int | 返回值 |  |
| Child.Privileges | string | 特权列表 |  |
| Child.Addr | int | 起始地址 |  |
| Child.Param1 | int | 参数1 |  |
| Child.Size | int | 地址大小 |  |
| Child.NewProtect | int | 新权限 | 0x1: 无权限<br/>0x10: 可执行<br/>0x100: 保护页面<br/>0x2: 只读<br/>0x20: 执行读<br/>0x200: 无缓存<br/>0x4: 只写<br/>0x40: 执行读写<br/>0x8: 只拷贝<br/>0x80: 执行写拷贝 |
| Child.OldProtect | int | 旧权限 | 0x1: 无权限<br/>0x10: 可执行<br/>0x100: 保护页面<br/>0x2: 只读<br/>0x20: 执行读<br/>0x200: 无缓存<br/>0x4: 只写<br/>0x40: 执行读写<br/>0x8: 只拷贝<br/>0x80: 执行写拷贝 |
| Child.Method | string | 请求方法 | CONNECT: CONNECT<br/>DELETE: DELETE<br/>GET: GET<br/>HEAD: HEAD<br/>OPTIONS: OPTIONS<br/>PATCH: PATCH<br/>POST: POST<br/>PUT: PUT<br/>TRACE: TRACE |
| Child.ProtoVersion | string | 协议版本 |  |
| Child.Referer | string | 来源 |  |
| Child.AcceptTypes | string | 接受类型 |  |
| Child.Flags | int | 选项标志 |  |
| Child.UserName | string | 用户名 |  |
| Child.Password | string | 密码 |  |
| Child.ProtoService | int | 访问类型 | 1: FTP<br/>2: GOPHER<br/>3: HTTP |
| Child.Header | string | 请求头 |  |
| Child.Agent | string | User-Agent |  |
| Child.AccessTypes | int | 接受类型 | 0: 注册表配置<br/>1: 直连网络<br/>2: 通过代理<br/>3: 无自动代理 |
| Child.Proxy | string | 代理服务 |  |
| Child.ProxyByPass | string | 免代理域名 |  |
| Child.EventBegin | int | 事件起始 |  |
| Child.EventEnd | int | 事件结束 |  |
| Child.Handle | int | 句柄 |  |
| Child.ContextFlags | int | 上下文类型 |  |
| Child.Eip | int | EIP寄存器 |  |
| Child.OldEip | int | EIP寄存器 |  |
| Child.BlobData | string | 二进制数据 |  |
| Child.FuncName | string | 函数名 |  |
| Child.ProtectType | int | 内存权限 | 0x1: 无权限<br/>0x10: 可执行<br/>0x100: 保护页面<br/>0x2: 只读<br/>0x20: 执行读<br/>0x200: 无缓存<br/>0x4: 只写<br/>0x40: 执行读写<br/>0x8: 只拷贝<br/>0x80: 执行写拷贝 |
| Child.AllocType | int | 分配类型 | 0x1000: 提交内存<br/>0x2000: 保留内存<br/>0x40000: 映射内存<br/>0x400000: 物理内存 |
| Child.Protocol | string | 协议类型 | tcp: tcp<br/>udp: udp |
| Child.SrcIp | string | 源IP（本机IP） |  |
| Child.SrcPort | int | 源端口（本机端口） |  |
| Child.DstIp | string | 目标IP（远程IP） |  |
| Child.DstPort | int | 目标端口（远程端口） |  |
| Child.Direct | int | 流量方向 | 1: 出站<br/>2: 入站 |
| Child.SendTotal | int | 发送总的字节数 |  |
| Child.RecvTotal | int | 收到总的字节数 |  |
| Child.Host | string | 域名 |  |
| Child.Url | string | URL |  |
| Child.FlowTags | string | 流数据标签 |  |
| Child.DnsAnswers | string | DNS应答IP |  |
| Child.IpIoc | string | IP威胁情报 | Black: 黑\(Black\)<br/>Gray: 灰\(Gray\)<br/>Unknown: 未知\(Unknown\)<br/>White: 安全\(White\) |
| Child.HostIoc | string | 域名威胁情报 | Black: 黑\(Black\)<br/>Gray: 灰\(Gray\)<br/>Unknown: 未知\(Unknown\)<br/>White: 安全\(White\) |
| Child.ServiceName | string | 服务名称 |  |
| Child.StartType | int | 启动类型 | 0: Boot启动<br/>1: System启动<br/>2: 自动启动<br/>3: 手动启动<br/>4: 禁止启动 |
| Child.TaskName | string | 任务名称 |  |
| Child.TaskArg | string | 任务参数 |  |
| Child.RemoteCallType | int | 远程调用类型 | 0x1: MMC20Application<br/>0x10: WMI<br/>0x2: InternetExplorer<br/>0x4: ShellWindows<br/>0x8: ShellBrowserWindows |
| Child.PrintType | int | 打印机类型 | 1: RpcAsyncAddPrinterDriver<br/>2: RpcAddPrinterDriverEx |
| Child.DocFileOpt | int | 勒索诱饵操作类型 | 0x10: 删除文件<br/>0x4: 重命名<br/>0x40: 文件大小改变<br/>0x8: 写文件<br/>0x80: 设置文件信息 |
| Child.PhishChain | string | 钓鱼链 |  |
| Child.ProcPid | int | 进程Pid |  |
| Child.ProcCmdline | string | 进程命令行 |  |
| Child.FileName | string | 文件名 |  |
| Child.FilePath | string | 文件路径 |  |
| Child.FileDriverType | string | 驱动器类型 | CDRom: CD光盘<br/>Fixed: 硬盘<br/>，NoRootDir: 非驱动<br/>Ramdisk: 内存磁盘<br/>Remote: 网络驱动器<br/>Removeable: 可移动介质<br/>Unknown: 未知 |
| Child.FileMd5 | string | 文件md5 |  |
| Child.CloudAttr | string | 云查属性 | Black: 黑\(Black\)<br/>Gray: 灰\(Gray\)<br/>Unknown: 未知\(Unknown\)<br/>White: 安全\(White\) |
| Child.FileSign | string | 文件签名 |  |
| Child.FileSignStatus | string | 文件签名状态 | Expired: 签名过期<br/>Invalid: 验证不通过<br/>Valid: 验证通过 |
| Child.FileSignWhite | int | 是否白签名 | 0: 不是<br/>1: 是 |
| Child.RegKeyPath | string | 注册表路径 |  |
| Child.RegValName | string | 注册表值名 |  |
| Child.RegValType | int | 注册表值类型 | 1: 字符串<br/>11: QWORD（64位整数）<br/>2: 可扩展字符串<br/>3: 二进制<br/>4: DWORD（32位整数）<br/>7: 多字符串 |
| Child.RegValData | string | 注册表值数据 |  |
| Child.RegOldValType | int | 注册表旧值类型 | 1: 字符串<br/>11: QWORD（64位整数）<br/>2: 可扩展字符串<br/>3: 二进制<br/>4: DWORD（32位整数）<br/>7: 多字符串 |
| Child.RegOldValData | string | 注册表旧值数据 |  |
| Child.RegGroupName | string | 注册表分组名称 | DOS虚拟机程序: DOS虚拟机程序<br/>IE临时文件夹: IE临时文件夹<br/>IE安全性设置: IE安全性设置<br/>IE插件扩展: IE插件扩展<br/>IE浏览器路径: IE浏览器路径<br/>IE源码查看器: IE源码查看器<br/>INI文件劫持: INI文件劫持<br/>IPSec策略设置: IPSec策略设置<br/>IP安全组策略: IP安全组策略<br/>SHELL名字空间: SHELL名字空间<br/>TCPIP网络设置: TCPIP网络设置<br/>URL前缀: URL前缀<br/>URL协议关联: URL协议关联<br/>Windows防火墙: Windows防火墙<br/>分层网络协议: 分层网络协议<br/>协议关联图标: 协议关联图标<br/>右键菜单: 右键菜单<br/>启动文件夹: 启动文件夹<br/>启动项: 启动项<br/>启动项登录脚本: 启动项登录脚本<br/>命令行劫持: 命令行劫持<br/>命令行工具: 命令行工具<br/>安全模式配置: 安全模式配置<br/>应用卸载设置: 应用卸载设置<br/>打印机支持程序: 打印机支持程序<br/>控制面板设置: 控制面板设置<br/>敏感启动项: 敏感启动项<br/>文件关联: 文件关联<br/>映像劫持: 映像劫持<br/>服务支持程序: 服务支持程序<br/>本地安全策略: 本地安全策略<br/>本地账户凭证: 本地账户凭证<br/>浏览器侧边栏: 浏览器侧边栏<br/>浏览器工具条: 浏览器工具条<br/>浏览器工具栏按钮: 浏览器工具栏按钮<br/>浏览器插件: 浏览器插件<br/>浏览器插件: 浏览器插件<br/>浏览器通信协议: 浏览器通信协议<br/>浏览器首页设置: 浏览器首页设置<br/>浏览器默认下载工具: 浏览器默认下载工具<br/>浏览器默认搜索引擎: 浏览器默认搜索引擎<br/>漏洞CLSID: 漏洞CLSID<br/>系统动态组件: 系统动态组件<br/>系统启动校验程序: 系统启动校验程序<br/>系统常用文件夹: 系统常用文件夹<br/>系统服务: 系统服务<br/>系统环境变量: 系统环境变量<br/>系统登录初始化程序: 系统登录初始化程序<br/>系统登录界面: 系统登录界面<br/>系统登录管理: 系统登录管理<br/>系统登录脚本: 系统登录脚本<br/>系统登陆管理项: 系统登陆管理项<br/>系统证书: 系统证书<br/>系统配置策略: 系统配置策略<br/>组策略启动项: 组策略启动项<br/>组策略脚本启动项: 组策略脚本启动项<br/>网络远程调用协议: 网络远程调用协议<br/>老版操作系统启动项: 老版操作系统启动项<br/>输入法设置: 输入法设置<br/>进程预加载项: 进程预加载项<br/>远程桌面服务: 远程桌面服务<br/>隐藏文件夹选项: 隐藏文件夹选项<br/>隐藏桌面图标设置: 隐藏桌面图标设置<br/>默认任务管理器: 默认任务管理器<br/>默认加载库: 默认加载库<br/>默认字库设置: 默认字库设置<br/>默认屏保程序: 默认屏保程序<br/>默认浏览器设置: 默认浏览器设置<br/>默认输入法设置: 默认输入法设置 |
| Child.Type | string | 节点类型 | ApiCall: 系統API<br/>File: 文件<br/>FileStatics: 文件统计<br/>Log: 日志<br/>Network: 网络<br/>Pipe: 管道<br/>Pipe: 管道<br/>Proc: 进程<br/>Reg: 注册表<br/>Script: 脚本 |
| Child.CallStack | string | 调用堆栈 |  |
| Child.ThreadId | int | 线程ID |  |
| Child.ProcGuid | string | 进程唯一ID |  |
| Child.ProcIntegrity | int | 进程完整性级别 | 1: 不可信<br/>2: 低<br/>3: 中<br/>4: 中+<br/>5: 高<br/>6: 系统<br/>7: 保护进程 |
| Child.ProcElevationType | int | 进程提权类型 | 1: UAC关闭<br/>2: UAC提权<br/>3: UAC限制权限 |
| Child.ProcExited | bool | 进程退出标志 |  |
| Child.ProcArch | string | 进程架构 | x64: x64<br/>x86: x86 |
| Child.ProcUserName | string | 进程用户名 |  |
| Child.ProcDomainName | string | 进程用户域名 |  |
| Child.ProcCurDir | string | 进程当前目录 |  |
| Child.ProcDesktop | string | 进程桌面名称 |  |
| Child.ProcTrust | string | 进程可信 | NoTrust: 不可信<br/>Trust: 可信 |
| Child.ProcChainTrust | string | 进程链可信 | NoTrust: 不可信<br/>Trust: 可信 |
| Child.ProcChainInfo | string | 进程链详情 |  |
| Child.FileStream | string | 文件流名称 |  |
| Child.FileFormat | string | 文件类型 | DLL: 动态链接库<br/>EXE: 可执行EXE<br/>NPE: 非PE<br/>SYS: 驱动 |
| Child.FileMd5Type | string | 文件md5类型 | FullMd5: 全文<br/>HalfMd5: 半文 |
| Child.FileSize | int | 文件大小 |  |
| Child.FileIssuer | string | 签名颁发机构 |  |
| Child.FileCompany | string | 文件公司名 |  |
| Child.FileDesc | string | 文件描述 |  |
| Child.FileVersion | string | 文件版本 |  |
| Child.FileOriginalName | string | 原始文件名 |  |
| Child.FileProductName | string | 文件产品名 |  |
| Child.FileProductVer | string | 文件产品版本号 |  |
| Child.FileLegalMark | string | 文件产品商标 |  |
| Child.FileCopyright | string | 文件版权 |  |
| Child.FileModifyTime | int | 文件修改时间 |  |
| Child.FileAccessTime | int | 文件访问时间 |  |
| Child.FileCreateTime | int | 文件创建时间 |  |
| Child.FileTags | string | 文件标签 | Browser: 浏览器渠道<br/>Browser:114高速浏览器: 114高速浏览器下载<br/>Browser:115极速浏览器: 115极速浏览器下载<br/>Browser:115浏览器: 115浏览器下载<br/>Browser:2345加速浏览器: 2345加速浏览器下载<br/>Browser:2345智能浏览器: 2345智能浏览器下载<br/>Browser:360安全浏览器: 360安全浏览器下载<br/>Browser:360极速浏览器: 360极速浏览器下载<br/>Browser:Edge浏览器: Edge浏览器下载<br/>Browser:GreenBrowser: GreenBrowser下载<br/>Browser:GT游戏浏览器: GT游戏浏览器下载<br/>Browser:hao123桔子浏览器: hao123桔子浏览器下载<br/>Browser:IE浏览器: IE浏览器下载<br/>Browser:iQ浏览器: iQ浏览器下载<br/>Browser:KR浏览器: KR浏览器下载<br/>Browser:MyIE浏览器: MyIE浏览器下载<br/>Browser:Opera: Opera下载<br/>Browser:QQ浏览器: QQ浏览器下载<br/>Browser:Safari浏览器: Safari浏览器下载<br/>Browser:Spartan浏览器: Spartan浏览器下载<br/>Browser:TT浏览器: TT浏览器下载<br/>Browser:UC浏览器: UC浏览器下载<br/>Browser:YY浏览器: YY浏览器下载<br/>Browser:世界之窗浏览器: 世界之窗浏览器下载<br/>Browser:世界之窗浏览器极速版: 世界之窗浏览器极速版下载<br/>Browser:傲游浏览器: 傲游浏览器下载<br/>Browser:搜狗浏览器: 搜狗浏览器下载<br/>Browser:淘宝浏览器: 淘宝浏览器下载<br/>Browser:火狐浏览器: 火狐浏览器下载<br/>Browser:猎豹浏览器: 猎豹浏览器下载<br/>Browser:瑞影浏览器: 瑞影浏览器下载<br/>Browser:百度浏览器: 百度浏览器下载<br/>Browser:百度浏览器hao123专版: 百度浏览器hao123专版下载<br/>Browser:糖果浏览器: 糖果浏览器下载<br/>Browser:花儿世界浏览器: 花儿世界浏览器下载<br/>Browser:谷歌浏览器: 谷歌浏览器下载<br/>Browser:超速浏览器: 超速浏览器下载<br/>Browser:闪游浏览器: 闪游浏览器下载<br/>Browser:随E浏览器: 随E浏览器下载<br/>Browser:青猴浏览器: 青猴浏览器下载<br/>Downloader: 下载器渠道<br/>Downloader:BitComet: BitComet下载<br/>Downloader:IDMan: IDMan下载<br/>Downloader:QQ旋风: QQ旋风下载<br/>Downloader:QQ旋风下载助手: QQ旋风下载助手下载<br/>Downloader:RaySource: RaySource下载<br/>Downloader:旋风高速下载引擎: 旋风高速下载<br/>Downloader:比特彗星: 比特彗星下载<br/>Downloader:电驴: 电驴下载<br/>Downloader:百度下载助手: 百度下载助手下载<br/>Downloader:百度云管家: 百度云管家下载<br/>Downloader:网际快车: 网际快车下载<br/>Downloader:网页迅雷: 网页迅雷下载<br/>Downloader:迅雷: 迅雷下载<br/>Downloader:迅雷云加速: 迅雷云加速下载<br/>Downloader:迅雷精简版: 迅雷精简版下载<br/>Downloader:迅雷迷你版: 迅雷迷你版下载<br/>Downloader:迷你快车: 迷你快车下载<br/>Downloader:迷你电驴: 迷你电驴下载<br/>Downloader:飞鸟下载器: 飞鸟下载器下载<br/>IM: IM渠道<br/>IM:FSLink: FSLink下载<br/>IM:MSN: MSN下载<br/>IM:Skype: Skype下载<br/>IM:YY语音: YY语音下载<br/>IM:京东咚咚: 京东咚咚下载<br/>IM:企业微信: 企业微信下载<br/>IM:微信: 微信下载<br/>IM:易信: 易信下载<br/>IM:润工作: 润工作下载<br/>IM:环信: 环信下载<br/>IM:百度Hi: 百度Hi下载<br/>IM:百度Hi: 百度Hi下载<br/>IM:网易CC语音: 网易CC语音下载<br/>IM:网易云信: 网易云信下载<br/>IM:腾讯QQ: 腾讯QQ下载<br/>IM:腾讯TM: 腾讯TM下载<br/>IM:腾讯通\(RTX\): 腾讯通\(RTX\)下载<br/>IM:钉钉: 钉钉下载<br/>IM:阿里旺旺: 阿里旺旺下载<br/>IM:飞书: 飞书下载<br/>IM:飞信: 飞信下载<br/>Mail: 邮箱渠道<br/>Mail:139邮箱: 139邮箱下载<br/>Mail:Foxmail: Foxmail下载<br/>Mail:PP助手: OutLook下载<br/>Mail:新浪邮箱: 新浪邮箱下载<br/>Mail:网易邮箱: 网易邮箱下载<br/>Mail:阿里邮箱: 阿里邮箱下载<br/>NetDisk: 网盘渠道<br/>NetDisk:115网盘: 115网盘下载<br/>NetDisk:360云盘: 360云盘下载<br/>NetDisk:360网盘: 360网盘下载<br/>NetDisk:优蛋: 优蛋下载<br/>NetDisk:华为网盘: 华为网盘下载<br/>NetDisk:坚果云: 坚果云下载<br/>NetDisk:城通网盘: 城通网盘下载<br/>NetDisk:天翼云盘: 天翼云盘下载<br/>NetDisk:夸克网盘: 夸克网盘下载<br/>NetDisk:微云: 微云下载<br/>NetDisk:微盘: 微盘下载<br/>NetDisk:百度网盘: 百度网盘下载<br/>NetDisk:纳米盘: 纳米盘下载<br/>NetDisk:酷盘: 酷盘下载<br/>NetDisk:金山快盘: 金山快盘下载<br/>NetDisk:阿里云盘: 阿里云盘下载<br/>NetShare: 网络共享渠道<br/>NewFile: 新入文件<br/>SoftMgr: 软件管理渠道<br/>SoftMgr:2345软件管家: 2345软件管家下载<br/>SoftMgr:360安全卫士: 360安全卫士下载<br/>SoftMgr:360驱动大师: 360驱动大师下载<br/>SoftMgr:91手机助手: 91手机助手下载<br/>SoftMgr:PP助手: PP助手下载<br/>SoftMgr:天极软件管家: 天极软件管家下载<br/>SoftMgr:微软电脑管家: 微软电脑管家下载<br/>SoftMgr:搜狗手机助手: 搜狗手机助手下载<br/>SoftMgr:爱思助手: 爱思助手下载<br/>SoftMgr:联想电脑管家: 联想电脑管家下载<br/>SoftMgr:腾讯电脑管家: 腾讯电脑管家下载<br/>SoftMgr:豌豆荚2: 豌豆荚2下载<br/>SoftMgr:软媒魔方软件管理: 软媒魔方软件管理下载<br/>SoftMgr:金山手机助手: 金山手机助手下载<br/>SoftMgr:金山毒霸: 金山毒霸下载<br/>SoftMgr:风灵软件管家: 风灵软件管家下载<br/>SoftMgr:驱动人生: 驱动人生下载<br/>SoftMgr:驱动人生软件管理: 驱动人生软件管理下载<br/>SoftMgr:驱动精灵: 驱动精灵下载<br/>TrustSource: 可信进程释放<br/>UnknownSource: 未知进程释放 |
| Child.ScanAttr | string | 威胁鉴定 | Black: 恶意<br/>Safe: 安全<br/>Unknown: 未知<br/>Virus: 恶意<br/>White: 安全 |
| Child.FileMappingType | mask | 映射方式 | 0x04: 读写<br/>0x08: 写复制<br/>0x10: 执行<br/>0x20: 执行读<br/>0x40: 执行读写<br/>0x80: 执行写复制 |
| Child.FileCreateOpName | string | 打开方式 | CREATE: 新建文件<br/>OPEN: 打开文件<br/>OVERWRITE: 覆盖写文件 |
| Child.FileCreateDisposition | int | 打开位置 | 1: 新建<br/>2: 新建覆盖<br/>3: 打开新建<br/>4: 打开存在<br/>5: 打开清空 |
| Child.FileCreateDesiredAccess | mask | 打开权限 | 0x10000000: 所有权限<br/>0x20000000: 执行权限<br/>0x40000000: 写权限<br/>0x80000000: 读权限 |
| Child.FileCreateShareAccess | mask | 共享权限 | 0x1: 共享读<br/>0x2: 共享写<br/>0x4: 共享删除 |
| Child.FileCreateFileAttributes | mask | 设置属性 | 0x1: 只读<br/>0x100: 临时<br/>0x2: 隐藏<br/>0x4: 系统<br/>0x40: 设备<br/>0x80: 常规 |
| Child.FileTotalWrite | int | 文件写入大小 |  |
| Child.FileTotalRead | int | 文件读取大小 |  |
| Child.OldFilePath | string | 源文件路径 |  |
| Child.OldFileTags | string | 源文件标签 | Browser: 浏览器渠道<br/>Browser:114高速浏览器: 114高速浏览器下载<br/>Browser:115极速浏览器: 115极速浏览器下载<br/>Browser:115浏览器: 115浏览器下载<br/>Browser:2345加速浏览器: 2345加速浏览器下载<br/>Browser:2345智能浏览器: 2345智能浏览器下载<br/>Browser:360安全浏览器: 360安全浏览器下载<br/>Browser:360极速浏览器: 360极速浏览器下载<br/>Browser:Edge浏览器: Edge浏览器下载<br/>Browser:GreenBrowser: GreenBrowser下载<br/>Browser:GT游戏浏览器: GT游戏浏览器下载<br/>Browser:hao123桔子浏览器: hao123桔子浏览器下载<br/>Browser:IE浏览器: IE浏览器下载<br/>Browser:iQ浏览器: iQ浏览器下载<br/>Browser:KR浏览器: KR浏览器下载<br/>Browser:MyIE浏览器: MyIE浏览器下载<br/>Browser:Opera: Opera下载<br/>Browser:QQ浏览器: QQ浏览器下载<br/>Browser:Safari浏览器: Safari浏览器下载<br/>Browser:Spartan浏览器: Spartan浏览器下载<br/>Browser:TT浏览器: TT浏览器下载<br/>Browser:UC浏览器: UC浏览器下载<br/>Browser:YY浏览器: YY浏览器下载<br/>Browser:世界之窗浏览器: 世界之窗浏览器下载<br/>Browser:世界之窗浏览器极速版: 世界之窗浏览器极速版下载<br/>Browser:傲游浏览器: 傲游浏览器下载<br/>Browser:搜狗浏览器: 搜狗浏览器下载<br/>Browser:淘宝浏览器: 淘宝浏览器下载<br/>Browser:火狐浏览器: 火狐浏览器下载<br/>Browser:猎豹浏览器: 猎豹浏览器下载<br/>Browser:瑞影浏览器: 瑞影浏览器下载<br/>Browser:百度浏览器: 百度浏览器下载<br/>Browser:百度浏览器hao123专版: 百度浏览器hao123专版下载<br/>Browser:糖果浏览器: 糖果浏览器下载<br/>Browser:花儿世界浏览器: 花儿世界浏览器下载<br/>Browser:谷歌浏览器: 谷歌浏览器下载<br/>Browser:超速浏览器: 超速浏览器下载<br/>Browser:闪游浏览器: 闪游浏览器下载<br/>Browser:随E浏览器: 随E浏览器下载<br/>Browser:青猴浏览器: 青猴浏览器下载<br/>Downloader: 下载器渠道<br/>Downloader:BitComet: BitComet下载<br/>Downloader:IDMan: IDMan下载<br/>Downloader:QQ旋风: QQ旋风下载<br/>Downloader:QQ旋风下载助手: QQ旋风下载助手下载<br/>Downloader:RaySource: RaySource下载<br/>Downloader:旋风高速下载引擎: 旋风高速下载<br/>Downloader:比特彗星: 比特彗星下载<br/>Downloader:电驴: 电驴下载<br/>Downloader:百度下载助手: 百度下载助手下载<br/>Downloader:百度云管家: 百度云管家下载<br/>Downloader:网际快车: 网际快车下载<br/>Downloader:网页迅雷: 网页迅雷下载<br/>Downloader:迅雷: 迅雷下载<br/>Downloader:迅雷云加速: 迅雷云加速下载<br/>Downloader:迅雷精简版: 迅雷精简版下载<br/>Downloader:迅雷迷你版: 迅雷迷你版下载<br/>Downloader:迷你快车: 迷你快车下载<br/>Downloader:迷你电驴: 迷你电驴下载<br/>Downloader:飞鸟下载器: 飞鸟下载器下载<br/>IM: IM渠道<br/>IM:FSLink: FSLink下载<br/>IM:MSN: MSN下载<br/>IM:Skype: Skype下载<br/>IM:YY语音: YY语音下载<br/>IM:京东咚咚: 京东咚咚下载<br/>IM:企业微信: 企业微信下载<br/>IM:微信: 微信下载<br/>IM:易信: 易信下载<br/>IM:润工作: 润工作下载<br/>IM:环信: 环信下载<br/>IM:百度Hi: 百度Hi下载<br/>IM:百度Hi: 百度Hi下载<br/>IM:网易CC语音: 网易CC语音下载<br/>IM:网易云信: 网易云信下载<br/>IM:腾讯QQ: 腾讯QQ下载<br/>IM:腾讯TM: 腾讯TM下载<br/>IM:腾讯通\(RTX\): 腾讯通\(RTX\)下载<br/>IM:钉钉: 钉钉下载<br/>IM:阿里旺旺: 阿里旺旺下载<br/>IM:飞书: 飞书下载<br/>IM:飞信: 飞信下载<br/>Mail: 邮箱渠道<br/>Mail:139邮箱: 139邮箱下载<br/>Mail:Foxmail: Foxmail下载<br/>Mail:PP助手: OutLook下载<br/>Mail:新浪邮箱: 新浪邮箱下载<br/>Mail:网易邮箱: 网易邮箱下载<br/>Mail:阿里邮箱: 阿里邮箱下载<br/>NetDisk: 网盘渠道<br/>NetDisk:115网盘: 115网盘下载<br/>NetDisk:360云盘: 360云盘下载<br/>NetDisk:360网盘: 360网盘下载<br/>NetDisk:优蛋: 优蛋下载<br/>NetDisk:华为网盘: 华为网盘下载<br/>NetDisk:坚果云: 坚果云下载<br/>NetDisk:城通网盘: 城通网盘下载<br/>NetDisk:天翼云盘: 天翼云盘下载<br/>NetDisk:夸克网盘: 夸克网盘下载<br/>NetDisk:微云: 微云下载<br/>NetDisk:微盘: 微盘下载<br/>NetDisk:百度网盘: 百度网盘下载<br/>NetDisk:纳米盘: 纳米盘下载<br/>NetDisk:酷盘: 酷盘下载<br/>NetDisk:金山快盘: 金山快盘下载<br/>NetDisk:阿里云盘: 阿里云盘下载<br/>NetShare: 网络共享渠道<br/>NewFile: 新入文件<br/>SoftMgr: 软件管理渠道<br/>SoftMgr:2345软件管家: 2345软件管家下载<br/>SoftMgr:360安全卫士: 360安全卫士下载<br/>SoftMgr:360驱动大师: 360驱动大师下载<br/>SoftMgr:91手机助手: 91手机助手下载<br/>SoftMgr:PP助手: PP助手下载<br/>SoftMgr:天极软件管家: 天极软件管家下载<br/>SoftMgr:微软电脑管家: 微软电脑管家下载<br/>SoftMgr:搜狗手机助手: 搜狗手机助手下载<br/>SoftMgr:爱思助手: 爱思助手下载<br/>SoftMgr:联想电脑管家: 联想电脑管家下载<br/>SoftMgr:腾讯电脑管家: 腾讯电脑管家下载<br/>SoftMgr:豌豆荚2: 豌豆荚2下载<br/>SoftMgr:软媒魔方软件管理: 软媒魔方软件管理下载<br/>SoftMgr:金山手机助手: 金山手机助手下载<br/>SoftMgr:金山毒霸: 金山毒霸下载<br/>SoftMgr:风灵软件管家: 风灵软件管家下载<br/>SoftMgr:驱动人生: 驱动人生下载<br/>SoftMgr:驱动人生软件管理: 驱动人生软件管理下载<br/>SoftMgr:驱动精灵: 驱动精灵下载<br/>TrustSource: 可信进程释放<br/>UnknownSource: 未知进程释放 |
| Child.FileSecurityAttr | mask | 文件安全属性 | 0x1: 拥有者安全信息<br/>0x10: LABEL安全信息<br/>0x100: 备份安全信息<br/>0x10000000: 未保护的SACL安全信息<br/>0x2: 组安全信息<br/>0x20: 属性安全信息<br/>0x20000000: 未保护的DACL安全信息<br/>0x4: DACL安全信息<br/>0x40: 范围安全信息<br/>0x40000000: 保护的SACL安全信息<br/>0x8: SACL安全信息<br/>0x80: 进程信任LABEL安全信息<br/>0x80000000: 保护的DACL安全信息 |
| Child.FileAttr | mask | 文件属性 | 0x2: 隐藏 |
| Child.ModifyCreateTime | mask | 修改创建时间 |  |
| Child.SetBasicOp | mask | 设置类型 | 0x1: 设置属性<br/>0x2: 修改创建时间 |
| Child.TrojanName | string | 病毒名 |  |
| Child.ModuleSize | int | 模块大小 |  |
| Child.ModuleBase | int | 模块起始地址 |  |
| Child.Cx | int | 坐标X |  |
| Child.Cy | int | 坐标Y |  |
| Child.WindowName | string | 窗口名 |  |
| Child.ClassName | string | 类名 |  |
| Child.AppVersion | int | 应用版本号 |  |
| Child.PipeOpName | string | 管道操作名称 | CREATE: 创建管道<br/>OPEN: 打开管道 |
| Child.PipeName | string | 管道名 |  |
| Child.RemoteThreadOpName | string | 线程操作名 |  |
| Child.ThreadStartAddr | int | 线程起始地址 |  |
| Child.HandleObjectOpName | string | 句柄操作名称 |  |
| Child.HandleAccessMask | int | 句柄访问权限 | 0x1: 结束进程<br/>0x10: 虚拟内存读<br/>0x100: 设置配额<br/>0x2: 创建线程<br/>0x20: 虚拟内存写<br/>0x4: 设置会话ID<br/>0x8: 虚拟内存操作<br/>0x80: 创建进程 |
| Child.DirPath | string | 目录路径 |  |
| Child.QueryClass | int | 信息类别 | 1: 目录信息<br/>2: 完整目录信息<br/>3: 额外目录信息<br/>4: 基础信息<br/>5: 标准信息 |
| Child.LnkPath | string | 快捷方式路径 |  |
| Child.ScriptFileName | string | 脚本名 |  |
| Child.ScriptFilePath | string | 脚本路径 |  |
| Child.ScriptFileMd5 | string | 脚本MD5 |  |
| Child.ScriptFileMd5Type | string | 脚本md5类型 | FullMd5: 全文<br/>HalfMd5: 半文 |
| Child.ScriptContent | string | 脚本内容 |  |
| Child.MailSubject | string | 邮件标题 |  |
| Child.Links | string | 邮件链接 |  |
| Child.Attachment | string | 邮件附件 |  |
| Child.FileStElapsedTime | int | 统计时长 |  |
| Child.FileStEnumDirCnt | int | 枚举目录数 |  |
| Child.FileStWriteDirCnt | int | 写入包含目录数 |  |
| Child.FileStWriteFileCnt | int | 写入文件数 |  |
| Child.FileStWriteExtCnt | int | 写入文件后缀数 |  |
| Child.FileSWriteSize | int | 写入大小 |  |
| Child.FileSWriteSpeed | int | 写入速度 |  |
| Child.FileStRenameDirCnt | int | 重命名包含目录数 |  |
| Child.FileStRenameFileCnt | int | 重命名文件数 |  |
| Child.FileStRenameExtCnt | int | 重命名文件后缀数 |  |
| Child.FileStRenameSrcExtCnt | int | 重命名文件源后缀数 |  |
| Child.FileStDeleteDirCnt | int | 删除包含目录数 |  |
| Child.FileStDeleteFileCnt | int | 删除文件数 |  |
| Child.FileStDeleteExtCnt | int | 删除文件后缀数 |  |
| Child.FileStExtWriteDirCnt | int | 后缀包含写入目录数 |  |
| Child.FileStExtWriteFileCnt | int | 后缀包含写入文件数 |  |
| Child.FileStExtWriteSize | int | 后缀包含写入文件大小 |  |
| Child.FileStExtDeleteDirCnt | int | 后缀包含删除目录数 |  |
| Child.FileStExtDeleteFileCnt | int | 后缀包含删除文件数 |  |
| Child.FileStExtRenameDirCnt | int | 后缀包含重命名目录数 |  |
| Child.FileStExtRenameFileCnt | int | 后缀包含重命名文件数 |  |
| Child.FileStExtRenameSrcExtCnt | int | 后缀包含重命名源后缀数 |  |
| Child.FileStExtName | string | 统计后缀名 |  |
| Child.VulId | int | 漏洞Id |  |
| Child.RemoteInjectEvent | string | 注入事件名称 |  |
| Child.RemoteProcPid | int | 远程进程Pid |  |
| Child.RemoteProcGuid | string | 远程进程唯一ID |  |
| Child.RemoteProcCmdline | string | 远程进程命令行 |  |
| Child.RemoteProcTid | int | 远程线程ID |  |
| Child.RemoteFileName | string | 远程进程名 |  |
| Child.RemoteFilePath | string | 远程进程路径 |  |
| Child.RemoteFileMd5 | string | 远程进程md5 |  |
| Child.RemoteFileMd5Type | string | 远程进程md5类型 | FullMd5: 全文<br/>HalfMd5: 半文 |
| Child.RemoteThreadId | int | 注入线程ID |  |
| Child.RemoteModuleName | string | 注入模块名 |  |
| Child.RemoteModulePath | string | 注入模块路径 |  |
| Child.RemoteModuleMd5 | string | 注入模块md5 |  |
| Child.RemoteModuleMd5Type | string | 注入模块md5类型 | FullMd5: 全文<br/>HalfMd5: 半文 |
| Child.RemoteModuleSize | int | 注入模块大小 |  |
| Child.RemoteModuleBase | int | 注入模块起始地址 |  |
| Common | object | 基础信息 |  |
| Common.EventId | int | 事件自增ID |  |
| Common.EventUUId | string | 事件唯一ID |  |
| Common.SessionId | int | 客户端启动号 |  |
| Common.KernelId | int | 内核事件ID |  |
| Common.Source | string | 事件来源 |  |
| Common.EventTime | int | 事件采集时间 |  |
| Common.AuthId | int | iOA授权ID |  |
| Common.Uid | int | iOA登录用户ID |  |
| Common.UserName | string | 企业账户 |  |
| Common.LoginStatus | int | 登录状态 | 1: 登录<br/>2: 未登录 |
| Common.Mid | string | 唯一标识码 |  |
| Common.Guid | string | GuidEx |  |
| Common.ClientVer | string | 客户端版本号 |  |
| Common.DeviceGroup | string | 终端分组信息 |  |
| Common.MonitorName | string | 监控名称 |  |
| Common.ReportId | int | 数据上报ID |  |
| Environment | object | 系统环境信息 |  |
| Environment.OsBit | string | 系统位数 | 32: 32位<br/>64: 64位 |
| Environment.OsVersion | string | 系统版本 | Win10: Win10<br/>Win11: Win11<br/>Win2000: Win2000<br/>Win2003: Win2003<br/>Win7: Win7<br/>Win8: Win8<br/>WinFuture: WinFuture<br/>WinVista: WinVista<br/>WinXP: WinXP |
| Environment.OsBuild | int | 系统build号 |  |
| Environment.OsProduectDesc | string | 系统版本描述 |  |
| Environment.OsUserName | string | 系统登录用户名 |  |
| Environment.SysStartTimes | int | 系统启动时间 |  |
| Environment.HostName | string | 主机名称 |  |
| Environment.ExportIp | string | 出口IP |  |
| Environment.MacAddr | string | MAC地址 |  |
| Environment.DomainName | string | 域 |  |
| Environment.OsType | string | 系统类型 | Linux: Linux<br/>macOS: macOS<br/>Windows: Windows |
| Alert | object | 告警字段 |  |
| Alert.RuleId | int | 命中的规则ID |  |
| Alert.RuleName | string | 命中的规则名称 |  |
| Alert.RuleNature | string | 命中的规则特性 |  |
| Alert.EventUuid | string | 告警去重ID |  |
| Alert.FixResult | string | 处置结果 |  |
| Alert.FixAction | string | 处置动作 |  |
| Alert.FixType | string | 处置方式 |  |
| Alert.UserOpt | string | 用户选择 |  |
| Alert.AlertSource | string | 告警来源 |  |
| Alert.BlockType | string | 拦截方式 |  |
| Alert.CloudRuleId | int | 云规则Id |  |
| Alert.CloudTitle | string | 云规则标题 |  |
| Alert.CloudEngineName | string | 云判定引擎 |  |
| Alert.IOCInfo | string | Ioc基本信息 |  |
| Alert.ExplainTags | string | 家族信息 |  |
| Alert.Whois | string | 域名信息 |  |

##### 采集日志动作类型取值范围

| 唯一Key | 说明 |
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
| Ransomware | 勒索攻击 |
| Phishing | 钓鱼攻击 |
| Assoc | 动作关联 |

##### 采集日志子动作名称取值范围

| 所属动作 | 唯一Key | 说明 |
| :--- | :--- | :--- |
| Assoc | FileToProc | 文件关联进程 |
| Assoc | InjectPayloadToFile | 注入模块文件关联 |
| Assoc | DefRemoteInject | 未知注入动作关联 |
| Assoc | ApcInject | APC注入动作关联 |
| Assoc | LnkToTarget | 快捷方式关联 |
| Assoc | FileToExplorerCopy | 桌面拷贝关联 |
| Assoc | FileToRundll32 | Rundll32执行关联 |
| Assoc | ScriptToHost | 脚本执行进程关联 |
| Assoc | FileRenameSource | 重命名源文件关联 |
| Assoc | SrcToMove | 文件移动关联 |
| Assoc | SrcToCopy | 文件拷贝关联 |
| Assoc | SrcToRename | 文件重命名关联 |
| Assoc | ArchiveToFile | 压缩包释放关联 |
| Assoc | RegToFile | 注册表值解析关联 |
| Assoc | RemoteThreadInject | 远程线程注入动作关联 |
| File | FileWriteClose | 文件写关闭 |
| File | FileRename | 文件重命名 |
| File | FileRead | 文件读 |
| File | FileReadDir | 枚举目录 |
| File | FileMapping | 文件映射 |
| File | FileCreate | 文件打开 |
| File | FileDelete | 文件删除 |
| File | NamedPipe | 命名管道事件 |
| File | FileStatics | 文件操作统计 |
| File | FileSetBasicInfo | 文件设置基本信息 |
| File | FileSetSecurity | 文件设置安全属性 |
| InjectHook | GetKeyState | 获取虚拟按键状态 |
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
| InjectHook | GetRawInputData | 获取原始输入数据 |
| InjectHook | RegisterHotKey | 注册热键 |
| InjectHook | SetWindowsHookEx | 设置消息钩子Ex |
| InjectHook | SetWinEventHook | 设置消息钩子 |
| InjectHook | GetDC | 获取显示设备 |
| InjectHook | BitBlt | 位块传输 |
| InjectHook | CreateCompatibleBitmap | 创建兼容位图 |
| InjectHook | NtUserFindWindowEx | 查找窗口（NTAPI） |
| InjectHook | GetWindowLongPtr | 获取指定窗口信息 |
| InjectHook | CreateService | 创建服务 |
| InjectHook | StartService | 启动服务 |
| InjectHook | ModifyService | 修改服务 |
| InjectHook | DeleteService | 删除服务 |
| InjectHook | StopService | 停止服务 |
| InjectHook | ReadConsoleW | Cmd命令执行 |
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
| LeftMove | RemoteAt | 远程计划任务（AT） |
| LeftMove | RemoteDeleteService | 远程删除服务 |
| LeftMove | RemoteModifyService | 远程修改服务 |
| LeftMove | RemoteStartService | 远程启动服务 |
| LeftMove | RemoteCreateService | 远程创建服务 |
| LeftMove | RemoteSheduleTask | 远程计划任务 |
| LeftMove | RemoteStopService | 远程停止服务 |
| LeftMove | RemoteWinRM | 远程WinRM访问 |
| LeftMove | FileWriteShareDir | 修改共享文件 |
| LeftMove | RemotePrint | 远程打印机漏洞 |
| LeftMove | RemoteDCOM-WMI | 远程执行WMI/DCOM |
| LeftMove | RemoteRegQueryValue | 远程注册表查询值 |
| LeftMove | RemoteRegSetValue | 远程注册表修改值 |
| LeftMove | RemoteRegCreateValue | 远程注册表创建值 |
| LeftMove | RemoteRegRenameKey | 远程注册表修改键 |
| LeftMove | RemoteRegDeleteKey | 远程注册表删除键 |
| LeftMove | RemoteRegCreateKey | 远程注册表创建键 |
| Module | LoadDriver | 加载驱动 |
| Module | LoadDll | 加载DLL |
| Network | SocketRequest | Socket请求 |
| Network | NetBind | 网络监听 |
| Network | VulAttack | 漏洞攻击 |
| Network | KerberosRequest | Kerberos请求 |
| Network | NetPing | Ping请求 |
| Network | HttpsRequest | Https请求 |
| Network | HttpRequest | Http请求 |
| Network | NetDnsQuery | DNS查询 |
| Phishing | PhishingNet | 钓鱼外联 |
| Proc | ProcessCreate | 进程创建 |
| Proc | RemoteThread | 远程线程注入 |
| Proc | ProcessHandleObject | 打开进程句柄 |
| Ransomware | DocTrap | 修改诱饵文件 |
| Reg | RegDeleteValue | 注册表删除值 |
| Reg | RegSetValue | 注册表设置值 |
| Reg | RegRenameKey | 注册表重命名键 |
| Reg | RegDeleteKey | 注册表删除键 |
| Reg | RegCreateKey | 注册表创建键 |
| Reg | RegQueryValue | 注册表读取值 |
| Script | ScriptScan | 脚本执行 |
| Script | DocumentOpen | 打开文档 |
| Script | MailOpen | 打开邮件 |
| WinEventLog | SchedTaskCreate | 创建计划任务 |
| WinEventLog | BackupDPMasterKey | 备份数据保护主密钥 |
| WinEventLog | PrivilegedOperation | 执行特权对象 |
| WinEventLog | PrivilegedCall | 调用特权服务 |
| WinEventLog | LogonAssignPrivilege | 新登录分配特权 |
| WinEventLog | ObjectPrivilegeChange | 更改对象权限 |
| WinEventLog | OpenSAMObject | 打开SAM对象句柄 |
| WinEventLog | LoginExplicitCredentials | 显式凭据登录 |
| WinEventLog | LoginClaimsInfo | 登录用户声明 |
| WinEventLog | LoginFailed | 登录失败 |
| WinEventLog | UserLocalGroupEnum | 用户本地组成员枚举 |
| WinEventLog | SystemTimeChange | 系统时间已更改 |
| WinEventLog | WmiCreateProcess | WMI创建进程 |
| WinEventLog | WmiOperation | WMI操作 |
| WinEventLog | AuditLogClear | 安全日志清除记录 |
| WinEventLog | LogShutdown | 事件日志记录服务已关闭 |
| WinEventLog | UserRightAssign | 用户权限分配 |
| WinEventLog | SACLPolicyChange | SACL审核策略更改 |
| WinEventLog | AccountCreate | 用户账户创建 |
| WinEventLog | AccountPwdChange | 用户密码更改 |
| WinEventLog | AccountPwdReset | 用户密码重置 |
| WinEventLog | LoginSuccess | 登录成功 |
| WinEventLog | RegisterSecurityEvent | 注册新的安全事件源 |
| WinEventLog | FirewallSettingChange | 更改 Windows 防火墙本地设置 |
| WinEventLog | SpGroupAssignLogon | 已将特殊组分配给新登录 |
| WinEventLog | NetShareObjAccess | 访问网络共享对象 |
| WinEventLog | NetShareObjAdd | 添加网络共享对象 |
| WinEventLog | NetShareObjModify | 修改网络共享对象 |
| WinEventLog | NetShareObjCheck | 检查网络共享对象的权限 |
| WinEventLog | SMBCheckSpnFail | SMB SPN 检查失败 |
| WinEventLog | CMCredentialBackup | 用户成功备份凭据管理器 |
| WinEventLog | ExtDeviceRecognized | 识别新的外部设备 |
| WinEventLog | UserTokenAdjust | 调整了用户权限 |
| WinEventLog | SchedTaskUpdate | 更新计划任务 |
| WinEventLog | SchedTaskDelete | 删除计划任务 |

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