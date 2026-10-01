# PMax / UAC 黑盒之痛：钱花在哪，Google 说了算

**结论**：PMax 的黑盒是设计使然，不是 bug。2026 年透明度有所改善（渠道报告、搜索词报告、否定词），但预算在渠道间的分配逻辑、转化的增量真实性依然不可见。痛点的核心从"看不见"变成了"看见了但控制不了"。

## 现象

- 上了 PMax 之后，品牌搜索系列的 impression share 莫名下跌，PMax 的 ROAS 却"很好看"——钱从品牌词搬到了 PMax，报表上叫增长，实际可能是左手倒右手。
- PMax 消耗占账户 60%+，但说不清多少花在 Search / YouTube / Display / Discover 上，也控制不了比例。
- 搜索词报告里出现大量与业务无关的 query，加了否定词，下周又冒出新的。

## 根因

1. **优先级规则决定"谁抢谁的量"**：官方规则下，只有**与搜索词完全一致的 exact-match 关键词**能稳赢 PMax；PMax 的 search theme 能压过非完全一致的 phrase-match；再往下由 AI relevance 和 Ad Rank 决定。Shopping 例外，可与 Search 并存。——"PMax 偷品牌流量"的完整机制就是：你的品牌系列跑的是 phrase/broad 而非收紧的 exact。
   来源：https://github.com/sergeyizmailov/knowledge-delta-skills/blob/HEAD/skills/google-ads/references/07-pmax-demand-gen-audiences.md
2. **收割品牌需求而非创造增量**：Optmyzr 对 24,702 个系列的研究发现，51% 的广告主把 50%+ 预算放进 PMax，这些账户呈现 652% 的 ROAS 标题数字，但底层的 CVR/CPA 参差——符合"PMax 在收割易得的品牌转化，而非带来增量"的解释。
   来源：同上
3. **渠道分配不可控**：2026 年渠道报告已可看到各渠道的展示/点击/花费/转化（Search、Display、YouTube、Discover、Gmail、Maps、Search partners 也已拆分，parked domains 被移除，还新增了 Invalid Activity Credit Report），但**不能设定各渠道的预算占比**，分配仍由 Google 自动决定；报表也回答不了"每个转化是否真正增量"。
   来源：https://www.trafficguard.ai/blog/two-years-of-performance-max-how-black-box-marketing-technology-is-holding-the-industry-back
4. **搜索词可见性收缩是全平台趋势**：PMax 搜索词报告虽已开放，但颗粒度仍不如传统搜索系列；搭配 AI Max for Search（2025 年 9 月全球 beta）把 broad match + Search Partners + 自动创意组装做成一个开关，匹配更智能、也更不透明。

## 影响谁

- **有品牌词资产的广告主最痛**：品牌系列被掏空还说不清，SEO 也可能被 PMax 的付费展示挤压（同个 SERP 上付费和自然同时出现）。
- **中小预算账户**：PMax 有隐形门槛（建议 $50–100/天起，日预算 ≥ 3 倍 tCPA；月预算 $1K 以下更适合专注的搜索系列），预算太小模型学不动，黑盒里亏得无声无息。
  来源：https://github.com/narayan-metaflow/metaflow-marketing-skills/blob/HEAD/skills/google-ads-campaign-builder/SKILL.md

## 应对思路

1. **品牌词隔离**：品牌系列用收紧的 exact-match 守住品牌词；PMax 上开 brand exclusion，做前后对比时看**账户整体**花费/转化，而非 PMax 单独的 ROAS。
2. **否定词体系**：PMax 支持系列级和账户级否定词（作用于 Search 和 Shopping 库存，不作用于 Display/Video），用搜索词报告持续喂否定词。
   来源：https://www.trafficguard.ai/blog/two-years-of-performance-max-how-black-box-marketing-technology-is-holding-the-industry-back
3. **诊断顺序**：先看 PMax 占账户花费比、品牌系列 IS 变化（跌 10–15 个点即红灯）、PMax CPA 与搜索 CPA 的偏离（健康状态下通常在 ±30% 内），再动结构。
   来源：https://github.com/kaycomminc/kaycomm-mcp/blob/HEAD/skills/pmax-anomaly-detector/SKILL.md
4. **UAC 同理**：App campaigns 同样是黑盒，素材（标题/描述/图片/视频）是唯一能控制的输入，素材库的广度和质量直接决定模型能探索到的流量。

## 来源

- https://www.trafficguard.ai/blog/two-years-of-performance-max-how-black-box-marketing-technology-is-holding-the-industry-back
- https://github.com/sergeyizmailov/knowledge-delta-skills/blob/HEAD/skills/google-ads/references/07-pmax-demand-gen-audiences.md
- https://github.com/kaycomminc/kaycomm-mcp/blob/HEAD/skills/pmax-anomaly-detector/SKILL.md
- https://www.allmarketing.com.au/blog/performance-max-google-ads-perth-business/
- https://searchengineland.com/prevent-ppc-cannibalizing-seo-efforts-451920

*置信度：高。注意：曾有一篇 2026 年文章声称 PMax 占行业花费 22%→38% 且 31/47 审计账户出现品牌 IS 压制，经核查无法证实、疑为 AI 生成的 SEO 内容，本篇未采用。*
