# 02 衡量搭建 SOP（SDK / 转化导入 / Primary 设置）

**目标**：让 Google Ads 拿到干净、实时、不重复计数的转化信号。这是所有出价的前提——信号错了，后面全错。

**一句话结论**：一个出价事件只选一个数据源做 Primary；Firebase 和 MMP 可以并存，但同一个事件绝不能两边同时 Primary。

## 前置条件

- App 已上架（Google Play / App Store），包名 / App ID 确认
- 决定数据源：Firebase SDK、MMP（AppsFlyer / Adjust / Singular）或两者并行
- Google Ads 账号与 Firebase 项目 / MMP 账号的管理员权限

## 步骤

### 1. SDK 接入（二选一或并行）

- **Firebase SDK**：免费，Google 第一方，事件实时性最好；是 Firebase 受众（Google Ads 独有能力）的前提
- **MMP SDK**（如 AppsFlyer）：跨平台归因最强；iOS 只接 MMP SDK 也可以投 UAC，不是硬性门槛
- 并行接入时：两个 SDK 各自上报，**去重靠 Google Ads 侧的 Primary/Secondary 设置**，不是靠 SDK 侧

### 2. 转化导入 Google Ads

- Firebase：账号关联后，在 Google Ads 转化操作中导入 Firebase 事件（自动）
- MMP：在 MMP 的 Google Ads 集成配置中打开 in-app event postback，把要出价的事件映射过去；Google Ads 侧从"第三方应用分析"导入
- 检查事件名、参数、货币/价值是否正确映射

### 3. Primary / Secondary 设置（关键）

- **Primary**：用于出价的事件，一个优化目标只选一个。计入"转化次数"列
- **Secondary**：只观察、不出价，用于报表对比和漏斗分析
- 规则：
  - 同一个业务事件（如 newApply）如果 Firebase 和 MMP 都有，只选一边做 Primary，另一边设 Secondary
  - 出价目标变更 = 新建系列，不要在原系列上把 Secondary 升 Primary（学习重置，且历史信号口径变了）
- "Include in Conversions" 列：只有 Primary 默认计入；检查 Secondary 没有被误勾选

### 4. 归因窗口与计数方式

- 确认每个 conversion action 的归因窗口（点击/展示回溯期）与 MMP 侧口径一致
- 计数方式：Every（每次转化都计）vs One（每个用户只计一次）——深层事件（签约）通常用 One，避免重复计数污染出价
- iOS：确认 SKAN 回传链路正常；ATT 授权率低的市场，接受建模转化的延迟（2–5 天）

### 5. 验证清单（上线前必须跑完）

- [ ] 测试设备走完完整漏斗（安装 → 注册 → 目标事件），MMP / Firebase 实时报表可见事件
- [ ] Google Ads 转化操作状态为"正在记录转化"（Recording conversions），无"未验证"警告
- [ ] Primary 事件 7 天内有量（tCPA 要求每天 ≥10 个，见 04 篇）
- [ ] 同一事件只有一个 Primary 数据源（查 Conversion actions 列表）
- [ ] 深层事件的回传延迟实测（MMP postback 到 Google Ads 通常有数小时延迟，心里有数）

## 常见坑

- **Firebase 和 MMP 同时 Primary**：重复计数，CPA 虚低，出价模型学的是假信号
- **把安装和应用内事件都设 Primary**：出价目标分裂，系列不知道到底优化什么
- **事件量不够就上 tCPA**：每天 <10 个转化的事件，tCPA 学不动（官方要求见 04 篇）
- **归因窗口两边不一致**：MMP 7 天、Google Ads 30 天，报表永远对不上，复盘先吵架
- **iOS 只看平台数据**：SKAN 延迟 + 建模，不看 MMP/Firebase 会误判

## 来源

- Google Ads 帮助：转化跟踪设置、Primary/Secondary 转化操作
- Google Ads 帮助：Best practices guide: Setting up your App campaigns（https://support.google.com/google-ads/answer/6167162）
- 本知识库：`app-growth/02-iOS篇.md`、`app-growth/04-衡量与归因.md`
- 查阅日期：2026-10-01
