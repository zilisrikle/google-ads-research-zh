# ASA 协同：与 Google UAC 的分工与归因去重

> 查阅时效：2026-10-01。ASA = Apple Search Ads（现官方称 Apple Ads）。本文基于 Apple 官方归因机制与社区实操共识，部分细节标注置信度。

## 概述

ASA 和 Google UAC 是 iOS 获客的**一收一放**组合：ASA 收割 App Store 搜索的高意图流量，UAC 在 Google 全网填量、做探索。两者最大的协同坑不在预算分配，而在**归因去重**——iOS 上同一安装可能同时出现在 ASA 后台、Google Ads 后台和 MMP 里，三方数字天然打架。

## 核心内容

### 1. 分工模型

| 维度 | ASA（Apple Search Ads） | Google UAC |
|---|---|---|
| 流量池 | App Store 搜索结果（Today 标签页、搜索标签页、产品页等版位） | Google 搜索、Play、YouTube、AdMob 等 Google 全网 |
| 定向逻辑 | **关键词定向**：用户主动搜"贷款""借钱"等词，意图明确 | 系统自动找量：给素材+出价，算法探索全网流量 |
| 角色 | **收割**：品牌词、品类词、竞品词，高 CVR、高意图 | **填量+探索**：规模、冷启动、触达 ASA 覆盖不到的人群 |
| 出价 | CPT（按点击）/ CPM，2026 年新增 Maximize Conversions（AI 自动出价） | tCPI / tCPA / tROAS |
| 创意 | 产品页截图/视频（CPP 可定制，最多 70 个，Creative Sets 已下线） | 素材资源（标题/描述/图片/视频/HTML5） |

经验法则：ASA 的 CPT 通常高于 UAC 的 CPI，但**首单转化率高**——因为搜索意图自带筛选。两者不是替代关系，是漏斗的上下游。

### 2. 预算分配逻辑

- **ASA 优先吃满高意图词**：品牌词必守（防竞品截流），品类词按 CPT/转化成本卡线
- **UAC 承担规模任务**：ASA 的量有天花板（取决于 App Store 该品类搜索量），增量靠 UAC
- **动态再平衡**：每周对比两渠道的**MMP 口径**边际转化成本，向便宜的一侧倾斜，而非按固定比例

### 3. 归因去重：iOS 的三条归因路径

这是本篇最重要的部分。自 2025-04-10 起，Apple Search Ads 接入 AdAttributionKit，形成**双归因**：

1. **AdServices API**：Apple 自有的 token 归因通道，一直存在，提供更丰富的优化信息
2. **AdAttributionKit（SKAN 1–3）**：隐私归因回传，与第三方渠道统一口径
3. **MMP 去重**：MMP 会对重叠的 Apple Ads 路径做去重，**不要指望每条安装都有一对 "AAK + AdServices" 记录**

实操规则：

- **MMP 是唯一真相源**：MMP（如 AppsFlyer）内的 ASA 渠道数据是去重后的，**永远不要把 ASA 后台安装数 + Google Ads 后台安装数直接相加**——会重复计算
- **三方数字分叉是正常的**：ASA 后台（AdServices 口径）、Google Ads（SKAN/建模口径）、MMP（去重+ATT 归因口径）方法论不同，数字必然不一致。对齐趋势和量级，不追求完全一致
- **归因窗口**：Apple Ads 默认 30 天点击、1 天展示归因（社区资料，置信度中）；WWDC 2025 新增可配置归因窗口与重叠再营销窗口（iOS 18.4+，需 Info.plist 配置）

### 4. 已知限制（2026）

- **Maximize Conversions 出价（2026-02 全量）目前只优化安装**，不优化安装后事件——跑 ASA 想优化深层事件仍需传统 CPT/CPA 手动出价（社区审计框架，置信度中）
- **ATT 授权率**直接影响 MMP 侧 ASA 数据的颗粒度；授权率低时更依赖 SKAN/AAK 回传

## 实操 checklist

- [ ] MMP 中 ASA 已配置为合作伙伴，AdServices.framework 已接入
- [ ] 确认 MMP 的 ASA 数据为去重后数据；报表以 MMP 口径为准
- [ ] 品牌词系列独立建，防竞品截流
- [ ] 每周用 MMP 口径对比 ASA vs UAC 边际成本，动态调预算
- [ ] ATT 弹窗时机/文案优化（影响 ASA 数据质量）
- [ ] iOS 18.4+ 评估是否启用可配置归因窗口（WWDC25 新能力）

## 来源

- Apple Search Ads 接入 AdAttributionKit（2025-04-10）：https://ppc.land/apple-search-ads-to-adopt-adattributionkit-for-unified-app-attribution/
- AdAttributionKit 与 SKAN 归因路径、MMP 去重（社区技术文档，置信度中高）：https://github.com/rylaa/ios-marketing-att-skill/blob/HEAD/references/adattributionkit-and-skan.md
- Apple Ads 审计框架：Maximize Conversions 限制、CPP 上限（社区，2026，置信度中）：https://github.com/rylaa/ios-marketing-att-skill/blob/HEAD/references/apple-ads-audit.md
- ASA 审计 skill（含 MMP 集成检查表）：https://github.com/muhammaddadu/ai-skill-collection/blob/HEAD/growth/ads-apple/SKILL.md
