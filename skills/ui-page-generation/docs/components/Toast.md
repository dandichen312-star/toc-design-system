# Toast 轻提示

## 1. 用途

Toast 用于在不打断当前流程的前提下，向用户反馈一次性的操作结果或简短信息。

Toast 不承载复杂内容，不承载长文案，不承载多步骤操作，也不用于需要用户决策的场景。

## 2. 类型

```txt
message：纯文本内容提示。
result-info：普通操作完成、成功反馈或信息反馈。
result-warning：警告、风险提示、阻断性错误。
loading：加载中、提交中、处理中。
```

本项目不单独定义 success Toast。普通成功、完成或通过反馈统一归入 `result-info`。

## 3. 内容结构

```txt
message:
  text

result-info:
  icon + text

result-warning:
  icon + text

loading:
  loading-icon + text
```

规则：

- `message` 只展示文本。
- `result-info` / `result-warning` 必须展示图标和文本。
- `loading` 必须展示加载图标和文本。
- Toast 内不出现按钮、关闭图标、链接、表单。

## 4. 生命周期

```txt
message:
  duration: 2s
  long-text-duration: 3s

result-info:
  duration: 2s

result-warning:
  duration: 2s

loading:
  duration: manual
  close: 由业务状态主动关闭，或切换为 result-info / result-warning
```

规则：

- 同一时刻页面上只允许存在一个 Toast。
- 新 Toast 触发时，旧 Toast 必须立即关闭。
- `loading` 不自动关闭，必须由业务代码显式关闭。

## 5. 文案规则

- 文案应短，优先一行展示。
- 内容提示最多 2 行。
- 超过 2 行的内容必须改用 Modal / Popup 或结果页承载。
- `result-info` / `result-warning` 的图标反馈文案建议保持单行。

## 6. 定位规则

```txt
页面级触发：
  viewport center

弹窗内触发：
  modal container center

底部浮层内触发：
  sheet container center
```

规则：

- Toast 不挤压页面布局，使用浮层方式展示。
- 页面级 Toast 基于视口水平垂直居中。
- 弹窗内 Toast 基于弹窗容器水平垂直居中。
- 底部浮层内 Toast 基于底部浮层容器水平垂直居中。
- AI 执行时必须按容器尺寸计算中心点：`x = (containerWidth - toastWidth) / 2`，`y = (containerHeight - toastHeight) / 2`。
- 禁止写死 Toast 的 x / y 坐标。
- Toast 不接触刘海、Home Indicator 或安全区边界。

## 7. 尺寸与布局

```txt
message:
  min-width: 88px
  max-width: 242px
  min-height: 50px
  padding-x: 16px
  padding-y: 14px
  layout: horizontal center

result-info / result-warning / loading:
  width: 96px
  height: 96px
  padding: 14px
  layout: vertical center
  icon-size: 32px
  icon-text-gap: 8px
```

## 8. Token 使用

```txt
Toast 背景：color-bg-toast + opacity-80
Toast 文字：color-text-inverse
Toast 图标：color-icon-inverse
Toast 文字：text-body-md
Toast 圆角：radius-toast
Toast 阴影：shadow-none
Toast 遮罩：color-bg-mask（仅 loading 需要阻断操作时使用）
```

## 9. 图标资源

```txt
result-info:
  assets/icons/toast-info.svg

result-warning:
  assets/icons/toast-warning.svg

loading:
  assets/icons/toast-loading.svg
```

规则：

- 图标必须使用固定 SVG 资源。
- 图标颜色使用 `color-icon-inverse`。
- 不允许临时绘制或替换图标。

## 10. 动效规则

```txt
进场：opacity 0 → 1
出场：opacity 1 → 0
loading：图标顺时针匀速旋转
```

规则：

- Toast 进出场只使用透明度变化。
- 不使用位移、缩放或弹跳动效。
- `loading` 图标必须旋转，文字保持静止。
- Toast 隐藏时必须停止 loading 动画。

## 11. 决策规则

AI 生成 Toast 前必须先执行类型判断，不允许直接默认使用 `message`。

```txt
1. 判断是否需要用户确认或决策。
   - 需要决策：不用 Toast，改用 Modal / Popup。
   - 不需要决策：继续判断 Toast 类型。

2. 判断反馈类型。
   - 成功、完成、通过、已保存、已提交、已领取等正向结果反馈：result-info
   - 独立输入框的轻量输入结果错误：message
   - 风险、失败、校验不通过、网络异常、非阻断错误：result-warning
   - 处理中、加载中、提交中：loading
   - 跳转第三方页面、即将前往第三方页面、普通短文本提示：message

3. 判断触发容器。
   - 页面级触发：viewport center
   - 弹窗内触发：modal container center
   - 底部浮层内触发：sheet container center
```

常见场景：

```txt
成功 / 完成 / 正向结果：
  result-info

中性短提示：
  message

独立输入框轻量错误 / 输入结果错误：
  message

跳转第三方页面 / 即将前往第三方页面：
  message

风险 / 错误 / 异常 / 校验失败：
  result-warning

处理中 / 加载中 / 提交中：
  loading
```

## 12. 禁止项

- 不要在 Toast 内放按钮、关闭图标、跳转链接、表单。
- 不要让 Toast 文案超过 2 行。
- 不要用 Toast 承载需要用户决策的内容。
- 不要让 Toast 与强弹窗争抢层级。
- 不要给 Toast 添加阴影。
- 不要使用除 `color-bg-toast` 以外的容器背景色。
- 不要把 `loading` 做成位移、缩放、闪烁动效。
- 不要硬编码颜色、字号、圆角、阴影或遮罩值。
- 不要硬编码 Toast 坐标。
