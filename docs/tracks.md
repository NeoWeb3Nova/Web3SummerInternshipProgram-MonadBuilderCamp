# 三条 Builder Track

> 开营仪式确认：本期分为 Tech / Ops / Research 三条主线。Research 是本期新增/强化方向，覆盖产品研究、数据分析、DAO 治理和底层共识研究。

## 如何选择主线

- 想“做出来” → 优先 Tech
- 想“让人知道、参与、增长” → 优先 Ops
- 想“讲清楚、分析清楚、找到真实问题” → 优先 Research
- 精力足够可以跨线学习，但需要选一个主线产出作为最终作品集核心。

---

## Tech Track: 技术与产品实现方向

### 适合谁

- 想成为 Web3 Frontend Engineer、DApp Engineer、Solidity Intern、DevRel Engineer
- 有编程基础，希望学会链上产品开发
- 想用 AI 工具快速完成从合约到前端的 MVP

### 核心技能树

- 钱包连接（MetaMask / WalletConnect / RainbowKit）
- 智能合约开发（Solidity）
- 合约框架（Foundry / Hardhat）
- 前端交互（viem / ethers.js / wagmi）
- 事件监听与索引器基础
- 测试与安全基础
- Monad Testnet 部署和验证
- README 与技术文档写作

### Monad 重点

- EVM 兼容意味着现有以太坊工具链可复用
- 可关注高吞吐链上的实时交互、agent payment、x402、账户抽象等方向
- 不要重复造轮子：钱包、索引器、RPC、预言机、账户抽象 provider 已有生态工具

### 建议学习路径

1. Solidity 基础语法
2. Foundry 环境搭建与测试
3. 在 Monad Testnet 部署合约
4. 用 Vite + React + wagmi / viem 搭建前端
5. 连接钱包并读取/写入合约
6. 记录合约地址、交易哈希、部署脚本
7. 写测试、写 README、写技术复盘

### 代表产出

- 可运行的 DApp Demo
- 合约地址与部署脚本
- GitHub Repo
- 部署文档
- 技术复盘
- 失败/调试记录

---

## Ops Track: 运营、增长与生态协作方向

### 适合谁

- 想进入 Community、Growth、Marketing、Event Ops、BD、Ecosystem 方向
- 对人和传播敏感，喜欢组织活动与内容
- 想通过内容、社群、活动帮助一个 Web3 项目获得真实用户反馈

### 核心技能树

- 生态调研与用户观察
- Meme / 内容 Campaign 设计
- 活动 SOP 编写
- 社区反馈机制
- 增长数据记录
- Demo Day 执行
- 项目叙事和用户教育

### Monad 重点

- 用“为什么高吞吐链重要”做用户教育
- 做 Monad 新人 onboarding 内容
- 观察开发者卡点：钱包、RPC、水龙头、部署、验证、索引器
- 把技术概念翻译成普通用户能理解的内容

### 建议实践路径

1. 选择 Monad 生态中的 3-5 个项目进行桌面研究
2. 加入相关社区，观察用户讨论与痛点
3. 设计一个 Meme / 内容 / 活动 Campaign
4. 执行最小版本并收集反馈
5. 记录数据与增长复盘
6. 把活动/内容沉淀成 SOP

### 代表产出

- Campaign 方案
- 传播数据截图
- 活动 SOP
- 用户反馈表
- 社区增长复盘
- Demo Day 执行记录

---

## Research Track: 研究、分析与叙事方向

### 适合谁

- 想成为 Ecosystem Researcher、Protocol Research Intern、Product Researcher、Technical Writer
- 喜欢阅读、分析、写作和讲故事
- 想把复杂技术讲清楚，或从用户/产品角度分析 Web3 项目

### 核心技能树

- 架构解释：把复杂协议讲清楚
- 生态地图绘制
- 项目分析框架
- DAO 治理研究
- 产品研究与需求分析
- 数据分析策略
- 区块链共识与底层研究
- 研究写作和公开表达

### Monad 重点

可选研究题：

- 为什么需要高吞吐区块链
- Monad vs Ethereum：执行与共识模型差异
- Monad vs Solana：性能、去中心化、EVM 兼容与开发者迁移成本
- 流水线化共识与执行如何提升吞吐
- 乐观并行执行如何处理状态冲突
- MonadDB 与状态访问性能瓶颈
- MonadBFT / RaptorCast / 区块传播机制
- x402 / agent payment 与 Monad 应用场景

### 建议研究路径

1. 阅读 `docs/monad-technical-notes.md`
2. 阅读 Monad 官方文档和 Box 分享对应主题
3. 建立自己的分析框架：技术 / 产品 / 生态 / 治理 / 数据
4. 选择 1 个核心问题深入研究
5. 写一篇 1000-2000 字研究文章或生态地图
6. 转换成公开展示材料或 Demo Day 叙事

### 代表产出

- 研究文章
- Product Thesis
- 项目分析
- 生态地图
- 技术图解
- 公开演讲/展示材料
