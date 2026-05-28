# Component Rules 组件使用规范

> 版本：0.1.0
> 状态：Draft
> 适用平台：Mobile / H5
> 依赖文档：DESIGN_TOKENS.md
> 维护方：Design Team / Frontend Team
> 更新时间：YYYY-MM-DD

## 1. 文档目的

本文件定义项目中高频 UI 组件的使用规则索引，用于统一设计稿、前端实现和 AI 页面生成。

AI 生成页面时，必须优先复用本文档索引中的组件规则，不得随意创造新的组件样式、状态或组合方式。

## 2. 全局组件原则

- 组件视觉必须使用 `DESIGN_TOKENS.md` 中的 token。
- 不允许在组件规则中新增原子 token。
- 不允许临时新增组件变体。
- 不允许用 `div` 模拟已有组件。
- 不允许临时绘制图标；图标必须引用 `Icon.md` 和 `assets/icons/` 中的资源。
- 如果现有组件无法满足设计稿，必须记录为组件缺口。
- 所有数字字符优先使用 `font-family-number`，包括标题、正文、表单、卡片、弹窗、通知、列表等组件文案中的数字；中文、英文、符号和单位仍使用组件原本字体。
- 数字字符切换为 `font-family-number` 后，文本宽度必须按实际字宽重新计算，不允许沿用旧字体下的固定窄宽。
- 独立数字、金额、利率、日期、倒计时、指标类文本默认不折行，使用 `hug-content` / `fit-content`；容器受限时优先调整容器或降级文本等级，不压缩数字文本导致换行。
- 独立展示的金融金额、额度、利率等核心数字必须使用 `AmountText` 规则。

## 3. 全局布局规则

适用于 Card、Form、List、Notice、Modal 内容区、Popup 内容区、表单项组、列表项组等承载内容的容器。

```txt
container-width:
  default: fill / 100%
  decided-by: parent container

container-height:
  default: hug-content / auto
  decided-by: inner content

layout:
  default: auto-layout / flex

horizontal-row:
  width: fill
  leading: fixed
  content: fill
  trailing: fixed / auto by component rule

vertical-stack:
  width: fill
  height: hug-content
  item-gap: token
```

规则：

- 容器宽度默认由父容器决定，使用 `fill` / `100%`。
- 容器高度默认由内部内容撑开，使用 `hug-content` / `auto`。
- 不允许为了还原静态视觉稿而固定容器高度，除非组件规范明确声明固定高度。
- 容器内部必须优先使用 Auto Layout / Flex 布局。
- 不允许用固定 `x / y` 坐标堆叠可变内容。
- 横向布局中，主内容区使用 `fill`，固定元素如 icon、button、tag 使用固定尺寸。
- 纵向布局中，模块之间使用 token 间距，不使用手动 y 坐标。
- 分割线、列表项、输入框组、说明文字区等横向元素宽度必须随容器内容区变化。
- 文案超出时按组件规则省略或换行，不允许挤压右侧操作区。
- 如果设计稿是静态宽度，AI 仍需要生成可适配父容器宽度的结构。

action-footer:
  position: bottom
  width: fill
  content-above: fill / scroll
  top-gap: spacing-16
  bottom-gap: visual-safe-gap
  device-layer: above action-footer

- 页面、弹窗、底部弹层中承载主操作按钮的 `action-footer` 必须吸附容器底部。
- `action-footer` 与上方正文内容之间固定保留 `spacing-16`。
- `action-footer` 吸附屏幕或容器底部时，按钮底部只保留可视安全间距，不把 `home-indicator` 的完整高度作为额外内边距叠加。
- Figma 完整页面中，`home-indicator` / 底部系统 bar 属于设备展示层，层级高于 `action-footer`。
- `action-footer` 上方内容区使用 `fill` 或 `scroll`，不把按钮混入正文流式布局。
- `action-footer` 吸底时，正文内容底部必须停在 `action-footer` 上方，并保留 `spacing-16` 间距。

## 4. 全局背景层规则

适用于所有带背景色、渐变背景、背景图或装饰图形的组件容器。

```txt
container:
  background-color: token
  background-layer: optional
  content-layer: required

background-layer:
  fill: solid / gradient / image
  fade-mask: required
  fade-start: 70%
  fade-end: 100%
  fade-to: color-bg-page
```

规则：

- 容器背景色必须使用对应背景 token，例如 `color-bg-card`、`color-bg-elevated`、`color-bg-page`。
- 渐变、背景图、装饰图形属于 `background-layer`。
- 线性渐变默认方向为 top → bottom，不使用 left → right。
- `background-layer` 必须位于内容层下方。
- `background-layer` 不参与内容 Auto Layout / Flex。
- `background-layer` 不受容器 padding 限制。
- `background-layer` 从容器左上角开始铺设。
- `background-layer` 宽度默认等于容器宽度。
- 页面级 `background-layer` 高度由 `PAGE_RULES.md` 决定。
- 组件级 `background-layer` 不自行定义页面高度；只有组件文档明确声明时，才定义自身背景层高度。
- `background-layer` 必须受容器圆角裁切，容器需要开启 `clips content` / `overflow hidden`。
- `background-layer` 无论填充纯色、渐变、背景图还是装饰图形，底部都必须渐隐到 `color-bg-page`，不允许硬切。
- 渐隐默认从背景层高度的 `70%` 开始，到 `100%` 完全融合到 `color-bg-page`。
- 渐隐层必须位于背景内容之上、内容层之下，只作用于背景层，不作用于正文、卡片、按钮或标题栏。
- 当用户提供 png / jpg / webp 背景图时，图片必须跟随背景层容器高度自适应，使用 `cover` 填满背景层后再应用底部渐隐。
- 内容区属于 `content-layer`，只有内容区使用 padding。
- 不允许把渐变背景放进内容 Auto Layout 中。

## 5. 全局前景对比规则

适用于所有覆盖在背景色、渐变背景、背景图或装饰图形上的文字和图标。

规则：

- 文本颜色必须根据文字所在区域的实际背景色自动切换，并满足 WCAG 2.1 AA 级对比度标准。
- 图标颜色必须跟随所在区域的实际背景色自动切换，和同区域文字保持一致的可读性。
- 渐变背景必须按文本所在位置判断，不允许将整个渐变 token 统一判定为深色或浅色。
- 当前景元素所在区域为深色背景时，文字优先使用 `color-text-inverse`，图标优先使用 `color-icon-inverse`。
- 当前景元素所在区域为浅色背景时，使用默认文字色：标题 `color-text-primary`，正文 `color-text-secondary`，辅助文字 `color-text-tertiary`，图标使用对应组件默认图标色。
- 如果无法判断实际背景色，必须选择满足 WCAG 2.1 AA 级对比度的前景颜色。

## 6. 全局行内数字高亮规则

适用于表单、卡片、弹窗、通知、列表等组件文案中的日期、倒计时、期限、倍数、次数和关键数字。

```txt
inline-highlight:
  usage: 文案中的局部日期、倒计时、期限、倍数、次数、关键数字
  default-size: 跟随所在文本字号
  font-family: font-family-number
  weight: 使用同字号的 text-button-* token
  color: color-text-highlight
```

映射规则：

```txt
所在文本为 text-body-md:
  高亮数字使用 text-button-md

所在文本为 text-body-sm:
  高亮数字使用 text-button-sm

所在文本为 text-caption:
  高亮数字使用 text-button-xs
```

规则：

- 日期、倒计时、期限等数字出现在说明文案中时，不使用 `AmountText`。
- 行内数字高亮不改变所在句子的字号和行高，只切换为同字号加粗 token。
- 行内数字高亮中的数字字符使用 `font-family-number`。
- 行内数字高亮颜色使用 `color-text-highlight`。
- 行内数字高亮只作用于关键数字本身，不整句高亮。
- 独立展示的金额、额度、利率、折扣主数字仍使用 `AmountText`。

## 7. 组件索引

```txt
Button: docs/components/Button.md
Icon: docs/components/Icon.md
Input: docs/components/Input.md
FormItem: docs/components/FormItem.md
Form: docs/components/Form.md
PickerSheet: docs/components/PickerSheet.md
Card: docs/components/Card.md
Modal / Popup: docs/components/ModalPopup.md
Toast: docs/components/Toast.md
Tag: docs/components/Tag.md
Tabs: docs/components/Tabs.md
Notice: docs/components/Notice.md
AmountText: docs/components/AmountText.md
```

## 8. AI 读取规则

- 页面生成读取与执行优先级以 `PAGE_RULES.md` 的“页面生成读取与执行优先级”为准。
- 生成页面时，先由 `PAGE_RULES.md` 判断页面类型、页面骨架、模块顺序、页面级间距、组件外部位置和组件可用宽度。
- 再读取本文档确认全局组件约束、组件选择原则、前景对比、背景渐隐、数字字体和禁止临时样式。
- 生成具体组件前，先识别当前页面实际需要用到哪些组件。
- 只读取与当前页面相关的组件文档。
- 不读取无关组件文档，避免上下文浪费。
- 如果组件规则与 `DESIGN_TOKENS.md` 冲突，以 `DESIGN_TOKENS.md` 的 token 定义为准。
- 如果页面规则与组件规则同时作用于同一模块：页面规则只决定组件放在哪里、占多宽、与上下模块间距多少；组件文档决定组件内部怎么排。
- 页面规则不能重写组件内部结构，组件规则不能改写页面模块顺序。
- 如果页面需要的组件不在索引中，记录为组件缺口，不要自行创造新组件规范。

## 9. 组件缺口记录格式

```md
## 组件缺口

- 组件名称：
- 使用场景：
- 当前缺口：
- 是否已有相似组件：
- 建议新增变体或组件：
- 是否影响页面生成：
```

## 10. 组件选择顺序

```txt
1. 已有组件
2. 已有组件的合法变体
3. 已有组件组合
4. 记录组件缺口
5. 用户确认后再新增组件或变体
```
