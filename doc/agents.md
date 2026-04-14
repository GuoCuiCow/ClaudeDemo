# Claude Code 子 Agent

本文档详细介绍 Claude Code 子 Agent 的概念和使用方法。

## 什么是子 Agent

子 Agent（子代理）是 Claude Code 中的独立 AI 代理，专门用于处理特定类型的任务。调用子 Agent 时，会启动一个专门的 AI 来处理该任务，完成后将结果返回给主对话。

## 系统内置子 Agent

Claude Code 内置了多个专业子 Agent：

| Agent 名称 | 用途 | 触发场景 |
|------------|------|----------|
| planner | 实现规划 | 复杂功能实现、架构设计 |
| architect | 系统设计 | 架构决策、技术选型 |
| tdd-guide | TDD 开发指导 | 新功能开发、Bug 修复 |
| code-reviewer | 代码审查 | 代码编写完成后 |
| security-reviewer | 安全分析 | 涉及安全的功能 |
| build-error-resolver | 构建错误修复 | 构建失败时 |
| e2e-runner | 端到端测试 | 关键用户流程测试 |
| refactor-cleaner | 重构清理 | 代码维护 |
| doc-updater | 文档更新 | 文档相关任务 |
| rust-reviewer | Rust 代码审查 | Rust 项目 |
| go-reviewer | Go 代码审查 | Go 项目 |
| python-reviewer | Python 代码审查 | Python 项目 |

## 自定义子 Agent

可以在项目中创建自定义子 Agent。

### 创建位置

- 项目级：`{项目}/.claude/agents/{agent-name}.md`
- 全局级：`~/.claude/agents/{agent-name}.md`

### Agent 文件结构

```yaml
---
name: doc-reviewer
description: 文档审查 agent
version: 1.0.0
model: sonnet
---

# Agent 说明

这里描述 agent 的用途和功能。

## 功能

1. 功能一描述
2. 功能二描述

## 使用方法

调用这个 agent 进行文档审查
```

### frontmatter 字段说明

| 字段 | 必填 | 说明 | 示例 |
|------|------|------|------|
| name | 是 | Agent 名称 | `doc-reviewer` |
| description | 是 | 简短描述 | `文档审查 agent` |
| version | 是 | 语义化版本号 | `1.0.0` |
| model | 否 | 使用的模型 | `sonnet`, `haiku`, `MiniMax-M2.5` |

## 使用子 Agent

### 方式一：使用 Agent 工具

```python
Agent({
  description: "审查代码",
  prompt: "请审查 src/auth/login.ts 文件的安全性问题",
  subagent_type: "security-reviewer"
})
```

### 方式二：在对话中提及

```
# 直接说明需要
请使用 code-reviewer 审查这个文件

# 或者
我需要安全审查，帮我看看这段代码
```

### 方式三：通过 Skills 触发

创建带有 trigger 的 agent，当用户输入匹配时自动触发。

## 子 Agent 使用场景

| 任务类型 | 推荐 Agent |
|----------|------------|
| 新功能规划 | planner |
| 架构设计 | architect |
| 写代码前测试 | tdd-guide |
| 代码审查 | code-reviewer |
| 安全审查 | security-reviewer |
| 构建问题 | build-error-resolver |