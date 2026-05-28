# Theme Presets 主题预设

## 1. 文档用途

本文件用于定义主题预设清单，以及 AI 在页面生成时选择主题、回退主题和禁止行为的规则。

本文件负责：

- 定义全局 `brand theme` 的选择规则。
- 定义模块 `scene theme` 的选择规则。
- 定义回退规则。
- 定义禁止项。
- 列出可用的 `brand theme` 预设清单。
- 列出可用的 `scene theme` 预设清单。

本文件不负责：

- 不重写组件样式。
- 不定义组件结构。
- 不新增 token。
- 不允许 AI 生成新主题名。

---

## 2. 全局 Brand Theme 选择规则

- `brand theme` 只能从预设清单中选择。
- AI 只允许“选择”，不允许“生成”。
- AI 可根据 logo 主色相，从预设主题中选择最接近的一套。
- AI 判断 logo 时只看主色相。
- logo 为复合色或渐变色时，取面积最大主色。
- AI 不允许生成新的 `theme-brand-*`。
- AI 不允许生成新的 brand token。
- 无法稳定判断时，回退到 `theme-brand-blue`。

---

## 3. 模块 Scene Theme 选择规则

- `scene theme` 只能由页面或模块显式声明。
- AI 不允许根据“会员 / VIP / 活动 / 权益”等语义自动套用 `scene theme`。
- AI 不允许生成新的 `theme-scene-*`。
- `scene theme` 只能从预设清单中选择。
- `scene theme` 只作用于显式声明模块，不作用于整页。

---

## 4. 回退规则

### 4.1 Brand Theme 回退

- `brand theme` 判断失败时，回退到 `theme-brand-blue`。

### 4.2 Scene Theme 回退

- `scene theme` 未显式声明时，不启用任何 `scene theme`。
- `scene theme` 未显式声明时，仅继续使用全局 `brand theme`。

---

## 5. 禁止项

- 不允许 AI 生成新的 `theme-brand-*`。
- 不允许 AI 生成新的 `theme-scene-*`。
- 不允许 AI 生成新的 brand token。
- 不允许仅因模块文案出现“会员 / VIP / 活动 / 权益”等语义词，就自动启用 `scene theme`。
- 不允许修改 `brand theme` 时自动联动修改 `scene theme`。
- 不允许修改 `scene theme` 时自动联动修改 `brand theme`。

---

## 6. Preset 固定字段

每个主题 preset 使用以下固定字段：

- `theme-name`
- `theme-type`
- `scope`
- `activation`
- `ai-selectable`
- `fallback`
- `declaration-required`

### 6.1 固定枚举

#### theme-type

- `brand`
- `scene`

#### activation

- `default`
- `preset-from-logo`
- `explicit-declaration`

#### ai-selectable

- `yes`
- `no`

#### fallback

- `self`
- `theme-brand-blue`
- `none`

#### scope

- `global-brand`
- `member-module`
- `activity-module`
- `vip-module`

#### declaration-required

- `yes`
- `no`

---

## 7. Brand Theme 预设清单

### 7.1 theme-brand-blue

- `theme-name`: `theme-brand-blue`
- `theme-type`: `brand`
- `scope`: `global-brand`
- `activation`: `default`
- `ai-selectable`: `yes`
- `fallback`: `self`
- `declaration-required`: `no`

说明：

- 作为全局默认品牌主题。
- 作为 `brand theme` 默认回退主题。
- 可被 AI 选择。

### 7.2 theme-brand-red

- `theme-name`: `theme-brand-red`
- `theme-type`: `brand`
- `scope`: `global-brand`
- `activation`: `preset-from-logo`
- `ai-selectable`: `yes`
- `fallback`: `theme-brand-blue`
- `declaration-required`: `no`

说明：

- 非默认品牌主题。
- 可被 AI 根据 logo 主色相选择。
- 判断失败时回退到 `theme-brand-blue`。

### 7.3 theme-brand-orange

- `theme-name`: `theme-brand-orange`
- `theme-type`: `brand`
- `scope`: `global-brand`
- `activation`: `preset-from-logo`
- `ai-selectable`: `yes`
- `fallback`: `theme-brand-blue`
- `declaration-required`: `no`

说明：

- 非默认品牌主题。
- 可被 AI 根据 logo 主色相选择。
- 判断失败时回退到 `theme-brand-blue`。

### 7.4 theme-brand-green

- `theme-name`: `theme-brand-green`
- `theme-type`: `brand`
- `scope`: `global-brand`
- `activation`: `preset-from-logo`
- `ai-selectable`: `yes`
- `fallback`: `theme-brand-blue`
- `declaration-required`: `no`

说明：

- 非默认品牌主题。
- 可被 AI 根据 logo 主色相选择。
- 判断失败时回退到 `theme-brand-blue`。

---

## 8. Scene Theme 预设清单

### 8.1 theme-scene-member-default

- `theme-name`: `theme-scene-member-default`
- `theme-type`: `scene`
- `scope`: `member-module`
- `activation`: `explicit-declaration`
- `ai-selectable`: `no`
- `fallback`: `none`
- `declaration-required`: `yes`

说明：

- 用于普通会员区。
- 用于普通会员权益模块。
- 用于普通会员 banner。
- 必须显式声明启用。
- 未声明时不回退到任何 `scene theme`。

### 8.2 theme-scene-member-premium

- `theme-name`: `theme-scene-member-premium`
- `theme-type`: `scene`
- `scope`: `member-module`
- `activation`: `explicit-declaration`
- `ai-selectable`: `no`
- `fallback`: `none`
- `declaration-required`: `yes`

说明：

- 只能用于高等级会员卡。
- 只能用于高等级会员权益区。
- 只能用于高等级会员专属模块。
- 不能用于普通会员区。
- 必须显式声明启用。
- 未声明时不回退到任何 `scene theme`。

---

## 9. AI 使用规则

- AI 先读取本文件，判断当前主题是否必须来自 preset。
- AI 读取 `brand theme` 时，只允许从 `theme-brand-*` 预设中选择。
- AI 读取 `scene theme` 时，只允许使用已显式声明的 `theme-scene-*` 预设。
- AI 不要生成新的主题名、scope、activation、fallback。
- AI 无法判断全局品牌主题时，统一回退到 `theme-brand-blue`。
