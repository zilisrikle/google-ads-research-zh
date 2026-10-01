# google-ads-research-zh

Google Ads 中文研究知识库。定位：**给应用增长（app-growth）团队用的实操型中文知识库**——以 UAC / 应用获客为加重主线，覆盖账户结构、衡量、出价、测试、诊断、放量的完整工作流。

目标读者：独立负责 Google Ads 应用获客的优化师、增长负责人，以及需要快速理解 Google Ads 机制的团队成员。不适合纯品牌广告或线下零售场景（本仓库不覆盖）。

## 目录导览

```
google-ads-research-zh/
├── README.md                  本页
├── pain-points/               痛点篇：8 大痛点 + 总览
│   ├── 01-measurement-attribution.md   衡量归因：信号越少，账越难算
│   ├── 02-blackbox-pmax-uac.md        PMax/UAC 黑盒：钱花在哪，Google 说了算
│   ├── 03-policy-finance-compliance.md 政策合规：封号、验证、申诉
│   ├── 04-cost-inflation.md           成本上涨：CPC 通胀的四个压力
│   ├── 05-learning-scaling.md         学习期与放量：乱动模型的代价
│   ├── 06-mcc-management.md           MCC 管理：账号一多，治理比投放难
│   ├── 07-creative-production.md      创意生产：算法只优化你给它的东西
│   ├── 08-trends-2026.md              2026 新兴变量：AI 搜索与自动化
│   └── MASTER-PAIN-POINTS.md          8 大痛点总览
├── workflow-mapping/          工作流篇（精简 8 篇 + 总览）
│   ├── 01-account-setup-mcc.md        开户与账户结构：MCC 规划、子账号切分、系列架构
│   ├── 02-measurement-setup.md        衡量搭建 SOP：SDK、转化导入、Primary/Secondary
│   ├── 03-uac-launch-sop.md           UAC 上线 SOP：建系列到过学习期的标准动作
│   ├── 04-budget-bidding.md           预算与出价：tCPI/tCPA/tROAS 选择与调价纪律
│   ├── 05-testing-framework.md        测试框架：实验设计、变量隔离、复盘
│   ├── 06-daily-optimization.md       日常优化：每日/每周看什么、不动什么
│   ├── 07-reporting-diagnosis.md      报告与诊断：归因口径、衰退诊断流程
│   ├── 08-scaling.md                  放量：放量信号、预算阶梯、边际成本
│   └── MASTER-WORKFLOW-MAP.md         全流程总览：八段流水线与阶段依赖
├── app-growth/                应用增长专区（加重）：UAC 完全指南、iOS/Android 双轨、衡量归因、MCC 跨账号、ACe 再营销、反作弊
└── extras/                    速查
    ├── uac-creative-specs.md          UAC 素材规格：文字/图片/视频/HTML5 官方规格
    └── finance-compliance-checklist.md 金融（借贷）合规清单：验证流程、产品红线、文案禁区
```

## 四部分关系

- **workflow-mapping** 是主线：按投放生命周期的真实顺序组织（01→08），每一篇的输出是下一篇的输入。先读 `MASTER-WORKFLOW-MAP.md` 建立全景，再按需深入
- **app-growth** 是加深：把 workflow 里与应用获客相关的部分（UAC、iOS 归因、MCC 跨账号）展开成专题
- **extras** 是工具：上线前对照检查的速查表，不负责讲"为什么"，只给"是什么、多少"
- **pain-points** 是反面教材：记录真实踩坑案例，与 workflow 的"正确做法"对照阅读

阅读顺序建议（app-growth 视角）：`MASTER-WORKFLOW-MAP.md` → 02（衡量）→ 03（上线）→ 04（出价）→ 07（诊断）→ 08（放量）→ extras 两篇。

## 研究方法

- 以 **Google Ads 官方帮助文档与广告政策页**为第一来源；规格数字、政策条款必须来自官方并标注查阅日期
- 官方未覆盖的实操经验（如调价纪律、诊断顺序）标注为"从业者共识"，与官方规则区分
- 不确定的内容标注置信度（高/中/待确认），绝不编造

## 置信度标注说明

- **高置信度**：可直接追溯到 Google 官方文档原文，文内附来源链接
- **中置信度**：来自可信第三方整理或从业者共识，官方未明确表态；可作为工作假设，关键决策前请二次确认
- **待确认**：公开资料中找不到明确说法，已在文中标出，请以账户内实际状态或官方实时文档为准

## 时效声明

Google Ads 功能与政策更新频繁。本仓库所有"官方数字"（预算倍数、素材规格、验证流程、政策条款）均以各篇标注的**来源链接 + 查阅日期**为准。执行任何涉及政策与规格的动作前，请复核 Google 官方实时文档。本仓库内容不替代官方政策，不构成法律建议。

## LICENSE 提示

本仓库为研究整理内容，仅供学习交流。引用的 Google 官方文档版权归 Google 所有；原创整理部分如需转载或商用请联系仓库维护者。
