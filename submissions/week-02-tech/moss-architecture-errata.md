# Moss 架构勘误与修订索引（Week 2 → Capability/Receipt）

> 日期：2026-07-20  
> 学员：Neo  
> 目的：Week 2 交付写于 **Plan + quantified expects** 时代；上游 #31 之后主线已切换到 **Capability tree + exhaustive Receipt**。本文索引「历史稿 / 修订稿 / 术语对照」，避免对外继续传播过时叙事。

---

## 1. 该读哪份？

| 用途 | 文件 |
|------|------|
| **当前正确（推荐公开复用）** | [`moss-beginner-guide-v2.md`](./moss-beginner-guide-v2.md) |
| **当前正确（推荐公开复用）** | [`moss-wechat-article-v2.md`](./moss-wechat-article-v2.md) |
| Week 2 历史证据（保留不删） | [`moss-beginner-guide.md`](./moss-beginner-guide.md) |
| Week 2 历史证据（保留不删） | [`moss-wechat-article.md`](./moss-wechat-article.md) |
| 本地活文档 | `experiments/moss/docs/architecture-explained.zh-CN.md` |
| 本地活文档 | `experiments/moss/MOSS-FOR-BEGINNERS.md` |
| 本地活文档 | `experiments/moss/MOSS-STUDY-NOTES.md` |
| 同步日志 | `experiments/moss/docs/ARCHITECTURE-SYNC.md` |

**规则：** 再发公众号 / 分享 / 简历引用，请用 **v2**；历史稿仅作课程当时交付留证。

---

## 2. 术语对照（旧 → 新）

| Week 2 旧说法 | 现行说法 | 说明 |
|---------------|----------|------|
| Plan | Capability tree / CapabilityNode | 写操作产物是嵌套树，不是扁平 plan 对象 |
| `txs[]` | `children` 内的 TransactionNode（+ 嵌套 Capability） | 每 Capability 恰好 1 笔 direct tx |
| quantified `expects` | 仿真 **Changes** + **Receipt** 穷尽覆盖 | 声明不再是证据边界 |
| effects 对账 | Receipt coverage（长度/顺序/同一 Change 对象） | 未覆盖或乱序 → Warning |
| `planHash` / `PLAN_TAMPERED` | 树结构校验 + 重新 action | 不再靠 planHash 防篡改主路径 |
| TokenTable 解析符号 | 只用地址或 `native` | Trusted/Package label 仅用于 Receipt 展示 |
| `plan(steps, flows)` | 返回 TransactionNode / 嵌套 Capability | 作者 API 已换 |
| observation plane | `@Receipt` 解析器 | 纯函数，只看 Changes |
| effects / assetsIn/Out | Receipt `text` + structured `outcome` | MCP 给 Agent 的是有序 leaf texts |
| 零 warning = Plan 做了它声明的事 | 零 warning = Changes 被穷尽解析且无 revert | 意图对齐仍靠 Agent 对照用户原话 |
| ADR 0004 / 0005 / 0006 / 0008 / 0009 | 已删除；看 0010 / 0011 / 0012 | 勿再链到已删 ADR |

---

## 3. 安全叙事如何改写（一句话）

| 旧 | 新 |
|----|----|
| 「作者声明 expects，模拟提取 effects，机械对账」 | 「模拟产生有序 Changes，Receipt 必须穷尽解释，再与用户意图对齐」 |
| 「未声明差异变成 warning」 | 「未覆盖 / 乱序 / 解析失败 / revert 变成 warning」 |
| 「相信 Plan 指纹」 | 「相信仿真证据 + 文字对齐 + 钱包终审」 |

**不变的硬边界：** Moss 永不签名、永不广播；任意 Warning 即停；签名权在钱包与用户。

---

## 4. 其他 Week 2 文件状态

| 文件 | 处理 |
|------|------|
| `moss-project-introduction.md` | 已轻量更新为新叙事 |
| `moss-open-source-challenge.md` | 顶部勘误 + 现行流程摘要 |
| `github-exploration-log-moss.md` | 顶部勘误指针（正文保留当时探索记录） |
| `moss-proof-of-work.md` | 设计要点改为 Capability/Receipt 表述 |
| `moss-open-source-contribution-plan.md` | 保留历史计划；贡献路径见 live fork |
| `*-submit.md` | 增加 v2 链接说明 |
| 排版 HTML / PNG / PDF | 历史排版产物未重渲；正文以 v2 Markdown 为准 |

---

## 5. 上游锚点

- Framework PR：https://github.com/nishuzumi/moss/pull/31  
- 领域语言：`CONTEXT.md`  
- ADR 0010 / 0011 / 0012  
- Agent 规则：`docs/agent-skill.md`  
