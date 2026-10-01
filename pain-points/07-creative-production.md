# 创意生产之痛：算法只优化你给它的东西

**结论**：Search Engine Land 2026 年的判断很直接——限制 PPC 表现的不再是出价，而是创意。PMax、Demand Gen、RSA、YouTube Shorts 全是"素材解锁流量"的逻辑：素材库的广度和质量决定了模型能探索到的空间。成熟账户的 plateau，十有八九是创意产能跟不上，而不是出价没调对。

## 现象

- 账户结构、出价都调到位了，效果涨一段就 plateau；加预算只有 diminishing returns。
- RSA 里 15 个标题写了 5 个就上线，asset strength 常年 "Average"；UAC 里横版视频缺失，竖版只有一条。
- 同一批素材跑三个月，CTR 缓慢下滑、CPM 缓慢上升——没人说得清疲劳阈值在哪。

## 根因

1. **RSA 是唯一的搜索广告格式**：2022 年中起 Expanded Text Ads 不能新建/编辑，RSA 成唯一选项。规格：最多 15 个标题（各 ≤30 字符，CJK 每个字算 2 个）、最多 4 条描述（各 ≤90 字符）。2025 年 2 月 20 日起的新规则：Headline 1 和 Description 1 只是"通常"出现，其余"可能"出现；系统可以只展示单个标题、把标题拼到描述开头、把闲置标题放进以前 sitelink 的位置、甚至从同广告组的另一条 RSA 借行——**每条标题必须能独立成句**，不能依赖上下文。
   来源：https://github.com/automatable-skool/ads-blueprint-day1/blob/HEAD/references/google-ads.md
2. **疲劳是 asset 级的，不是 ad 级的**：一条 RSA 是逐个 asset 疲劳的，看整条广告的 CTR 会掩盖问题；要看 per-asset 的 performance label，把 LOW/POOR 的 asset 换掉。
   来源：https://github.com/logly/mureo/blob/HEAD/skills/ad-fatigue-check/SKILL.md
3. **视频是 PMax / Demand Gen / Shorts 的入场券**：没有视频素材，大量版位根本进不去；Google 推出的 Asset Studio 和 PMax creative experiments 说明官方也在逼广告主补创意课。
   来源：https://searchengineland.com/creative-limiting-ppc-performance-469143
4. **Shared ads 退场**：2025 年 10 月 15 日起 API v22 不再支持新建跨广告组共享广告，2026 年 Q1 全面停止投放；旧共享广告的表现数据**不迁移**到新广告——依赖共享广告做规模化的账户要重建，历史数据清零。
   来源：https://bestmediainfo.com/mediainfo/advertising/google-to-phase-out-shared-ads-in-google-ads-api-by-early-2026-9481092
5. **AI Max 加剧"烂素材的规模化"**：AI Max 把 broad match + Search Partners + 自动创意组装做成一个开关，素材库强则高效、素材库薄则平庸标题被大规模组合投放。
   来源：https://expertbeacon.com/free-google-ads-tools/

## 影响谁

- **小团队最痛**：创意产能是人力密集型，大品牌有 in-house 团队/代理商产线，小广告主靠"一套素材跑一年"。
- **B2B / 高客单**：可用的信任状素材（客户证言、数据）少，RSA 标题容易写成正确的废话。
- **App 广告主**：UAC 对视频（横+竖）、图片多尺寸有硬性数量要求，缺一条都可能限流某个版位。

## 应对思路

1. **数量纪律**：RSA 填满 15 标题 + 4 描述是 baseline 不是进阶；UAC 按官方最低量（5 标题、5 描述、4+ 图片、横竖视频各至少 1 条）起步。
2. **Asset 级管理**：每月看一次 per-asset 表现标签，换掉 LOW/POOR； pinning 只用于必须固定的信息（品牌词、合规披露），别 pin 死所有位置。
3. **疲劳监控**：相邻两周 CTR 趋势 + CPM 漂移双指标；Google 展示/视频侧没有 ad 级 frequency，CTR 趋势是主要信号。
4. **UGC 化**：手机实拍的 raw 素材在 YouTube / Demand Gen 上往往跑赢精修广告片——把客户/用户变成素材供应链。

## 来源

- https://searchengineland.com/creative-limiting-ppc-performance-469143
- https://github.com/automatable-skool/ads-blueprint-day1/blob/HEAD/references/google-ads.md
- https://github.com/logly/mureo/blob/HEAD/skills/ad-fatigue-check/SKILL.md
- https://bestmediainfo.com/mediainfo/advertising/google-to-phase-out-shared-ads-in-google-ads-api-by-early-2026-9481092
- https://expertbeacon.com/free-google-ads-tools/

*置信度：高。*
