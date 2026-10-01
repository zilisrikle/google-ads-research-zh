# 转化事件策略：Primary、代理事件与防重复计数

## 概述

转化事件策略回答三个问题：哪个事件进出价（Primary vs Secondary）、选深事件还是浅事件（代理事件 vs 深层转化）、多数据源并行时如何不重复计数。核心原则：**出价事件 = 有足够量级的最深层事件**，量级和价值不可兼得时，先保量级。

## Primary vs Secondary

Google 官方定义：

- **Primary**：计入报表的 Conversions 列；只要其所属 goal 被用于出价，就参与 Smart Bidding。注意：即使未被用于优化的 Primary，也可能被 Google 用于增强预测（enhance predictions）。
- **Secondary**：只计入 All conversions 列，纯观察，不参与出价。**唯一例外**：被加入 custom goal 的 Secondary 会参与出价——custom goal 成员不看 Primary/Secondary 标记。
- GA4 导入的转化默认是 Secondary，只能在 Google Ads 侧升级为 Primary。

实操含义：Conversions 列是 Smart Bidding 真正追逐的东西。把浅层事件（如 page view、first_open）和深层事件同时设为 Primary，算法会把预算推向更便宜的浅事件，稀释对高价值事件的出价压力。

## 代理事件 vs 深层转化事件

深层事件（签约、购买、放款）价值最高，但量级稀疏时模型学不动；代理事件（申请、注册、加购）量级大，但与终极目标的相关性必须验证。

**量级门槛**：

| 层级 | 日事件量 | 状态 |
|---|---|---|
| 最低 | 10 / 天（不同用户） | Google 官方 App 系列文档的硬门槛：出价事件每天至少 10 个不同用户完成，否则必须换更浅的事件 |
| 推荐 | 30–50 / 天 | 稳定优化 |
| 理想 | 100+ / 天 | 高精度优化；同时有助于通过 iOS SKAN 隐私阈值（crowd anonymity） |

**出价策略的量级要求**（官方）：tROAS 在搜索 / 购物 / 展示要求 30 天内 15 个转化；Demand Gen 价值出价要求 35 天内 50 个带价值转化。2026 年 3 月 Google 更新：不再要求投放前先积累"转化银行"，系统会用账户内所有转化训练模型——但这不降低对稳定量级的要求，判断 tCPA 仍建议至少 30 个转化、tROAS 至少 50 个转化。

**标准迁移路径**：tCPI 起量（验证安装量级）→ 新建系列切 tCPA（代理事件）→ 代理事件量级稳定后再建新系列切深层事件。每次切换出价事件都是一次新的学习，不要原地切换。

**预算配比**（官方）：tCPI 日预算 ≥ 目标 CPI × 50；tCPA 日预算 ≥ 目标 CPA × 10。

## 防重复计数（Firebase + MMP 并行）

Google Ads 的去重键是**单个转化操作内的 transaction ID**——跨转化操作没有自动去重。Firebase 版 `signContract` 和 MMP 版 `signContract` 是两个独立的转化操作，会各自计数。

规则：

1. **同一业务事件只保留一个 Primary**，其余数据源版本一律 Secondary。
2. 切换数据源时按官方 GA4 迁移流程操作：先把旧数据源（第三方）Primary 降级为 Secondary，再把新数据源（GA4 / Firebase）Secondary 升级为 Primary。不要同时存在两个 Primary 的过渡期。
3. 计数方式：购买 / 收入类用 Every（每次转化都算钱），线索 / 申请类用 One（一次点击只算一次，防重复提交刷量）。该设置只对未来生效，不追溯历史。
4. 报表只看 Conversions 列（Primary）；All conversions 列是各数据源之和，**永远不要把不同数据源的数字加总**。

## 实操 checklist

- [ ] 出价事件日量 ≥10 不同用户，否则换更浅的代理事件
- [ ] Conversions 列里只有一个业务事件是 Primary
- [ ] 线索类事件计数方式为 One，收入类为 Every
- [ ] 代理事件与深层目标的相关性已验证（如 newApply→signContract 转化率稳定）
- [ ] 切换出价事件时新建系列，不在原系列上直接换（避免学习重置叠加口径断裂）
- [ ] tCPA 判断前累计 ≥30 转化，tROAS ≥50 转化

## 来源

- Google Ads 官方：Primary 与 Secondary 转化操作 — https://support.google.com/google-ads/answer/11461796?hl=en-GB
- Google Ads 官方：按目标设置 App 系列（10 用户 / 天门槛、tCPI×50 预算）— https://support.google.com/google-ads/answer/6167156?hl=en
- Google Ads 官方：GA4 迁移 App 系列（Primary/Secondary 切换流程）— https://support.google.com/google-ads/answer/13823094?hl=en&ref_topic=10556935
- Google Ads 官方：建模转化（最长 5 天稳定）— https://support.google.com/google-ads/answer/10081327?hl=en
- 学习期与量级判断（2026 年 3 月更新）— https://ppc.land/learning-phase/
- 操作手册（社区）：事件量级梯度、预算配比 — https://github.com/j-naish/business-agent-skills/blob/HEAD/skills/google-ads-planning/references/app-campaigns.md
- 操作手册（社区）：tROAS 量级门槛 — https://github.com/j-naish/business-agent-skills/blob/HEAD/skills/google-ads-planning/references/budget-planning.md
