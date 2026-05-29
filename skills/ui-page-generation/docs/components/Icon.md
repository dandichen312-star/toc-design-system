# Icon 图标

## 1. 用途与边界

Icon 用于表达操作、状态、说明和导航含义，例如信息提示、进入下一步、清除、编辑、拍摄、搜索、密码显隐等。

Icon 只定义图标资源、尺寸、颜色和风格。图标所在组件的点击区域、布局位置和交互行为由对应组件定义。

## 2. 风格

```txt
style: outline
viewBox: 24x24
stroke-width: 1.5px
stroke-linecap: round
stroke-linejoin: round
fill: none
color: currentColor
```

规则：

- 默认使用线性 outline 图标。
- 同一组件内图标必须使用同一风格。
- 不允许用文字字符临时替代图标。
- 不允许在组件中临时手动画图标。

## 3. 尺寸

```txt
icon-sm: 12px
icon-md: 16px
icon-lg: 20px
touch-area: 24px
```

规则：

- 表单输入框内普通 suffix 图标默认使用 `icon-md / 16px`。
- 关闭按钮等轻量操作可使用 `icon-sm / 12px`，点击区域仍由组件定义。
- 图标点击区域不得小于组件规则声明的尺寸。

## 4. 颜色

```txt
default: color-icon-tertiary
brand: color-text-brand
inverse: color-icon-inverse
```

规则：

- 弱图标、辅助图标使用 `color-icon-tertiary`。
- 可点击品牌操作图标使用 `color-text-brand`。
- 深色背景上的图标使用 `color-icon-inverse`。

## 5. 基础图标资源

```txt
info: assets/icons/icon-info.svg
arrow-right: assets/icons/icon-arrow-right.svg
back: assets/icons/icon-back.svg
clear: assets/icons/icon-clear.svg
edit: assets/icons/icon-edit.svg
camera: assets/icons/icon-camera.svg
search: assets/icons/icon-search.svg
eye: assets/icons/icon-eye.svg
eye-off: assets/icons/icon-eye-off.svg
close: assets/icons/icon-close.svg
check: assets/icons/icon-check.svg
message: assets/icons/icon-message.svg
```

## 5.1 页面与组件扩展图标

```txt
tab-home: assets/icons/icon-tab-home.svg
tab-home-active: assets/icons/icon-tab-home-active.svg
tab-account: assets/icons/icon-tab-account.svg
tab-account-active: assets/icons/icon-tab-account-active.svg
status-waiting: assets/icons/icon-status-waiting.svg
status-success: assets/icons/icon-status-success.svg
status-fail: assets/icons/icon-status-fail.svg
checkbox-default: assets/icons/icon-checkbox-default.svg
checkbox-selected: assets/icons/icon-checkbox-selected.svg
task-auth: assets/icons/icon-task-auth.svg
task-profile: assets/icons/icon-task-profile.svg
card-task-default: assets/icons/card-task-default.svg
benefit-limit: assets/icons/icon-benefit-limit.svg
benefit-coupon: assets/icons/icon-benefit-coupon.svg
product-default: assets/icons/icon-product-default.svg
toast-info: assets/icons/toast-info.svg
toast-warning: assets/icons/toast-warning.svg
toast-loading: assets/icons/toast-loading.svg
```

## 5.2 品牌与业务扩展图标

```txt
home-brand-logo: assets/icons/home-brand-logo.svg
address: assets/icons/icon-address.svg
customer-service: assets/icons/icon-customer-servic.svg
notice-bar-default: assets/icons/icon-notice-bar-default.svg
notice-bar-default-alt: assets/icons/icon-notice-bar-default-1.svg
```

规则：

- `home-brand-logo` 用于首页 Header / 额度主卡等品牌 logo 位；尺寸由页面模块决定，不强制 24×24。
- `icon-customer-servic` 为历史文件名（缺 e），引用时保持文件名不变。
- Notice 条图标优先 `icon-notice-bar-default`；设计稿双态时可使用 `-1` 变体。

## 5.3 空状态插图图标

```txt
empty-network: assets/icons/icon-empty-network.svg
empty-notice: assets/icons/icon-empty-notice.svg
empty-bankcard: assets/icons/icon-empty-bankcard.svg
empty-coupon: assets/icons/icon-empty-coupon.svg
empty-cardpackage: assets/icons/icon-empty-cardpackage.svg
empty-loan-record: assets/icons/icon-empty-loan-record.svg
```

规则：

- 空状态 icon 用于 `result-page` / `list-page` 空态区，尺寸通常大于 24px，由页面空态布局决定。
- 空状态 icon 可使用 fill / 渐变，不强制 outline 24×24 规范；仍须来自 `assets/icons/`。

## 6. AI 使用规则

- 生成组件前，先检查是否需要图标。
- 需要图标时，必须优先引用 `assets/icons/` 中已有 SVG。
- 如果缺少图标，只记录 icon 缺口，不临时绘制。
- 组件文档只声明图标语义，例如 `suffix: camera`，不要复制 SVG path。
- SVG 必须使用 `currentColor`，颜色由组件 token 控制。
