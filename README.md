# Claude Code 快速入门指南

Claude Code 是 Anthropic 推出的官方 CLI 工具，用于与 Claude AI 助手交互。

## 目录

- [安装](#安装)
  - [安装 Git](#安装-git)
  - [安装 Node.js](#安装-nodejs)
  - [安装 Claude Code CLI](#安装-claude-code-cli)
  - [安装 ccSwitch](#安装-ccswitch)
  - [安装 VSCode](#安装-vscode)
  - [安装 Claude Code 插件](#安装-claude-code-插件)
  - [获得 API Key](#获得-api-key)
- [首次配置](#首次配置)
- [详细使用指南](#详细使用指南)
- [基础用法](#基础用法)
- [交互模式命令](#交互模式命令)
- [常用参数](#常用参数)
- [核心功能](#核心功能)
- [最佳实践](#最佳实践)
- [技能系统](#技能系统)
- [常见问题](#常见问题)

## 安装

### 安装 Git

Git 是版本控制工具，是开发必备的基础组件。

**官网地址：**
- 官网下载：https://git-scm.com/download/
- Windows 版：https://git-scm.com/download/win
- macOS 版：https://git-scm.com/download/mac
- 文档：https://git-scm.com/doc

```bash
# macOS (使用 Homebrew)
brew install git

# Windows
# 方法1: 官网下载 https://git-scm.com/download/win
# 方法2: 使用 winget
winget install Git.Git

# Linux (Ubuntu/Debian)
sudo apt update
sudo apt install git
```

安装完成后配置用户名和邮箱：
```bash
git config --global user.name "你的名字"
git config --global user.email "your@email.com"
```

### 安装 Node.js

Node.js 是 JavaScript 运行时，很多开发工具都基于 Node.js。

**官网地址：**
- 官网下载：https://nodejs.org/
- 文档：https://nodejs.org/docs/latest/
- nvm (Node 版本管理器)：https://github.com/nvm-sh/nvm
- nvm-windows：https://github.com/coreybutler/nvm-windows

```bash
# macOS (使用 nvm 推荐)
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.0/install.sh | bash
source ~/.bashrc
nvm install --lts
nvm use --lts

# Windows
# 方法1: 官网下载 https://nodejs.org/
# 方法2: 使用 winget
winget install OpenJS.NodeJS.LTS
# 方法3: 使用 nvm-windows
# 下载 https://github.com/coreybutler/nvm-windows/releases

# Linux (Ubuntu/Debian)
curl -fsSL https://deb.nodesource.com/setup_lts.x | sudo -E bash -
sudo apt install -y nodejs
```

验证安装：
```bash
node --version  # 应显示 v18.x.x 或更高
npm --version   # 应显示 8.x.x 或更高
```

### 安装 Claude Code CLI

Claude Code 是 Anthropic 官方 CLI 工具。

**官网地址：**
- 官网：https://docs.anthropic.com/en/docs/claude-code
- GitHub：https://github.com/anthropics/claude-code
- Releases 下载：https://github.com/anthropics/claude-code/releases

```bash
# macOS (使用 Homebrew)
brew install claude-code

# 或者通过 npm
npm install -g @anthropic-ai/claude-code

# Windows
winget install Anthropic.ClaudeCode

# Linux
# 方法1: npm
npm install -g @anthropic-ai/claude-code
# 方法2: 直接下载
# 从 https://github.com/anthropics/claude-code/releases 下载二进制文件
```

验证安装：
```bash
claude --version
```

### 安装 ccSwitch

ccSwitch 是一个 Claude Code 的辅助工具，可以帮助管理多个 Claude 配置。

**官网地址：**
- GitHub：https://github.com/anthropics/ccswitch
- npm 包：https://www.npmjs.com/package/ccswitch

```bash
# 通过 npm 全局安装
npm install -g ccswitch

# 或者从 GitHub 克隆
git clone https://github.com/anthropics/ccswitch.git
cd ccswitch
npm install
npm link
```

验证安装：
```bash
ccswitch --version
```

### 安装 VSCode

VSCode 是微软推出的免费代码编辑器，功能强大且插件丰富。

**官网地址：**
- 官网下载：https://code.visualstudio.com/
- 文档：https://code.visualstudio.com/docs
- 扩展市场：https://marketplace.visualstudio.com/

```bash
# macOS
# 方法1: 官网下载 https://code.visualstudio.com/
# 方法2: Homebrew
brew install --cask visual-studio-code

# Windows
winget install Microsoft.VisualStudioCode

# Linux
# Ubuntu/Debian
sudo apt install code
# 或从官网下载 .deb 包
```

### 安装 Claude Code 插件

在 VSCode 中安装 Claude Code 插件，获得更好的 IDE 集成体验。

**官网地址：**
- VSCode 扩展市场：https://marketplace.visualstudio.com/items?itemName=anthropic.claude-code
- Claude Code 插件文档：https://docs.anthropic.com/en/docs/claude-code/vscode

1. 打开 VSCode
2. 按 `Ctrl+P` (Windows/Linux) 或 `Cmd+P` (macOS)
3. 输入 `ext install anthropic.claude-code`
4. 按 Enter 安装
5. 安装完成后点击 "Reload" 重启 VSCode

或者在 VSCode 扩展商店搜索 "Claude Code" 并安装。

### 获得 API Key

API Key 是调用 Claude API 的凭证，需要从 Anthropic 官网获取。

**官网地址：**
- 控制台：https://console.anthropic.com/
- API Keys 页面：https://console.anthropic.com/keys
- 文档：https://docs.anthropic.com/en/docs/api

1. 访问 https://console.anthropic.com/
2. 注册账号或登录
3. 进入 "API Keys" 页面
4. 点击 "Create API Key" 创建新密钥
5. 复制并妥善保存密钥（只会显示一次）

> 注意：API Key 需要妥善保管，不要泄露给他人。使用 API 会产生费用。

## 首次配置

获得 API Key 后，可以通过以下两种方式配置 Claude Code。

### 方法一：直接配置

1. 安装完成后，运行 `claude` 命令
2. 系统会提示你登录或设置 API 密钥
3. 输入刚才获得的 API 密钥

首次配置建议设置常用选项：
```bash
# 设置默认模型
claude config set model sonnet

# 查看当前配置
claude config list
```

### 方法二：使用 ccSwitch 配置

ccSwitch 可以帮助管理多个 Claude 配置文件，方便切换不同的 API 配置。

**1. 初始化 ccSwitch**

```bash
ccswitch init
```

这会在 `~/.claude/` 目录下创建必要的配置文件。

**2. 添加配置文件**

```bash
# 添加新配置
ccswitch add

# 或指定配置名称
ccswitch add my-config
```

按照提示输入：
- 配置名称（如 `default`, `work`, `personal`）
- API Key
- 其他可选配置（模型、Base URL 等）

**3. 查看配置列表**

```bash
ccswitch list
```

输出示例：
```
default   (active)
work
personal
```

**4. 切换配置**

```bash
# 切换到指定配置
ccswitch switch work

# 查看当前配置
ccswitch current
```

**5. 删除配置**

```bash
ccswitch remove work
```

**配置文件位置**

ccSwitch 会在 `~/.claude/` 目录下创建多个配置文件：
- `settings.json` - 主配置文件
- `settings.{name}.json` - 各配置的独立文件

通过 ccSwitch，可以轻松在不同的 API 配置之间切换，方便演示或使用不同的 API Key。

## 详细使用指南

详细使用说明请参考 doc 目录下的专项文档：

- **[doc/commands.md](doc/commands.md)** - 常用命令：对话启动、交互模式、命令行参数、配置命令
- **[doc/agents.md](doc/agents.md)** - 子 Agent：系统内置 Agent、自定义 Agent、使用方法
- **[doc/skills.md](doc/skills.md)** - Skills：Skill 定义规范、使用方法、项目级/全局 Skills

## 基础用法

### 启动对话

```bash
claude
# 或指定模型
claude --model sonnet

# 使用 haiku 模型（最便宜）
claude --model haiku

# 使用 opus 模型（最强）
claude --model opus
```

### 交互模式命令

- `quit` / `exit` - 退出对话
- `compact` - 压缩上下文，减少 token 使用
- `resume` - 从摘要恢复对话
- `tokens` - 查看当前 token 使用情况
- `help` - 查看所有可用命令

### 常用参数

```bash
# 指定模型 (haiku/sonnet/opus)
claude --model sonnet

# 启用思考模式
claude --think

# 设置系统提示
claude --system "你是一个专业程序员"

# 查看版本
claude --version

# 指定项目目录
claude --project /path/to/project

# 禁用思考模式
claude --no-think
```

## 核心功能

### 1. 文件操作

Claude Code 可以直接读取、编辑和创建文件：

- `Read` - 读取文件内容
- `Edit` - 编辑文件 (精确替换)
- `Write` - 创建/覆写文件
- `Glob` - 搜索文件
- `Grep` - 搜索文件内容

### 2. 执行命令

- `Bash` - 执行 shell 命令
- `Agent` - 启动子代理执行复杂任务

### 3. 记忆系统

- 自动保存对话摘要
- 支持持久化记忆 (通过 `Write` 工具保存到文件)
- 查看记忆: `claude --memory`

### 4. MCP 集成

支持多种 MCP (Model Context Protocol) 服务:
- 文件系统操作
- 数据库连接
- API 集成
- 等等

配置 MCP: 编辑 `~/.claude/settings.json`

## 最佳实践

### 项目工作流

1. **先 research**: 使用 Agent 探索代码库
2. **规划**: 使用 planner agent 规划实现
3. **TDD**: 使用 tdd-guide agent 开发
4. **review**: 使用 code-reviewer agent 审查

### 上下文管理

- 定期使用 `compact` 压缩上下文
- 大项目使用 plan mode 规划
- 关键信息保存到记忆文件

### 权限控制

在 `~/.claude/settings.json` 中配置:
- `allowedTools` - 允许的工具
- `autoApprove` - 自动批准的工具

## 技能系统

Claude Code 支持自定义技能 (skills):

```bash
# 查看可用技能
claude --skills

# 使用技能
/claude-code:docs
```

### 创建自定义技能

在项目根目录创建 `.claude/skills/` 目录，添加 skill 定义文件。

详细规范请参考 [.claude/skills/demo-reference/SKILL.md](.claude/skills/demo-reference/SKILL.md)

## 常见问题

**Q: 如何跳过确认?**
A: 设置 `autoApproveTools` 或使用 `--dangerously-auto-approve` (谨慎使用)

**Q: 如何使用特定项目?**
A: `claude --project /path/to/project`

**Q: API 费用如何?**
A: 按 token 计费，Haiku 最便宜，Opus 最贵

**Q: 提示配额不足怎么办?**
A: 使用 `compact` 命令压缩上下文，或开启新对话

**Q: 如何切换模型?**
A: 使用 `--model` 参数指定，或在配置中设置默认模型

## 相关资源

- 官方文档: https://docs.anthropic.com/en/docs/claude-code
- API 文档: https://docs.anthropic.com/en/docs/api
- GitHub: https://github.com/anthropics/claude-code