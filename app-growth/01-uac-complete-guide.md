# UAC 完全指南（App Campaigns）

## 概述

UAC（Universal App Campaigns，现官方名称为 App campaigns）是 Google 推广移动应用的自动化广告系列类型。核心特征：**广告主只控制三件事——素材、预算、出价目标**，其余（定向、版位、出价、广告组合）全部由 Google AI 自动化完成。广告可投放至 Google 搜索、Google Play、YouTube、展示广告网络、Discover 等版位，Google 动态组合素材生成广告。

## 三类广告系列

| 系列 | 官方名称 | 目标 | 可用出价 | 版位 | 平台限制 |
|---|---|---|---|---|---|
| 拉新 | App campaigns for installs（ACi） | 获取新安装，或获取"会完成指定应用内事件"的新用户 | tCPI / tCPA / tROAS / Maximize conversions（不设目标） | 搜索、Play、YouTube、展示等全版位 | iOS + Android |
| 再营销 | App campaigns for engagement（ACe） | 召回已安装用户，促成指定应用内事件（加购、购买、复购等） | tCPA / tROAS | 搜索、YouTube、展示等（不含 Play 商店内） | iOS + Android |
| 预注册 | App campaigns for pre-registration（ACpre） | 应用上线前积累预注册用户 | 预注册目标成本 | Play、YouTube、展示 | **仅 Android** |

要点：ACe 的广告不会出现在 Google Play 内（用户已安装，无需商店流量）；ACpre 仅支持 Android，因为预注册是 Google Play 独有机制。

## 出价策略

- **tCPI（目标每次安装费用）**：只关心安装量与安装成本。冷启动默认起点。
- **tCPA（目标每次转化费用）**：对指定应用内事件出价。官方要求：**每天至少有 10 个不同用户完成该事件**，否则数据不足以学习，应换更上层的事件。
- **tROAS（目标广告支出回报率）**：对事件价值出价，需要稳定回传 conversion value。2025 年起 tROAS 与"不设目标的 Maximize conversions"已在 iOS 全量可用（此前 iOS 长期仅支持 tCPI/tCPA）。
- **Ad Revenue Optimization**：针对广告变现类应用的专用出价策略（行业来源，置信度中）。
- ACi 还有一个中间形态："Install volume"目标 + 定向"Users likely to perform an in-app action"（可能完成应用内事件的用户），官方建议其 tCPI 出价**至少比纯拉新系列高 20%**，让系统区分两类用户的价值。

## 预算规则与学习期

- **预算/出价比**：官方示例——目标 CPI 为 $2，日预算至少 $100，即 **50 倍**。行业共识：tCPI 系列 50–100 倍，tCPA 系列 10–20 倍。比例过低会触发"Limited by budget"状态，系统无法充分学习。
- **学习期**：新建或大改后约 **7–14 天**。期间不改出价、不改预算、不做大幅素材调整、不改定向；容忍短期 CPI/CPA 波动；尤其 iOS 不看少于 2 天的数据做判断。
- **Audience signals**：ACi 可选功能，提供种子受众信息帮助 Google AI 冷启动，官方明确其作用是"克服冷启动挑战"。
- 广告系列命名建议包含操作系统（Android/iOS），一个系列只能选一个平台。

## 系列结构补充

- **广告组上限**：每个 App 系列最多 100 个广告组（引自官方文档 answer/6372658，经第三方整理引用，置信度中）。实操中远用不到上限——Google 官方建议按大地理分组做 2 个系列（拉新 + 行为）即可，碎片化会稀释转化信号。
- **素材来源有两条**：手动上传 + 自动抓取应用商店页（图标、标题、评分、截图）。商店页本身就是素材，ASO 与 UAC 素材是同一套视觉资产。
- **投放细节**：tCPA/tROAS 的 ACi 系列，广告可能持续投放至转化窗口结束（官方说明）；系统会为适配版位自动裁剪文本与图片。
- **Feeds**：可在 App 系列中接入数据 Feed，突出应用内特定内容（商品、活动），对电商与内容类应用的 ACe 尤其有用。

## 实操 checklist

- [ ] 确认目标：纯拉新选 ACi，再营销选 ACe，上线前造势选 ACpre（Android）
- [ ] 衡量先行：转化事件已接入（Firebase / MMP 回传），tCPA 事件确认日活 ≥10 用户
- [ ] 预算 ≥ 50×tCPI（或 ≥10×tCPA），避免 Limited by budget
- [ ] ACi 冷启动配置 Audience signals
- [ ] 学习期 7–14 天内冻结出价、预算、定向与大改素材
- [ ] iOS 与 Android 分系列创建，命名标注 OS

## 来源

- 系列类型：https://support.google.com/google-ads/answer/15997092
- ACi 搭建流程：https://support.google.com/google-ads/answer/12575501
- 按目标搭建（含预算/出价/学习期规则）：https://support.google.com/google-ads/answer/6167156?hl=en
- 2026 年 UAC 实操指南（tROAS 登陆 iOS、预算比例、系列结构，行业来源）：https://eppcdigital.com/most-complete-guide-for-google-universal-app-campaigns-includes-11-best-practices-suggestions-for-creatives/
