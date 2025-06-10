# 🎯 MCP Feedback Collector

基于Node.js的MCP反馈收集器，用于充分利用Cursor额度。

## ✨ 特性

- 🎨 **现代界面**: VS Code主题风格的Web界面
- 🔧 **MCP集成**: 完整支持Model Context Protocol
- 💬 **AI对话功能**: 支持第三方AI助手，支持文字和图片对话
- 🖼️ **图片支持**: 完整的图片上传、处理和显示功能

## 📋 系统要求

- **Node.js**: 18.0.0 或更高版本
- **浏览器**: Chrome, Firefox, Safari, Edge
- **操作系统**: Linux, Windows, macOS

## 📝 本地安装

### 环境准备

首先确保Node.js版本符合要求（18.0.0或更高版本）：

```bash
# 查看当前Node.js版本
node -v
```

#### Linux (Ubuntu/Debian)

如果版本不符合要求，并且没有特殊的版本控制需求，建议卸载后安装最新版（不能直接覆盖安装，因为会冲突）：

```bash
# 卸载现有版本
sudo apt-get remove nodejs
sudo apt-get purge nodejs
sudo apt-get autoremove

# 安装最新版本 (Node.js 22.x)
curl -fsSL https://deb.nodesource.com/setup_22.x | sudo bash -
sudo apt-get install -y nodejs
```

#### Windows

1. 在控制面板中完全卸载现有的Node.js相关程序
2. 访问 [https://nodejs.org/en/download](https://nodejs.org/en/download)
3. 下载最新的Windows安装包
4. 运行安装包进行安装

### 项目安装

```bash
# 克隆项目
git clone https://github.com/Mriris/mcp-feedback-collector-web.git
cd mcp-feedback-collector-web
# 安装并构建
npm install
npm run build
```

请确保各个环节无报错。

## ⚙️ 配置说明

### Cursor规则

在Cursor规则中添加以下配置：

```text
当需要向用户提问时，务必调用 MCP；在完成用户请求前切勿直接结束流程，而应调用 MCP 并持续执行 mcp-feedback-collector.collect_feedback，直至用户反馈为空后再结束。所有回复（包括代码注释）均须使用简体中文，语言应简明易懂，避免生硬的机器翻译式表述；如需编写或修改代码，请直接在对应文件内完成，勿让用户手动复制。
```

或

```text
Whenever you want to ask a question, always call the MCP. Whenever you're about to complete a user request, call the MCP instead of simply ending the process. Keep calling MCP until the user's feedback is empty, then end the request. mcp-feedback-collector.collect_feedback
```

### MCP Tools

如果cursor没有其他MCP，直接将以下内容复制即可。否则请仔细观察JSON结构，然后添加进去，注意逗号和括号。

```json
{
  "mcpServers": {
    "mcp-feedback-collector": {
      "command": "node",
      "args": ["你的项目路径/dist/cli.js"],
      "env": {
        "MCP_API_KEY": "api-key(可选)",
        "MCP_API_BASE_URL": "http://127.0.0.1",
        "MCP_DEFAULT_MODEL": "模型名称(可选)",
        "MCP_WEB_PORT": "5080",
        "MCP_DIALOG_TIMEOUT": "60000"
      }
    }
  }
}
```

## 🏗️ 项目架构

```text
src/
├── cli.ts              # CLI入口
├── index.ts            # 主入口
├── config/             # 配置管理
├── server/             # 服务器实现
├── utils/              # 工具函数
├── types/              # 类型定义
└── static/             # 静态文件
```
