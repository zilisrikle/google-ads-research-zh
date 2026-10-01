# 成本上涨之痛：CPC 通胀是四个压力叠加的结果

**结论**：搜索 CPL 的上涨不是单一原因，而是一个 benchmark 研究点出的四重压力复合：竞争密度、信号丢失、自动化反馈环、AI  mediated 的流量发现方式变化。其中 AI Overviews 对付费点击率的压缩已有硬数据（38%），但冲击高度集中在信息类 query，交易类 query 影响很小——恐慌之前先看自己的 query 结构。

## 现象

- 一份覆盖数千账户的 Google Ads benchmark 研究：搜索 CPL 最近一个完整年度同比涨约 5%，而**前一年涨了约 24%**——上涨不平滑，转型期（cookie 后、AI 出价环境）没跟上 best practice 的账户被涨得最狠。
  来源：https://expertbeacon.com/why-google-ad-costs-are-rising-in-2026/
- Seer Interactive 对 53 个品牌、547 万 query、24.3 亿展示的研究：出现 AI Overviews 的 query 上，付费 CTR 为 16.2%，无 AIO 的为 21.8%（2026 年 2 月），**低 38%**；AIO 已覆盖约 48% 的被跟踪 query（一年前 31%）。
  来源：https://authoritytech.io/blog/ai-overviews-paid-ctr-entity-mass-fix
- SparkToro 估计 2026 年 6 月约 68% 的 Google 搜索以 zero-click 结束。

## 根因

1. **竞争密度**：更多广告主、更多垂类挤向高意图商业词，Ad Rank 门槛推高实际 CPC。
2. **信号丢失**：cookie 退化、iOS 限制、consent 缺口 → Smart Bidding 可学习的数据又少又脏 → 模型被迫放宽定向、效率下降。
3. **自动化反馈环**：Smart Bidding 和 PMax 会拼命优化你喂给它的任何转化信号，包括低质/重复线索——算法追的是量，不一定是利润。
4. **AI 改变流量发现**：AI Overviews 直接在结果页回答信息类 query，用户不滚动就看不到广告；广告主被迫把预算挪向底部漏斗的付费搜索，那里的竞争进一步加剧。
   来源：https://expertbeacon.com/why-google-ad-costs-are-rising-in-2026/
5. **冲击分布极不均匀**（关键细节）：Pew 对 6.8 万真实 query 的研究发现 AIO 使点击率相对下降 46.7%；但**品牌词 query 的 CTR 反而上升**（被 AIO 引用等于背书），被引用的品牌比未被引用的多拿 91% 的付费点击；交易/商业类 query 的 AIO 触发率 <10%、影响极小；重灾区是医疗（88%）、教育（83%）、对比类（95.4%）。
   来源：https://medium.com/@noocgs/ai-overviews-now-cover-48-of-google-queries-heres-what-marketers-should-actually-do-7a4b06adc42f
6. **Shopping 的"反鳄鱼效应"**：Smarter Ecommerce 对 1,750 亿展示的分析发现，2025 年中到 2026 年中，Shopping 广告展示中位数从约 185 万降到 140 万，CTR 中位数从 1.20% 升到 1.55%——推测 Google 优先在低点击概率 query 上展示 AIO 以保住收入，剩下的展示本身意图更高。**展示跌了不等于亏了**，别只看展示数就砍预算。
   来源：https://www.seroundtable.com/google-shopping-ads-imp-ctr-42021.html

## 影响谁

- **信息类/内容型流量依赖者最痛**（教育、医疗、媒体），交易型电商和品牌词为主的账户影响小。
- **没跟上衡量和结构 best practice 的账户**：成本 spike 集中发生在转型期掉队的账户，而非"贵行业"。
- **小预算本地广告主**：有报告称本地服务类在 AIO 出现时 CTR 跌幅可达 60%+，不过该数据来自单方报告，置信度中等。
  来源：https://markets.financialcontent.com/dailypennyalerts/article/marketersmedia-2026-7-28-ai-search-impact-on-google-ads-performance-report-released-for-local-services

## 应对思路

1. **先诊断 query 结构**：拉搜索词报告，看自己的 AIO 暴露面——交易/品牌词占比高则无需恐慌；信息类 query 占比高才需要动作。
2. **别用展示数做决策**：看转化量和转化价值；Shopping 账户尤其注意"反鳄鱼效应"，展示跌 + CTR 升可能是流量提纯。
3. **修信号**：成本上涨的四个压力里，"信号丢失"和"自动化反馈环"是自己能修的——收紧转化定义（只把真有价值的事件设 Primary）、补 server-side 信号。
4. **品牌资产进 AI 答案**：被 AIO 引用的品牌多拿 91% 付费点击——SEO/内容侧争取 entity 权威度，付费侧守住品牌词。

## 来源

- https://expertbeacon.com/why-google-ad-costs-are-rising-in-2026/
- https://authoritytech.io/blog/ai-overviews-paid-ctr-entity-mass-fix
- https://medium.com/@noocgs/ai-overviews-now-cover-48-of-google-queries-heres-what-marketers-should-actually-do-7a4b06adc42f
- https://www.seroundtable.com/google-shopping-ads-imp-ctr-42021.html
- https://www.dailysabah.com/opinion/op-ed/googles-ai-answer-engine-is-quietly-strangling-open-web

*置信度：高（多家独立研究交叉：Seer、Pew、SparkToro、Smarter Ecommerce）。CPL +5%/+24% 为某 benchmark 研究的数字，跨研究口径不完全可比，看趋势而非绝对值。*
