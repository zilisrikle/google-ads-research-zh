# UAC Android 投放篇

## 概述

Android 是 UAC 数据链最完整、学习最快的平台：无 ATT 限制，Google Play 与 Firebase 提供第一方确定性数据，归因以用户级为主、建模为辅。与 iOS 相比，Android 的核心优势是**信号多、延迟低、学习快**，通常作为新应用验证 PMF 与素材方向的第一站。

## Google Play 数据链路

- **账号关联**：将 Google Play 开发者账号与 Google Ads 关联（Product Linking），打通安装与应用内事件数据。
- **Download 事件自动创建**：搭建 Android 版 ACi 时，若账号内尚无该应用的 download 事件，系统会自动创建一个并持续保留——这是 Android 独有的便利，iOS 无此机制。
- **Play Install Referrer**：应用通过 Play Install Referrer API 获取确定的安装来源信息，是 Android 归因准确率高的技术基础（行业共识）。
- **Firebase 第一方数据**：Android 上 Firebase 事件是用户级、实时的，可直接作为出价事件，无需经过 SKAN 式的聚合与延迟。
- **预注册（ACpre）**：仅 Android 支持，利用 Google Play 预注册机制在上线前蓄水。

## 与 iOS 的核心差异

| 维度 | Android | iOS |
|---|---|---|
| 用户级归因 | 有（Install Referrer + Firebase/MMP） | 基本无（ATT 拒绝后走聚合） |
| 归因延迟 | 小时级 | 3–5 天（含 SKAN 回传 + 建模） |
| 学习速度 | 快，判断窗口可较短 | 慢，判断窗口 ≥7 天 |
| 系列数量限制 | 无 SKAN 式硬性合并要求 | 官方建议 ACi ≤8 个 |
| 深度链接 | Deferred deep links（安装后跳转指定页） | Deep links（已安装用户跳转） |
| 典型 CPI | 相对低（行业共识） | 通常数倍于 Android（行业共识） |
| 预注册系列 | 支持 | 不支持 |

## 实操要点

- **冷启动更快**：Android 上 tCPI 起量后，可更快验证事件量级是否达到 tCPA 门槛（每天 ≥10 个不同用户完成事件）。
- **Deferred deep links**：在广告组 Advanced Options 的 App URL 字段配置，用户安装并首次打开后直达指定应用内页面，对电商、内容类应用的承接转化很关键。
- **商店页即素材**：UAC 会自动抓取 Play 商店页的图标、标题、评分与截图参与广告组合。更新商店截图与标题时，要意识到它同时在改广告素材。
- **设备碎片化**：Android 机型、系统版本分散，素材需覆盖多分辨率；但 UAC 自动组合已部分消化此问题，重点仍是三比例素材齐全。
- **作弊水位更高**：Android 归因链开放，激励欺诈、设备农场相对 iOS 更常见（行业共识）。MMP 的反作弊（如 Protect360）建议开启，并定期审计异常安装源。
- **Android 经验不可直接外推 iOS**：CPI、CVR、事件率在两个平台差异巨大；iOS 预算与判断窗口需单独规划，不用 Android 数据定 iOS 出价。
- **语言定向**：Google 不翻译广告，只投放与素材语言匹配的语言定向；多语言市场需按语言拆系列或至少拆广告组（官方说明）。

## 实操 checklist

- [ ] 关联 Google Play 开发者账号，确认 download 事件已自动创建
- [ ] Firebase / MMP 的 Android 事件回传正常，关键事件设为 Primary
- [ ] 配置 deferred deep links（ App URL 字段）
- [ ] Android 与 iOS 分系列，命名标注 OS，预算与出价独立设置
- [ ] 开启 MMP 反作弊，定期审计安装质量
- [ ] Android 先行验证素材与事件，再复制方法论到 iOS（不复制出价）

## 来源

- ACi 搭建（含 Play download 事件自动创建、deep links）：https://support.google.com/google-ads/answer/12575501
- 系列类型与 ACpre（Android only）：https://support.google.com/google-ads/answer/15997092
- iOS/Android 差异与 iOS 最佳实践对照：https://business.google.com/us/accelerate/resources/articles/drive-better-performance-and-measurement-for-ios-app-campaigns/

注：Android Privacy Sandbox（含 Attribution Reporting API）的推进状态本文未覆盖，待补充研究。
