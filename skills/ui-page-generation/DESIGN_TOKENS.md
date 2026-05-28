# H5 Design Tokens 设计规范

> 版本：0.1.0
> 状态：Draft
> 适用平台：Mobile / H5
> 维护方：Design Team / Frontend Team
> 更新时间：YYYY-MM-DD

## 1. 文档目的

本文件定义项目的设计 Tokens，用于统一设计稿、组件实现、前端开发和 AI 页面生成。

Design Tokens 是设计系统中最小的可复用设计变量，用于表达颜色、字体、间距、圆角、阴影、动效、层级等基础视觉规则。

AI、设计师和开发者在生成或实现 UI 时，必须优先使用本文件定义的 Tokens，避免直接使用临时样式值。

---

## 2. Token 分层

本项目的 Tokens 分为三层：

### 2.1 基础 Token Primitive Tokens

基础 Token 只表达原始设计值，不直接表达业务含义。

示例：

```txt
color-blue-500
color-gray-100
font-size-14
spacing-16
radius-8
```

### 2.2 语义 Token Semantic Tokens

语义 Token 表达具体 UI 含义，应优先用于页面和组件。

示例：

```txt
color-text-primary
color-bg-page
color-border-default
color-action-primary
```

### 2.3 组件 Token Component Tokens

组件 Token 表达某个组件内部的默认视觉规则。

示例：

```txt
button-bg-primary
button-text-primary
card-bg
input-border-default
```

---

## 3. 命名规则

Token 名称统一使用 kebab-case。

### 3.1 基础 Token 命名

```txt
{category}-{scale}-{step}
```

示例：

```txt
color-blue-500
color-gray-50
font-size-14
spacing-16
radius-8
```

### 3.2 语义 Token 命名

```txt
{category}-{role}-{state?}
```

示例：

```txt
color-text-primary
color-text-disabled
color-bg-page
color-border-default
color-action-primary-pressed
```

### 3.3 组件 Token 命名

```txt
{component}-{part}-{property}-{state?}
```

示例：

```txt
button-bg-primary
button-text-primary
input-border-focused
card-bg-default
modal-radius-default
```

---

## 4. Token 定义格式

每个 Token 应至少包含：

```txt
名称：
类型：
值：
用途：
使用范围：
```

示例：

```txt
名称：color-text-primary
类型：color
值：var(--color-gray-900)
用途：主要正文和标题文字
使用范围：页面标题、正文、重要信息
```

---

# 5. 颜色 Tokens

## 5.1 基础颜色

### 品牌色

```txt
color-brand-50:
  type: color
  value: #EEF6FF
  usage: 品牌浅色背景

color-brand-100:
  type: color
  value: #CAE5FF
  usage: 品牌弱强调背景

color-brand-500:
  type: color
  value: #0C66FF
  usage: 品牌主色

color-brand-600:
  type: color
  value: #004CD7
  usage: 品牌按压态

color-brand-700:
  type: color
  value: #003596
  usage: 品牌深色强调
```

### 中性色

```txt
color-gray-0:
  type: color
  value: #FFFFFF
  usage: 白色背景

color-gray-50:
  type: color
  value: #F3F6FB
  usage: 页面背景

color-gray-100:
  type: color
  value: #EBEBEB
  usage: 弱背景、禁用背景

color-gray-200:
  type: color
  value: #BEC2CB
  usage: 默认边框、分割线

color-gray-300:
  type: color
  value: #9FA5AC
  usage: 辅助文字、弱强调信息

color-gray-500:
  type: color
  value: #545E69
  usage: 辅助文字

color-gray-700:
  type: color
  value: #353E4A
  usage: 次要文字

color-gray-900:
  type: color
  value: #11181F
  usage: 主要文字

color-gray-1000:
  type: color
  value: #000000
  usage: 遮罩、纯黑
```

### 功能色

```txt
color-warning-500:
  type: color
  value: #FFB020
  usage: 警告状态

color-danger-500:
  type: color
  value: #FF0000
  usage: 错误、失败、危险操作

color-info-500:
  type: color
  value: #0C66FF
  usage: 信息提示、公告通知、公共条文字或图标

color-highlight-500:
  type: color
  value: #FF7606
  usage: 高亮突出强调色，例如金额强调、营销利益点、重点数字
```

## 5.2 语义颜色

### 文本颜色

```txt
color-text-primary:
  type: color
  value: var(--color-gray-900)
  usage: 主要文字、标题、关键数据

color-text-secondary:
  type: color
  value: var(--color-gray-700)
  usage: 次要文字、说明信息

color-text-tertiary:
  type: color
  value: var(--color-gray-200)
  usage: 辅助文字、占位文字

color-text-disabled:
  type: color
  value: var(--color-gray-500)
  usage: 禁用文字

color-text-inverse:
  type: color
  value: var(--color-gray-0)
  usage: 深色背景上的文字

color-text-brand:
  type: color
  value: var(--color-brand-500)
  usage: 品牌强调文字

color-text-danger:
  type: color
  value: var(--color-danger-500)
  usage: 错误文字、危险提示

color-text-highlight:
  type: color
  value: var(--color-highlight-500)
  usage: 高亮强调文字，例如金额、优惠、利益点、强提示文案
```

### 图标颜色

```txt
color-icon-tertiary:
  type: color
  value: var(--color-gray-300)
  usage: 弱图标、辅助图标、弹窗关闭图标

color-icon-inverse:
  type: color
  value: var(--color-gray-0)
  usage: 深色背景上的反白图标，例如 Toast 图标、深色按钮图标
```

### 背景颜色

```txt
color-bg-page:
  type: color
  value: var(--color-gray-50)
  usage: 页面默认背景

color-bg-card:
  type: color
  value: var(--color-gray-0)
  usage: 卡片、内容容器背景

color-bg-elevated:
  type: color
  value: var(--color-gray-0)
  usage: 弹窗、浮层、下拉面板背景

color-bg-disabled:
  type: color
  value: var(--color-gray-100)
  usage: 禁用态背景

color-bg-mask:
  type: color
  value: rgba(0, 0, 0, 0.7)
  usage: 弹窗遮罩

color-bg-toast:
  type: color
  value: var(--color-gray-900)
  usage: Toast 轻提示背景色，透明度使用 opacity-80

color-bg-brand:
  type: color
  value: var(--color-brand-500)
  usage: 品牌主背景
```

### 边框颜色

```txt
color-border-default:
  type: color
  value: var(--color-gray-50)
  usage: 默认边框、分割线

color-border-subtle:
  type: color
  value: var(--color-gray-100)
  usage: 弱分割线

color-border-strong:
  type: color
  value: var(--color-gray-200)
  usage: 强边框

color-border-brand:
  type: color
  value: var(--color-brand-500)
  usage: 品牌边框、选中态边框

color-border-danger:
  type: color
  value: var(--color-danger-500)
  usage: 错误边框
```

---

# 6. 字体 Tokens

## 6.1 字体族

```txt
font-family-base:
  type: fontFamily
  value: "PingFang SC", "Helvetica Neue", Arial, sans-serif
  usage: 默认中文字体

font-family-number:
  type: fontFamily
  value: "xftech 2.0", "PingFang SC", sans-serif
  usage: 金额、额度、日期、倒计时、利率、倍数、次数等数字字符
  asset:
    regular: assets/fonts/number/xftech2.0-Regular.ttf
    medium: assets/fonts/number/xftech2.0-medium.ttf
    bold: assets/fonts/number/xftech2.0-bold.ttf
  font-style:
    regular: Regular
    medium: medium
    bold: bold
```

## 6.2 字重

```txt
font-weight-regular:
  type: fontWeight
  value: 400
  usage: 默认正文

font-weight-medium:
  type: fontWeight
  value: 500
  usage: 中等强调

font-weight-semibold:
  type: fontWeight
  value: 600
  usage: 标题、按钮文字

font-weight-bold:
  type: fontWeight
  value: 700
  usage: 强调标题、关键数字
```

## 6.3 字号

```txt
font-size-10: 10px
font-size-12: 12px
font-size-13: 13px
font-size-14: 14px
font-size-15: 15px
font-size-16: 16px
font-size-18: 18px
font-size-20: 20px
font-size-24: 24px
font-size-28: 28px
font-size-32: 32px
font-size-amount-sm: 24px
font-size-amount-md: 32px
font-size-amount-lg: 42px
font-size-amount-hero: 48px
```

## 6.4 行高

```txt
line-height-16: 16px
line-height-18: 18px
line-height-20: 20px
line-height-22: 22px
line-height-24: 24px
line-height-28: 28px
line-height-32: 32px
line-height-36: 36px
line-height-40: 40px
line-height-50: 50px
line-height-56: 56px
```

## 6.5 语义文本样式

```txt
text-title-lg:
  type: typography
  font-size: var(--font-size-24)
  line-height: var(--line-height-32)
  font-weight: var(--font-weight-bold)
  usage: 页面大标题

text-title-md:
  type: typography
  font-size: var(--font-size-20)
  line-height: var(--line-height-28)
  font-weight: var(--font-weight-semibold)
  usage: 页面标题、模块标题

text-title-sm:
  type: typography
  font-size: var(--font-size-18)
  line-height: var(--line-height-24)
  font-weight: var(--font-weight-semibold)
  usage: 卡片标题

text-section-title:
  type: typography
  font-size: var(--font-size-16)
  line-height: var(--line-height-24)
  font-weight: var(--font-weight-semibold)
  usage: 页面区块标题，例如福利权益、产品推荐

text-body-md:
  type: typography
  font-size: var(--font-size-14)
  line-height: var(--line-height-22)
  font-weight: var(--font-weight-regular)
  usage: 默认正文

text-body-sm:
  type: typography
  font-size: var(--font-size-12)
  line-height: var(--line-height-18)
  font-weight: var(--font-weight-regular)
  usage: 辅助说明

text-input:
  type: typography
  font-size: var(--font-size-15)
  line-height: var(--line-height-22)
  font-weight: var(--font-weight-regular)
  usage: 输入框 label、placeholder、未完成输入文本

text-input-value:
  type: typography
  font-size: var(--font-size-15)
  line-height: var(--line-height-22)
  font-weight: var(--font-weight-medium)
  usage: 输入完成后的结果文本

text-caption:
  type: typography
  font-size: var(--font-size-10)
  line-height: var(--line-height-16)
  font-weight: var(--font-weight-regular)
  usage: 标签、极弱说明

text-button-lg:
  type: typography
  font-size: var(--font-size-16)
  line-height: var(--line-height-24)
  font-weight: var(--font-weight-semibold)
  usage: 大按钮文字，例如页面主 CTA、底部主按钮、大卡片主行动按钮

text-button-md:
  type: typography
  font-size: var(--font-size-14)
  line-height: var(--line-height-22)
  font-weight: var(--font-weight-medium)
  usage: 中按钮文字，例如卡片内按钮、弹窗按钮、表单内按钮

text-button-sm:
  type: typography
  font-size: var(--font-size-12)
  line-height: var(--line-height-18)
  font-weight: var(--font-weight-medium)
  usage: 小按钮文字，例如列表项按钮、行内短按钮

text-button-xs:
  type: typography
  font-size: var(--font-size-10)
  line-height: var(--line-height-16)
  font-weight: var(--font-weight-medium)
  usage: 极小按钮文字，例如验证码按钮、局部弱操作
```

## 6.6 数字与金额文本样式

金额、额度、利率、还款金额、优惠金额等金融数字，必须优先使用金额文本 Token。金额主体数字使用 `font-family-number`，金额符号、单位和中文文案可使用基础字体，避免符号和单位喧宾夺主。

### 金额字号

```txt
font-size-amount-hero:
  type: fontSize
  value: 48px
  usage: 最大金额字号，例如首页核心额度、主视觉金额

font-size-amount-lg:
  type: fontSize
  value: 42px
  usage: 大金额字号，例如重要卡片主金额

font-size-amount-md:
  type: fontSize
  value: 32px
  usage: 中金额字号，例如详情页重点金额

font-size-amount-sm:
  type: fontSize
  value: 24px
  usage: 小金额字号，例如列表、辅助金额
```

### 金额文本样式

```txt
text-amount-hero:
  type: typography
  font-family: var(--font-family-number)
  font-size: var(--font-size-amount-hero)
  line-height: var(--line-height-56)
  font-weight: var(--font-weight-bold)
  usage: 最大金额，例如首页核心可借额度、到账金额

text-amount-lg:
  type: typography
  font-family: var(--font-family-number)
  font-size: var(--font-size-amount-lg)
  line-height: var(--line-height-50)
  font-weight: var(--font-weight-bold)
  usage: 大金额，例如重要卡片主金额、还款金额

text-amount-md:
  type: typography
  font-family: var(--font-family-number)
  font-size: var(--font-size-amount-md)
  line-height: var(--line-height-40)
  font-weight: var(--font-weight-bold)
  usage: 中金额，例如详情页重点金额、优惠金额

text-amount-sm:
  type: typography
  font-family: var(--font-family-number)
  font-size: var(--font-size-amount-sm)
  line-height: 32px
  font-weight: var(--font-weight-semibold)
  usage: 小金额，例如列表金额、辅助金额

text-amount-symbol:
  type: typography
  font-family: var(--font-family-base)
  font-size: var(--font-size-16)
  line-height: var(--line-height-24)
  font-weight: var(--font-weight-semibold)
  usage: 金额符号，例如 ¥

text-amount-unit:
  type: typography
  font-family: var(--font-family-base)
  font-size: var(--font-size-12)
  line-height: var(--line-height-18)
  font-weight: var(--font-weight-regular)
  usage: 金额单位，例如 元、期、%
```

### 金额数字使用规则

- 金额、额度、利率、还款金额、优惠金额优先使用 `text-amount-*`。
- 金额主体数字必须使用 `font-family-number`。
- 金额符号和单位可使用 `text-amount-symbol` / `text-amount-unit`。
- 不允许为了突出金额临时放大字号或加粗，必须使用已有金额文本 Token。
- 如果设计稿出现新的金额字号，需要先记录为缺失 Token，不得由 AI 自动新增。

---

# 7. 间距 Tokens

## 7.1 基础间距

```txt
spacing-0: 0px
spacing-2: 2px
spacing-4: 4px
spacing-6: 6px
spacing-8: 8px
spacing-10: 10px
spacing-12: 12px
spacing-16: 16px
spacing-20: 20px
spacing-24: 24px
spacing-32: 32px
spacing-40: 40px
spacing-48: 48px
```

## 7.2 语义间距

```txt
spacing-page-padding-x:
  type: spacing
  value: var(--spacing-16)
  usage: 页面左右安全边距

spacing-page-padding-y:
  type: spacing
  value: var(--spacing-12)
  usage: 页面上下间距

spacing-section-gap:
  type: spacing
  value: var(--spacing-12)
  usage: 页面模块之间的间距

spacing-card-padding:
  type: spacing
  value: var(--spacing-16)
  usage: 卡片内边距

spacing-list-gap:
  type: spacing
  value: var(--spacing-8)
  usage: 列表项之间的间距

spacing-form-gap:
  type: spacing
  value: var(--spacing-16)
  usage: 表单项之间的间距
```

---

# 8. 圆角 Tokens

## 8.1 基础圆角

```txt
radius-0: 0px
radius-2: 2px
radius-4: 4px
radius-8: 8px
radius-12: 12px
radius-16: 16px
radius-20: 20px
radius-24: 24px
radius-full: 999px
```

## 8.2 语义圆角

```txt
radius-card:
  type: radius
  value: var(--radius-8)
  usage: 卡片圆角

radius-button:
  type: radius
  value: var(--radius-full)
  usage: 按钮圆角

radius-input:
  type: radius
  value: var(--radius-8)
  usage: 输入框圆角

radius-toast:
  type: radius
  value: var(--radius-8)
  usage: Toast 轻提示圆角

radius-modal:
  type: radius
  value: var(--radius-16)
  usage: 弹窗圆角

radius-sheet:
  type: radius
  value: var(--radius-12)
  usage: 底部弹层圆角
```

---

# 9. 边框 Tokens

```txt
border-width-0:
  type: borderWidth
  value: 0px
  usage: 无边框

border-width-hairline:
  type: borderWidth
  value: 0.5px
  usage: 移动端细线

border-width-1:
  type: borderWidth
  value: 1px
  usage: 默认边框

border-style-solid:
  type: borderStyle
  value: solid
  usage: 默认实线边框
```

---

# 10. 阴影 Tokens

```txt
shadow-none:
  type: shadow
  value: none
  usage: 无阴影

shadow-sm:
  type: shadow
  value: 0 1px 3px rgba(0, 0, 0, 0.08)
  usage: 轻微浮起

shadow-md:
  type: shadow
  value: 0 4px 12px rgba(0, 0, 0, 0.10)
  usage: 卡片、浮层

shadow-lg:
  type: shadow
  value: 0 8px 24px rgba(0, 0, 0, 0.12)
  usage: 弹窗、强浮层
```

---

# 11. 渐变 Tokens

```txt
gradient-surface-warm:
  type: gradient
  direction: vertical
  stops:
    0%: #FFEAD1
    100%: rgba(255, 255, 255, 0)
  usage: 暖色营销背景、优惠权益背景

gradient-surface-brand-soft:
  type: gradient
  direction: vertical
  stops:
    0%: #CAE5FF
    100%: rgba(255, 255, 255, 0)
  usage: 蓝色轻营销背景、信息权益背景

gradient-surface-brand-strong:
  type: gradient
  direction: vertical
  stops:
    0%: #0C66FF
    50%: rgba(59, 157, 255, 0.8)
    100%: rgba(243, 246, 251, 0)
  usage: 强品牌营销背景、活动页顶部背景
```

规则：

- 渐变仅作为背景层，不承载内容。
- 渐变默认从容器顶部开始，方向为垂直向下。
- 渐变层高度由 `COMPONENT_RULES.md` 的全局背景层规则或页面模板决定。
- 内容层必须位于渐变层之上。
- 文本颜色必须根据文字所在区域的实际背景色自动切换，并满足 WCAG 2.1 AA 级对比度标准。

---

# 12. 透明度 Tokens

```txt
opacity-mask:
  type: opacity
  value: 0.7
  usage: 遮罩

opacity-30:
  type: opacity
  value: 0.3
  usage: 禁用态、弱分割线、弱化装饰元素

opacity-70:
  type: opacity
  value: 0.7
  usage: 中分割线、较强弱化元素

opacity-80:
  type: opacity
  value: 0.8
  usage: Toast 容器背景、强浮层背景
```

---

# 13. 层级 Tokens

```txt
z-index-base:
  type: zIndex
  value: 0
  usage: 默认层级

z-index-sticky:
  type: zIndex
  value: 100
  usage: 吸顶区域

z-index-dropdown:
  type: zIndex
  value: 300
  usage: 下拉层

z-index-overlay:
  type: zIndex
  value: 500
  usage: 遮罩层

z-index-modal:
  type: zIndex
  value: 700
  usage: 弹窗

z-index-toast:
  type: zIndex
  value: 900
  usage: Toast、全局提示
```

---

# 14. 动效 Tokens

```txt
motion-duration-fast:
  type: duration
  value: 120ms
  usage: 快速反馈

motion-duration-normal:
  type: duration
  value: 200ms
  usage: 默认转场

motion-duration-slow:
  type: duration
  value: 300ms
  usage: 复杂转场

motion-ease-standard:
  type: cubicBezier
  value: cubic-bezier(0.2, 0, 0, 1)
  usage: 默认缓动
```

---

# 15. 平台映射规则

## 15.1 H5

H5 实现推荐使用 CSS Variables：

```css
:root {
  --color-text-primary: var(--color-gray-900);
  --color-bg-page: var(--color-gray-50);
  --spacing-page-padding-x: var(--spacing-16);
}
```

## 15.2 移动端

移动端应根据技术栈转换单位：

```txt
iOS:
- font-size → pt
- spacing → pt
- radius → pt

Android:
- font-size → sp
- spacing → dp
- radius → dp
```

如果项目单位体系未确认，不允许 AI 自行转换单位。

---

# 16. 使用规则

## 16.1 设计师使用规则

- 设计稿必须优先使用语义 Token。
- 不得随意新增临时颜色、字号、间距。
- 新增 Token 前必须确认是否已有近似 Token。
- 组件内部样式应尽量沉淀为组件 Token。

## 16.2 开发使用规则

- 页面样式优先使用语义 Token。
- 组件实现可以使用组件 Token。
- 不得在业务页面中硬编码设计值。
- 不得直接修改基础 Token 来适配单个页面。

## 16.3 AI 使用规则

AI 生成页面时必须遵守：

- 优先使用语义 Token。
- 不得创造不存在的 Token。
- 不得硬编码已有 Token 能表达的值。
- 不得自行新增颜色、字号、间距、圆角。
- 遇到缺失 Token 必须明确报告。
- 组件视觉规则应优先参考组件文档。
- 页面布局规则应优先参考页面模板文档。

---

# 17. 缺失 Token 处理

当发现缺失 Token 时，按以下格式记录：

```md
## 缺失 Token

- 使用场景：
- 当前设计值：
- 建议 Token 名称：
- Token 类型：
- 是否为一次性需求：
- 是否建议加入设计系统：
```

---

# 18. 更新记录

## 0.1.0

- 初始化 Design Tokens 文档。
