---
type: mixed
density: balanced
style: blueprint-editorial
palette: graphite-cyan-red-yellow
image_count: 4
---

# Moss 文章配图 Outline

## Illustration 1

**Position**: 第一节“协议能力层 + 签名前验证层”段落后
**Purpose**: 显示 Moss 在 Agent 与 Wallet 之间的位置和职责边界
**Visual Content**: USER INTENT → AI AGENT → MOSS（PLAN / SIMULATE / HALT）→ WALLET → ONCHAIN；私钥只在 Wallet 一侧
**Filename**: `01-framework-moss-boundary.png`

## Illustration 2

**Position**: 第二节“Prompt 无法机械比较”段落后
**Purpose**: 对比“能调用”与“可验证”的安全差异
**Visual Content**: 左侧 DIRECT CALL 直接通向链上风险；右侧 VERIFIED PLAN 经过 EXPECTS、SIMULATE、EFFECTS、WARNING 再进入签名
**Filename**: `02-comparison-call-vs-verify.png`

## Illustration 3

**Position**: 第三节“任何未声明差异都会变成 warning”金句后
**Purpose**: 解释双 tracer、状态继承和 effects reconciliation
**Visual Content**: CALL TRACER 与 PRESTATE TRACER 双轨输入 EFFECTS，再与 EXPECTS 对账；差异流向 WARNING / HALT
**Filename**: `03-flowchart-dual-tracer.png`

## Illustration 4

**Position**: 第五节“模拟是一张安全网，不是未来状态的预言机”段落后
**Purpose**: 明确模拟通过的时间边界
**Visual Content**: 左侧 SIMULATION SNAPSHOT 检查 Plan、effects、warning；中间时间变化；右侧 WALLET RECHECK 与 USER SIGN，市场状态仍可能变化
**Filename**: `04-comparison-simulation-boundary.png`
