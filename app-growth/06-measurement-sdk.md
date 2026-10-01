# 衡量 SDK 选型：Firebase vs MMP

## 概述

Google Ads 应用衡量有两类数据源：Firebase SDK（Google 第一方）和 MMP（AppsFlyer、Adjust、Singular 等第三方）。结论先行：**只接 MMP 也能跑 UAC**，但会失去两项关键能力——tROAS 出价和 App 系列受众排除。Firebase 免费且是 Google 出价信号的 baseline；两者可以并行，官方推荐 Firebase 打底、MMP 按需叠加。

## 能力矩阵

| 能力 | Firebase SDK | MMP（AppsFlyer / Adjust / Singular） |
|---|---|---|
| 安装 / 应用内事件归因 | ✓（经 GA4 / Google Ads） | ✓，跨渠道最强 |
| tCPI / tCPA 出价 | ✓ | ✓（in-app event postback 回传） |
| tROAS 出价（收入事件） | ✓ | ✗——AppsFlyer 官方文档明确：tROAS 仅支持 Firebase SDK 收入事件，MMP 收入事件不可用 |
| 受众搭建（ACe 再营销名单） | ✓ 原生受众 | △ 可建（third-party link 支持建 remarketing list），但 App 系列的用户排除仅支持按 Firebase 事件优化的系列 |
| SKAN 管理 | 由 Google 端管理（Google Ads API 提供 CV schema 配置） | ✓（如 AppsFlyer Conversion Studio 管理 CV 映射；SDK 6.14+ 支持 SKAN 4 / AAK） |
| 回传实时性 | 分钟级 | in-app postback 分钟级（中置信度，官方未给精确数字）；SKAN 数据为 Google 每日批量同步，非实时 |
| 跨渠道归因（Meta / TikTok / ASA） | 弱（Google 生态内） | ✓ 最强项 |
| 反作弊 | 弱 | ✓（Protect360 等） |
| 成本 | 免费 | 按归因量收费（AppsFlyer 首年约 12,000 conversions 免费额度，之后按量——第三方来源，中置信度） |

只接 MMP 时的官方限制（AppsFlyer 帮助文档，"Advertising without the Firebase SDK"）：

1. **tROAS 不可用**——tROAS 优化仅支持 Firebase SDK 收入事件。
2. **受众排除不可用**——只有按 Firebase SDK 事件优化的 App 系列才能排除用户。

## 场景选型

- **只投 Google**：Firebase 足够，可选是否叠加 MMP。
- **多渠道投放（Meta / TikTok / ASA）**：MMP 必需，统一跨渠道归因口径。
- **跑 tROAS / 收入优化**：必须接 Firebase，MMP 收入事件不能用于 tROAS 出价。
- **做 ACe 再营销 / 受众排除**：Firebase 优先。
- **强反作弊需求**：MMP。

决策顺序建议：先看是否跑 tROAS（是→Firebase 必接）；再看渠道数量（多渠道→MMP 必接）；最后看预算——MMP 按归因量收费，日安装量小、只投 Google 的团队可以先只接 Firebase，等放量或扩渠道时再叠加 MMP，避免过早付费。

## 并行方案

两者不冲突，可以同时接入。规则只有一条：**同一业务事件只选一个数据源做 Primary**，另一个降为 Secondary 只看报表（防重复计数见 07-conversion-strategy.md）。Google 官方 GA4 迁移文档的标准流程也是：第三方 Primary 降级为 Secondary，GA4 升级为 Primary。

iOS 侧注意：SKAN 转化值（conversion value）只应由一端管理写入，避免 Firebase 端和 MMP 端同时调用 updateConversionValue 导致口径打架。

一个典型组合示例（多渠道投放的贷款 App）：Firebase 接入用于 Google UAC 出价（tCPA）与 ACe 受众排除；AppsFlyer 接入用于 Meta / TikTok / ASA 的跨渠道归因与反作弊。出价事件（如 newApply）在 Google Ads 侧只保留 Firebase 版本为 Primary，AppsFlyer 版本设为 Secondary 做跨渠道对账。这样 Google 出价吃第一方信号，财务核算有 MMP 精确口径，互不干扰。

另外注意 2025 年 11 月起的新标识 odm_info：经由 AppsFlyer SDK / S2S 提供的 iOS 安装与再安装聚合归因标识，用于无设备 ID 场景下的 Google Ads 归因。MMP 侧的标识能力仍在演进，选型时以 AppsFlyer 官方集成的最新文档为准。

## 实操 checklist

- [ ] 确认出价策略是否需要 tROAS——需要则 Firebase 必接
- [ ] 确认是否需要跨渠道归因——需要则 MMP 必接
- [ ] 并行时列出"事件 × 数据源"矩阵，每个出价事件只标一个 Primary
- [ ] iOS 确认 SKAN CV schema 由哪一端管理
- [ ] 检查 MMP 的 Google Ads 集成中 in-app event postback 已开启并映射到出价事件

## 来源

- AppsFlyer 官方：Google Ads 集成与无 Firebase SDK 的限制 — https://support.appsflyer.com/hc/en-us/articles/115002504686-Google-Ads-AdWords-Integration-setup-for-advertisers
- Google Ads 官方：关联第三方应用分析 — https://support.google.com/google-ads/answer/7365001?authuser=19
- Google Ads 官方：用第三方应用分析衡量应用转化 — https://support.google.com/google-ads/answer/7382633
- Google Ads 官方：GA4 迁移 App 系列指南 — https://support.google.com/google-ads/answer/13823094?hl=en&ref_topic=10556935
- Google Developers：受众细分（Firebase / 第三方 SDK 建应用行为名单）— https://developers.google.com/google-ads/api/docs/remarketing/audience-segments/getting-started
- 操作手册（社区）：Firebase baseline + MMP 并行建议 — https://github.com/j-naish/business-agent-skills/blob/HEAD/skills/google-ads-planning/references/app-campaigns.md
