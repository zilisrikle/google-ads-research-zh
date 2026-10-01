# 归因口径对齐：Google Ads / MMP / SKAN 为什么打架

## 概述

同一天的安装数，Google Ads、MMP、SKAN 三方永远对不上。这是方法论差异，不是 bug。结论先行：**不要试图让三方数字相等**，而是理解每个差异因子的方向，决策时按场景选口径——日常出价看 Google 建模转化，跨渠道分预算看 SKAN，财务核算看 MMP / 自有 BI。

## 差异因子表

| # | 因子 | Google Ads | MMP（以 AppsFlyer 为例） | SKAN |
|---|---|---|---|---|
| 1 | 统计时间锚点 | 按**点击日期**记转化 | 按**转化事件日期**记 | 按回传到达 / 解码日期 |
| 2 | 归因窗口 | install 默认点击后 30 天；in-app 默认 90 天 | 各家默认不同，需手动对齐 lookback | 点击 30 天 / 展示 24h（Apple 固定） |
| 3 | 延迟 | 建模转化最长 5 天稳定 | postback 分钟级 | 首窗口回传 24–48h 随机延迟；二三窗口 24–144h |
| 4 | 隐私阈值 | 建模补足 | 精确事件级（ATT 授权用户） | crowd anonymity 未达标（tier 0）则无转化值、无二三窗口 |
| 5 | 重装定义 | 可配置 | 可配置 | Apple 固定定义，不可配置 |
| 6 | 点击时间认定 | 用广告 serving 信号定 last click | 把 click time 视为 install time | — |
| 7 | 转化值精度 | 精确 | 精确 | 只有 64 个值（0–63）+ coarse 三档 |
| 8 | 展示归因 | 建模转化不含 VTC | 含（按配置） | 含 VTC |
| 9 | 归因模型 | 默认 DDA | 多为 last click / 可配 | Apple 规则 |

几个最容易踩坑的细节：

- **时间锚点错位是最大头的"差异"**：Google 把转化记在点击那天，MMP 记在转化发生那天。正确对比方法是：取 Google 某点击日期区间的转化，对比 MMP 归因到同一点击日期区间的转化（把 MMP 的转化日期窗口向后延长覆盖 Google 的转化窗口），而不是直接对比"今天"的数字。
- **SKAN 互通的时间错位**：Google 把收到的 SKAN 回传共享给 AppsFlyer 时，用自家 serving 信号判定 last click，而 AppsFlyer 把 click time 当作 install time。AppsFlyer 每天 01:00 UTC 从 Google 拉取前 45 天数据，聚合报表会追溯更新，raw data 不追溯——同一份 SKAN 数据在两边日期分布不同。
- **iOS 三框架分工**（Google 官方）：SKAN 适合长期跨渠道预算规划（约 30 天看一次）；conversion modeling 适合日常优化（颗粒度细、覆盖 SKAN 拿不到的数据）；ICM（Integrated Conversion Measurement，基于 on-device measurement）是 Google 正在推的新框架，未来 iOS 衡量会从建模转化转向 ground truth 归因。
- **MCC 跨账号转化**会覆盖子账号归因设置：开了 manager 级跨账号转化跟踪后，报表要在 manager 层看，子账号层的归因设置不再生效。

## 决策时以哪个为准

| 场景 | 准星 | 为什么 |
|---|---|---|
| 日常出价 / 调预算 | Google Ads 建模转化 | Smart Bidding 吃的就是这个口径，用别的口径调等于和算法对着干 |
| 跨渠道预算分配 | SKAN（~30 天看一次） | 唯一跨 ad network 可比的口径 |
| 财务 ROI 核算 | MMP / 自有 BI | 精确事件级，可对账 |
| 排查追踪故障 | 分开看，不对比 | 先确认事件有没有进各系统，再谈数字 |

## 实操 checklist

- [ ] 对比 Google vs MMP 时，先统一到"点击日期"锚点再比
- [ ] 确认 MMP 的 lookback 窗口与 Google 转化窗口对齐
- [ ] iOS 日常优化看建模转化，不拿 SKAN 日数据调出价
- [ ] SKAN 报表每月看一次，用于跨渠道预算决策
- [ ] 开了 MCC 跨账号转化的账户，归因相关报表在 manager 层看
- [ ] 任何情况下不把三方数字加总

## 来源

- Google Developers：应用转化归因差异排查（时间锚点、窗口对齐）— https://developers.google.com/app-conversion-tracking/api/discrepancies
- Google Ads 官方：iOS App 系列衡量与报告（三框架对比、lookback 窗口）— https://support.google.com/google-ads/answer/16771743?hl=en&ref_topic=10505848
- AppsFlyer 官方：从 Google Ads 获取 SKAN 回传数据（45 天回溯、点击时间认定差异）— https://support.appsflyer.com/hc/en-us/articles/4403215779857-Get-SKAN-postback-data-from-Google-Ads
- Google 官方：iOS App 系列衡量最佳实践（SKAN vs 建模分工）— https://business.google.com/us/accelerate/resources/articles/drive-better-performance-and-measurement-for-ios-app-campaigns/
- SKAN 机制详解（窗口、延迟、隐私层级）— https://ppc.land/skadnetwork/
- 操作手册（社区）：跨账号归因覆盖 — https://github.com/j-naish/business-agent-skills/blob/HEAD/skills/google-ads-planning/references/measurement.md
