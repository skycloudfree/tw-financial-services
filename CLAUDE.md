# TW Financial Services Plugins

台灣金融市場 Claude 插件集合。每個子目錄是一個獨立插件。

## 倉庫結構

```
├── plugins/
│   ├── vertical-plugins/
│   │   ├── tw-financial-analysis/  # 核心金融分析（必裝）
│   │   ├── tw-equity-research/     # 台股研究
│   │   ├── tw-investment-banking/  # 台灣投資銀行
│   │   ├── tw-private-equity/      # 台灣私募股權
│   │   ├── tw-wealth-management/   # 台灣財富管理
│   │   ├── tw-fund-admin/          # 台灣基金行政管理
│   │   └── tw-operations/          # 台灣營運作業
│   └── agent-plugins/              # 10 個專用代理插件
├── managed-agent-cookbooks/        # 10 個受管代理工作流程
└── marketplace.json                # 市集清單（註冊所有插件）
```

## 插件結構

每個插件遵循以下佈局：
```
plugin-name/
├── .claude-plugin/plugin.json   # 插件清單（名稱、displayName、描述、版本）
├── commands/                    # 斜線命令（.md 檔案）
│   └── command-name.md          # 每個檔案 = 一個斜線命令
├── skills/                      # 特定任務的知識文件
│   └── skill-name/SKILL.md      # 詳細工作流程指引
├── hooks/                       # 事件驅動自動化
└── .mcp.json                    # MCP 伺服器設定（指向 TWSEMCPServer）
```

## 關鍵檔案

- `marketplace.json`: 市集清單 — 註冊所有插件及其來源路徑
- `plugin.json`: 插件元資料 — name、displayName、description、version
- `commands/*.md`: 斜線命令，以 `/tw-plugin-name:command` 方式呼叫
- `skills/*/SKILL.md`: 特定任務的詳細知識和工作流程
- `.mcp.json`: MCP 資料來源連線設定（指向 TWSEMCPServer）

## 垂直插件一覽

| 插件目錄 | 斜線命令前綴 | 指令數 | 技能數 |
|---------|-------------|-------|-------|
| `tw-financial-analysis` | `/tw-financial-analysis:` | 7 | 13 |
| `tw-equity-research` | `/tw-equity-research:` | 9 | 9 |
| `tw-investment-banking` | `/tw-investment-banking:` | 7 | 9 |
| `tw-private-equity` | `/tw-private-equity:` | 10 | 10 |
| `tw-wealth-management` | `/tw-wealth-management:` | 6 | 6 |
| `tw-fund-admin` | (僅技能，無指令) | 0 | 6 |
| `tw-operations` | (僅技能，無指令) | 0 | 2 |

## 代理插件一覽

| 目錄 | 插件名稱 | 顯示名稱 |
|------|---------|---------|
| `earnings-reviewer` | `tw-earnings-reviewer` | 財報審閱助手 |
| `gl-reconciler` | `tw-gl-reconciler` | 總帳調節助手 |
| `kyc-screener` | `tw-kyc-screener` | KYC審查助手 |
| `market-researcher` | `tw-market-researcher` | 市場研究助手 |
| `meeting-prep-agent` | `tw-meeting-prep-agent` | 會議準備助手 |
| `model-builder` | `tw-model-builder` | 模型建構助手 |
| `month-end-closer` | `tw-month-end-closer` | 月結關帳助手 |
| `pitch-agent` | `tw-pitch-agent` | 簡報提案助手 |
| `statement-auditor` | `tw-statement-auditor` | 對帳單審計助手 |
| `valuation-reviewer` | `tw-valuation-reviewer` | 估值審閱助手 |

## 資料來源

所有插件透過 MCP 協定連接 **TWSEMCPServer**（基於台灣證交所 OpenAPI），提供台股行情、財報、產業、總體經濟等 **143 個金融資料工具**，無需額外 API Key。

## 開發工作流程

1. 直接編輯 markdown 檔案 — 改動立即生效
2. 用 `/tw-plugin-name:command` 語法測試命令
3. 當觸發條件匹配時，Skills 自動激活
4. 執行測試計畫驗證結構完整性

## 產品文件

- `README.md` — 繁體中文版完整說明（含安裝指引、插件總覽、使用範例）
- `README.en.md` — 英文版總覽（供國際開發者使用）

## 測試

執行以下命令驗證插件結構：
```bash
# Phase 1: 結構性測試（96 項檢查）
# Phase 2: 內容審計（8 項檢查）
# Phase 3: 跨插件一致性（5 項檢查）
# Phase 4: 功能性 CLI 檢查
# Phase 5: 邊界案例（4 項檢查）
```
