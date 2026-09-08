# Skill 模块

本目录汇集 iOA 团队官方发布的 **Agent Skill 包**。Skill 是一种可被 AI 编程助手（如 CodeBuddy）自动加载的能力扩展包，包含领域知识、标准工作流（SOP）与可执行脚本，能让 Agent 更准确、更高效地完成 iOA 相关任务。

## 已发布 Skill 列表

| Skill 名称 | 简介 | 版本 | 下载 |
|---|---|---|---|
| [ioa-openapi-invoke](Skill模块/ioa-openapi-invoke/SKILL.md) | 通用 iOA 开放 API 调用技能。用自然语言即可调用任意云规范 OpenAPI（授权、查账号/终端/资源、EDR、合规等），内置 TC3-HMAC-SHA256 签名、多客户配置切换、读写保护与敏感字段 RSA 加密。 | latest | [ioa-openapi-invoke.tar.gz](Skill模块/ioa-openapi-invoke.tar.gz ':ignore') |

## 安装方式

以 CodeBuddy 为例（其他兼容 Skill 协议的 Agent 类似）：

1. 点击上方"下载"链接，获取 `ioa-openapi-invoke.tar.gz`。
2. 解压到 Agent 的 skills 目录：

   ```bash
   # macOS / Linux
   mkdir -p ~/.codebuddy/skills
   tar -xzf ioa-openapi-invoke.tar.gz -C ~/.codebuddy/skills/

   # Windows (PowerShell)
   New-Item -ItemType Directory -Force -Path "$env:USERPROFILE\.codebuddy\skills" | Out-Null
   tar -xzf ioa-openapi-invoke.tar.gz -C "$env:USERPROFILE\.codebuddy\skills\"
   ```

3. 安装 Python 依赖：

   ```bash
   cd ~/.codebuddy/skills/ioa-openapi-invoke
   pip install -r requirements.txt
   ```

4. 初始化你自己的 iOA 客户配置：

   ```bash
   cd scripts
   python ioa_cli.py init --customer <your-name>
   ```

5. 重启（或让 Agent 重新扫描技能目录），随后即可通过自然语言触发，例如：
   - "给张三授权 OA 系统"
   - "查一下终端 10.1.2.3 的合规状态"
   - "调用 iOA 接口列出所有本地账号"

## 相关文档

- Skill 执行指引（面向 Agent）：[SKILL.md](Skill模块/ioa-openapi-invoke/SKILL.md)
- 使用手册（面向用户）：[README.md](Skill模块/ioa-openapi-invoke/README.md)
- 接口调用速查：[接口调用速查.md](Skill模块/ioa-openapi-invoke/references/接口调用速查.md)

## 安全须知

- SecretId / SecretKey 属于高危凭证，请妥善保管，切勿提交到公共仓库。
- 建议通过环境变量 `IOA_BASE_URL / IOA_SECRET_ID / IOA_SECRET_KEY` 注入，或使用 `configs/<customer>.json` 并对文件加权限保护（`chmod 600`）。
- 写操作（创建/修改/删除/授权 等）在 Skill 中默认拦截，需显式 `--confirm-write` 才会执行，请在生产环境慎用。
