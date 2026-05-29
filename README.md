# toc-design-system
金融信贷产品 UI 设计规范库，包含组件规则、页面结构指南及 AI 生成约束。

## Cursor Skill 安装

运行下面命令安装到本机 Cursor skills 目录：

```bash
git clone https://github.com/dandichen312-star/toc-design-system.git ~/.cursor/skills/toc-design-system
```

安装后，Cursor Agent 在处理金融信贷产品 Mobile / H5 页面、Figma 页面生成、设计规范、组件规则时，可以使用这个 skill。

如果要让「新建/重做业务页面前必须先需求梳理」在项目中自动生效，还需要把仓库内规则复制到目标项目：

```bash
mkdir -p .cursor/rules
cp ~/.cursor/skills/toc-design-system/rules/design-prerequisite-gate.mdc .cursor/rules/
```

## 手动更新

如果仓库有新版本，使用下面命令更新：

```bash
git -C ~/.cursor/skills/toc-design-system pull --ff-only
```

## 自动更新

macOS / Linux 可以用定时任务自动拉取更新。打开终端运行：

```bash
(crontab -l 2>/dev/null; echo "*/30 * * * * git -C \"$HOME/.cursor/skills/toc-design-system\" pull --ff-only >/tmp/toc-design-system-skill-update.log 2>&1") | crontab -
```

这会每 30 分钟自动更新一次。

## 目录说明

```text
SKILL.md
rules/
  design-prerequisite-gate.mdc
skills/requirements-analysis/
  SKILL.md
  QUESTION_BANK.md
  OUTPUT_TEMPLATE.md
  examples.md
skills/ui-page-generation/
  DESIGN_TOKENS.md
  theme-presets.md
  theme-scope.md
  PAGE_RULES.md
  COMPONENT_RULES.md
  docs/components/
  assets/icons/
```

`SKILL.md` 是 Cursor 识别 skill 的入口文件；`skills/requirements-analysis/` 存放需求澄清、问答题库和 PRD 模板；`skills/ui-page-generation/` 存放具体设计规范、主题规则、组件规则和图标资源；`rules/design-prerequisite-gate.mdc` 用于项目级前置门禁。
