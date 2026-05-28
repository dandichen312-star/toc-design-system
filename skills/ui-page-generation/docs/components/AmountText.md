# AmountText 金额文本

## 1. 用途

AmountText 用于金融金额、额度、利率、优惠金额、还款金额、分期金额等重点数字展示。

AmountText 只用于数字金额类内容，不用于普通标题或正文。

## 2. 等级

```txt
hero
large
medium
small
symbol
unit
```

## 3. Token 使用

```txt
最大金额：text-amount-hero
大金额：text-amount-lg
中金额：text-amount-md
小金额：text-amount-sm
金额符号：text-amount-symbol
金额单位：text-amount-unit
金额高亮颜色：color-text-highlight
普通金额颜色：color-text-primary
弱金额颜色：color-text-secondary
```

## 4. 使用场景

```txt
hero：
  页面核心额度、主视觉金额、可借额度。

large：
  重要卡片主金额、还款金额、到账金额。

medium：
  详情页重点金额、优惠金额、分期金额。

small：
  列表金额、辅助金额、说明区金额。

symbol：
  ¥、￥ 等金额符号。

unit：
  元、期、%、折、日利率、月利率等单位。
```

## 5. 组合规则

```txt
金额主体
金额符号 + 金额主体
金额主体 + 金额单位

示例：
10,000
¥10,000
10,000元
```

- 金额主体视觉层级最高。
- 金额符号不应比金额主体更突出。
- 金额单位不应比金额主体更突出。
- 金额符号和金额单位互斥，不允许同时出现。
- `hero` / `large` / `medium` 金额不能与 `¥` 或 `￥` 组合。
- `hero` / `large` / `medium` 金额可使用纯数字，或使用数字 + `元`。
- `small` 金额可按业务需要使用 `¥` 或 `元`，但不能同时使用。
- 金额颜色按业务语义选择普通色或高亮色。
- 金额小数最多保留 2 位。
- 金额小数后两位为 `00` 时隐藏小数部分，例如 `186,000.00` 显示为 `186,000`。
- 金额小数后两位不为 `00` 时保留小数，例如 `186,000.88` 保持 `186,000.88`。

## 6. 布局规则

```txt
AmountText:
  width: hug-content / fit-content
  min-width: fit-content
  wrap: false
  white-space: nowrap
```

规则：

- 金额主体使用 `font-family-number` 后，必须按实际字宽重新计算文本宽度。
- 金额主体不允许折行，不允许因为容器宽度不足拆成两行。
- AmountText 位于横向布局时，金额文本使用 `hug-content`，相邻说明区使用 `fill`。
- AmountText 位于居中布局时，金额文本自身 `hug-content`，父级内容组负责居中。
- 如果金额超出容器宽度，优先调整容器内其他弹性区域；仍无法容纳时，按组件规则降级金额等级，例如 `hero → large → medium`，不得压缩数字宽度导致折行。

## 7. AI 使用规则

- 首页核心额度使用 `hero`。
- 重要卡片金额使用 `large`。
- 详情页重点金额使用 `medium`。
- 列表或辅助金额使用 `small`。
- 金额主体必须使用数字字体。
- 金额符号和单位不能与金额主体同等突出。
- 金额符号和金额单位不能同时出现。
- `hero` / `large` / `medium` 金额禁止使用 `¥` 或 `￥`。
- 金额强调优先使用 `color-text-highlight`。
- 普通金额使用 `color-text-primary`。
- 弱金额使用 `color-text-secondary`。
- 不允许临时放大字号或加粗金额。
- 不允许用普通正文样式展示核心金额。
- 不允许固定窄宽导致金额折行。
- 不允许展示无效小数 `.00`。
