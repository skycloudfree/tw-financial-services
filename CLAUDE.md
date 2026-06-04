# TW Financial Services Plugins

台灣金融市場 Claude 插件集合。每个子目录是一个独立插件。

## 仓库结构

```
├── tw-financial-analysis/  # 核心金融分析（必装）
├── tw-equity-research/     # 台股研究
├── tw-investment-banking/  # 台灣投行
```

## 插件结构

每个插件遵循以下布局：
```
plugin-name/
├── .claude-plugin/plugin.json   # 插件清单（名称、描述、版本）
├── commands/                    # 斜杠命令（.md 文件）
├── skills/                      # 特定任务的知识文件
├── hooks/                       # 事件驱动自动化
└── .mcp.json                    # MCP 服务器配置
```

## 关键文件

- `marketplace.json`: 市场清单 — 注册所有插件及其源路径
- `plugin.json`: 插件元数据 — 名称、描述、版本
- `commands/*.md`: 斜杠命令，以 `/plugin:command-name` 方式调用
- `skills/*/SKILL.md`: 特定任务的详细知识和工作流
- `.mcp.json`: MCP 数据源连接配置（指向 TWSEMCPServer）

## 数据源

所有插件通过 MCP 协议连接 **TWSEMCPServer**（基于台灣證交所 OpenAPI），提供台股行情、财报、行业、宏观等 143 个金融数据工具，无需额外 API Key。

## 开发工作流

1. 直接编辑 markdown 文件 — 改动立即生效
2. 用 `/plugin:command-name` 语法测试命令
3. 当触发条件匹配时，Skills 自动激活
