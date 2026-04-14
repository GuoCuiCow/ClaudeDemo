---
name: demo-reference
description: 参考型skill示例 - 展示skill定义的规范和最佳实践
version: 1.0.0
trigger: "用户请求查看skill定义示例或参考规范"
---

# 参考型 Skill 示例

这是一个参考型skill，用于向同事演示如何正确定义Claude Code的skill。

## Skill 定义规范

### Frontmatter 元数据

每个skill必须包含以下frontmatter字段：

```yaml
---
name: skill名称
description: 简短描述 - 用户在技能列表中看到的文字
version: 1.0.0
trigger: "触发条件 - 可选，用于自动触发"
---
```

### 字段说明

| 字段 | 必填 | 说明 |
|------|------|------|
| name | 是 | 技能名称，使用kebab-case |
| description | 是 | 一句话描述，控制在50字以内 |
| version | 是 | 语义化版本号 |
| trigger | 否 | 触发条件，支持正则匹配 |

## 内容结构

1. **开头** - 简要说明这个skill的用途
2. **主体** - 详细说明规则、步骤或规范
3. **示例** - 提供具体的使用示例
4. **注意事项** - 说明边界情况和注意点

## 命名规范

- 文件名: `kebab-case.md`
- 内部标题: 中文描述，使用 `#` 或 `##`
- 代码块: 使用适当的语言标识符

## 使用方式

```bash
# 查看可用skills
claude --skills

# 使用skill
/skill-name
# 或
Skill({ skill: "skill-name" })
```

## 触发模式

- **手动触发**: 用户输入 `/skill-name` 或通过Skill工具调用
- **自动触发**: 当trigger匹配用户输入时自动执行

> 提示: 参考型skill通常作为模板或规范文档，不执行具体任务。