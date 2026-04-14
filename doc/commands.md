# Claude Code 常用命令

本文档详细介绍 Claude Code 的常用命令。

## 对话启动命令

```bash
# 启动交互式对话
claude

# 初始化新项目（创建 CLAUDE.md）
claude --init
claude --init /path/to/project

# 指定模型启动
claude --model sonnet
claude --model haiku
claude --model opus

# 指定项目目录
claude --project /path/to/project

# 指定项目并启动对话
claude /path/to/project
```

**模型说明：**

| 模型 | 特点 | 适用场景 |
|------|------|----------|
| haiku | 最快速、最便宜 | 简单任务、日常对话 |
| sonnet | 平衡（推荐默认） | 大多数开发任务 |
| opus | 最强能力 | 复杂推理、深度分析 |

## 交互模式命令

在 Claude Code 交互模式中可直接使用的命令：

| 命令 | 简写 | 说明 |
|------|------|------|
| `quit` | `q` | 退出对话 |
| `exit` | `e` | 退出对话 |
| `compact` | `c` | 压缩上下文，减少 token 使用 |
| `resume` | `r` | 从对话摘要恢复完整上下文 |
| `tokens` | `t` | 查看当前 token 使用情况 |
| `context` | - | 查看上下文详细消耗 |
| `status` | - | 查看当前会话状态 |
| `cost` | - | 查看本次会话花费 |
| `rewind` | - | 返回上一轮对话 |
| `doctor` | - | 检查配置和环境问题 |
| `help` | `h` | 显示所有可用命令 |
| `clear` | - | 清屏 |

**compact 命令：**
```
> compact
# Claude 会压缩当前对话内容为摘要，释放上下文空间
# 适用于长对话后需要继续深入讨论的场景
```

**resume 命令：**
```
> resume
# 从压缩后的摘要恢复完整对话历史
# 需要先执行过 compact 才能使用
```

**tokens 命令：**
```
> tokens
# 输出示例：
# Input tokens: 12,345
# Output tokens: 8,901
# Total: 21,246
```

**context 命令：**
```
> context
# 输出当前上下文的详细消耗信息
# 包括：
# - 当前使用的模型
# - Tokens 总使用量及百分比
# - 分类统计（System prompt, System tools, Custom agents, Memory files, Skills, Messages, Free space, Autocompact buffer）
# - Custom Agents 详细列表及各自 token 消耗
# - Memory Files 详细列表
# - Skills 详细列表及 token 消耗
```

**status 命令：**
```
> status
# 输出当前会话状态：
# - 当前模型
# - 项目目录
# - 已用 token 数量
# - 对话轮数
```

**cost 命令：**
```
> cost
# 输出本次会话的费用统计：
# - Input/Output token 数量
# - 预计费用（基于当前模型定价）
```

**rewind 命令：**
```
> rew
# 返回上一轮对话，撤销最后一次 AI 响应
# 可用于重新生成更好的回答
```

**doctor 命令：**
```
> doctor
# 检查并报告配置问题：
# - API Key 是否有效
# - 网络连接状态
# - 配置文件完整性
# - 插件状态
```

## 命令行参数

```bash
# 常用参数
claude --version              # 查看版本
claude --help                 # 查看帮助

# 模型参数
claude --model sonnet         # 指定模型
claude --model haiku          # 使用轻量模型
claude --model opus           # 使用最强模型

# 思考模式
claude --think                # 启用思考模式
claude --no-think             # 禁用思考模式

# 系统提示
claude --system "你是一个专业的Python开发者"

# 项目参数
claude --project /path/to/project
claude /path/to/project       # 快捷方式

# 输出格式
claude --verbose              # 详细输出
claude --json                 # JSON 输出（适用于脚本）

# 其他
claude --print-only           # 只打印不交互
```

## 配置命令

```bash
# 查看配置
claude config list            # 列出所有配置
claude config get <key>      # 获取单个配置

# 设置配置
claude config set model sonnet
claude config set temperature 0.7

# 删除配置
claude config unset <key>

# 常用配置项
claude config set model sonnet           # 默认模型
claude config set temperature 0.7       # 采样温度
claude config set max_tokens 4096        # 最大输出 token
```

## 命令使用场景

| 场景 | 推荐命令 |
|------|----------|
| 日常开发对话 | `claude` |
| 复杂任务规划 | `claude --think` |
| 快速简单任务 | `claude --model haiku` |
| 深度分析 | `claude --model opus` |
| 长对话压缩 | 交互模式输入 `compact` |