# MCC 跨账号：共享能力三栏表

> 查阅时效：2026-10-01。Google Ads 功能更新频繁，操作前以官方文档最新版为准。

## 概述

一个 MCC 下的子账号**默认是隔离的**——广告系列、预算、出价策略互不可见。跨账号共享分三档：**原生共享**（MCC 自带）、**需显式配置**（不开等于没有）、**不可共享**（只能复制/重建）。混淆这三档是 MCC 管理最常见的翻车点。

## 核心内容

### 第一档：原生共享（MCC 自带，无需配置）

- **统一登录与跨账号报表**：一个登录管理所有子账号，可拉跨账号汇总报表
- **用户权限集中管理**：在 MCC 层邀请用户、分配 Admin / Standard / Read-only / Billing / Email-only，权限向下继承到子账号（子账号也可单独加人）
- **标签（Labels）与 MCC 层自动化规则/提醒**：可在 MCC 层按账号维度打标签、设提醒
- **Change history**：每个子账号独立保留 2 年变更记录（MCC 不合并，但可在各子账号查看）

### 第二档：需显式配置（不开等于没有）

**1. 跨账号转化跟踪（Cross-account conversion tracking）**

- 在 MCC 创建 conversion action，子账号选用。适合多账号投同一个 App/网站的场景：App 侧只需在 MCC 建一个 third-party app analytics link ID，所有用 MCC 转化的子账号共用该 link ID 回传转化
- 硬规则：**一个子账号同一时间只能用账号级转化或 MCC 级转化，不能混用**；切换后广告系列会自动改用 MCC 的默认转化目标，需检查出价目标是否被换掉
- 子账号可见 MCC 的 conversion action 但**无权修改**，只有 MCC 能改
- Smart Bidding 会跨账号学习"Conversions"列里的所有转化（即使分属不同账号、不同出价策略）——这是把双刃剑：数据共享加速学习，也可能把不同业务线的信号混在一起

**2. 持续受众共享（Continuous audience sharing）**

- MCC 设置里勾选 "Add this manager as an audience manager for all sub accounts"，MCC 拥有/被共享的名单自动同步给所有现有及未来子账号；也可反向勾选特定子账号，把子账号名单拉上来共享
- 生效延迟**最长 48 小时**；共享名单在子账号的修改会全局生效
- 注意：名单共享需要名单所有者的合规授权，跨客户 MCC 之间共享名单有隐私政策风险

**3. MCC 级共享列表（否定关键词 / 展示位置排除）**

- 可在 MCC 的 Shared Library 建否定关键词列表，子账号的 Shared Library 会显示 "Shared from a manager account"，再**逐个手动应用到子账号的广告系列**——建列表是 MCC 级，应用是账号级
- 展示位置排除列表（excluded placement list）同理走 shared set 机制

**4. 合并账单（Consolidated billing）**

- 多子账号一张发票，需满足 Google 的账单资格（国家/币种等要求），在 MCC 账单设置中申请

### 第三档：不可共享，只能复制/重建

- **广告系列、预算、出价策略**：组合出价策略（portfolio bid strategy）只在单个账号内有效，不能跨账号
- **素材资源库（Asset library）**：账号级，跨账号需重新上传
- **实验（Experiments/Drafts）、自动规则、脚本**：按账号独立配置
- **账号级转化操作**：一旦子账号启用 MCC 级转化跟踪，原账号级转化操作即停用（历史数据保留，可切回）

### 三栏速查表

| 能力 | 档位 | 备注 |
|---|---|---|
| 跨账号报表、统一登录 | 原生共享 | — |
| 用户权限（5 档角色） | 原生共享 | MCC 层分配，向下继承 |
| 跨账号转化跟踪 | 需显式配置 | 二选一，不可与账号级混用 |
| 受众持续共享 | 需显式配置 | 48 小时生效，需合规授权 |
| MCC 级否定词/排除列表 | 需显式配置 | 建在 MCC，逐个应用到子账号系列 |
| 合并账单 | 需显式配置 | 需满足账单资格 |
| 广告系列/预算/出价策略 | 不可共享 | 复制重建 |
| 素材资源库 | 不可共享 | 逐账号上传 |
| 实验/脚本/自动规则 | 不可共享 | 逐账号配置 |

## 实操 checklist

- [ ] 新子账号接入 MCC 后先确认：用 MCC 级转化还是账号级转化（二选一，定下来不轻易换）
- [ ] 受众共享开启后等 48 小时再验证名单是否出现在子账号
- [ ] 切换转化跟踪方式后，逐个广告系列检查出价目标是否被重置为 MCC 默认目标
- [ ] 跨业务线子账号慎用 MCC 级转化：Smart Bidding 会跨账号混学
- [ ] 每季度清理 MCC 用户权限（离职、个人邮箱、未开 2SV 的账号）

## 来源

- About cross-account conversion tracking（官方）：https://support.google.com/google-ads/answer/3030657
- Share audience segments from manager account（官方）：https://support.google.com/google-ads/answer/6123188?hl=en&ref_topic=7554360
- MCC 可跨账号共享否定关键词列表（Search Engine Land，2017，功能延续至今）：http://searchengineland.com/adwords-managed-accounts-can-finally-share-negative-keyword-lists-across-accounts-267266
- App 转化 link ID 共享机制（官方文档镜像）：https://github.com/bsisduck/google-search-ads-analytics-docs/blob/HEAD/Docs/google-ads-help/answer-7365001.md
