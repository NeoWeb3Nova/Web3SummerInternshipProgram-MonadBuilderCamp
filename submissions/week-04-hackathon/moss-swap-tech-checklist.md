# Moss Swap 技术验证 Checklist｜给 Neo

> 用途：Day 4 前证明「一笔 Swap 能否稳定产出决策收据所需的结构化证据」  
> 负责人：Neo（Dev / Tech Lead）  
> 原则：先验证证据能否生成，再谈 UI / 上链锚定；**不自动签名、不托管私钥**  
> 关联：`team-matching-card.md` · `problem-idea-card.md` · `experiments/moss/examples/`

---

## 0. 本周技术要回答的问题

| # | 问题 | 成功标准 |
|---|------|----------|
| 1 | Moss Kuru 能否稳定走完 `action → simulate`？ | 本地可复现；有日志或 JSON 落盘 |
| 2 | simulate 输出是否够填「决策收据」最小字段？ | 见 §3 字段表，核心字段有来源 |
| 3 | 能否绑定「用户意图 ↔ Capability ↔ 待签名 tx」？ | 同一版本 ID / 哈希可对照 |
| 4 | 哪些必须真实、哪些可 Mock？ | 写入 Start Card 的真实 vs Mock 表 |
| 5 | 头号技术风险是什么？ | 一句话 + 1 周内如何验证 |

**非目标（本周不做）：** 多协议、自动执行、法律责任判定、完整聊天上链、生产级合约审计。

---

## 1. 环境就绪（30–45 min）

参考：`experiments/moss/examples/agent-swap/README.md`  
路径：`experiments/moss/`

| # | 检查项 | 命令 / 动作 | 状态 |
|---|--------|-------------|------|
| 1.1 | Node 22+、pnpm 可用 | `node -v` · `pnpm -v` | [ ] |
| 1.2 | 依赖已装、包已 build | `pnpm install` · `pnpm build` | [ ] |
| 1.3 | Monad Foundry / anvil（fork 路径） | `foundryup --network monad`（若走 fork） | [ ] |
| 1.4 | 会用哪条 RPC | 本地 fork `8545` / 公开 RPC（写清） | [ ] |
| 1.5 | **永不**把开发私钥用于公网有资金属性账户 | 确认只用 Anvil dev key 或空测试钥 | [ ] |

### 推荐验证路径（二选一）

| 路径 | 适用 | 入口 |
|------|------|------|
| **A. agent-swap（优先）** | 完整：构造 → 模拟 → 未签名 JSON → 可选 wallet send on fork | `examples/agent-swap` |
| **B. simple-flow kuru-swap** | 更快：quote + swap capability + simulate | `examples/simple-flow/src/kuru-swap.ts` |

**建议顺序：** 先 B 确认 simulate 能出 Receipt；再 A 确认「未签名树落盘 + 不经钥匙给 Moss」。

---

## 2. 端到端路径 Checklist

### Path B｜最小 simulate（先绿）

```bash
# 在 experiments/moss 下，按 monorepo 实际 filter 调整
# 示例意图：1 MON → USDC，Kuru
```

| # | 步骤 | 期望结果 | 状态 | 证据位置 |
|---|------|----------|------|----------|
| 2.1 | `registry.action("kuru", "quote", …)` | 返回 `kind === "query"`，有报价数据 | [ ] | 日志 / 截图 |
| 2.2 | `registry.action("kuru", "swap", …)` | 返回 `kind === "capability"`，未签名树 | [ ] | capability JSON |
| 2.3 | `simulator.simulate(capability)` | 有 `results[]`、receipt / warnings | [ ] | simulation JSON |
| 2.4 | 有 Warning 或 halted | **停止，不进入签名**（行为符合安全边界） | [ ] | 记录 Warning 原文 |
| 2.5 | 无 Warning | 打印 ordered Receipt text；人工对照「MON→USDC」意图 | [ ] | 对照笔记 |

### Path A｜agent-swap 落盘（收据数据源）

| # | 步骤 | 期望结果 | 状态 | 证据位置 |
|---|------|----------|------|----------|
| 2.6 | `pnpm --filter @themoss/example-agent-swap fork` | 本地 fork 起来 | [ ] | |
| 2.7 | `… swap -- verified-capability.json` | 写出未签名 JSON；Warning 时 stop | [ ] | `verified-capability.json` |
| 2.8 | 人工 Review Receipts + structured Outcomes | 能回答：付出/收到/滑点/sender | [ ] | 笔记 |
| 2.9 | （可选）`wallet -- send …` | **仅 local fork**；得最终 tx hash | [ ] | tx hash |
| 2.10 | Agent/MCP 路径（可选） | 若走 MCP：禁止手改 Capability 树 | [ ] | |

### 已知坑（提前避）

| 坑 | 处理 |
|----|------|
| 公网 RPC 不支持 `debug_traceCall` | 用 Monad anvil fork 或确认 RPC 支持 trace |
| 报价与 simulate 之间价格漂移 | 记录时间戳；收据绑定**同一次** action 输出 |
| Receipt 文本是展示层 | **以 structured Outcomes 为证据**，文本仅辅助 |
| 参数改过却复用旧 capability | 必须重新 `action` + `simulate` |
| 把密钥交给 Agent/Moss | 禁止；只签已 review 的树 |

---

## 3. 决策收据 · 最小数据模型（验证能否填满）

> 目标：一份 JSON 能在事后回答「当时意图是什么、模拟说了什么、用户确认了什么、链上执行了什么」。  
> **不宣称法律责任。**

### 3.1 字段表

| 字段 | 必须？ | 本周数据来源 | 有则打勾 | 缺口处理 |
|------|--------|--------------|----------|----------|
| `receiptId` | 必须 | 本地生成 UUID | [ ] | 自建 |
| `createdAt` | 必须 | ISO 时间 | [ ] | 自建 |
| `userIntent` | 必须 | 自然语言或结构化「1 MON → USDC」 | [ ] | 手写 / UI 输入 |
| `protocol` | 必须 | 固定 `kuru` | [ ] | 写死首版 |
| `capabilityTree` | 必须 | Moss `action` 输出 | [ ] | 真实 |
| `capabilityHash` | 必须 | 对规范化 JSON 做 hash | [ ] | 自建 hash 函数 |
| `simulation` | 必须 | `simulate` 的 results / outcomes | [ ] | 真实 |
| `warnings[]` | 必须 | simulate warnings | [ ] | 真实；有则 status=blocked |
| `humanSummary` | 必须 | 付出 / 收到 / 风险 三行 | [ ] | **可 Mock 文案**，字段要留 |
| `userDecision` | 必须 | `confirmed` / `rejected` / `blocked` | [ ] | UI 或 CLI 标记 |
| `unsignedTxHashes` 或 tx 摘要 | 尽量 | 待签名交易标识 | [ ] | 从 capability 节点提取 |
| `finalTxHash` | 可选本周 | wallet send 后 | [ ] | fork 上真实；无则 Mock 说明 |
| `anchorTxHash` | 可选下下周 | 收据 hash 上链 | [ ] | **本周 Mock** |
| `privacyNote` | 必须 | 「敏感详情本地，链上仅哈希」 | [ ] | 文案常量 |

### 3.2 最小 JSON 骨架（实现时对齐）

```json
{
  "receiptId": "uuid",
  "createdAt": "2026-07-29T21:00:00+08:00",
  "version": "0.1.0",
  "userIntent": {
    "text": "swap 1 MON to USDC",
    "tokenIn": "NATIVE",
    "tokenOut": "USDC",
    "amountIn": "1",
    "slippageBps": 50
  },
  "protocol": "kuru",
  "capabilityHash": "0x…",
  "capabilityTree": {},
  "simulation": {
    "halted": false,
    "results": [],
    "outcomes": []
  },
  "warnings": [],
  "humanSummary": {
    "pay": "1 MON",
    "receive": "~X USDC (sim)",
    "risks": []
  },
  "userDecision": {
    "status": "confirmed",
    "decidedAt": "…"
  },
  "execution": {
    "finalTxHash": null,
    "note": "optional on local fork"
  },
  "anchor": {
    "mode": "local_only",
    "contentHash": "0x…",
    "chainTxHash": null
  },
  "disclaimer": "Records facts only. Does not assign legal liability."
}
```

### 3.3 绑定完整性（安全关键）

| # | 检查 | 状态 |
|---|------|------|
| 3.3.1 | 改 capability 任一参数后，`capabilityHash` 必须变 | [ ] |
| 3.3.2 | 有 Warning 时 `userDecision` 不得为 confirmed（除非显式 override 并记录） | [ ] |
| 3.3.3 | `humanSummary` 与 structured outcomes **不一致**时，标记 `summaryTrust=derived_unverified` | [ ] |
| 3.3.4 | Moss 进程拿不到签名私钥 | [ ] |

---

## 4. 真实运行 vs Mock（填完交给 Day 5 Start Card）

| 能力 | 真实 / Mock / 人工 | 理由 | 状态 |
|------|-------------------|------|------|
| Kuru quote + swap capability | | | [ ] |
| simulate + warnings | | | [ ] |
| 自然语言 → 结构化意图 | | 可正则/固定句式 | [ ] |
| humanSummary 中文解释 | | 可规则模板 | [ ] |
| 用户确认按钮 / CLI confirm | | | [ ] |
| 钱包签名 + 广播 | | 建议仅 local fork | [ ] |
| 决策收据 JSON 落盘 | | | [ ] |
| 收据 contentHash | | 本地 keccak/sha256 | [ ] |
| 哈希锚定 Monad 合约 | | 可整段 Mock | [ ] |
| 多协议 / 跨链 | 砍掉 | 范围外 | [x] |

**默认建议（可改）：**

- **真实：** capability 构造、simulate、警告停签、收据 JSON + hash  
- **Mock / 简化：** 自然语言解析、精美 UI 文案、链上 anchor 合约  
- **人工：** 第一次 Review 对照表、Demo 讲解脚本  

---

## 5. 验证实验记录模板（Neo 每跑一轮填一条）

```markdown
### 验证轮次｜日期时间

| 字段 | 内容 |
|------|------|
| **路径** | A agent-swap / B simple-flow / 其他 |
| **网络** | local fork / 其他 |
| **意图** | 1 MON → USDC，slippage= |
| **quote OK?** | 是/否 |
| **capability OK?** | 是/否 |
| **simulate OK?** | 是/否 · halted? · warnings 数 |
| **能否填满收据最小字段?** | 是/否 · 缺哪些 |
| **耗时** | action __s · simulate __s |
| **产物路径** | `…/verified-capability.json` 等 |
| **阻塞** | |
| **下一步** | |
```

---

## 6. 完成定义（Definition of Done · 技术侧 Day 4）

全部满足才算「技术风险基本可控」：

- [ ] 至少 **1 次** 可复现的 Kuru `action → simulate` 成功记录  
- [ ] 至少 **1 份** 未签名 capability JSON（或等价）落在仓库或本地证据目录  
- [ ] 决策收据最小字段表：**必须字段**有来源（真或明确 Mock）  
- [ ] 真实 vs Mock 表填完，可直接贴进 Start Card  
- [ ] 写下 **头号技术风险** 一句话 + 若失败时的缩小方案  
- [ ] 与 Riso 交叉：若访谈说「不要事后收据」，技术范围缩到签前 summary + capability 绑定即可  

### 头号风险草稿（验证后改）

| 字段 | 内容 |
|------|------|
| **风险类型** | 技术 / 需求 / 协作 |
| **描述** | 例：公网 RPC 无法稳定 trace；或 structured outcome 不够生成用户能懂的三行摘要 |
| **1 周内最小验证** | 例：只在 local fork 跑通 + UI 用固定模板摘要 |
| **失败时缩小** | 砍 anchor；收据仅本地；甚至只做签前确认页（Week 3 能力） |

---

## 7. 今日时间盒（约 6 小时内可切）

| 块 | 时长 | 动作 |
|----|------|------|
| 环境 | 0.5–1h | §1 绿灯 |
| Path B | 1–1.5h | quote → swap → simulate |
| 收据映射 | 1h | §3 字段对照 + 骨架 JSON 手工填一版 |
| Path A（可选） | 1–1.5h | 落盘 + fork send |
| 边界文档 | 0.5h | §4 表 + 头号风险 |
| 同步 | 0.25h | stand-up 三句 + 把阻塞丢群里 |

**若 2 小时内 Path B 仍红：** 停止深挖；改用 **已有 Week 3 日志/截图 + Mock simulate JSON** 证明「数据结构可设计」，把「主网稳定 simulate」标为 Build Sprint 风险，不阻塞 Day 4 需求结论。

---

## 8. 安全边界（硬约束 · 复制自团队协议）

1. 不托管用户私钥；Moss 不接收签名密钥。  
2. 只规划与模拟，**不**自动签名、**不**自动广播。  
3. 有 Warning / halted → 默认停止。  
4. 测试网 / fork 证据可核验；禁止编造 tx hash。  
5. AI 生成代码须人工过目再进 Demo。  

---

## 9. 产物建议落盘位置

```text
submissions/week-04-hackathon/
  moss-swap-tech-checklist.md     ← 本文件
  evidence/                       ← 可选新建
    YYYYMMDD-kuru-simulate.json
    YYYYMMDD-decision-receipt-draft.json
    YYYYMMDD-tech-notes.md
```

敏感路径、私钥、完整助记词 **不要**提交仓库。

---

## 10. 与 Riso / eleven 的接口

| 你产出 | 对方怎么用 |
|--------|------------|
| 「simulate 稳定 / 不稳定」结论 | Riso 决定 Demo 是否承诺实时模拟 |
| 真实 vs Mock 表 | Day 5 Start Card 直接粘贴 |
| humanSummary 能自动生成吗 | eleven 决定文案是规则模板还是纯设计稿 |
| Warning 列表样例 | eleven 风险区 UI 用真实文案 |

访谈若显示用户**只要签前三行、不要收据**：你把 §3 缩成 `intent + capabilityHash + summary + decision`，砍 `anchor` 与完整时间线。
