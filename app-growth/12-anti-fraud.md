# 反作弊：识别、工具与出价污染隔离

> 查阅时效：2026-10-01。移动作弊手法进化快，以下为当前主流形态与防御手段。

## 概述

反作弊不是"省预算"的卫生工作——作弊流量一旦进入转化回传，会**污染 Smart Bidding 的学习样本**，模型会主动去找更多"长得像作弊者"的流量，形成越优化越亏的死亡螺旋。防御的第一优先级永远是：**别让脏转化回传给媒体**。

## 核心内容

### 1. 主流作弊形态与数据特征

| 作弊类型 | 手法 | 数据特征 |
|---|---|---|
| **SDK spoofing** | 不装 App，直接向 MMP 服务器伪造安装与应用内事件的网络请求 | 安装量与应用商店下载数对不上；事件时间戳异常规整；无真实设备行为 |
| **Click injection / spamming** | 批量点击/伪造点击，抢 last-click 归因 | 点击→安装时间极短且集中；单一渠道点击量畸高但留存断崖 |
| **Incentivized fraud（激励欺诈）** | 激励墙/任务平台用户为奖励而安装，毫无真实意图 | D1 留存断崖、应用内行为 ≈ 0、广告参与度为 0 |
| **Device farm / emulator（设备农场）** | 真机/模拟器群控批量操作 | 同一设备型号/IP 段集中爆发；行为模式高度重复 |
| **DeviceID reset fraud** | 反复重置设备 ID 冒充新用户 | 同一设备指纹对应大量"新用户" |

通用识别信号：**留存断崖**（D1 留存远低于自然量）、**行为真空**（有安装无任何应用内事件）、**商店数对不上**（MMP 安装数 >> 应用商店新增）、**geo 错位**（非目标市场集中爆量）。

### 2. 作弊污染 tROAS/出价模型的机制

1. 作弊者伪造的安装/事件被计为转化，回传给 Google Ads
2. Smart Bidding 把这些转化当**正样本**学习——"这类流量容易转化"
3. 模型主动加价抢更多同类流量（作弊流量通常便宜、量大、"转化率"极高，模型最爱）
4. 真实 CPA 爆炸，但平台报表 CPA 依然"好看"——因为分子分母都被污染了

关键点：Google 官方文档明确，Smart Bidding 会学习"Conversions"列里的**所有**转化信号。脏数据不是"浪费一点预算"，而是**系统性带偏模型**。

### 3. 防御工具栈（以 AppsFlyer 为例）

- **Protect360**：实时反作弊套件。含 DeviceRank（给每台设备打分，C=欺诈 ~ AAA=可信，类似信用分），自动拦截已知的 spoofing、劫持类作弊
- **Validation rules（验证规则）**：自定义拦截逻辑（如 geo 不符、OS 版本异常、黑名单渠道），支持 **Tagged 模式**——先标记不拦截，观察误伤率再转正。这是上线任何拦截规则的标准动作
- **Advanced Security Module（Protect360 插件，Android beta）**：在首次启动后、归因前实时评估安装，拦截归因欺骗。需 Android SDK v6.15.2+
- **IO Builder: Fraud Appendix**：投放前就和渠道把作弊判定基准写进合同，避免事后扯皮

### 4. 隔离方法

1. **MMP 侧拦截优先**：在 MMP 把作弊安装/事件 block 掉，**不向 Google Ads 回传**——这是最关键的一步，回传了就晚了
2. **分渠道看留存与行为**：任何新渠道/代理商，前两周只看 D1 留存和关键行为率，不看 CPI
3. **异常即暂停**：某渠道安装量突增但行为真空，先停后查，不要等"再观察几天"
4. **定期审计**：应用商店下载数 vs MMP 安装数，每月对一次账

## 实操 checklist

- [ ] Protect360（或同类）已开启，DeviceRank 低分设备自动拦截
- [ ] 新验证规则一律先用 Tagged 模式跑 1–2 周，确认误伤率再转 Implemented
- [ ] 被判定作弊的转化**不**回传 Google Ads（检查 MMP postback 配置）
- [ ] 每月对账：应用商店新增 vs MMP 安装数，差异 > 10% 彻查
- [ ] 新渠道冷启动期考核 D1 留存 + 行为率，不考核 CPI
- [ ] 代理商合同写入 Fraud Appendix 作弊基准

## 来源

- What is SDK spoofing / Advanced Security Module（AppsFlyer 官方）：https://support.appsflyer.com/hc/en-us/articles/39145848948625--Beta-Advanced-Security-Protect360-Module
- Validation rules（AppsFlyer 官方，含 Tagged 模式）：https://support.appsflyer.com/hc/en-us/articles/115004703926-Implement-validation-rules-to-prevent-fraud
- State of ad fraud 2026（AppsFlyer 行业报告）：https://www.appsflyer.com/resources/reports/state-fraud-marketers-report/
- Smart Bidding 跨转化学习机制（Google 官方）：https://support.google.com/google-ads/answer/3030657
