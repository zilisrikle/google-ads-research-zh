# 政策合规之痛：封号、验证、申诉，一次都不能错

**结论**：Google Ads 的政策执法是"三轨制"，读错轨道代价完全不同；金融（含借贷）是验证最严、变化最快的行业之一，2026 年 7 月欧盟/EEA 24 国 newly 纳入金融服务验证。合规不是法务的事，是投放的生命线。

## 现象

- 2025 年 Google 共封禁 2,490 万个广告账户——规模化执法的背景下，误伤和申诉是常态。
- 贷款广告主：广告或落地页缺 APR、还款条款、总费用披露即拒登；验证材料一次填错可能直接导致封号，且某些被封账户**必须先通过验证才能申诉**。
- 2026 年 7 月 21 日起，超过 6 个月的政策决定不再支持在账户内申诉——没有过渡期，老 enforcement 记录的纠错通道被直接关闭。

## 根因

1. **三轨执法，误判轨道最贵**：
   - **Egregious（严重违规）**：检出即封、无警告、实质永久；申诉仅在" compelling circumstances"下恢复；会**连坐关联账户并阻止新开户**。包括：规避系统、协同欺诈、假货、恶意软件、不可接受的商业行为等。
   - **Strike-track**：警告 → 3 天暂停 → 7 天暂停 → 封号，每步可恢复。
   - **Limited Ad Serving**：不是封号，是展示限流（降 30–90%），有独立申诉表，合规+验证后可恢复。
   - 落地页问题（如失效页面）**不属于** egregious，至少提前 7 天警告；但 cloaking 属于"规避系统"，直接进严重轨道。
   来源：https://github.com/sergeyizmailov/claude-skills/blob/HEAD/skills/google-ads/references/09-policy-and-compliance.md
2. **金融服务验证持续扩张**：2025 年 6 月 debt services 并入统一金融服务验证框架（澳大利亚、巴西、德国、爱尔兰、韩国、西班牙等需经第三方 G2 验证）；**2026 年 7 月 enforcement 扩展到 24 个欧盟/EEA 国家**，泛欧投放需按国家逐个验证（如奥地利、比利时、荷兰、芬兰各走一遍）；30 天窗口内未完成则金融广告被拒登（非金融系列可继续跑）；提交虚假验证信息可直接封号。
   来源：https://ppc.land/google-expands-financial-ad-verification-to-24-eu-and-eea-countries/
3. **连坐规则**：2025 年 6 月起，单个账户的状态与 manager account（MCC）合规挂钩——MCC 下的问题账户会牵连其他账户。
   来源：https://ppc.land/google-ads-kills-appeals-for-policy-decisions-over-6-months-old/
4. **申诉通道收紧**：99% 的申诉在 24 小时内解决，但 2026 年 7 月 21 日起超 6 个月的政策决定不再能从账户内申诉，且无过渡期。
   来源：同上
5. **封号原因分布**（2025 年千例分析）：规避系统 38%、不可接受的商业行为 38%、可疑支付 8%、验证失败 ~5%、多账户政策 ~3%。
   来源：https://github.com/cgallic/kai-cmo-harness/blob/HEAD/harness/references/google-ads-policy-reference.md

## 影响谁

- **金融/借贷/保险广告主**：验证 + 披露双重要求，合规成本最高；香港等市场的借贷广告还需叠加本地牌照披露。
- **代理商 / MCC 管理者**：连坐规则下，一个客户出问题可能牵连整个 MCC 的其他客户账户。
- **高增长期账户**：支付方式变更、异地登录、多账户操作都可能触发"可疑支付/规避系统"误判。

## 应对思路

1. **先判轨道再行动**：Policy Manager 里看清引用的具体政策；egregious 别抱幻想走常规申诉，strike-track 按步骤在每个窗口内修复。
2. **金融广告主**：APR、还款条款、总费用必须在广告或落地页首屏清晰披露；验证走官方通道、逐国完成，材料一次做对（错一次的代价可能是封号）。
3. **申诉纪律**：引用具体政策条文、逐条说明合规点、附牌照/认证文件；**不要重复提交未修改的拒登广告**，会触发账户级处罚；所有申诉留档。
   来源：https://www.auditsocials.com/platforms/google-ads-policy-guide
4. **MCC 隔离**：高风险客户与核心客户分 MCC 管理；支付主体、域名、主体信息保持干净一致，减少"关联账户"误判面。

## 来源

- https://ppc.land/google-expands-financial-ad-verification-to-24-eu-and-eea-countries/
- https://ppc.land/google-ads-kills-appeals-for-policy-decisions-over-6-months-old/
- https://github.com/sergeyizmailov/claude-skills/blob/HEAD/skills/google-ads/references/09-policy-and-compliance.md
- https://github.com/cgallic/kai-cmo-harness/blob/HEAD/harness/references/google-ads-policy-reference.md
- https://www.auditsocials.com/platforms/google-ads-policy-guide

*置信度：高（政策类以官方口径为准；千例封号分析为第三方样本，比例供参考）。*
