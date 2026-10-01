# 03 UAC 上线 SOP（从建系列到过学习期）

**目标**：把一个 UAC 系列从 0 推到稳定过学习期，不犯"上线即乱动"的经典错误。

**一句话结论**：上线前 7 天只做三件事——看花费进度、看拒登、看追踪；其他什么都不动。

## 前置条件

- 02 篇衡量 SOP 全部通过（Primary 事件有量、追踪验证完成）
- 素材包就绪：5 标题 + 5 描述 + 各版式图片 ≥1 + 横/竖视频各 ≥1（规格见 `extras/uac-creative-specs.md`）
- 商店列表页（标题、截图、描述）已优化——UAC 会自动抓取商店素材，列表页本身就是广告素材
- 如需深度链接（Deep links），提前配置并测试

## 步骤

### 1. 选择系列子类型

| 子类型 | 用途 | 前置要求 |
|---|---|---|
| App installs（ACi） | 拉新，以安装量为目标 | 无 |
| App engagement（ACe） | 再营销，定向已安装用户做应用内行为 | 有一定安装基数（量级太小跑不动） |
| Pre-registration | 上线前预约 | 仅 Android |

- iOS 和 Android 必须分系列建
- 拉新与再营销分系列（目标、受众、出价逻辑完全不同）

### 2. 预算与出价（数字来自官方最佳实践）

- **ACi（tCPI）**：日预算 ≥ 目标 CPI × 50
- **ACe / in-app action（tCPA）**：日预算 ≥ 目标 CPA × 10，且所选事件每天 ≥10 个转化
- 路径建议：先 tCPI 跑安装量 → 事件量稳定（每天 30+）→ **新建系列**切 tCPA，不要原地切换出价策略
- "Users likely to perform an in-app action"定向：tCPI 至少比纯拉新系列高 20%

### 3. 定向设置

- 地域、语言：与素材语言严格对应（UAC 文案不会被自动翻译，见官方规格页 Note）
- ACe：上传受众名单（Firebase / MMP / Customer Match），注意名单量级和新鲜度
- 起始出价：按历史 CPI/CPA 的中位数设，不要拍脑袋压低——压太低直接没量，学不动

### 4. 上线检查清单

- [ ] 转化目标 = 且仅 = 1 个 Primary 事件
- [ ] 预算满足 50× / 10× 规则
- [ ] 素材数量达标（标题/描述各 5，图片视频各版式 ≥1）
- [ ] 地域、语言、排除设置正确
- [ ] 系列状态为 Eligible，无政策警告

### 5. 学习期纪律（上线后 0–7 天，强制）

- **不动**：不出价、不改预算、不换素材、不改目标
- **只看**：
  - 日花费是否为预算的 80–120%（花不动 = 出价/预算/素材有问题；超花 = 正常，Google 日预算可超 2 倍、月不超 30.4×）
  - 素材拒登（Disapproved）——立即处理，这是唯一允许动的
  - 追踪健康（转化延迟、Primary 事件量）
- 判定节点：至少 7 天滑动平均后再做第一次判断；iOS 再加 2–3 天 SKAN 延迟缓冲
- 学习期被重置的行为：改出价策略、改转化目标、大幅改预算（>30%）、换素材大面积——都会重进学习

## 常见坑

- **上线 3 天没量就降出价/加预算**：学习期数据无意义，乱动只会延长学习
- **tCPI 和 tCPA 来回切**：每次切都是新学习，不如一开始就选对
- **素材一次只传 1 标题 1 描述**：组合空间太小，Ad Strength 上不去，等于自废武功
- **iOS 和 Android 同一系列**：CPI 差几倍，出价模型被平均，兩边都跑不好
- **ACe 名单太小**：几千人的名单，tCPA 直接没量——先做大池子（见 app-growth/06 篇）

## 来源

- Google Ads 帮助：Best practices guide: Setting up your App campaigns（https://support.google.com/google-ads/answer/6167162）——预算 50×/10×、每天 10 个转化、tCPI +20% 规则均出自此页
- Google Ads 帮助：App campaigns specs and format requirements（https://support.google.com/google-ads/answer/17091671）
- Google Ads 帮助：About assets and ads in App campaigns（https://support.google.com/google-ads/answer/6357595）
- 查阅日期：2026-10-01
