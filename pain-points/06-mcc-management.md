# MCC 管理之痛：账号一多，治理比投放更难

**结论**：MCC 本身不难用，难的是它放大的三件事——权限失控、数据割裂、连带责任。2025 年 6 月起单个账户的违规状态与 MCC 合规挂钩，一个客户出事可能牵连整个 MCC，这是多账户管理者必须重估风险的一条规则。

## 现象

- MCC 下几十个子账户，离职员工的权限半年没清，个人邮箱管理员一堆，谁在管哪个账户说不清。
- A 账户的受众/转化在 B 账户不可见——以为"同一 MCC 下自动共享"，实际每个共享都要显式配置。
- 代理商场景：一个高风险客户被封，连带 MCC 下其他客户账户受影响，救火时才发现没有隔离。

## 根因

1. **连带责任规则**（2025 年 6 月）：Google 把单个账户的状态与 manager account 合规挂钩——MCC 下的问题账户会牵连其他账户。这是 2026 年多账户管理最大的规则变化。
   来源：https://ppc.land/google-ads-kills-appeals-for-policy-decisions-over-6-months-old/
2. **共享不是默认的**：跨账号转化跟踪、受众共享（continuous audience sharing）、否定词/排除列表共享，全部需要 MCC 层显式开启或配置；"同一 MCC"只解决登录和权限，不解决数据互通。配错还会导致转化重复计数。
3. **权限治理**：MCC 的用户/管理员模型是"一次授权、长期有效"，没有强制轮换；个人邮箱管理员、离职未清、前代理商残留权限是三类常见坑。（从业者共识，置信度中）
4. **账单与主体**：多主体、多币种、多时区的 MCC 里，账单主体和付款资料混乱是封号的高危诱因（"可疑支付活动"占 2025 年封号原因的 8%）。
   来源：https://github.com/cgallic/kai-cmo-harness/blob/HEAD/harness/references/google-ads-policy-reference.md

## 影响谁

- **代理商 / 代运营**：客户越多，连带风险越大；必须在"管理效率"和"风险隔离"之间做取舍。
- **集团型广告主**（多品牌/多地区）：跨账号数据割裂导致衡量口径不统一，各子账户自说自话。
- **App 广告主**：MCC 下多应用、多地区子账户时，转化操作（Firebase vs MMP 导入）和 Primary/Secondary 设置一旦在子账户间不一致，优化信号直接污染。

## 应对思路

1. **风险隔离**：高风险/新客户与核心客户分 MCC；至少做到子账户层面的主体、域名、支付资料干净独立。
2. **权限季度审计**：清离职、清个人邮箱管理员、开 passkey/2FA；MCC 管理员数量最小化。
3. **共享清单化**：建一张"MCC 共享配置表"——哪些转化操作是 MCC 级、哪些受众开了持续共享、哪些否定词列表是共享的；新开子账户时按表勾选，而不是凭记忆。
4. **Change history 是 MCC 级的**：跨账户诊断先拉各子账户的 change history 再下结论，避免把"别人动了共享配置"误判成"模型抽风"。

## 来源

- https://ppc.land/google-ads-kills-appeals-for-policy-decisions-over-6-months-old/
- https://github.com/cgallic/kai-cmo-harness/blob/HEAD/harness/references/google-ads-policy-reference.md

*置信度：连带责任规则高（官方政策新闻）；权限治理与共享配置细节为从业者共识，置信度中，建议对照 Google Ads 帮助中心最新文档复核具体操作路径。*
