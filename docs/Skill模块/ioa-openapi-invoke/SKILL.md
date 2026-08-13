---
name: "ioa-openapi-invoke"
description: "通用 iOA 开放 API 调用技能。让客户针对自己的 iOA 系统（自有后台地址 + SecretId/SecretKey）调用任意云规范 OpenAPI 接口。支持一句话授权：客户说『给某账号授权某资源』即自动查账号、查资源，存在则授权、不存在则告知。也可查询账号/终端/资源/EDR 事件/合规状态，或执行创建账号、加黑名单等。内置 TC3-HMAC-SHA256 签名、多客户配置切换、读写保护、敏感字段 RSA 加密。触发词：给账号授权资源、授权、绑定资源、调用 iOA 接口、iOA OpenAPI、查询账号/终端/设备、调用开放API、ioa api。"
---

# iOA 通用开放 API 调用技能（Agent 执行指引）

> 本文件是 Agent 的执行指引。安装/配置/排障的完整说明见同级 `README.md`；接口示例与 body 模板见 `references/接口调用速查.md`。

## 适用判断
当用户想「调用某个 iOA 接口 / 查账号·终端·资源 / 授权 / 创建账号 / 加黑名单 / 查 EDR 或合规」时启用。脚本在本文件同级 `scripts/`，命令均在 `scripts/` 下执行。

## 前置：确保有可用配置
调用都需要 `--config ../configs/<customer>.json`（或已设 `IOA_BASE_URL/IOA_SECRET_ID/IOA_SECRET_KEY` 环境变量）。
- 若客户尚未配置：引导执行 `python ioa_cli.py init --customer <name>`（向导填 base_url + SecretId/SecretKey，私有化下 service 留空）。配置细节见 README。
- 调用前先 `python ioa_cli.py test --config ../configs/<customer>.json` 验通。

## ⭐ 能力一：一句话授权
用户说「给 张三 授权 OA系统」「把 财务系统 授权给 lisi」时，**直接用 `grant`**，勿让用户拼接口：
```bash
python ioa_cli.py grant --account <账号> --resource <资源名> --config ../configs/<customer>.json
```
- 多资源：重复 `--resource` 或 `--resource A,B`；同名资源消歧：`--resource-area <资源组>`；只看不下发：`--dry-run`。
- 行为：账号✅资源✅→授权成功；账号不存在→告知并停止；资源不存在→告知（列相似项）；同名多项→提示加 `--resource-area`。
- 这是写操作：执行前向用户复述「将给账号 X 授权资源 Y」。

## ⭐ 能力二：自然语言调用任意接口
除授权外，所有接口走通用 `call`。按 5 步翻译用户意图：

1. **找 Action**：先查下表；没有就到 `references/接口调用速查.md`，仍无则到 `references/api-docs/云规范接口/版本：2022-06-01/`（技能内置的全量接口文档）按目录/关键字检索对应 `.md`，读取 Action、输入参数、示例 body。
2. **构造 body**：查询类用 `Condition`：`{"Condition":{"PageNum":1,"PageSize":50,"FilterGroups":[{"Filters":[{"Field":"X","Operator":"eq","Values":["v"]}]}],"Sort":{"Field":"X","Order":"asc"}}}`；操作符 `eq/like/ilike/nlike/gt/egt/lt/elt/array_any`。写类按文档示例填字段。
3. **名称→ID 解析**（关键）：用户给名字、接口要 ID 时，先发一次只读 `call` 换 ID：

   | 名称 | 解析接口 | 取字段 |
   |---|---|---|
   | 账号名/UserId | `Assets/Account/DescribeLocalAccounts` | `AccountId` |
   | 账号分组名 | `Assets/DescribeAccountGroups` | `Id` |
   | 资源名 | `GatewayResource/DescribeBusinessResources`（传 `ServiceName`）| `ServiceId` |
   | 资源组名 | `GatewayResource/DescribeResourceModules` | `AreaId` |
   | 终端名/IP/登录名 | `Assets/Device/DescribeDevices`（8.0+ 默认） | `DeviceId` |
   | 终端分组名 | 枚举平台默认分组 ID（见「版本约定」节）；`Assets/DescribeDevicesGroups` 8.0+ 常返回空 | `GroupId` |

4. **发起调用**：
   - 只读：`python ioa_cli.py call --action <Action> --body '<json>' --config ../configs/<customer>.json`
   - 写操作（Create/Modify/Delete/Save/Add/Remove/Reset/Bind…）：加 `--confirm-write`，**执行前复述并确认**。
   - 含密码等敏感字段：加 `--pwd-field <字段名>` 自动 RSA 加密。
5. **解读响应**：成功取 `Data`；失败按打印的 `API 错误(Code): Message` 说明或调整重试。

### 常见意图 → Action
| 用户这样说 | Action | 写? |
|---|---|---|
| 查账号 / 列账号 | `Assets/Account/DescribeLocalAccounts` | 否 |
| 查组织架构 / 账号分组 | `Assets/DescribeAccountGroups` | 否 |
| 查终端 / 设备列表 | `Assets/Device/DescribeDevices`（默认 8.0+；仅 8.0 以前用 `Assets/DescribeDevices`） | 否 |
| 查终端分组 | 优先枚举平台默认分组 ID（见下节表）；`Assets/DescribeDevicesGroups` 8.0+ 常返回空/路由错误，勿依赖 | 否 |
| 查某终端的软件 | `Assets/DescribeDeviceSoftwares` | 否 |
| 查终端合规状态 | `EndpointControl/DescribeCompliances` | 否 |
| 查 EDR 事件 / 告警 | `EDR/ListEvents` | 否 |
| 查业务资源 | `GatewayResource/DescribeBusinessResources` | 否 |
| 查资源组 | `GatewayResource/DescribeResourceModules` | 否 |
| 查账号已授权资源 | `Assets/DescribeAccountDirectResources` | 否 |
| 创建本地账号 | `Assets/Account/CreateLocalAccount`（Password 加密）| 是 |
| 修改 / 重置 / 启停账号 | `Assets/Account/ModifyLocalAccount` / `ResetLocalAccountPassword` | 是 |
| 创建业务资源 | `GatewayResource/CreateBusinessResource` | 是 |
| 授权 / 解绑资源 | `NGN/SaveAccountResources` / `NGN/DeleteAccountResources` | 是 |
| 设备加 / 移黑名单 | `NGN/AddBlackDevices` / `NGN/RemoveBlackDevices` | 是 |

> 表中没有的需求，走 Step 1 检索文档后用 `call`——没有“调不了的接口”，只是 body 不同。可直接套用的 NL 示例与 body 模板见 `references/接口调用速查.md` 第 6/7 节；全量接口定义见 `references/api-docs/`。

## 版本约定：默认按 8.0+（后续版本均从 8.0 起，无需再兼容 8.0 以前）
**所有设备相关调用一律按 8.0+ 写法（即下面的内容），旧版写法仅作历史兼容备注，不再默认使用。**

- **接口**：`Assets/Device/DescribeDevices`（8.0 以前旧路径 `Assets/DescribeDevices` 在 8.0+ 环境**静默返回空 `[]` 且不报错**，易误判为"环境没终端"，勿再使用）。
- **参数放请求顶层**（不能用 `Condition` 包裹，否则报 `InvalidParameter.RequestParam`）：
  ```json
  {"OsType": 0, "GroupId": 1, "PageNum": 1, "PageSize": 50}
  ```
- **总数读取**：响应 `Data.Paging.Total`（`Items` 为明细列表）。`PageSize` 最大 5000。
- **平台默认分组 ID**（私有化固定常量，与 OsType 配对使用）：

  | 平台 | OsType | 全网终端 | 未分组终端 |
  |---|---|---|---|
  | Windows | 0 | 1 | 2 |
  | Linux | 1 | 40000101 | 40000102 |
  | macOS | 2 | 40000201 | 40000202 |
  | Android | 4 | 40000401 | 40000402 |
  | iOS | 5 | 40000501 | 40000502 |

- **统计终端总数**：遍历各平台「全网终端」分组取 `Paging.Total` 求和即可（实测口径与明细去重一致）；「未分组终端」分组通常与全网分组不重叠，可用作交叉校验。
- **账号接口无此问题**：`Assets/Account/DescribeLocalAccounts` 等账号类接口新旧版本通用（`Condition` 包裹分页），实测正常返回 `Data.Page.Total`。
- 异常兜底：若 `Assets/Device/DescribeDevices` 报 `InvalidRequestRoute`（理论上仅 8.0 以前环境会出现），才退回旧路径 `Assets/DescribeDevices`（`Condition`/`Filters` 包裹）。

## 命令与参数
| 子命令 | 作用 |
|---|---|
| `init` | 向导生成客户配置 |
| `test` | 连通性 + 签名测试 |
| `grant` | 一句话授权 |
| `call` | 调用任意接口 |
| `encrypt` / `pubkey` | 字段 RSA 加密 / 取公钥 |

`call` 关键参数：`--action`、`--body`/`--body-file`、`--confirm-write`、`--pwd-field`、`--version`、`--raw`、`--config`。

## 安全红线（必须遵守）
- 写操作默认被拦截；执行前核对**目标客户**与参数、向用户复述确认，再加 `--confirm-write`。
- 多客户务必核对 `--config`，严禁把 A 客户操作下发到 B 客户。
- 凭证即管理员权限：勿打印/外泄 `secret_key`；勿提交真实配置（`.gitignore` 已忽略）。
- `base_url` 仅指向客户自有 iOA 后台，不连接其它内网地址。
