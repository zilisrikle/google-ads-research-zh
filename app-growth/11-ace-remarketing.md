# App 再营销（ACe）：名单、出价与验证期

> 查阅时效：2026-10-01。ACe（App campaigns for engagement）是 Google Ads 的应用再营销系列类型。

## 概述

ACe 专门投**已安装用户**，目标是召回（re-engagement）而非拉新。与拉新系列（ACi）最大的区别：ACe 的命门是**名单质量**，不是素材——名单不准，出价再低也只是在浪费展示。

## 核心内容

### 1. 名单构建：4 种官方支持的受众类型

Google 官方要求 ACe 名单必须从以下 4 种类型创建（可组合）：

1. **All users**（全体用户）
2. **Users who've used your app recently**（近期活跃）
3. **Users who haven't used your app recently**（近期沉默——召回主力）
4. **Users who took specific actions within your app**（发生过特定应用内行为，如加购未付、申请未提交）

另可上传 mobile device ID 或 customer list 建名单（需符合资格）。

### 2. Firebase 受众 vs MMP 名单推送：关键差异

| 维度 | Firebase（GA4 for Firebase） | MMP（AppsFlyer 等）名单推送 |
|---|---|---|
| 名单生成 | Firebase 项目关联 Google Ads 后自动生成 "All users" 名单；可在 Firebase/GA4 按事件组合自定义 | 在 MMP 侧按事件/归因维度圈人，通过集成推送给 Google Ads |
| 出价能力 | 完整：支持 tROAS（需 Firebase SDK 收入事件） | **tROAS 不支持**——Google 明确只认 Firebase SDK 的收入事件，MMP 收入事件不能用于 tROAS 出价 |
| 受众排除 | 支持（基于 Firebase 事件的排除） | **不支持**——优化目标为 MMP 事件时，不能做受众排除 |
| 实时性 | 第一方，延迟低 | 经 postback 回传，有延迟 |

结论：只接 MMP 能跑 ACe（tCPI/tCPA），但**名单丰富度、出价上限（无 tROAS）、排除能力**三项不如 Firebase。双 SDK 并行时，同一事件只选一个数据源做 Primary，避免重复计数。

### 3. 名单不填充的排查

官方列出的常见原因：Google Play 未关联（Android "All users" 名单依赖它）、应用内转化跟踪未配置、SDK 事件 ping 没发到 Google Ads、GA4 与 Google Ads 的事件参数名不一致、选了 "Start with an empty list" 且没勾选过去 30 天回填。排查顺序：关联状态 → 转化跟踪 → 事件参数对齐。

### 4. 定向与出价策略

- **分层建系列**：按沉默时长分层（如 7 天沉默 / 30 天沉默 / 90 天沉默），沉默越深 tCPA 可放宽——召回一个 90 天沉默用户的价值低于 7 天沉默用户，出价应反映 LTV 差异
- **按行为分层**：发生过关键行为未转化（如 preApply 未提交）单独建高优先级名单，出价高于泛沉默名单
- **深链（deep link）**：广告落地到 App 内对应页面，而非首页； relevance 直接影响 CVR
- **频次**：ACe 本身无频次上限设置，靠预算和 tCPA 间接控制；名单小、预算大必然导致高频次骚扰，预算应与名单规模匹配

### 5. 验证期方法：有效线与红线

ACe 必须回答一个问题：**这些召回是增量，还是用户自己会回来？** 方法：

- **Holdout 对照组**：预留 10–20% 名单不投放，对比投放组 vs 对照组的回访/转化率，差值才是增量 lift（Google 官方出过 remarque 工具做 Customer Match 名单的 treatment/control 切分）
- **有效线示例**：连续两周，投放组每周转化 ≥ X 且增量 CPS < 拉新 CPS × 系数（如 0.6）
- **红线示例**：连续 3 天 CPS 超过阈值 → 预算 -20%；单周转化 < Y → 判定召回无效，停投复盘名单
- **冻结期纪律**：验证期内不改名单定义、不改出价、不改预算，否则 lift 不可比

## 实操 checklist

- [ ] Firebase 项目已关联 Google Ads（自动获得 All users 名单）
- [ ] 4 种名单类型至少建出"沉默用户"和"关键行为未转化"两层
- [ ] 确认出价事件的数据源（Firebase/MMP），MMP 事件无 tROAS、无受众排除
- [ ] 设置 holdout 对照组（10–20%），验证期 ≥ 2 周
- [ ] 预算与名单规模匹配，避免小名单大预算造成频次轰炸
- [ ] 广告配置 deep link 到行为对应页面

## 来源

- Fix audience population issues in App campaigns（官方，含 4 种受众类型与排查）：https://support.google.com/google-ads/answer/15399471?hl=en
- Advertising without the Firebase SDK 的限制（AppsFlyer 官方文档，2026-09 更新）：https://support.appsflyer.com/hc/en-us/articles/115002504686-Google-Ads-AdWords-Integration-setup-for-advertisers
- ACe 增量验证思路（Moburst）：https://www.moburst.com/blog/app-retargeting-on-google-ads-a-complete-guide/
- remarque：Customer Match 名单 treatment/control 工具（Google marketing solutions，非官方支持）：https://github.com/google-marketing-solutions/remarque
- ACe 上线要求（2021 年文章，250,000 安装门槛可能已过时，置信度低）：https://ppc.land/google-launches-app-campaigns-for-engagement-in-google-ads/
