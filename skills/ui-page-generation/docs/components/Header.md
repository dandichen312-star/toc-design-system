# Header 标题栏

## 1. 用途与范围

Header 用于承载页面顶部导航、标题和次级操作。

范围：

- 适用于金融 APP / H5 的通用内页标题栏。
- 适用于首页标题栏变体。
- 不包含系统状态栏。
- 不包含底部导航。

## 2. 基础结构

```txt
Header
├── left-area
│   └── back / close 可选
├── title-area
│   └── title 可选
└── right-area
    └── icon / text-action 可选
```

规则：

- Header 基础元素包括左侧返回按钮、标题、右侧操作 icon / 文案按钮。
- Header 允许无左侧返回按钮。
- 右侧操作区允许为空。
- 右侧操作数量限制：
  - 操作 icon 最多 2 个
  - 文案按钮最多 1 个
- 右侧文案按钮和右侧 icon 不允许同时出现。

## 3. 标题规则

```txt
header-title:
  font-size: font-size-16
  line-height: line-height-24
  font-weight: font-weight-medium
  color: color-text-primary
```

规则：

- 标题默认单行展示。
- 标题字号固定使用 `font-size-16`。
- 标题行高使用 `line-height-24`。
- 标题字重使用 `font-weight-medium`，即中粗，不使用 `font-weight-semibold` 或 `font-weight-bold`。
- 标题默认颜色使用 `color-text-primary`；透明沉浸态或深色背景上按 `COMPONENT_RULES.md` 的前景对比规则切换为 `color-text-inverse`。
- 标题文案建议控制在 `11` 个字符内。
- 标题超长时默认截断。
- 通用 Header 标题默认居中。
- 首页 Header 标题默认居左。
- 无左侧返回按钮时，标题仍然居左。
- Header 默认不支持副标题。
- 首页为 Header 特殊变体，可按首页规则单独处理。

## 4. 左侧操作规则

规则：

- 左侧区域默认只放一个返回操作。
- 默认使用返回 icon。
- 不允许使用 icon 加文案的返回形式。
- 允许替换为关闭按钮，但需要业务特别说明。
- 返回交互规则写入组件规范中统一定义。

## 5. 右侧操作规则

规则：

- 右侧操作默认用于承载次级功能。
- 右侧文案按钮字数建议不超过 `4` 个字符。
- 右侧操作区允许为空。
- 右侧操作不与标题争抢视觉权重。

## 6. 布局与尺寸规则

```txt
height: 44px
padding-x: spacing-16
touch-area: 32 x 32
```

规则：

- Header 高度固定为 `44px`。
- Header 左右内边距固定使用 `spacing-16`。
- Header 左右内容区域根据屏幕宽度自适应。
- 左右操作点击热区为 `32 x 32`。
- Header 与状态栏之间不额外增加顶部间距。

## 7. 背景与滚动态规则

规则：

- 通用 Header 默认背景为白色。
- 首页 Header 默认背景为透明。
- 页面滚动后，Header 背景统一过渡为白色。
- Header 在滚动吸顶态下不显示阴影。
- 默认态与滚动态之间需要渐变过渡。
- 顶部状态栏区域底色需要与 Header 当前底色保持一致变化。

## 8. 第一版变体范围

```txt
common-header:
  usage: 通用内页

home-header:
  usage: 首页

no-back-header:
  usage: 无返回按钮页面

transparent-header:
  usage: 沉浸态 / 透明态
```

规则：

- 第一版需要支持以下变体：
  - 通用内页 Header
  - 首页 Header
  - 无返回按钮 Header
  - 透明 / 沉浸态 Header
- Header 需要支持以下右侧操作状态：
  - 右侧单 icon
  - 右侧双 icon
  - 右侧单文案
  - 右侧无操作
- Header 需要支持无标题状态。

## 9. AI 使用规则

- 非首页页面优先使用通用内页 Header。
- 首页优先使用首页 Header 变体。
- 需要返回时优先使用左侧返回 icon，不生成自定义返回样式。
- 需要关闭场景时，只有在业务特别说明下才替换为关闭按钮。
- 右侧操作默认理解为次级功能，不升级为主操作。
- Header 返回与页面内容区中的 Button 返回分开理解，不混用。

## 10. 禁止项

- 不要新增副标题结构。
- 不要在 Header 中同时放右侧文案和右侧 icon。
- 不要使用 icon 加文案的左侧返回形式。
- 不要临时修改 Header 高度。
- 不要将 Header 返回和 Button 返回混为同一规则。
