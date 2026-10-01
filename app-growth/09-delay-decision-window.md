# 延迟与判断窗口：为什么必须用 7 天滑动平均做决策

## 概述

iOS 衡量的延迟是叠加的：SKAN 回传延迟 + 建模转化延迟 + 报表处理延迟 + 转化滞后（按点击日期记）。结论先行：**任何基于最近 2–3 天数据的出价调整都是噪音交易**；日常决策用 7 天滑动平均且剔除最近 3–5 天，SKAN 按月看，学习期内只看花费和追踪健康、不看 CPA。

## 延迟链条（按环节拆）

1. **SKAN 回传**：三个转化窗口为安装后 0–2 天、3–7 天、8–35 天；首窗口回传有 24–48 小时随机延迟，二三窗口 24–144 小时。只有首窗口能带精细转化值（0–63）。完整 SKAN 数据要等 35 天窗口走完 + 最长 6 天延迟。
2. **建模转化**：Google 官方明确最长 **5 天**才能完全处理并稳定，转化价值会在数天内被追溯调增。
3. **Google Ads 报表处理**：last-click 口径约 3 小时，其他归因模型约 15 小时；点击 / 展示 / 花费约 1 小时。
4. **MMP postback**：应用内事件回传分钟级（中置信度）；SKAN 数据由 Google 每日 01:00 UTC 批量同步给 MMP（如 AppsFlyer），dashboard 再晚 7 小时更新，Google 管道偶发延迟会追溯补数。
5. **转化滞后（conversion lag）**：转化记在点击日期而非转化日期——最近 N 天的 CPA 永远虚高，这不是恶化，是记账方式。

## 学习期

- App 系列：官方要求 14 天内不改出价、预算、创意，让系统稳定。
- Smart Bidding 学习期一般 7–14 天；预算大幅调整（>20%）、切换出价策略、更换转化操作都会重置学习。
- 2026 年 3 月 Google 更新：不再要求投放前预先积累转化银行，系统用账户内全部转化训练——学习期变短不等于可以提前下结论。

## 判断窗口实操

| 场景 | 窗口 | 看什么 |
|---|---|---|
| 每日巡检 | 当天 | 日花费是否为预算 80–120%、拒登素材、追踪健康；**不看 CPA** |
| 出价 / 预算调整 | 7 天滑动平均，剔除最近 3–5 天 | CPA 趋势（等建模稳定后再看） |
| tCPA 结论 | 累计 ≥30 个转化 | 官方建议的最小判断样本 |
| tROAS 结论 | 累计 ≥50 个转化 | 同上 |
| SKAN 复盘 | 30 天看一次 | 跨渠道预算分配依据，不用于日常优化 |
| 学习期内 | 14 天冻结 | 只看花费和追踪，不断 CPA |

为什么是"7 天滑动平均剔除 3–5 天"：建模转化最长 5 天稳定，意味着最近 5 天的数字还会被追溯修正；7 天窗口平滑了周内波动（周末效应），剔除未稳定天数后剩下的是可信区间。

## 红线

- 学习期内改出价、改预算、换转化事件。
- 用 2–3 天数据调 tCPA / tROAS。
- 拿 SKAN 日粒度数据做日常优化（官方明确 SKAN 适合 30 天粒度的长期决策）。
- 看到最近 3 天 CPA 飙升就降预算——大概率是转化滞后造成的虚高。

## 实操 checklist

- [ ] 建系列时即定好 14 天冻结期并写入排期
- [ ] 日报只看花费进度和追踪健康，CPA 只看 7 天滑动平均
- [ ] 任何出价 / 预算调整前确认已剔除最近 3–5 天未稳定数据
- [ ] tCPA / tROAS 调整幅度单次 ≤20%，调整后重新冻结
- [ ] SKAN 数据每月拉一次，不接入日报

## 来源

- Google Ads 官方：建模转化（最长 5 天稳定、追溯调增）— https://support.google.com/google-ads/answer/10081327?hl=en
- Google Ads 官方：按目标设置 App 系列（7–14 天稳定期）— https://support.google.com/google-ads/answer/6167156?hl=en
- Google Ads 官方：iOS App 系列衡量最佳实践（SKAN 30 天一看、等完整转化窗口）— https://business.google.com/us/accelerate/resources/articles/drive-better-performance-and-measurement-for-ios-app-campaigns/
- AppsFlyer 官方：SKAN 数据同步节奏（每日 01:00 UTC、追溯更新）— https://support.appsflyer.com/hc/en-us/articles/4403215779857-Get-SKAN-postback-data-from-Google-Ads
- 各平台报表延迟对照（Google Ads 3h / 15h）— https://weltpixel.com/blogs/news/how-long-until-conversions-show-up-reporting-delays-by-platform
- SKAN 窗口与延迟机制 — https://ppc.land/skadnetwork/
- 学习期机制（2026 年 3 月更新）— https://ppc.land/learning-phase/
