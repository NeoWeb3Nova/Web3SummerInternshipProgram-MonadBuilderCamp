# Team Build Plan｜Moss Mini Demo Squad

> 周次：Week 3｜Day 2  
> 团队：Moss Mini Demo Squad  
> 成员：Neo（Dev）· Riso（PM）· eleven（UI）  
> 日期：2026-07-20

---

## 本周目标

**Friday 前做出一条可演示的 swap 链路：自然语言意图 → Moss Capability 树 → simulate → 确认页 → 钱包签名，并留下 Demo Evidence。**

---

## 任务拆分

### Research 方向（Riso 主导 + Neo 协助）

| 任务 | 负责人 | 截止 | 产出 | 依赖 |
|------|--------|------|--------|------|
| 确认问题真实性 | Riso | Day 2 21:00 | Problem & User Card 定稿 | 无 |
| 竞品/替代方案调研 | Riso | Day 3 12:00 | 1–2 个竞品分析和差异点 | 无 |
| 准备用户测试问题 | Riso | Day 3 21:00 | 3–5 个测试问题和反馈收集表 | 无 |
| 收集 Day 4 用户反馈 | Riso | Day 4 21:00 | Feedback Log | Neo 的 Demo 入口 |
| 起草 Pitch 结构 | Riso | Day 5 12:00 | 3 分钟 Pitch 提纲 | 全部 Demo Evidence 齐 |

### Ops 方向（Riso / eleven 共担）

| 任务 | 负责人 | 截止 | 产出 | 依赖 |
|------|--------|------|--------|------|
| 制定一句话项目介绍 | Riso | Day 2 21:00 | 用于社群和测试招募的一句话 | 无 |
| 招募 3–5 位测试者 | Riso | Day 3 21:00 | 测试者名单和沟通记录 | 一句话介绍 |
| 设计 Demo 演示流程 | eleven | Day 4 12:00 | 3 分钟 Demo 脚本 | UI 线框定稿 |
| 准备录屏/展示素材 | eleven | Day 5 12:00 | 录屏或 Demo 截图 | Demo 可运行 |

### Dev 方向（Neo 主责）

| 任务 | 负责人 | 截止 | 产出 | 依赖 |
|------|--------|------|--------|------|
| 搭建前端项目骨架 | Neo | Day 3 12:00 | 可运行的 Vite + React + wagmi 框架 | 无 |
| 实现意图解析（预置模板） | Neo | Day 3 18:00 | 用户输入 → 结构化参数 | 无 |
| 接入 Moss Kuru swap + simulate | Neo | Day 3 21:00 | 能返回 Capability 树和 Receipt 的 API/Hooks | 项目骨架 |
| 实现确认页 UI | Neo + eleven | Day 4 12:00 | 展示 Receipt 的确认页 | simulate Hook 齐 |
| 连接钱包签名广播 | Neo | Day 4 18:00 | 用户点击后能触发签名（至少展示待签名） | 确认页 |
| 生成 Demo Evidence | Neo | Day 5 12:00 | 交易哈希 / 合约地址 / 录屏 | 钱包签名广播通 |
| 写 Demo README 和运行指南 | Neo | Day 5 18:00 | 可复现的运行说明 | 全部完成 |

---

## 每日 Stand-up 主题

| 日期 | 主题 |
|------|------|
| Day 2（今） | 问题定稿、范围锁定、Monad Fit、Build Plan |
| Day 3 | 项目骨架搭建 + Moss simulate 跑通 |
| Day 4 | UI 确认页 + 用户测试 |
| Day 5 | Demo 录屏 + Pitch + Retro |

---

## 依赖关系图

```text
Riso（PM/Research/Ops）
  │
  ├── 问题定稿 / 竞品调研 / 用户测试 / Pitch
  │
Neo（Dev）
  │
  ├── 前端骨架 → 意图解析 → Moss simulate → 钱包签名 → Demo Evidence
  │
eleven（UI）
  │
  └── 线框 → 高保真/设计稿 → Demo 录屏素材 → 配合 Pitch
```

---

## 风险与缓解

| 风险 | 缓解 |
|------|------|
| Kuru mainnet simulate 不稳定 | 先用离线 mock 验证 UI，再切 mainnet |
| 钱包签名调试耗时 | 先做到展示待签名交易，再补广播 |
| UI 进度滞后 | eleven 先用线框/截图，Neo 用简单表单先跑通功能 |
| 测试用户找不到 | Riso 提前在 Builder 群和社区发招募消息 |

---

## 看板列

建议看板列：`Backlog` → `This Week` → `Doing` → `Review` → `Done`

Riso 在 Day 2 stand-up 后锁定看板工具（GitHub Projects 或 Notion）。
