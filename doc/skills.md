# Claude Code Skills

本文档详细介绍 Claude Code Skills（技能）的概念和使用方法。

## 什么是 Skills

Skills（技能）是 Claude Code 的可复用功能模块，定义了一组特定的任务或行为模式。Skills 可以包含：
- 具体的任务执行步骤
- 模板化的输出格式
- 特定场景的处理逻辑

## Skill 定义规范

### 文件位置

- 项目级：`{项目}/.claude/skills/{skill-name}/SKILL.md`
- 全局级：`~/.claude/skills/{skill-name}/SKILL.md`

### 文件结构

```yaml
---
name: skill名称
description: 简短描述
version: 1.0.0
trigger: "触发条件（可选）"
---

# Skill 标题

Skill 详细说明...

## 功能说明

描述这个 skill 能做什么...

## 使用方法

```bash
# 使用方式
```

## 示例

### 示例 1

...
```

### frontmatter 字段说明

| 字段 | 必填 | 说明 | 示例 |
|------|------|------|------|
| name | 是 | 技能名称，使用 kebab-case | `demo-task` |
| description | 是 | 简短描述，50字以内 | `任务型 skill 示例` |
| version | 是 | 语义化版本号 | `1.0.0` |
| trigger | 否 | 触发条件，支持正则 | `"用户请求演示任务"` |

## 使用 Skills

### 方式一：使用 Skill 工具

```python
Skill({
  skill: "demo-task",
  args: "README.md"
})
```

### 方式二：在对话中调用

```
# 使用斜杠命令
/demo-task

# 或者直接说明
请使用 demo-task skill 处理这个文件
```

### 方式三：自动触发

如果 skill 定义了 trigger，当用户输入匹配时会自动执行。

## 项目级 Skills

项目级 Skills 只在当前项目目录下可用。

### 创建示例

```
my-project/
├── .claude/
│   └── skills/
│       ├── demo-reference/
│       │   └── SKILL.md
│       └── demo-task/
│           └── SKILL.md
├── src/
└── package.json
```

### 使用范围

- 只在 `my-project` 目录下有效
- 切换到其他项目后不可见

## 全局 Skills

全局 Skills 在所有项目目录下都可用。

### 创建位置

- Windows: `C:\Users\{用户名}\.claude\skills\`
- macOS/Linux: `~/.claude/skills/`

### 使用范围

- 所有项目目录都可见
- 跨项目复用

### 查看全局 Skills

```bash
claude --skills
# 输出所有可用的 skills，包括项目级和全局级
```

## Skill 触发模式

### 手动触发

- 输入 `/skill-name`
- 使用 Skill 工具调用

### 自动触发

在 frontmatter 中定义 trigger：
```yaml
---
trigger: "用户请求审查"
---
```
当用户输入匹配 trigger 时自动执行。

## Skill 使用场景

| 场景 | 推荐操作 |
|------|----------|
| 复用任务模板 | 创建 Skill |
| 规范化输出 | 在 Skill 中定义格式 |
| 自动化流程 | 设置 trigger 自动触发 |
| 团队共享 | 放在项目级 `.claude/skills/` |
| 个人工具 | 放在全局 `~/.claude/skills/` |