# 学习期与放量之痛：每一次手贱，模型都要重新交学费

**结论**：Smart Bidding 时代，学习期不是"等一等就好"的玄学，而是有明确纪律的成本项：学习期的花费效率更低，每次重置都要重交一次。2026 年有两个新变量——Google 官方说冷启动不再需要攒转化数据（全账户转化都参与训练），以及 8 月的出价目标改版把 target 变成了"保留价"。放量的核心矛盾没变：想快，就要接受边际成本上升。

## 现象

- 系列状态长期卡在 "Learning"，优化师每天微调预算/出价/受众，越调越学不出来——最常见的死循环。
- 放量时一天加 50% 预算，CPA 当场爆炸；或者反过来，tCPA 设了个"理想值"，系列直接限流没量。
- 2026 年 8 月 17 日出价目标改版后，一批老账户发现"达标"的系列突然开始花超、效率回落——因为系统现在按你写的 target 字面交付。

## 根因

1. **学习期是付费的**：学习期的花费效率低于稳定期，每次重置（改预算超阈值、换转化操作、换出价策略、大改定向）都要重新经历。频繁微调 = 永远在交学费。
2. **官方口径的变化**（2026 年 3 月，Google 产品经理）：Smart Bidding 冷启动**不再需要先攒一笔转化数据**，因为系统用账户内**所有**转化做训练。但这不等于学习期消失——Demand Gen 价值出价仍要求 35 天内 50 个带价值转化才达标、之后 14 天冻结；App campaigns 同样 14 天冻结；AI Max for Search 学习期 1–2 周、日预算下限 $50。
   来源：https://ppc.land/learning-phase/
3. **2026 年 8 月改版：target 从"期望"变成"保留价"**：系统按你声明的 tCPA/tROAS 字面交付。Google 给三个选项：保留 target、按近期实际对齐、或加预算在现有 target 下放量。target 改动超 20% 触发新的学习期。——"两年前设了个数字再也没看过"的账户是这次的重灾区。
   来源：https://ppchero.com/google-ads-target-bid-strategy-changes/
4. **放量的数学**：预算改动超 ~20% 即触发学习；放量纪律是每周 +15–20%，降预算可以更激进（恢复比增长快）。判断 tCPA 至少看 30 个转化，tROAS 至少 50 个（Google Ads 产品联络人 Ginny Marvin 建议 lead-gen 按 50 个转化或完整一个月评估，剔除爬坡期）。
   来源：https://github.com/neversight/learn-skills.dev/blob/HEAD/data/skills-md/eliasmalmsandberg/google-ads-skills/google-ads-bidding/SKILL.md ；https://ppc.land/learning-phase/
5. **新风险：有写权限的 AI agent**：2026 年 4 月 Meta 开放 AI Connectors 后已出现 agent 频繁改动触发反复重置的案例；Google 侧同理——给 agent/脚本写权限必须加"学习期保护"规则。
   来源：https://ppc.land/learning-phase/（Meta 侧案例，Google 侧为类推，置信度中）

## 影响谁

- **小预算账户最痛**：PMax 建议 $50–100/天起、日预算 ≥ 3 倍 tCPA；月预算 $1K 以下硬上 PMax，大概率在"学不动"和"不敢动"之间横跳。
  来源：https://github.com/narayan-metaflow/metaflow-marketing-skills/blob/HEAD/skills/google-ads-campaign-builder/SKILL.md
- **放量期账户**：边际 CPA 上升是正常的，错的是用"平均 CPA 不变"的预期去要求放量。
- **多系列频繁调价的团队**：人力操作本身就是重置源。

## 应对思路

1. **冻结纪律**：学习期（7–14 天，App/Demand Gen 14 天）内不碰预算、出价、定向、创意；判断 tCPA/tROAS 前先攒够 30/50 个转化。
2. **放量阶梯**：每周 +15–20%，单次不超 20%；降预算可一次到位。target 与预算的改动至少间隔一个转化周期。
3. **8 月改版后必做**：审计所有 "Limited by budget" 系列，对比改版前后 30–90 天实际 CPA/ROAS 与 target 的 gap——跑得比 target 好很多的系列，优先把 target 对齐到实际值（想保效率）或加预算（想保量）。
4. **结构前置**：把"是否需要合并系列"在上线前想好；Google 搜索广告产品经理 2026 年 2 月称，语义相近的广告组/系列合并**不需要**太长的学习期（模型看语义特征而非系列 ID），但换转化操作或上 AI Max 需要。
   来源：https://ppc.land/learning-phase/

## 来源

- https://ppc.land/learning-phase/
- https://ppchero.com/google-ads-target-bid-strategy-changes/
- https://firstlaunch.in/blog/campaign-learning-phase/
- https://github.com/neversight/learn-skills.dev/blob/HEAD/data/skills-md/eliasmalmsandberg/google-ads-skills/google-ads-bidding/SKILL.md
- https://github.com/narayan-metaflow/metaflow-marketing-skills/blob/HEAD/skills/google-ads-campaign-builder/SKILL.md

*置信度：高（官方表态 + 从业者共识交叉）。AI agent 触发重置为跨平台类推，置信度中。*
