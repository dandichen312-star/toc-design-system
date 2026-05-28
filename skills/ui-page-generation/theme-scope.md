# Theme Scope 主题作用范围

## 1. 文档用途

本文件用于定义主题在页面生成中的作用范围，说明哪些组件或模块会受主题影响，哪些不会受主题影响，以及 AI 在页面生成时如何判断当前模块应读取哪一类主题。

本文件只负责：

- 定义 `brand theme` 的作用范围。
- 定义 `scene theme` 的作用范围。
- 定义不参与换肤的固定语义范围。
- 定义主题作用的优先读取规则。

本文件不负责：

- 不定义具体颜色值。
- 不定义具体 theme preset 内容。
- 不新增 token。
- 不重写组件样式。
- 不替代 `Button.md`、`Card.md`、`Header.md` 等组件文档。

---

## 2. Brand Theme 影响范围

`brand theme` 用于全局品牌相关换色。

### 2.1 总原则

- 不按“整个组件整体换色”理解主题切换。
- 组件内部凡是绑定了主题色相关 token 的部位，跟随当前 `brand theme` 变化。
- 未绑定主题色相关 token 的部位，不参与主题变化。
- 特殊态如果不涉及主题色，不写入主题规则。

### 2.2 总清单

`brand theme` 可影响的典型部位包括：

- `Button` 中使用主题色 token 的部位。
- `Tabs` 中使用主题色 token 的部位。
- `Tag` 中使用主题色 token 的部位。
- 使用主题色 token 的图标。
- 链接文案。
- 选中态文字。
- 选中态描边。
- 选中态指示器。
- 品牌浅底。
- 品牌渐变。

### 2.3 组件范围说明

#### Button

- `Button` 内凡是使用主题色相关 token 的部位，跟随当前主题变化。
- `Button` 内未使用主题色 token 的部位，不变。

#### Tabs

- `Tabs` 内凡是使用主题色相关 token 的部位，跟随当前主题变化。
- `Tabs` 内未使用主题色 token 的部位，不变。

#### Tag

- `Tag` 内凡是使用主题色相关 token 的部位，跟随当前主题变化。
- `Tag` 中非 `brand` 语义不变。

#### Icon

- 所有组件中的图标，只要绑定的是主题色 token，就跟随当前主题变化。
- 未绑定主题色 token 的图标不变。

#### Card

- `Card` 容器本身不默认跟主题变化。
- `Card` 内只有绑定了主题色相关 token 的内容才变化。

#### Header

- `Header` 容器本身不因主题自动换色。
- `Header` 内凡是使用主题色相关 token 的部位，跟随当前主题变化。

#### Notice

- `Notice` 单独特判。
- `info / warning / danger` 语义部分固定不变。
- `Notice` 本体不因主题自动整体换色。
- 只有其中明确使用 `brand token` 的链接、操作文案、品牌操作图标，才跟随主题变化。

---

## 3. Scene Theme 影响范围

`scene theme` 用于模块级场景主题，不用于整页主题。

### 3.1 总原则

- `scene theme` 只作用于显式声明的模块。
- `scene theme` 不作用于整页。
- `scene theme` 不因页面文案语义自动触发。
- `scene theme` 不影响未声明模块。

### 3.2 典型模块清单

#### member-module

- 会员卡。
- 会员权益区。
- 会员 banner。
- 会员专属按钮区。

#### activity-module

- 活动 banner。
- 活动权益卡。
- 活动入口卡。
- 活动说明区。

---

## 4. 不参与换肤范围

以下固定语义不参与 `brand theme` 或 `scene theme` 切换：

- `highlight`
- `info`
- `warning`
- `danger`
- `neutral`

规则：

- 只要某个部位绑定的是以上固定语义 token，就不参与主题切换。

---

## 5. 主题作用优先读取规则

1. 先判断当前模块是否显式声明 `scene theme`。
2. 有则该模块优先使用 `scene theme`。
3. 无则使用全局 `brand theme`。
4. 未显式声明 `scene theme` 的模块，不回退到任何 `scene theme`。
5. 不允许仅因“会员 / VIP / 活动 / 权益”等文案语义，就自动启用 `scene theme`。
6. 修改 `brand theme` 时，不自动修改任何 `scene theme`。
7. 修改 `scene theme` 时，不自动修改全局 `brand theme`。
8. 哪条主题要变，必须由人工明确说明。
9. AI 不允许联动修改另一条主题。

---

## 6. AI 使用规则

- AI 先读取本文件，判断当前模块是否处于 `brand theme` 或 `scene theme` 作用范围内。
- AI 不要把“组件支持主题色”理解为“页面必须出现该组件”。
- AI 不要因为模块文案像会员区、活动区，就自动附加 `scene theme`。
- AI 只在模块已显式声明 `scene theme` 时，才切换该模块的 `brand` 映射来源。
- AI 不要修改固定语义色的使用方式。
