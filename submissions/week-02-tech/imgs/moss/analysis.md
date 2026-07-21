# Moss 公众号文章配图分析

## 内容类型

技术深度分析 × 开源实践。文章不是产品宣传，而是解释 Moss 如何把 Agent 链上执行从概率推理推进到签名前的确定性验证。

## 配图目的

- 把抽象安全边界转成一眼可读的系统关系。
- 解释直接工具调用与可验证 Plan 的区别。
- 把双 tracer、状态继承和 effects 对账机制可视化。
- 明确模拟能证明什么、不能承诺什么。

## 核心论点

1. Moss 位于 Agent 与 Wallet 之间，负责构建、模拟和叫停，但不签名。
2. 调用不回滚不等于符合用户意图；`expects` 提供可量化边界。
3. `callTracer` 与 `prestateTracer` 共同恢复真实 effects，并支持多步状态继承。
4. 零 warning 只表示模拟时点未越界，不是未来执行或收益保证。

## 视觉策略

- 密度：balanced，共 4 张。
- 类型：framework、comparison、flowchart、comparison。
- 风格：blueprint editorial，延续封面的高能科技感，但正文插图降低噪声、强化结构。
- 配色：石墨黑背景；青蓝表示验证与安全；红色表示风险；黄色表示 warning；白色表示中性信息。
- 文字：只使用文章中的英文术语，避免长段中文和模型乱码。
- 比例：16:9 landscape。
