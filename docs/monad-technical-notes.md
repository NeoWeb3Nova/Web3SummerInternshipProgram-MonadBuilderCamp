# Monad 技术学习笔记（来自开营仪式 Box 分享）

## 来源

- 会议：Web3 暑期实习计划开营仪式
- 分享人：Box / Monad Foundation 中国区 DevRel
- 关联文档：`docs/opening-ceremony.md`、`docs/opening-ceremony-transcript.md`

---

## 1. 为什么需要高吞吐区块链

Box 的核心判断：未来链上应用的瓶颈不是“有没有新应用”，而是底层基础设施能否承载爆发式使用。

历史上每次链上热点都会带来交易量冲击：

- DeFi Summer
- NFT 热潮
- Meme coin / 高频链上活动
- BTC 铭文
- 高频支付、AI agent、链上计算等未来场景

类比：早期建设六车道时看似浪费，但城市发展起来后，六车道反而不够用。区块链也是如此，基础设施要为未来应用爆发预留吞吐空间。

---

## 2. Monad 的定位

Monad 试图在三件事之间取得平衡：

1. 高性能
2. 去中心化
3. EVM 完全兼容

它不是通过牺牲验证者数量或提高节点硬件门槛来换性能，而是希望通过软件架构优化抬高链的性能上限。

会议中提到的关键数据：

| 指标 | 数值 / 描述 |
|------|-------------|
| Gas throughput | 500M gas/s |
| Block time | 0.4 秒 |
| Sustained TPS | 10,000 |
| Validators | 约 200 个 |
| EVM 兼容 | MetaMask、Foundry、Hardhat、RPC、DeFi 应用低成本迁移 |
| 节点理念 | 尽量让普通消费级设备也能运行，而不是依赖超级服务器 |

---

## 3. 架构创新

### 3.1 流水线化共识与执行

传统链常见模式：

```text
执行 -> 共识 -> 执行 -> 共识 -> 执行 -> 共识
```

Monad 的目标：把共识和执行并行起来。

```text
共识 n+2 区块时，同时执行 n+1 区块
```

关键点：

- 共识阶段只负责交易排序和打包
- 共识阶段不计算交易是否成功、状态变化、gas 消耗等执行结果
- 执行阶段再计算交易的真实状态变更
- 好处是减少等待，让系统同时利用共识和执行资源

### 3.2 多线程乐观并行执行

Monad 乐观假设：多数交易之间没有状态冲突。

流程：

1. 多笔交易从同一状态快照开始并行执行
2. 执行后按交易顺序校验状态读写
3. 如果发现冲突，只重执行相关交易
4. 如果没有冲突，就直接提交结果

直觉类比：高速公路多车道。大多数车在不同车道并行前进；只有发生并线冲突时，才局部调整。

收益：即使少量交易需要重执行，也通常比所有交易串行执行更快。

### 3.3 MonadDB 状态访问

状态访问是链性能瓶颈之一。以太坊早期数据库设计难以充分利用现代 SSD 并发读写能力。

MonadDB 的目标：

- 针对 SSD 架构优化状态读写
- 支持更高效的并发访问
- 减少执行阶段等待状态读取的时间

---

## 4. 共识层创新

会议中提到的方向：

- MonadBFT
- RaptorCast / 高效区块传播
- 延迟 / GIL 相关优化

Research Track 可进一步研究：

- MonadBFT 和传统 BFT 共识的差异
- RaptorCast 如何降低区块传播成本
- Monad 如何在 0.4 秒出块下维持全球节点通信
- 去中心化程度、节点硬件门槛、性能之间的权衡

---

## 5. 开发者工具链

Monad 对 EVM 生态兼容，意味着已有以太坊工具可以继续使用：

- MetaMask
- Foundry
- Hardhat
- Ethers.js
- Viem
- Wagmi
- RPC / Block Explorer
- 既有 DeFi 合约和前端模式

会议中还提到 Monad 相关 AI skill / 文档，可用于：

- 水龙头
- 合约开发建议
- 部署方式
- 合约验证
- 前端部署
- 索引器部署

---

## 6. 可作为个人项目的切入点

### Tech 方向

- 简单 EVM DApp 迁移到 Monad Testnet
- 多交易并发体验 demo
- Agent payment / x402 概念 demo
- 本地 fork Monad 主网做协议联调实验

### Research 方向

- Monad vs Ethereum 执行模型对比
- Monad vs Solana：性能、去中心化、开发者迁移成本
- MonadBFT / RaptorCast 机制解释
- Monad 生态地图与工具链分析

### Ops 方向

- Monad 新人开发者 onboarding 内容
- Monad 技术概念图解 campaign
- “为什么高吞吐链重要”内容传播实验
- Hackathon 参赛者工具包整理

---

## 7. 下一步学习清单

- [ ] 阅读 Monad 官方文档
- [ ] 配置 Monad Testnet 钱包和 RPC
- [ ] 完成一笔链上交易
- [ ] 用 Foundry 部署 HelloWorld 合约
- [ ] 写一篇 500-1000 字解释：为什么 Monad 需要高吞吐
- [ ] 梳理一个 Monad 生态项目或工具
- [ ] 选择一个可在 Week 3/4 做成 demo 的方向
