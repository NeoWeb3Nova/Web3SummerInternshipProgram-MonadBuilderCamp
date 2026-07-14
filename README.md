# Web3 暑期实习计划 - Monad Builder Camp

> 21 天做出你的第一个链上产品。第 4 周参与 Hackathon，第 5 周整理成作品集。

- **项目目录**: `/home/neo/workspace/projects/Web3SummerInternshipProgram-MonadBuilderCamp`
- **来源**: [Web3 暑期实习计划报名开启：21 天做出你的第一个链上产品](https://x.com/LXDAO_Official/status/2066328174963933518)
- **项目介绍**: https://web3career.build/zh/programs/Web3-Summer-Intership-Progra?tab=overview
- **学习面板**: https://web3career.build/zh/programs/Web3-Summer-Intership-Progra?tab=learning（登录后查看每周/每日任务列表）
- **开营仪式**: 2026-07-05 (周日) 19:00 UTC+8
- **活动时间**: 2026/06/15 起报名，周期约 5 周
- **费用**: 免费
- **开营仪式笔记**: `docs/opening-ceremony.md`
- **开营仪式完整转录**: `docs/opening-ceremony-transcript.md`
- **DevRel 成长之路笔记**: `docs/devrel-growth.md`
- **DevRel 成长之路完整转录**: `docs/devrel-growth-transcript.md`
- **Monad 技术笔记**: `docs/monad-technical-notes.md`
- **Web3Career 平台入口记录**: `docs/web3career-platform.md`
- **LXDAO × GoPlus AI Agent 安全分享笔记**: `docs/ai-agent-security-lxdao.md`
- **AgentGuard 实现概览**: `docs/agentguard-implementation-overview.md`
- **Web3 技术分享：如何从 0 到 1 使用 AI 开发笔记**: `docs/ai-dev-zero-to-one-notes.md`
- **Web3 技术分享：如何从 0 到 1 使用 AI 开发完整转录**: `docs/ai-dev-zero-to-one-transcript.md`
- **LXDAO × GoPlus AI Agent 安全分享完整转录**: `docs/ai-agent-security-lxdao-transcript.md`
- **修复后视频**: `D:/WindowsDownload/Video/Web3实习计划开营式 - X.repaired.mp4`

---

## 三个关键词

- **系统学习**: 解决 Web3 信息碎片化，用 5 周路径把概念、链上体验、项目实践串起来。
- **Learn by Building**: 从第一笔交易、第一份合约、Mini Demo 到 Hackathon，不等“学完”再实践。
- **AI-native Builder**: 把 AI 当作学习和开发伙伴，但记录「AI 帮了什么，人做了什么判断」。
- **Career Evidence**: 让每次学习都沉淀为可展示、可验证、可复用的成果。

## 每日节奏

- **19:00**: 嘉宾分享 / 行业一线经验
- **20:00**: Co-learning / 助教答疑
- **工作日**: 每日打卡并提交学习记录
- **周末**: 休息、补档、复盘

## 三条 Builder Track

| Track | 方向 | 代表交付物 |
|-------|------|-----------|
| Tech | 技术与产品实现 | Demo、合约地址、GitHub Repo、部署文档、技术复盘 |
| Ops | 运营、增长与生态协作 | Campaign、传播数据、活动 SOP、增长复盘、Demo Day 执行记录 |
| Research | 研究、分析与叙事 | 研究文章、Product Thesis、项目分析、公开展示材料 |

## 计划节奏

| 周次 | 主题 | 关键动作 |
|------|------|----------|
| Week 1 | 进入 Onchain World | 钱包、网络配置、第一次交易、第一次 Monad 合约部署 |
| Week 2 | 选择 Builder Track | 分轨任务：Tech / Ops / Research |
| Week 3 | 跨轨协作与 Mini Demo | 跨轨小组把想法推进成 prototype |
| Week 4 | Monad Builder Hackathon | 提交可运行产品、Repo、Pitch Deck、Demo Video、Final Presentation |
| Week 5 | Resume & Portfolio Workshop | 作品集、简历 bullet、README、面试表达、后续机会连接 |

## 目录结构

```
.
├── README.md              # 本文件：项目总览
├── docs/                  # 项目文档、计划、笔记
│   ├── overview.md        # 活动基本信息与关键链接
│   ├── opening-ceremony.md # 开营仪式纪要（完整修复后字幕整理）
│   ├── opening-ceremony-transcript.md # 开营仪式完整转录
│   ├── devrel-growth.md # DevRel 成长之路分享会纪要
│   ├── devrel-growth-transcript.md # DevRel 成长之路分享会完整转录
│   ├── monad-technical-notes.md # Monad 技术学习笔记（基于 Box 分享）
│   ├── web3career-platform.md # Web3Career 概览页与学习面板入口记录
| │   ├── ai-agent-security-lxdao.md # LXDAO × GoPlus AI Agent 安全分享笔记
| │   ├── agentguard-implementation-overview.md # AgentGuard 实现概览
| │   ├── ai-dev-zero-to-one-notes.md # Web3 技术分享：如何从 0 到 1 使用 AI 开发笔记
| │   ├── ai-dev-zero-to-one-transcript.md # Web3 技术分享：如何从 0 到 1 使用 AI 开发完整转录
| │   ├── ai-agent-security-lxdao-transcript.md # LXDAO × GoPlus AI Agent 安全分享完整转录
| │   ├── schedule.md        # 5 周节奏
│   ├── tracks.md          # 三条赛道说明
│   └── deliverables.md    # 交付物标准
...
│   ├── week-01.md
│   ├── week-02-tech.md
│   ├── week-02-ops.md
│   ├── week-02-research.md
│   ├── week-03.md
│   ├── week-04-hackathon.md
│   └── week-05-portfolio.md
├── daily/                 # 每日打卡与学习日志
│   └── YYYY-MM-DD.md      # 每日记录模板
├── submissions/           # 每周/阶段提交物
│   ├── week-01/
│   ├── week-02-tech/
│   ├── week-02-ops/
│   ├── week-02-research/
│   ├── week-03/
│   ├── week-04-hackathon/
│   └── week-05-portfolio/
├── experiments/           # 代码实验、PoC、脚本
│   ├── monad-wallet-setup/
│   ├── first-contract-deploy/
│   ├── week-02-contract/
│   ├── week-02-frontend/
│   └── week-03-prototype/
├── assets/                # 图片、截图、参考材料
└── scripts/               # 自动化脚本
```

## 快速入口

- [活动官网与报名](https://x.com/LXDAO_Official/status/2066328174963933518)
- [Web3Career 学习面板](https://web3career.build/zh/programs/Web3-Summer-Intership-Progra?tab=learning)
- [Monad 官方文档](https://docs.monad.xyz/)

## 贡献与记录原则

- 每日学习记录提交到 `daily/YYYY-MM-DD.md`。
- 每周交付物提交到 `submissions/week-<N>/`。
- 代码实验和 PoC 放到 `experiments/`。
- 关键分享会笔记和完整转录放到 `docs/`。
- 每次重大更新后及时 `git commit` 并 `git push`。

---

有任何问题或建议，欢迎在本仓库提 Issue 或直接修改提交。
