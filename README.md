# AutoLabMCP

<div align="center">

![Python](https://img.shields.io/badge/Python-3.12+-blue.svg)
![License](https://img.shields.io/badge/License-MIT-green.svg)
![FastMCP](https://img.shields.io/badge/FastMCP-0.1.0+-orange.svg)

</div>

### 致谢

- 2025·AI for Science Hackathon·上海站
- Lucien
- 上海交通大学

### 🚀 项目简介

AutoLabMCP 是一个基于 [Model Context Protocol (MCP)](https://modelcontextprotocol.io/) 的自进化动态工具系统，**主要面向Science的湿实验场景**。它能够让 AI Agent 根据实验需求自主创建设备驱动、实验流程编排，根源上免去一线科研人员的代码编写的困扰，实现真正的自动化实验的"自动化驱动"。

### ✨ 核心特性

- **🔧 动态工具加载**：实时监控工具目录，自动发现和加载新工具
- **🔒 环境隔离**：每个工具在独立的 Python 虚拟环境中运行，避免依赖冲突
- **⚡ 智能缓存**：只在工具调用时重新加载相关工具，提高性能
- **🔄 自动发现**：支持 GitHub 搜索和 AI 增强的网络搜索
- **📊 变更追踪**：实时检测工具变更并记录详细差异
- **🛡️ 错误隔离**：工具错误不会影响主服务器稳定性

### 🏗️ 系统架构

```mermaid
graph TB
    A[Lab AI Agent] --> B[Dynamic MCP Server]
    B --> C[Tool Loader]
    B --> D[Environment Manager]
    B --> E[Proxy Manager]
    B --> F[Change Manager]
    
    C --> G[tools/]
    D --> H[Virtual Environments]
    E --> I[Tool Proxies]
    F --> J[Change History]
    
    G --> K[Tool 1]
    G --> L[Tool 2]
    G --> M[Tool N...]
```

### 📦 安装

#### 前置要求
- Python 3.12+
- pip

#### 安装依赖
```bash
pip install -r requirements.txt
```

#### 配置设置
编辑 `config.json` 文件：
```json
{
    "openai": {
        "api_key": "your-openai-api-key",
        "base_url": "https://api.openai.com/v1/"
    },
    "agent": {
        "api_key": "",
        "base_url": "https://api.anthropic.com",
        "model": "claude-sonnet-4-20250514"
    }
}
```

### 🚀 快速开始

#### 1. 启动 Playwright MCP 服务器（终端 1）
需要安装nodejs
```bash
npx @playwright/mcp@latest --port 8931
```

#### 2. 启动动态 MCP 服务器（终端 2）
```bash
python dynamic_mcp_server.py
```

#### 3. 运行 Agent 演示（终端 3）
```bash
python agent_demo_tool_calling.py
```

#### 服务器信息
- **协议**：SSE (Server-Sent Events)
- **地址**：`http://127.0.0.1:3002/sse/`
- **工具目录**：`./tools/`

### 🛠️ 内置工具

| 工具名称 | 功能描述 | 应用场景 |
|---------|---------|---------|
| `search_github` | 搜索 GitHub Python 项目 | 发现开源库和 API |
| `advanced_web_search` | AI 增强的网络搜索 | 获取最新技术信息 |
| `create_tool_environment` | 创建新工具环境 | 快速搭建工具开发环境 |
| `get_tools_changes` | 获取工具变更信息 | 监控工具更新 |
| `refresh_tools` | 手动刷新工具目录 | 强制重新加载工具 |

### 🎯 使用示例

#### Agent 自进化流程
1. **任务分析**：Agent 分析任务需求，判断是否需要新工具
3. **环境创建**：使用 `create_tool_environment` 创建新工具
4. **自动集成**：系统自动发现并加载新工具
5. **任务执行**：使用新创建的工具完成任务

### 📁 项目结构

```
AutoLabMCP/
├── 📄 README.md                    # 项目文档
├── ⚙️ config.json                 # 配置文件
├── 📦 requirements.txt             # Python 依赖
├── 🚀 dynamic_mcp_server.py        # 主服务器
├── 🤖 agent_demo_tool_calling.py   # Agent 演示
├── 📋 system_prompt.md             # 系统提示词
└── 🛠️ tools/                      # 工具目录
    ├── 🔧 tool_env_manager.py      # 环境管理器
    ├── 🔄 tool_proxy.py            # 工具代理管理器
    ├── ⚡ tool_execution_script.py  # 工具执行脚本
    ├── 📂 tool_loader_script.py    # 工具加载脚本
    ├── 📝 logger_config.py         # 日志配置
    └── 🔨 json_patch.py            # JSON 补丁工具
```

### 许可证

本项目基于 MIT 许可证开源 - 查看 [LICENSE](LICENSE) 文件了解详情。

