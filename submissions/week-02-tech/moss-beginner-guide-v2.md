# 第一次跑通 Moss：零私钥完成一笔 Monad 链上交易模拟（v2 · Capability/Receipt）

> **修订版 · 2026-07-20**  
> 对齐上游 Capability Tree + Exhaustive Receipt（#31）。  
> Week 2 历史稿：[`moss-beginner-guide.md`](./moss-beginner-guide.md)（Plan/expects 叙事，仅作留证）  
> 勘误总表：[`moss-architecture-errata.md`](./moss-architecture-errata.md)

> 学 Moss 的第一步，不是连接钱包，也不是先读完整套架构。先用一条命令跑通 `discover → load → action → simulate`，亲眼看到一笔**未签名交易**如何在真实链上状态中被模拟，并翻译成可核对的 Receipt 文字。

如果你第一次打开 Moss 仓库，很容易被 `core`、`simulator`、协议包、MCP Server 和一整套 ADR 劝退。

先别急着逐个包啃源码。

这篇教程只完成一个最小目标：**不使用私钥、不花真实资金，把 1.5 MON 包装成 WMON 的交易构建出来，并在 Monad 主网当前状态上完成模拟验证。** 跑通之后，再拆解四段输出，最后把 Moss 接入 AI Agent。

环境参考：Node.js 22+、pnpm 11；命令以官方 monorepo 为准。

## 一、先理解边界：Moss 做什么，不做什么？

Moss 是面向 Monad 的 Agent 协议能力层。它把不同 DApp 的交互统一成四步：

```text
discover → load → action → simulate
```

你可以这样理解：

1. **discover**：找出「谁能完成这件事」（protocol + method）；  
2. **load**：读取「参数契约、意图说明、风险标签」；  
3. **action**：构建一棵 **Capability 树**（未签名交易，可嵌套子能力）；  
4. **simulate**：用 `debug_traceCall` 回放，抽出有序 **Changes**，经 **Receipt** 穷尽解析，返回可核对文字与 Warning。

Moss 的边界同样重要：**它永不签名，也永不发送交易。** 私钥留在钱包中；Moss 只负责构建和验证。

这也是为什么可以用任意公开地址完成实验：不会动用该地址资产，只把它当作模拟发送者。

> 安全提醒：Moss 仍是未经审计的 Alpha 软件。零 Warning 只代表**模拟时点**的 Changes 可被完整解析且未 revert，不代表未来执行一定成功。签名前仍要在钱包中逐笔核对，并只用小额资金测试。

### 和旧教程差在哪？（30 秒）

| 旧（Plan 时代） | 新（现行） |
|-----------------|------------|
| action 产出 Plan + expects | action 产出 Capability 树 |
| simulate 把 effects 与 expects 对账 | simulate 要求 Receipt **穷尽覆盖** Changes |
| 看 assetsIn/Out 摘要 | 看有序 Receipt **texts** + structured outcome |
| planHash 防篡改 | 结构校验；改参数请重新 action |

## 二、准备环境：5 分钟完成安装

### 1. 检查 Node.js 与 pnpm

```bash
node --version   # ≥ 22
pnpm --version   # 11.x
```

### 2. 克隆并构建

```bash
git clone https://github.com/nishuzumi/moss.git
cd moss
pnpm install
pnpm build
```

### 3. 先跑离线测试

```bash
pnpm test:offline
```

不访问主网也能验证工具链。完整 `pnpm test` 会打 Monad RPC，但仍不签名、不广播。

## 三、一条命令跑通标准流程

```bash
pnpm --filter @themoss/example-simple-flow wrap
```

示例会：

1. discover `wrap`  
2. load `wmon.wrap`  
3. action 生成 wrap 的 Capability 树（1.5 MON）  
4. simulate 并打印结果  

不需要私钥，也不会上链。

成功时，应看到模拟 **无 halted**、相关结果 **warnings 为空**，并提示：在把未签名交易交给钱包前，**用有序 Receipt 文字与用户意图对齐**。

注意：这表示「可以进入钱包复核」，不是「交易已执行」或「结果已保证」。

可选：

```bash
pnpm --filter @themoss/example-simple-flow swap
```

## 四、读懂输出：四步究竟验证了什么？

### 1. discover：按用户动作找能力

```text
protocol: wmon
method: wrap
verb: wrap
category: token
```

搜的是用户视角 `wrap`，不是合约函数名 `deposit()`。

### 2. load：读取调用契约

- intent：把原生 MON 包装成 WMON  
- risk：含 `fundOut`  
- `amount`：人类可读小数，如 `"1.5"`，不要预换算成 wei  
- 参数类型与字段说明分离（Zod 值契约 + 字段角色描述）

### 3. action：生成 Capability 树，而不是直接发交易

形态概念上：

```json
{
  "kind": "capability",
  "protocol": "wmon",
  "method": "wrap",
  "params": { "amount": "1.5" },
  "children": [
    {
      "kind": "transaction",
      "transaction": {
        "from": "0x…",
        "to": "0x…WMON…",
        "data": "0xd0e30db0",
        "value": "0x…"
      }
    }
  ]
}
```

要点：

- 只有未签名交易  
- 每个 Capability **恰好一笔** direct transaction  
- 更复杂流程用**子 Capability**（例如 approve → swap）嵌套  

### 4. simulate：Changes → Receipt → 覆盖校验

模拟器会：

1. DFS 压平 Capability 树  
2. `debug_traceCall` 回放每笔交易（可链式 state overrides）  
3. 抽出有序 Changes（event / nativeTransfer）  
4. 调用 `wmon.wrap` 注册的 Receipt 解析器  
5. 校验：**每条 Change 都被解释，顺序一致**  

你应关注：

- `reverted` / Warning 码是否为空  
- Receipt 文字是否描述「wrap 1.5 MON → WMON、账户是否正确」  
- MCP 场景下：有序 **leaf texts** 是否与用户原话一致  

**核心不是「模拟成功」四个字，而是：仿真证据被穷尽解析，且语义上对得上用户意图。**  
规则只有一句：**任何 Warning 都必须停止，不能交给签名方。**

## 五、新手最容易踩的 5 个坑

### 坑 1：Node.js 版本过低

需要 Node ≥ 22。装饰器/构建异常先查版本。

### 坑 2：把「无 Warning」当成落链成功

只构建与模拟；没有签名，没有广播。

### 坑 3：RPC 不支持 `debug_traceCall`

模拟依赖 debug 命名空间。默认 `https://rpc.monad.xyz` 通常可用；部分公共 RPC 会屏蔽。

### 坑 4：自己预换算 wei / 用代币符号当身份

金额用人类可读字符串；代币身份只用 **地址或 `native`**，不要靠符号猜地址。

### 坑 5：无 Warning 后跳过意图对齐

无 Warning 只说明 Changes 被完整解析。Agent 仍须对照用户原话：是 wrap 还是 swap？金额与账户对不对？这叫 **intent alignment**。

## 六、把 Moss 接入 AI Agent

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

安全任务示例：

> 使用 Moss 查询在 Monad 上把 1 MON 换成 USDC。必须依次 discover → load → action → simulate；有任何 Warning 立即停止；无 Warning 后仍要把**每一条有序 Receipt 文字**与我的原话对齐。不要签名，不要发送交易。

安全 Agent 清单：

1. 不自己编 calldata；改参数就重新 action  
2. 每个写能力树强制 simulate  
3. 任何 Warning 立即停止  
4. 无 Warning 后仍做 intent alignment  
5. 不索要私钥、不擅自广播  

## 七、跑通以后，如何参与开源？

1. **文档层**：教程、FAQ、排错（注意对齐现行架构）  
2. **测试层**：capability 形状、Receipt 覆盖、live e2e  
3. **协议层**：从 `packages/protocols/_template` 接入新协议  

推荐阅读：

- `packages/system/src/wmon.ts`  
- `packages/core/src/framework.ts`（flatten + coverage）  
- `docs/protocol-onboarding.md`  
- `docs/adr/0010`、`0011`  
- 本地：`experiments/moss/docs/architecture-explained.zh-CN.md`  

先在 Issue 与 Maintainer 对齐范围，再提小而可审查的 PR。

## 写在最后

```text
用户意图
  ↓
discover / load
  ↓
action → Capability 树（未签名）
  ↓
simulate → Changes → Receipt（穷尽覆盖）
  ↓
无 Warning + 意图对齐
  ↓
独立钱包复核与签名
```

Moss 的目标不是让 Agent 更快控制资产，而是让 Agent 只能提交一个**受约束、可解释、可模拟、可叫停的交易提案**。

---

### 参考资料

- Moss：https://github.com/nishuzumi/moss  
- Getting started（中文）：`docs/getting-started.zh-CN.md`  
- MCP tools：`docs/mcp-tools.md`  
- Agent skill：`docs/agent-skill.md`  
- ADR 0011：Capability trees and exhaustive Receipts  
- 勘误索引：[`moss-architecture-errata.md`](./moss-architecture-errata.md)  
- 本地通俗讲解：`experiments/moss/docs/architecture-explained.zh-CN.md`  

作者：Neo｜Dev Builder（Tech）  
修订：2026-07-20  
