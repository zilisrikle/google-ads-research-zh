# UAC 素材规格速查

**一句话**：UAC 素材"数量即权力"——标题/描述各 5 条是硬性推荐，图片视频各版式至少 1 个，否则组合空间和 Ad Strength 双输。

> 数字来源：Google Ads 官方帮助文档，查阅日期 2026-10-01。执行前请复核官方实时页面（Google 会不定期调整）。

## 文字素材

| 类型 | 字符上限 | 数量 | 是否必填 |
|---|---|---|---|
| Headlines（标题） | 30 字符 | 1–5，推荐 5 | 是 |
| Descriptions（描述） | 90 字符 | 1–5，推荐 5 | 是 |

- 每条文字必须**独立成句、任意组合都通顺**（官方原话：each line must make sense independently or in any combination）
- 语言定向必须与文案语言一致——**UAC 文案不会被自动翻译**
- 中文/日文/韩文等双字节字符按 2 个字符计（RSA 侧的计数规则，写中文标题时按 15 个汉字规划）

来源：https://support.google.com/google-ads/answer/17091671

## 图片素材

格式：`.jpg` / `.png`，单个文件 ≤5MB。

| 版式 | 比例 | 推荐尺寸 | 最低尺寸 | 数量上限 | 推荐下限 |
|---|---|---|---|---|---|
| 横版 | 1.91:1 | 1200 × 628 px | 600 × 314 px | 20 | ≥1 |
| 竖版 | 4:5 | 1200 × 1500 px | 320 × 400 px | 20 | ≥1 |
| 方形 | 1:1 | 1200 × 1200 px | 200 × 200 px | 20 | ≥1 |

- 图片为选填，但有助于 Ad Strength 达到 Excellent
- 不上传视频时，Google 可能用商店素材自动生成视频（质量不可控，建议自己传）

来源：https://support.google.com/google-ads/answer/17091671

## 视频素材

- 必须先上传到 YouTube，才能用于 UAC
- 时长：**10–60 秒**（各版式统一）
- 版式：横版 16:9、竖版 9:16、方形 1:1，每种最多 20 个，推荐每种 ≥1 个
- 最低配置建议：横版 + 竖版各 1 条（覆盖 YouTube / Shorts / 展示版位）
- 选填，但对 Ad Strength 和版位覆盖影响大

来源：https://support.google.com/google-ads/answer/17091671

## HTML5 / Playable 素材

| 要求 | 规格 |
|---|---|
| 文件 | .ZIP 包，≤5MB，包内 ≤512 个文件 |
| 数量 | 每个广告组 ≤20 个 .ZIP |
| 编码 | 非 ASCII 字符必须用 UTF-8 |
| 适配 | 响应式设计（全屏渲染，尺寸不一） |
| 声音/视频 | 支持，但 Playable 中**用户交互前不得自动播放声音** |
| 定向标签 | 需在 HTML head 中声明 orientation meta（如 portrait / landscape） |
| 不支持 | AMPHTML；不可用于 pre-registration 和 engagement（ACe）系列 |

- 计费：按 engagement（用户首次交互/点击）计费，CPE
- 转化窗口：engagement 后 30 天内安装计为转化

来源：https://support.google.com/google-ads/answer/9981650

## 素材准备 Checklist（上线前）

- [ ] 标题 5 条（每条独立成句，≤30 字符/15 汉字）
- [ ] 描述 5 条（≤90 字符）
- [ ] 横/竖/方形图片各 ≥1（1200px 系列尺寸）
- [ ] 横版 + 竖版视频各 ≥1（10–60 秒，已传 YouTube）
- [ ] Playable（如用）：ZIP ≤5MB，orientation 声明正确，非 ACe 系列
- [ ] 文案语言 = 系列语言定向
- [ ] 无政策违禁词（金融行业见 `finance-compliance-checklist.md`）

查阅日期：2026-10-01
