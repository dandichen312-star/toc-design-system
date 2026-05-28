# Notice 公告提示

## 1. 用途

Notice 用于公告、通知、公共条、信息提示、风险提示等短信息展示。

Notice 只表达提示信息，不承载复杂表单或多步骤操作。

## 2. 类型

```txt
info
warning
danger
```

## 3. 状态

```txt
default
closable
link
```

## 4. Token 使用

```txt
信息提示文字或图标：color-info-500
警告提示文字或图标：color-warning-500
危险提示文字或图标：color-danger-500
正文文字：text-body-sm
链接文字：color-text-brand
背景色：使用页面已有浅色背景或品牌浅色背景
圆角：radius-card 或 radius-8
```

## 5. 内容规则

- 文案应短，表达明确。
- Notice 正文默认限制为 `1` 行。
- Notice 正文不允许自动换行撑高公告条。
- 未超出可用宽度时，正文静态展示，不播放、不滚动。
- 超出可用宽度时，正文使用横向滚动播放，左侧图标、右侧关闭或跳转操作保持固定。
- 横向滚动方向默认为从右向左。
- 横向滚动速度必须符合人眼阅读效率，不允许使用跑马灯式快速滚动。
- 中文公告推荐阅读速度为 `4-6` 个汉字 / 秒，折算为视觉速度约 `32-40px/s`。
- 单轮滚动时长不低于 `8s`，滚动首尾停顿各 `1s`。
- 循环播放时，上一轮文案末尾与下一轮文案开头之间保留 `spacing-32`。
- 如果系统开启减少动态效果，超长公告降级为单行省略，并提供点击查看详情。
- 需要跳转时使用 `link` 状态。
- 可关闭公告使用 `closable` 状态。
- 风险类提示必须避免弱化严重性。

```txt
notice-text:
  max-lines: 1
  white-space: nowrap
  overflow: hidden

notice-marquee:
  trigger: text-width > available-width
  direction: right-to-left
  speed: 32-40px/s
  min-duration: 8s
  start-delay: 1s
  end-delay: 1s
  loop-gap: spacing-32
```

## 6. AI 使用规则

- 普通公告、通知、公共条使用 `info`。
- 本项目公告提示不使用绿色成功色。
- 风险、还款、逾期、扣费等重要提醒根据严重程度使用 `warning` 或 `danger`。
- 可跳转公告使用 `link` 状态。
- 可关闭公告使用 `closable` 状态。
- 不允许单独创造公告条专属颜色 token。
- 不允许使用 `success` 表示公告或成功提示。
- 不允许因为公告文案过长而临时增加 Notice 高度。
- 不允许让滚动正文带动图标、关闭按钮或跳转操作一起滚动。
