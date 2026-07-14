# AgentGuard 实现概览：本地优先的 AI Agent 运行时安全控制层

> 来源：AgentGuard 官网（含 Runtime Policy 控制台页面 /runtime/policy）、GitHub 仓库、API 文档  
> 整理日期：2026-07-14  
> 整理目的：为后续可能复刻或集成 AgentGuard 提供可直接落地的架构参考与 MVP 路径

---

## 核心结论

AgentGuard 的核心不是「检查提示词」，而是一个 **以本地运行时拦截为主体、以云端策略控制台为配置中心的 AI Agent 安全控制层**。它将以下四个能力组合起来：

- **静态扫描（Deep Scan / SkillScanner）**：安装前检测 Skills、Plugins、MCP Server、依赖包中的恶意代码与风险特征。
- **运行时拦截（Runtime Guard / ActionScanner）**：在 Agent 执行高危动作前进行判断，输出 `allow / alert / approval / block`。
- **信任注册表（SkillRegistry）**：记录组件身份、hash、能力边界与信任等级，动态降权。
- **云端策略控制台（Cloud Policy Console）**：Web 端配置策略模式、风险矩阵、自定义规则，本地 AgentGuard 通过 `agentguard policy pull` 拉取并应用。
- **审计与事件回传（Audit + Event Ingest）**：本地生成不可篡改审计日志，将脱敏运行时事件回传云端进行验证与报告。

---

## 1. 产品定位与覆盖范围

AgentGuard 面向以下 AI 开发环境：

- Claude Code
- Codex
- Cursor
- MCP Server
- OpenClaw
- Hermes Agent 等

目标是在 Agent 执行高风险动作之前进行判断、阻断或要求确认。官网强调覆盖的动作类型包括：

- shell 命令执行
- 文件访问（读 / 写 / 删除）
- 工具调用
- 网络请求
- 密钥访问
- 敏感数据写入
- webhook 外传
- Web3 交易与签名

---

## 2. 公开产品三层结构

### 2.1 Runtime Guard

在 Agent 调用工具前拦截动作。判断结果由云端策略控制台配置，页面 `/runtime/policy` 展示了四档决策：

- `allow`（放行）：允许直接执行
- `alert`（告警）：执行后记录并告警
- `approval`（审批）：弹窗要求用户确认
- `block`（拦截）：直接拒绝

### 2.2 策略模式

`/runtime/policy` 页面提供三种策略模式：

| 模式 | 说明 | 适用阶段 |
|------|------|----------|
| `Observe` | 只记录，不拦截 | 上线初期观察真实流量 |
| `Balanced` | 严重风险直接拦截，敏感动作走审批 | 默认推荐 |
| `Strict` | 大部分高风险动作进入审批或拦截 | 高安全要求场景 |

### 2.3 风险矩阵（Balanced 默认）

`/runtime/policy` 页面将风险分成 5 类，每类都可配置为四档决策之一：

| 风险类别 | Balanced 默认 | 说明 |
|----------|----------------|------|
| 破坏性命令 | block | 如 `rm -rf /` |
| 远程代码执行 | block | 如 `curl \| bash` |
| 部署动作 | approval | 可能影响生产环境 |
| 数据外泄 | block | 传输敏感信息到可疑地址 |
| 密钥访问 | approval | 读取 `.env`、`.ssh` 等敏感文件 |

### 2.4 自定义规则（来自 /runtime/policy 页面）

**受保护路径（Protected Paths）**

- `~/.ssh/**`
- `~/.aws/**`
- `~/.config/**/credentials*`
- `**/.env*`
- `**/*private-key*`
- `**/*seed*`

**阻止域名（Blocked Domains）**

- `discord.com/api/webhooks`
- `hooks.slack.com/services`
- `api.telegram.org/bot`

**阻止命令（Blocked Commands）**

- `rm -rf /`
- `curl ... | bash`
- `wget ... | sh`
- `base64 -d | bash`
- `git push --force`

**允许命令示例（Allowed Commands）**

- `git status *`
- 其他经评估无风险的确定性命令

### 2.5 策略同步与验证

`/runtime/policy` 页面的策略不仅存在浏览器端，而是：

1. Web 控制台配置并保存到云端策略服务
2. 本地 AgentGuard 执行 `agentguard policy pull` 拉取最新策略
3. 本地运行时拦截 Agent 动作
4. 将脱敏运行时事件回传云端
5. 控制台对比“云端策略版本”与“本地上报版本”，验证本地是否接入并生效

```text
Web 控制台 /runtime/policy
  -> 配置策略模式、风险矩阵、自定义规则
  -> 保存到云端策略服务
  -> 本地执行 agentguard policy pull
  -> 本地运行时拦截 Agent 动作
  -> 根据策略返回 allow / alert / approval / block
  -> 脱敏运行时事件回传云端
  -> 控制台验证策略版本一致性
```

### 2.6 Deep Scan

扫描 Skills、Plugins、MCP Server 代码、包、Agent runtime 代码。官网披露：

- 6 类检测器
- 24 条安全规则
- 覆盖：凭证泄露、提示注入、恶意命令、数据外传、权限滥用、URL 分析

### 2.7 OpenClaw Environment Patrol

持续巡检环境漂移，包括：

- Skill 完整性
- Secrets 暴露
- 网络暴露
- 定时任务
- 文件变化
- 审计日志
- 环境配置
- 信任注册表健康度

---

## 3. 代码层四个核心模块

### 3.1 SkillScanner：静态扫描器

源码里 `SkillScanner` 会优先尝试调用外部 `skill-scanner`，失败后回退到内置规则扫描。

内置扫描流程：

1. 遍历目录
2. 按文件扩展名选择规则
3. 扫描内容
4. 对 Markdown 只扫描 fenced code block
5. 提取并解码 base64 后二次扫描
6. 汇总证据
7. 按命中的规则严重程度计算风险等级

**可复刻方法：**

- 建一个规则库：每条规则包含 `id`、`severity`、`patterns`、可选 `validator`。
- 文件遍历时忽略无关目录，例如 `.git`、`node_modules`。
- 对代码、Markdown、配置文件采用不同扫描策略。
- 对 base64、混淆字符串、远程加载命令做二次解析。
- 输出统一结构：`risk_level`、`risk_tags`、`evidence`、`summary`、`metadata`。

### 3.2 SkillRegistry：信任注册表

`SkillRegistry` 负责记录某个 Skill/Plugin 是否可信、允许哪些能力、是否过期、hash/version 是否变化。

查找逻辑：

1. 先精确匹配
2. 再按来源匹配
3. 如果记录过期、被撤销、hash/version 变化，就降级为 `untrusted`

**可复刻方法：**

- 给每个组件建立身份：`id`、`source`、`version_ref`、`artifact_hash`。
- 保存信任等级：`trusted`、`restricted`、`untrusted`。
- 保存能力模型：网络白名单、文件白名单、是否允许执行命令、允许访问哪些 secret、Web3 链白名单等。
- 组件更新后重新计算 hash，不一致则自动降权。
- 信任升级或能力扩大时要求人工确认。

### 3.3 ActionScanner：运行时决策引擎

`ActionScanner` 收到一个动作 envelope 后：

1. 先查 actor 对应的能力
2. 按动作类型路由：
   - `web_search`
   - `network_request`
   - `exec_command`
   - `web3_tx`
   - `web3_sign`
   - `secret_access`
   - `read_file`
   - `write_file`
3. 根据风险返回 `allow / confirm / deny`

**典型规则（需更新为四档决策语义）：**

- 搜索词或请求体包含私钥/助记词：`block` 或 `approval`。
- 命令是危险命令、远程脚本执行、fork bomb：`block`。
- 文件路径命中 `.env`、`.ssh`、AWS credentials、Kube config：`approval` 或 `block`，取决于策略。
- 路径穿越：`block`。
- 网络请求到非白名单域名：`alert`、`approval` 或 `block`，取决于策略。
- Web3 交易检查 phishing origin、恶意地址、无限授权、交易模拟结果：可配置为 `approval` 或 `block`。

### 3.4 Adapters / Hooks：接入不同 Agent 平台

README 说明各平台接入方式：

- **Claude Code**：`PreToolUse` / `PostToolUse`
- **OpenClaw**：`before_tool_call` / `after_tool_call`
- **Hermes**：`pre_tool_call` / `post_tool_call`

OpenClaw 还会在插件注册时：

- 自动扫描插件
- 确定信任等级
- 推断能力
- 注册到 trust registry
- 建立 `toolName -> pluginId` 映射

---

## 4. 完整执行链（更新后，含云端策略同步）

```text
Agent 想执行动作
  -> 平台 Hook 捕获 tool call
  -> 适配器把平台事件转成统一 ActionEnvelope
  -> 本地执行 agentguard policy pull 获取最新策略
  -> ActionScanner 查询 SkillRegistry
  -> 根据动作类型运行检测器
  -> 根据云端策略输出 allow / alert / approval / block
  -> 执行、弹审批、或阻断
  -> 写入本地审计日志
  -> 脱敏运行时事件回传云端
  -> 控制台验证策略版本一致性
```

---

## 5. 云端 API 与策略

文档公开的云端 API：

### 5.1 运行时评估

- `POST /api/v1/actions/evaluate`：动作评估
- `GET /api/v1/policies/effective`：获取策略
- `POST /api/v1/events/ingest`：同步脱敏审计事件

### 5.2 供应链扫描

- `POST /api/v1/scan`
- `POST /api/v1/scan-url`
- `POST /api/v1/scan-registry`
- `GET /api/v1/report/:scanId`

### 5.3 认证

- `X-API-Key`
- Bearer Token

---

## 6. 隐私边界

官网 FAQ 说明：

- **本地模式**：不会上传完整代码、提示词、secret 或文件内容。
- **启用云服务时**：可能上传脱敏后的动作预览和 metadata，用于审批、审计和报告。

---

## 7. 可复刻 MVP 实现路径

如果自己实现一个类似 AgentGuard 的本地工具，建议按以下顺序推进：

### 7.1 CLI 基础命令

```bash
agentguard scan <path>
agentguard protect
agentguard trust list
agentguard trust attest <path>
agentguard report
```

### 7.2 统一动作模型

命令、文件、网络、secret、工具调用都转成同一个 JSON envelope。

### 7.3 规则扫描器

先用正则 + validator，不急着上 AI。

### 7.4 本地信任库

JSONL 或 SQLite 都可以，记录组件 hash、能力、信任等级。

### 7.5 Hook 接入

优先接一个平台，比如 Codex 或 Claude Code。

### 7.6 审计日志

本地 `audit.jsonl`，每条记录保存：

- actor
- action
- decision
- risk_tags
- evidence
- timestamp

### 7.7 云端能力

基于 `/runtime/policy` 页面揭示的云端策略中心：

- **策略模式：** `Observe` / `Balanced` / `Strict`
- **风险矩阵：** 按风险类别配置 `allow / alert / approval / block`
- **自定义规则：**
  - 受保护路径
  - 阻止域名
  - 阻止命令
  - 允许命令
- **策略下发：** `本地执行 agentguard policy pull 拉取`
- **验证机制：** 控制台对比云端策略版本与本地上报版本
- **脱敏审计同步：** 同步运行时事件 metadata 用于验证与报告

### 7.8 威胁情报（可选）

恶意包、域名、MCP server、prompt injection payload 的订阅更新。

---

## 8. 关键设计原则

1. **以云端为配置中心，以本地为执行主体（Cloud-Config, Local-Enforce）**：策略在 Web 端配置，本地拉取后离线也能拦截。
2. **四档决策语义（allow / alert / approval / block）**：比三档更细，支持“记录不阻”的观察模式。
3. **默认拒绝（Default Deny）**：未明确授权的高危动作应被拦截。
4. **最小权限（Least Privilege）**：Skill 的能力白名单应尽可能收紧。
5. **本地优先（Local First）**：敏感判断尽量在本地完成，减少原始数据上云。
6. **可审计（Auditability）**：所有拦截、放行、审批、修复动作均生成结构化日志。
7. **完整性绑定（Integrity Binding）**：组件 hash 变化自动触发信任降级。
8. **执行前判断（Pre-execution Policy）**：核心防御点在动作执行前，而不是事后检测。
9. **策略验证闭环（Policy Verification Loop）**：云端策略版本与本地上报版本对比，确保本地已接入并生效。

---

## 9. 与本项目（AI × Web3 Builder Camp）的关联

AI Agent 安全是 Web3 Builder 不可忽视的基础能力。无论是 Tech 轨做链上 Agent、Ops 轨做自动化工具，还是 Research 轨分析安全协议，理解 AgentGuard 这类控制层的设计都能帮助：

- 识别自己项目中的过度授权与供应链风险。
- 为 Hackathon 项目加入「人机确认」或「策略守卫」卖点。
- 在作品集里展示对 Agent 安全生命周期的系统性理解。

---

## 参考来源

- AgentGuard 官网：https://www.agentguard.one/
- GitHub 仓库：https://github.com/GoPlusSecurity/agentguard
- API 文档：https://www.agentguard.one/docs/api
- LXDAO × GoPlus AI Agent 安全分享笔记：`docs/ai-agent-security-lxdao.md`

---

## 10. 下一步可选方向

1. 将本概览扩展为一份完整白皮书（架构图 + API 设计 + 部署指南 + 策略控制台流程图）。
2. 在 `experiments/agentguard-mvp/` 下实现一个可运行的 TypeScript/Python 原型，优先复刻 `agentguard policy pull` 和四档决策引擎。
3. 为 Hermes Agent 写一个 `pre_tool_call` Hook 适配器。
4. 制作 AgentGuard 与 Pillar、Windsurf、Lasso 等方案的竞品对比表。
5. 继续研究 AgentGuard 其他页面：`dashboard`、`runtime`、`feed`、`api-keys`、`usage`、`docs`，形成更完整的产品与技术拆解。
