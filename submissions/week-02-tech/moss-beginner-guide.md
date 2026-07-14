# 第一次跑通 Moss：零私钥完成一笔 Monad 链上交易模拟

> 学 Moss 的第一步，不是连接钱包，也不是先读完整套架构。先用一条命令跑通 `discover → load → action → simulate`，亲眼看到一笔未签名交易如何在真实链上状态中被验证。

如果你第一次打开 Moss 仓库，很容易被 `core`、`simulator`、协议包、MCP Server 和一整套 ADR 劝退。

先别急着逐个包啃源码。

这篇教程只完成一个最小目标：**不使用私钥、不花真实资金，把 1.5 MON 包装成 WMON 的交易构建出来，并在 Monad 主网当前状态上完成模拟验证。** 跑通之后，我们再拆解终端里的四段输出，最后把 Moss 接入 AI Agent。

我在 Moss 源码提交 `94adfea` 上实际执行了本文命令。环境为 Node.js `v22.22.2`、pnpm `11.10.0`；构建成功，离线测试通过，Wrap 示例返回 `warnings: []`。

## 一、先理解边界：Moss 做什么，不做什么？

Moss 是面向 Monad 的 Agent 协议能力层。它把不同 DApp 的交互统一成四步：

```text
discover → load → action → simulate
```

你可以把它们理解成：

1. `discover`：找出「谁能完成这件事」；
2. `load`：读取「该怎么调用、参数是什么意思、有什么风险」；
3. `action`：构建未签名交易和量化预期，得到 Plan；
4. `simulate`：在真实链上状态中回放 Plan，把实际 effects 与预期对账。

Moss 的边界同样重要：**它永不签名，也永不发送交易。** 私钥留在钱包中，Moss 只负责构建和验证。

这也是为什么本文可以使用任意公开地址完成实验：我们不会动用这个地址的资产，只把它当作模拟交易的发送者。

> 安全提醒：Moss 仍是未经审计的 Alpha 软件。零 warning 只代表模拟时点没有发现未声明差异，不代表未来执行一定成功。签名前仍要在钱包中逐笔核对，并只用小额资金测试。

## 二、准备环境：5 分钟完成安装

### 1. 检查 Node.js 与 pnpm

Moss 当前要求 Node.js 22 或更高版本，并使用 pnpm 11。

```bash
node --version
pnpm --version
```

如果机器没有 pnpm，可以安装：

```bash
npm install -g pnpm
```

### 2. 克隆并构建 Moss

```bash
git clone https://github.com/nishuzumi/moss.git
cd moss
pnpm install
pnpm build
```

这是一个 pnpm monorepo。`pnpm build` 会依次构建 Core、Simulator、ERC 接口层、System、Kuru 协议包与 MCP Server。

### 3. 先跑离线测试

```bash
MOSS_SKIP_E2E=1 pnpm test
```

`MOSS_SKIP_E2E=1` 会跳过 Monad 主网 live e2e，适合先确认本地工具链。本文实测各包测试均通过；涉及链上状态的用例会被明确标记为 skipped，而不是静默伪造结果。

如果你去掉这个环境变量，完整测试会访问 Monad 主网 RPC，但仍不会签名或发送交易。

## 三、一条命令跑通标准流程

在仓库根目录执行：

```bash
pnpm --filter @themoss/example-simple-flow wrap
```

这个示例会构建「把 1.5 MON 包装成 WMON」的 Plan，并通过默认 Monad 主网 RPC 进行模拟。它不需要私钥，也不会把交易发到链上。

成功时，终端最后会看到：

```text
warnings: []

✓ No warnings — the unsigned txs may be handed to a wallet for review.
```

注意这句话的准确含义：**未签名交易可以交给钱包继续检查**，而不是「交易已执行」或「结果已保证」。

## 四、读懂输出：四步究竟验证了什么？

### 1. discover：按用户动作找能力

第一段输出会找到 WMON 的 `wrap` capability：

```text
protocol: wmon
method: wrap
verb: wrap
category: token
```

这里搜索的是用户视角的资金动作 `wrap`，不是合约函数名 `deposit()`。Agent 不需要先猜协议函数，再手工拼 ABI。

### 2. load：读取调用契约

第二段输出会告诉调用方：

- 意图是把原生 MON 包装成 WMON；
- 风险标签包含 `fundOut`；
- `amount` 接受人类可读的小数字符串，例如 `"0.5"`；
- 不要提前把金额换算成 wei。

这一步把协议知识写进了机器可读的调用契约。Agent 可以理解参数，不必凭经验猜精度。

### 3. action：生成 Plan，而不是直接发交易

第三段输出是 Plan。最值得看的不是 calldata，而是 `expects`：

```json
{
  "out": [
    {
      "token": "native",
      "amountMax": "1500000000000000000"
    }
  ],
  "in": [
    {
      "token": "WMON_ADDRESS",
      "amountMin": "1500000000000000000"
    }
  ],
  "approvals": [],
  "nfts": []
}
```

它声明了这笔计划允许发生什么：最多流出 1.5 MON，至少收到等量 WMON，不应出现授权或 NFT 变化。

Plan 还包含 `chainId`、`account`、未签名交易 `txs` 与 `planHash`。如果 Plan 在传递过程中被修改，模拟器会重新计算哈希并产生 `PLAN_TAMPERED` warning。

### 4. simulate：用实际 effects 对账

第四段输出会展示实际模拟结果：

- `reverted: false`：调用没有回滚；
- `assetsOut`：流出 1.5 MON；
- `assetsIn`：收到 1.5 WMON；
- `approvals: []`：没有代币授权；
- `warnings: []`：实际 effects 没有越过 Plan 声明的边界。

Moss 的核心不是「模拟成功」，而是**把 Plan 声明的 expects 与模拟提取的 effects 做机械对账**。未声明流出、超额授权、最低流入不足、Plan 被篡改或交易回滚，都会变成 warning。

规则只有一句：**任何 warning 都必须停止，不能交给签名方。**

## 五、新手最容易踩的 5 个坑

### 坑 1：Node.js 版本过低

Moss 的根目录明确要求 Node.js ≥ 22。遇到装饰器、构建或类型解析异常时，先检查版本，不要急着修改源码。

### 坑 2：把 `warnings: []` 当成落链成功

示例只构建与模拟，Moss 没有签名，也没有广播交易。模拟是一道签名前安全网，不是交易回执。

### 坑 3：RPC 不支持 `debug_traceCall`

Moss 模拟依赖 `debug_traceCall`、`callTracer`、`prestateTracer` 和 state overrides。部分免费 RPC 会屏蔽 `debug` 命名空间。默认的 `https://rpc.monad.xyz` 已被项目验证可用。

### 坑 4：不要自己换算 wei

Moss 的金额参数使用人类可读小数字符串，运行时负责读取代币精度并缩放。提前换算会把语义与链上单位混在一起。

### 坑 5：零 warning 后跳过用户意图检查

零 warning 只说明 Plan 做了它自己声明的事。Agent 仍需把 `effects` 与用户原话比较：用户说的是 Swap 还是 Supply？付出的资产和数量是否符合授权？收款和授权对象是否合理？这一步叫 intent alignment，不能由机械对账替代。

## 六、把 Moss 接入 AI Agent

跑通命令行后，可以把同一套能力暴露给支持 MCP 的客户端。先确保已经执行 `pnpm build`，然后配置：

```json
{
  "mcpServers": {
    "moss": {
      "command": "node",
      "args": ["<MOSS绝对路径>/packages/mcp-server/dist/cli.js"],
      "env": {
        "MOSS_RPC_URL": "https://rpc.monad.xyz"
      }
    }
  }
}
```

重启 MCP 客户端后，可以先给 Agent 一个不涉及真实签名的任务：

> 使用 Moss 查询在 Monad 上把 1 MON 换成 USDC 的计划。必须依次执行 discover、load、action、simulate；如有任何 warning，立即停止；零 warning 后仍要把 effects 与我的原始意图逐项对齐。不要签名，不要发送交易。

一个安全的 Agent 流程至少要满足：

1. 不自己编 calldata；
2. 每个 Plan 都强制模拟；
3. 任何 warning 立即停止；
4. 零 warning 后仍检查意图对齐；
5. 只展示人类可读摘要，不索要私钥，不擅自发送交易。

## 七、跑通以后，如何参与开源？

新手不一定要从核心代码开始。Moss 的贡献指南把 Docs 与 Examples 列为高价值贡献方向之一。

你可以从三个层级进入：

1. **文档层**：补充教程、FAQ、错误排查和真实使用案例；
2. **测试层**：为已有 capability 增加 discover / load、Plan 形状或 live e2e 证据；
3. **协议层**：从 `packages/protocols/_template` 复制模板，接入新的 Monad 协议。

如果准备写协议适配器，推荐先读：

- `packages/system/src/wmon.ts`：注释最完整的入门实现；
- `packages/erc`：理解动态地址与标准 ABI；
- `packages/protocols/kuru`：理解报价、精度和链上读取；
- `docs/protocol-onboarding.md`：协议接入 Definition of Done；
- `CONTRIBUTING.md`：分支、changeset、测试与 PR 证据要求。

不要一上来就做一个巨大 Adapter。先在 Issue 中与 Maintainer 对齐范围，再提交小而可审查的改动。

## 写在最后：真正的入门标准是什么？

跑完一条 Wrap 命令，不代表你已经理解 Moss 的全部实现。但你已经建立了最重要的心智模型：

```text
用户意图
  ↓
discover / load
  ↓
action 生成未签名 Plan + expects
  ↓
simulate 提取 effects + warnings
  ↓
零 warning + 意图对齐
  ↓
交给独立钱包复核与签名
```

Moss 的目标不是让 AI Agent 更快地控制资产，而是让 Agent 只能提交一个**受约束、可解释、可模拟、可叫停的交易提案**。

对于新人，最好的学习顺序也同样克制：先跑通，再读输出；先理解边界，再读源码；先完成一个可复验的小改动，再谈复杂协议接入。

---

### 参考资料

- Moss GitHub：https://github.com/nishuzumi/moss
- 中文 README：https://github.com/nishuzumi/moss/blob/main/README.zh-CN.md
- 中文新手指南：https://github.com/nishuzumi/moss/blob/main/docs/getting-started.zh-CN.md
- MCP Tools Reference：https://github.com/nishuzumi/moss/blob/main/docs/mcp-tools.md
- Agent Skill Guide：https://github.com/nishuzumi/moss/blob/main/docs/agent-skill.md
- Contributing：https://github.com/nishuzumi/moss/blob/main/CONTRIBUTING.md

作者：Neo｜Dev Builder（Tech）
