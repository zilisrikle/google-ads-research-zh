# 衡量归因之痛：信号越少，账越难算

**结论**：2026 年 Google Ads 的衡量问题不是"工具不够"，而是"看到的数字本身就是估计值"——建模转化混进报表无单独列、归因模型只剩 DDA 和末次点击、iOS 数据延迟且粗糙。先接受"报表是估计"这个前提，再谈优化。

## 现象

- 账户没有任何改动，转化量某天突然跳变 10–20%，查 change history 干干净净——波动来自 consent/modeling 混合比例变化，而非真实效果变化。
- 同一笔转化，Google Ads、GA4、MMP/CRM 三方数字永远对不上，DDA 的小数转化（如 18.33 个转化）没法向老板解释。
- iOS 应用广告：SKAN 回传延迟 24–72 小时以上、聚合、无用户级归因，优化师 фактически 在"开盲盒"调出价。

## 根因

1. **建模转化不可见**：Modeled conversions 直接混进标准报表列，没有独立的"modeled"列。consent 拒绝用户带来的转化由模型估算，比例一变报表就抖。
   来源：https://github.com/sergeyizmailov/knowledge-delta-skills/blob/HEAD/skills/google-ads/references/06-tracking-attribution.md
2. **归因模型被砍到只剩两个**：2023 年 6 月起 first-click / linear / time-decay / position-based 停止新建，2023 年 9 月存量自动迁到 DDA，**2026 年 7 月中旬四种模型彻底下线**，只剩 Data-Driven Attribution（默认）和 Last Click。
   来源：同上
3. **Cookie 与 ITP**：Safari ITP 下 JS 写的第一方 cookie 只有 7 天寿命；server-side GTM 用真第一方域名写 cookie 可延长到 90 天，但 CNAME 到第三方 IP 会被 ITP 视为第三方 cookie 而失效，必须用 A/AAAA 记录指到自己的 IP 段。
   来源：同上
4. **Consent Mode v2**：EEA 地区投放个性化广告/衡量必须部署，拒绝 consent 的流量靠建模回补，建模比例越高，报表与真实的 gap 越大。
5. **iOS 侧**：ATT 下绝大多数用户 opt-out，SKAN postback 聚合、延迟、conversion value 粗糙；iOS 的 SKAN CAC 与 web CAC 口径不可比。
   来源：https://github.com/san-npm/skills-ws/blob/HEAD/skills/customer-acquisition/SKILL.md

## 影响谁

- **效果差异最大的是中小广告主**：大广告主有 MMM + 增量实验 + CRM 对账三件套（2026 年最佳实践就是这三者的三角验证），小广告主只能看平台报表，被建模数字牵着走。
  来源：https://github.com/san-npm/skills-ws/blob/HEAD/skills/customer-acquisition/SKILL.md
- **应用广告主（UAC）**：iOS 归因三方分叉（Google / MMP / SKAN）是方法论差异，强求一致是缘木求鱼。
- **Lead-gen / B2B**：表单转化易被重复/低质污染，Smart Bidding 会追着"量"而非"质"跑。

## 应对思路

1. 把平台转化数当"带误差棒的估计值"，用 CRM/财务口径做月度对账，定一个固定的 reconciliation 节奏。
2. Server-side tagging + Enhanced Conversions / 离线转化导入，把第一方信号喂回去（B2B 必传 closed-won，而不只是表单）。
3. 大预算账户：MMM 做顶层分配、geo 实验校准增量、平台归因只做日常 pacing——三者分工，不混用。
4. iOS：接受 7 天+ 滑动窗口做决策，不用 2–3 天数据调出价；SKAN conversion value schema 按收入/价值分层设计，而非简单映射事件。

## 来源

- https://github.com/sergeyizmailov/knowledge-delta-skills/blob/HEAD/skills/google-ads/references/06-tracking-attribution.md
- https://github.com/san-npm/skills-ws/blob/HEAD/skills/customer-acquisition/SKILL.md
- https://medium.com/@yoann.morand/discuss-set-up-challenge-the-conversion-tracking-common-ground-b541764f200f
- https://ppc.land/google-analytics-drops-three-major-features-that-will-reshape-how-marketers-track-campaigns/

*置信度：高（多源交叉）。具体建模比例数字因账户而异，文中未给绝对值。*
