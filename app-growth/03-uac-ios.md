# UAC iOS 投放篇

## 概述

iOS 是 UAC 最难的平台。ATT（App Tracking Transparency）切断 IDFA 后，用户级归因基本消失，iOS 投放依赖三条数据链：**SKAdNetwork/AdAttributionKit 的聚合回传、ATT 授权用户的 IDFA 数据、Google 的建模转化**。三者数字天然对不上，这是方法论差异，不是 bug。

## ATT 与数据链

- ATT 授权率低是常态：拒绝授权的用户只能走 SKAN/AAK 聚合归因 + 建模。
- Google 官方建议：评估 ATT 提示是否适合你的应用；可先展示 warm-up（预热解释页）再弹系统提示，提高授权率；授权用户越多，可观测转化越多，建模与优化质量越高。
- **On-device conversion measurement**（设备端转化衡量）：Google 官方推荐方案，事件数据不出设备、不含用户标识，用于增强 iOS 优化与报告。有两个变体：纯事件数据版，以及（有登录体系、收集邮箱/电话时）叠加第一方数据的版本。
- 出价策略选择直接挂钩隐私方案——Google 官方原话：用 tCPA/tROAS 的广告主**应**实施 ATT 提示和/或 on-device measurement；**若两者都不做，官方推荐用 tCPI**。

## SKAdNetwork 现状（2026）

- Apple 目前支持 **SKAN 3 与 SKAN 4**；SKAN 4.0 引入 3 个回传窗口（0–2 天、3–7 天、8–35 天），窗口 1 必填且是唯一支持 fine + coarse 值的窗口。
- **SKAN 5.0 从未发布**。Apple 在 WWDC24 推出 **AdAttributionKit（AAK，iOS 17.4+）** 作为事实上的继任者；SKAN 未被官方宣布废弃，但不再更新。两者并存，Apple 会综合评估两个框架做归因裁决。
- AAK 的关键改进：回传同时发给广告平台**和**开发者 App；原生支持再营销衡量；支持欧盟第三方应用市场；iOS 18.4（WWDC25 更新）支持重叠再营销窗口（conversion tags）、回传自带国家代码、提供开发者测试工具。
- **Crowd anonymity tiers（人群匿名层级）**：设备按同类转化量决定回传粒度。量小的系列会落到 Tier 0/1，几乎拿不到数据——**小预算 iOS 系列在数据层面被系统性惩罚**，这是合并系列的底层原因。
- Google 的建模**只用 fine conversion values（0–63），不支持 coarse values**（Google 官方文档明确说明）。

## Conversion Value 设计

- 配置入口三选一：**Google Analytics（Firebase）、第三方 MMP、Google Ads API**——官方强烈建议只选一个地方配置，避免冲突。
- Schema 设计原则：64 个值（0–63）映射对你业务最重要的应用内事件/收入区间；**schema 里出现的事件必须同时是 Google Ads 里可出价（biddable）的转化事件**，否则优化无从谈起。
- 典型映射思路（行业共识）：低值 = 安装/浅层事件，中值 = 注册/关键行为，高值 = 付费/深层事件；或按累计收入区间分层。不要把 64 个值平均分配给无差别的事件。
- 回传延迟：SKAN 回传本身有 24–48 小时延迟，加上建模，iOS 数据稳定需要 **3–5 天**。判断窗口至少 7 天滑动平均。

## iOS 与 Android 必须分系列

1. **产品硬约束**：一个 App 系列创建时只能选一个平台（Android 或 iOS），无法混投。
2. **归因机制根本不同**：Android 有确定性用户级归因（Play Install Referrer + Firebase/MMP），iOS 是聚合 + 建模。混在一起系统无法建立统一的价值模型。
3. **出价与预算逻辑不同**：iOS CPI 通常数倍于 Android，学习所需预算、判断窗口、事件策略都不同。
4. **SKAN campaign ID 限制**：Google 官方建议 **iOS 拉新系列合并至 8 个或更少**，过多系列会让 SKAN 的 campaign 级报告失准。

## 实操 checklist

- [ ] 三选一确定 CV schema 配置入口（Firebase / MMP / API），全团队对齐
- [ ] 设计 0–63 映射：事件必须与 Google Ads 可出价事件一致
- [ ] 评估 ATT 提示 + warm-up 页；或部署 on-device measurement
- [ ] 不做 ATT/on-device → 只用 tCPI，不碰 tCPA/tROAS
- [ ] iOS ACi 系列 ≤8 个，按大地理分组 consolidation
- [ ] iOS 判断窗口 ≥7 天，接受 3–5 天数据延迟
- [ ] Firebase、MMP、SKAN、Google 四方数字分叉视为正常，只在量级异常时排查

## 来源

- iOS 系列 SKAN 报告（官方）：https://support.google.com/google-ads/answer/14892597
- SKAN conversion value schema 配置（官方）：https://support.google.com/google-ads/answer/13286653?hl=en
- GA4 配置 SKAN schema（官方）：https://support.google.com/analytics/answer/13165271?hl=en
- iOS 系列效果与衡量最佳实践（Google 官方，≤8 系列/ATT/on-device/tCPI 建议）：https://business.google.com/us/accelerate/resources/articles/drive-better-performance-and-measurement-for-ios-app-campaigns/
- AAK 与 SKAN 对比及匿名层级（行业整理，2026）：https://github.com/rylaa/ios-marketing-att-skill/blob/HEAD/references/adattributionkit-and-skan.md
- SKAN 现状分析（含未废弃说明，行业来源）：https://ppc.land/skadnetwork/
- WWDC25 AAK 更新（行业来源）：https://segwise.ai/blog/wwdc-2025-adattributionkit-update-6-improvements-catch
