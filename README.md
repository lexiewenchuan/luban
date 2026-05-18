# Luban

目标是从零搭建一套可扩展、可配置、可观察、可长期维护的命令行 AI Agent 系统。

它不只是“调用一下大模型 API”，而是把 **模型适配、工具系统、记忆、上下文注入、子 Agent 编排、插件机制、会话管理、Tracing、国际化** 这些能力组织成一个完整框架。

---

## 项目定位

Luban 面向两类场景：

1. **学习型场景**：帮助开发者理解一个 Agent 系统由哪些核心模块组成
2. **工程型场景**：作为可扩展底座，用于继续迭代自己的 AI CLI / Agent 产品

这个项目的重点价值在于：
- 不只关注“模型回答”
- 更关注 **Agent 如何调用工具、管理上下文、保存记忆、拆分任务、持续运行**

---

### 1. 完整的 Agent 架构拆分
多个层次：
- 模型层
- 工具层
- 记忆层
- 上下文层
- 编排层
- 插件层
- 会话层
- 仪表盘 / CLI 层

### 2. 工程能力
- 支持多模型供应商接入
- 支持工具调用与 MCP 兼容
- 支持子 Agent 派发
- 支持长期记忆与上下文压缩
- 支持 tracing 与审计日志
- 支持中英文双语 CLI

---

## 核心功能

### 多模型适配
- 基于 LiteLLM + httpx 双模式
- 支持 Anthropic、OpenAI、本地模型及自定义代理
- 支持 Extended Thinking 等模式扩展

### 工具系统
- 提供一批内置工具：文件、Shell、搜索、Web、任务、记忆、会话、自查等
- 支持 MCP 协议兼容
- 可作为真正可执行的 Agent，而非纯聊天机器人

### 记忆管理
- 短期对话历史管理
- 长上下文压缩
- 长期结构化记忆（用户画像 / 事实 / 教训）
- 为“多轮持续协作”提供基础

### 上下文注入
- 支持 `soul.md`、`agents.md`、`memory.md`、Skills 等文件注入
- 支持热更新
- 方便做人格、规则、知识与工作流定制

### 子 Agent 编排
- 支持 `spawn_agent` / `resume_agent`
- 可将任务拆给隔离子 Agent 执行
- 适合复杂任务、多步骤执行与并行工作流

### 插件与扩展能力
- 通过目录扫描加载插件
- 支持 hook 机制
- 可扩展 tracing、日志、外部平台集成等能力

### 可观测性
- Tracing 仪表盘
- 审计日志
- 会话持久化
- 对 Agent 运行过程更容易调试与分析

---

## 技术栈

- **语言**：Python 3.11+
- **模型接入**：LiteLLM、httpx
- **协议 / 工具生态**：MCP
- **配置系统**：Pydantic v2 + TOML
- **终端交互**：Rich + prompt_toolkit
- **文件监听**：watchdog
- **重试机制**：tenacity
- **测试 / 代码质量**：pytest、ruff

---

## 项目结构

```text
luban/
├── src/agentkit/
│   ├── cli/             # CLI 入口、命令系统、交互层
│   ├── config/          # 配置模型与 TOML 读写
│   ├── context/         # 上下文文件加载与热更新
│   ├── memory/          # 短期/长期记忆与压缩
│   ├── model/           # LLM 客户端与模型适配
│   ├── orchestration/   # Agent Loop 与子 Agent 编排
│   ├── plugins/         # 插件机制
│   ├── session/         # 会话管理
│   ├── skills/          # Skills 加载与管理
│   ├── tools/           # 内置工具系统
│   ├── tracing/         # Tracing / Span
│   ├── dashboard/       # 本地仪表盘
│   ├── audit.py         # 审计日志
│   └── cleanup.py       # 数据清理
├── tests/               # 单元测试
├── examples/            # 插件示例
├── PRD.md               # 产品与实现设计文档
├── README.md
└── pyproject.toml
```

---

## 我在这个项目里体现的能力

这个项目适合从以下角度评估我：

- **系统设计**：是否能把复杂 Agent 系统分层设计清楚
- **Python 工程化**：是否有规范的目录结构、配置、测试与依赖管理
- **AI 应用理解**：是否理解模型、工具、上下文、记忆、编排之间的关系
- **可维护性设计**：是否提前考虑日志、追踪、插件、国际化、工作空间隔离
- **产品意识**：不仅写底层，还考虑 CLI 使用体验和首次配置流程

---

## 快速开始

### 安装

```bash
git clone https://github.com/lexiewenchuan/luban.git
cd luban

python -m venv .venv
source .venv/bin/activate
pip install -e ".[dev]"
```

### 运行

```bash
luban
```

首次运行会进入向导，引导你配置：
- 语言
- 模型供应商与 API Key
- Base URL
- 搜索引擎
- Embedding 模型（可选）

---

## 开发命令

```bash
pytest
ruff check src/
ruff format src/
```

---

---

## 相关文档

- `PRD.md`：产品设计与实现方案
- `examples/`：插件示例
- `tests/`：测试用例

---

## License

MIT

