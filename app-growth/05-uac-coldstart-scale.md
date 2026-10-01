# UAC 冷启动与放量

## 概述

UAC 的增长路径是固定的三段式：**tCPI 起量 → 验证事件量级 → tCPA/tROAS 深化**。跳过任何一段都会付出代价：直接对深层稀疏事件出价会导致系统长期无法退出学习；长期停留在 tCPI 则买到的是廉价低质安装。冷启动的目标不是便宜，而是**快速攒够学习数据**。

## 0-1 SOP

**阶段 0：衡量先行（上线前）**
- Firebase 或 MMP 接入完成，关键事件回传 Google Ads 并设为 Primary
- iOS：CV schema 三选一配置完成；确认 ATT 策略或 on-device measurement
- 素材底线：5 标题 + 5 描述 + 三比例图片/视频各 ≥1

**阶段 1：tCPI 起量（第 1–2 周）**
- 出价：品类均值的 80–100%（行业共识），宁可略高不要压价——冷启动压价等于让系统去找最便宜的低质流量
- 预算：≥ 50×tCPI（官方示例：$2 CPI → $100/天），推荐 50–100 倍
- 配置 Audience signals 缩短冷启动；iOS 与 Android 分系列
- 冻结：不调出价、不调预算、不换定向；容忍 CPI 波动

**阶段 2：中间态（可选，事件量级不足时）**
- 若核心事件每天 <10 个用户，**不建 tCPA 系列**。改用 ACi 的"Install volume + Users likely to perform an in-app action"定向，tCPI 出价比纯拉新高 ≥20%（官方建议），买"更可能发生深层行为"的安装
- 同时继续补素材、扩量，让事件自然爬坡

**阶段 3：tCPA 迁移（事件达标后）**
- 触发条件：核心事件**每天稳定 ≥10 个不同用户**（官方门槛），建议观察 5–7 天确认稳定
- 动作：**新建** tCPA 系列，不在原 tCPI 系列上直接切换出价策略（切换会重置学习）
- 出价：以 Firebase/MMP 观测到的实际 CPA 为起点，持平或略高
- 预算：≥ 10×tCPA（ACe 再营销系列建议 ≥15×，行业共识）
- 原 tCPI 系列保留作为流量基本盘，双轨并行 1–2 周后再视情况收缩

## 预算调整节奏

- 学习期内（7–14 天）**零调整**，这是铁律。
- 学习完成后单次调整幅度：行业共识 ±20–30%；tCPA/tROAS 目标值调整同样小步（±10–20%），大步跳变会触发重新学习或直接停投。
- 目标与预算不同时大动：一次只动一个变量，否则无法归因效果变化。
- 预算上调后观察 ≥3 天（iOS ≥7 天）再做下一次决策。

## 放量信号与红线

**可放量信号（需同时满足）**
- CPA 连续 5–7 天稳定在目标 ±20% 内
- 事件量级持续 ≥ 门槛（tCPA 每天 ≥10 用户）且有上升趋势
- 素材侧有 ≥1 条 Best 评级素材且花费占比健康

**红线（触发即停手排查）**
- 连续 3 天 CPA 超目标 50%+：先查追踪（事件断流？重复计数？），再查素材疲劳，最后才动出价
- 事件量级跌破 10/天：降回中间态，不要硬撑 tCPA
- iOS 四方数据（Firebase/MMP/SKAN/Google）出现量级分叉：先对口径，再做优化动作
- 预算消耗 <50% 且状态 Limited by budget：预算/出价比失衡，提高预算而非压出价

## 增量验证（放量前）

平台归因 ≠ 增量。Google 已将增量实验（incrementality experiments）门槛降至约 $5,000 起、结果直接在 Ads UI 内查看（行业来源，置信度中，2026）。放量决策前至少做一次 geo 或开关实验；更大预算可用 Google 开源的 Meridian（MMM）做交叉验证。土办法依然有效：选定地理、做一次显著预算调整、看趋势是否跟随。

## 实操 checklist

- [ ] 衡量、素材、iOS schema 三项上线前就绪
- [ ] tCPI 起量：出价 80–100% 品类均值，预算 ≥50×tCPI，Audience signals 已配
- [ ] 2 周内冻结一切大改；iOS 用 7 天滑动平均判断
- [ ] 事件 ≥10 用户/天稳定 5–7 天 → 新建 tCPA 系列迁移，不原地切换
- [ ] 调整单次 ±20–30%，一次只动一个变量
- [ ] 放量前跑增量实验，不只看平台归因

## 来源

- 出价/预算/学习期/事件门槛（官方）：https://support.google.com/google-ads/answer/6167156?hl=en
- ACi 搭建与 Audience signals（官方）：https://support.google.com/google-ads/answer/12575501
- iOS 最佳实践（官方）：https://business.google.com/us/accelerate/resources/articles/drive-better-performance-and-measurement-for-ios-app-campaigns/
- 2026 实操指南（预算比例、增量实验门槛、系列结构，行业来源）：https://eppcdigital.com/most-complete-guide-for-google-universal-app-campaigns-includes-11-best-practices-suggestions-for-creatives/
