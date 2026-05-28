# Button 按钮

## 1. 用途与范围

Button 用于触发页面中的操作行为，包括提交、确认、跳转、取消、删除、重新获取、查看详情等。

Button 只表达“操作”，不用于纯信息展示。

范围：

- 适用于通用按钮。
- 不包含 VIP 专属按钮、特殊运营按钮、活动定制按钮。

## 2. 变体

```txt
primary：页面主操作，如提交、确认、立即借款、立即还款、下一步。
secondary：次要操作，如取消、返回、稍后处理。
text：弱操作、协议入口、辅助跳转、重新获取验证码。
danger：不可逆且需要强警示的危险操作，第一版少用，不因动作有风险就默认使用。
```

## 3. 状态

```txt
default
disabled
loading
```

规则：

- 按钮可有点击反馈，但不单独定义 `pressed` 视觉状态。
- `disabled` 用于不可点击状态，例如表单未完成、未勾选协议、业务状态不可操作。
- `loading` 用于提交中或请求处理中，必须锁定重复点击。

## 4. 内容结构

```txt
label
icon + label
label + icon
```

规则：

- `label` 是默认结构。
- `icon + label` 用于表达动作类型或状态提示。
- `label + icon` 用于跳转、展开、进入下一步等方向性操作。
- 图标不能单独替代按钮文字，除非后续定义独立 IconButton 规范。

## 5. 尺寸规格

按钮尺寸必须按下列规格使用，不允许临时创造高度、字号或字重。

```txt
xlarge:
  height: 54px
  text-style: text-button-lg
  usage: 大卡片主行动按钮、核心营销卡片主按钮

large:
  height: 48px
  text-style: text-button-lg
  usage: 页面主 CTA、底部固定操作区、弹窗主按钮、重要表单提交

medium:
  height: 36px
  text-style: text-button-md
  usage: 卡片内普通按钮、表单内按钮、普通模块操作

small:
  height: 32px
  text-style: text-button-sm
  usage: 小卡片主按钮、列表项操作

mini:
  height: 24px
  text-style: text-button-sm
  usage: 小卡片辅助按钮、行内短按钮

micro:
  height: 22px
  text-style: text-button-xs
  usage: 极小辅助操作、验证码按钮、局部文本旁按钮
```

## 6. 宽度规则

按钮宽度由承载容器和使用场景决定，不允许随意写固定宽度。

```txt
full：撑满父容器可用宽度。
auto：宽度由内容决定。
fixed：固定宽度，必须来自组件规则、页面模板或设计稿标注。
equal：多个按钮在同一容器中等分宽度。
```

## 7. 容器对应规则

容器规则优先级高于按钮变体规则。AI 必须先判断按钮所在容器，再选择按钮变体、尺寸和宽度。

```txt
页面底部固定操作区：
  variant: primary
  size: large
  width: full

表单提交区：
  variant: primary
  size: large
  width: full

页面主 CTA：
  variant: primary
  size: large
  width: full

大卡片主行动按钮：
  variant: primary
  size: xlarge
  width: full 或 fixed

卡片内普通按钮：
  variant: primary 或 secondary
  size: medium
  width: full 或 fixed

卡片内文字操作：
  variant: text
  size: small 或 mini
  width: auto

弹窗底部单按钮：
  variant: primary
  size: large
  width: full

弹窗底部双按钮：
  variant: secondary + primary
  size: large
  width: equal

列表项右侧操作：
  variant: primary
  size: small
  width: fixed

公告条内操作：
  variant: text
  size: mini
  width: auto

营销 Banner 内按钮：
  variant: primary 或 secondary
  size: small 或 medium
  width: fixed
```

## 8. 弹窗按钮组合

```txt
单主按钮：
  Primary

双按钮：
  左 Secondary，右 Primary

主按钮 + 次文本：
  上 Primary，下 Text
  gap: spacing-16

主按钮 + 危险文本：
  上 Primary，下 Danger Text
  gap: spacing-16

双次级按钮：
  左 Secondary，右 Secondary
```

规则：

- 弹窗双按钮中，弱动作在左，强动作在右。
- 弹窗内除 `text` 按钮外，所有按钮高度固定使用 `large / 48px`。
- “放弃 / 离开 / 忍痛离开”这类动作优先使用次文本或 danger text，不与主按钮同权。

### 次文本规格

```txt
普通次文本：
  variant: text
  text-style: text-body-md
  text-color: color-text-tertiary
  width: auto

强调次文本：
  variant: text
  text-style: text-button-md
  text-color: color-text-brand
  width: auto

危险次文本：
  variant: danger text
  text-style: text-button-md
  text-color: color-text-primary
  width: auto
```

规则：

- 普通次文本用于弱操作、非关键跳转。
- 强调次文本用于需要保留品牌识别的辅助操作。
- 危险次文本用于放弃、离开、取消权益等操作，但不使用红色，避免过度警示。
- 次文本不与主按钮同权展示。

## 9. Token 使用

```txt
主按钮背景：color-brand-500
主按钮文字：color-text-inverse
主按钮按压反馈：color-brand-600

次按钮文字：color-text-brand
次按钮边框：color-border-brand
次按钮背景：color-bg-card

文本按钮文字：按次文本规格使用

危险按钮文字或背景：color-danger-500

禁用按钮背景：color-bg-disabled
禁用按钮文字：color-text-disabled

按钮圆角：radius-button
按钮文字：按尺寸规格使用 text-button-*
```

## 10. 决策规则

```txt
1. 先判断按钮所在容器。
2. 如果容器有标准组合，优先使用容器规则。
3. 容器不明确时，再使用通用按钮语义规则。
4. 在同一个容器内，先复用标准组合，再调整按钮文案。
```

场景映射：

```txt
立即借款 / 立即还款 / 下一步 / 确认开通：
  primary

取消 / 返回 / 稍后处理：
  secondary

查看详情 / 协议 / 规则 / 辅助入口 / 重新获取验证码：
  text

删除 / 注销 / 解除绑定：
  primary + 二次确认

放弃权益 / 放弃申请 / 离开当前流程：
  主按钮 + 次文本

同时存在“查看当前状态”和“继续推进”：
  主按钮 + 次文本
```

## 11. 项目默认按钮策略

第一版项目按钮策略用于约束 AI 在高频场景中选择按钮变体、尺寸、宽度和组合，避免把弱入口放大成主按钮，或把风险动作默认画成红色危险按钮。

### 高频场景默认组合

```txt
页面底部固定操作区：
  variant: primary
  size: large
  width: full

表单提交按钮：
  variant: primary
  size: large
  width: full

首页金额大卡主按钮：
  variant: primary
  size: xlarge
  width: full

协议 / 规则 / 查看说明类入口：
  variant: text
  width: auto
```

### 弱操作默认规则

- “查看详情”默认优先使用 `text`，特殊场景下可按页面层级升级为 `secondary`。
- “稍后处理 / 暂不处理”默认优先使用 `secondary`，特殊场景下可按业务调整。
- “重新获取验证码”默认优先使用 `text`，特殊场景下可按业务调整。
- 按钮场景中的“返回”默认优先使用 `secondary`。
- Header 返回与 Button 返回分开定义：
  - Header 返回属于 Header 组件规范。
  - Button 返回属于页面内容区操作按钮规范。

### 风险动作默认规则

- “删除 / 注销 / 解除绑定”类动作不默认使用 `danger` 视觉按钮。
- 这类动作可按业务流程使用默认主按钮，但必须结合确认机制控制风险。
- “放弃权益 / 放弃申请 / 离开当前流程”默认使用“主按钮 + 次文本”组合。
- 危险或高风险动作默认需要二次确认。

### danger 使用边界

- `danger` 变体在项目第一版中属于少用按钮类型。
- `danger` 仅用于不可逆且需要强警示的操作。
- 如果业务动作具有风险，但页面主行动必须突出，默认优先使用 `primary + 二次确认`。
- 不要因为动作存在风险，就默认把按钮改成 `danger`。

### 按钮组合优先级

- 同一区域默认只允许 1 个主按钮。
- 同时存在“继续推进”和“查看当前状态”时，默认使用“主按钮 + 次文本”组合。
- 同时存在“确认”和“取消”时，默认使用“左 secondary + 右 primary”组合。
- 不允许主按钮、次按钮、次文本三种动作同时并列出现。

### 容器内按钮优先级

- 首页活动卡 / 权益卡中的按钮默认优先使用 `primary` 或 `secondary`，不优先使用 `text`。
- 列表项右侧操作默认使用 `primary`。
- 结果页主按钮默认使用 `primary`，放在内容区内，不固定到底部操作区。
- Card 内辅助入口默认优先使用 `text`，不放大为主按钮。

## 12. 与页面规则和组件规则的边界

- Button 组件规范决定按钮的变体、尺寸、宽度、组合和风险表达方式。
- 页面布局规则决定按钮所在页面区块的位置和是否固定。
- Card 组件规范决定按钮在卡片内部的层级和容器关系。
- Header 组件规范中的返回操作不等同于页面内容区中的 Button 返回。

## 13. 禁止项

- 不要同时出现两个同权重主按钮。
- 不要让两个 `primary` 并列。
- 不要左强右弱。
- 不要把高风险操作无确认地做成品牌主按钮。
- 不要因为动作存在风险就默认使用 `danger`。
- 不要把权益短入口放大成主按钮。
- 不要让辅助入口与 `primary` 争抢视觉权重。
- 不要让主按钮、次按钮、次文本三种动作在同一区域同时并列。
- 不要给按钮使用卡片圆角。
- 不要自定义新的按钮颜色体系。
- 不要临时创建新的按钮高度、字号、字重或宽度。
- 不要用普通 `div` 模拟按钮。
