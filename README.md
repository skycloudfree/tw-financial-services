# Claude 金融服務插件 — 台灣市場適用版

本套件為 Claude AI 助手適配台灣金融市場的專業金融服務插件，專為投資銀行、股票研究、私募股權與財富管理等專業人士設計。

## 主要特色

- **台灣市場術語**：所有術語已轉換為台灣市場慣用詞彙
- **本地資料來源**：透過 TWSEMCPServer 連接公開資訊觀測站、證交所、櫃買中心資料
- **完整工作流程**：從研究分析到報告產出的端到端解決方案
- **106 個專業技能**：涵蓋財務模型、研究報告、KYC、基金行政等領域

---

## 安裝指南

### 需求

- Claude Code 或 Claude Desktop
- 網路連線（用於取得市場資料）

### 安裝步驟

```bash
# 1. 新增本地市集
claude plugin marketplace add ./marketplace.json

# 2. 安裝核心插件（必選）
claude plugin install tw-financial-analysis

# 3. 按需求安裝功能插件
claude plugin install tw-equity-research
claude plugin install tw-investment-banking
claude plugin install tw-private-equity
claude plugin install tw-wealth-management
claude plugin install tw-fund-admin
claude plugin install tw-operations
```

---

## 外掛總覽

### 倉庫結構

```
├── plugins/
│   ├── vertical-plugins/       # 7 個垂直領域插件
│   │   ├── tw-financial-analysis/    # 核心財務分析（必裝）
│   │   ├── tw-equity-research/       # 台股研究
│   │   ├── tw-investment-banking/    # 台灣投資銀行
│   │   ├── tw-private-equity/        # 台灣私募股權
│   │   ├── tw-wealth-management/     # 台灣財富管理
│   │   ├── tw-fund-admin/            # 台灣基金行政管理
│   │   └── tw-operations/            # 台灣營運作業
│   └── agent-plugins/          # 10 個專用代理插件
├── managed-agent-cookbooks/    # 10 個受管代理工作流程
└── marketplace.json            # 外掛市集註冊檔
```

### 1. 財務分析 (tw-financial-analysis) — 必裝核心

| 功能 | 說明 |
|------|------|
| DCF 估值 | 建立貼現現金流估值模型 |
| 可比公司分析 | 進行同業比較分析 |
| LBO 模型 | 槓桿收購模型 |
| 3 表財務模型 | 損益表、資產負債表、現金流量表 |
| 同業競爭分析 | 競爭格局與市場定位分析 |

**指令範例**：
```bash
/tw-financial-analysis:dcf 2330              # 為台積電建立 DCF 模型
/tw-financial-analysis:comps 2317            # 進行鴻海可比公司分析
/tw-financial-analysis:competitive-analysis  # 同業競爭分析
```

### 2. 投資銀行 (tw-investment-banking)

| 功能 | 說明 |
|------|------|
| CIM 撰寫 | 投資人簡報製作 |
| Teaser 製作 | 交易概要文件 |
| 買方名單 | 潛在買家清單建立 |
| 併購模型 | M&A 財務模型 |

**指令範例**：
```bash
/tw-investment-banking:cim       # 撰寫投資人簡報
/tw-investment-banking:teaser    # 製作交易概要
/tw-investment-banking:buyer-list # 建立買方名單
```

### 3. 股票研究 (tw-equity-research)

| 功能 | 說明 |
|------|------|
| 財報分析 | 季報/年報分析 |
| 初始覆蓋報告 | 股票研究報告生成 |
| 產業概覽 | 產業趨勢分析 |
| 篩選策略 | 投資想法篩選 |

**指令範例**：
```bash
/tw-equity-research:earnings 2330    # 分析台積電財報
/tw-equity-research:initiate 2317     # 建立鴻海初始覆蓋報告
/tw-equity-research:sector 半導體     # 產業概覽分析
```

### 4. 私募股權 (tw-private-equity)

| 功能 | 說明 |
|------|------|
| 交易發掘 | 潛在投資標的篩選 |
| 盡職調查 | DD 清單與準備 |
| IC 簡報 | 投資委員會簡報 |
| 報酬分析 | 投資報酬分析 |

**指令範例**：
```bash
/tw-private-equity:source          # 發掘交易機會
/tw-private-equity:dd-checklist    # 盡職調查清單
/tw-private-equity:ic-memo         # IC 簡報製作
```

### 5. 財富管理 (tw-wealth-management)

| 功能 | 說明 |
|------|------|
| 客戶會議 | 會議準備資料 |
| 財務規劃 | 個人理財規劃 |
| 投資組合調整 | 資產配置建議 |
| 稅務規劃 | 稅務虧損收割 |

**指令範例**：
```bash
/tw-wealth-management:client-review  # 客戶會議準備
/tw-wealth-management:financial-plan # 財務規劃
/tw-wealth-management:tlh            # 稅務虧損收割
```

### 6. 基金行政管理 (tw-fund-admin)

| 功能 | 說明 |
|------|------|
| 差異追蹤 | 總帳與明細帳差異根因分析 |
| GL 調節 | 總帳調節作業 |
| NAV 核對 | 資產淨值核對 |
| Roll-forward | 科目滾動計算 |

### 7. 營運作業 (tw-operations)

| 功能 | 說明 |
|------|------|
| KYC 文件解析 | 客戶身份審查文件解析 |
| KYC 法規評估 | 洗錢防制與法規遵循評估 |

---

## 代理插件

每個代理插件擁有專屬技能集與受管代理工作流程（3 階段 pipeline）。

| 代理插件 | 顯示名稱 | 用途 |
|---------|---------|------|
| `tw-earnings-reviewer` | 財報審閱助手 | 處理法說會→更新模型→產出報告 |
| `tw-gl-reconciler` | 總帳調節助手 | 比對總帳與明細帳差異，產出異常報告 |
| `tw-kyc-screener` | KYC審查助手 | 解析開戶文件，AML 規則引擎，制裁名單比對 |
| `tw-market-researcher` | 市場研究助手 | 產業研究、同業比較、主題式報告 |
| `tw-meeting-prep-agent` | 會議準備助手 | 客戶簡報包：持股、新聞、議程 |
| `tw-model-builder` | 模型建構助手 | 從股票代號即時建立 DCF/LBO/三表模型 |
| `tw-month-end-closer` | 月結關帳助手 | 應計項目、滾動計算、關帳文件包 |
| `tw-pitch-agent` | 簡報提案助手 | 同業比較→模型→品牌化簡報 |
| `tw-statement-auditor` | 對帳單審計助手 | LP 對帳單審計與 NAV 勾稽 |
| `tw-valuation-reviewer` | 估值審閱助手 | 估值報告審閱、Waterfall、LP 報告 |

---

## 受管代理工作流程 (Managed Agent Cookbooks)

每個 cookbook 定義 3 階段 pipeline（讀取→審核→輸出），適用於生產環境自動化：

| Cookbook | Subagents | 產出 |
|----------|-----------|------|
| `earnings-reviewer/` | transcript-reader → model-updater → note-writer | 研究報告 + 模型 `.xlsx` |
| `gl-reconciler/` | reader → critic → resolver | 異常報告 |
| `kyc-screener/` | doc-reader → rules-engine → escalator | 法遵呈報 `.xlsx` |
| `market-researcher/` | sector-reader → comps-spreader → note-writer | 產業報告 `.docx` + 可選 `.pptx` |
| `meeting-prep-agent/` | profiler → news-reader → pack-writer | 客戶簡報 `.pptx` |
| `model-builder/` | data-puller → builder → auditor | 財務模型 `.xlsx` |
| `month-end-closer/` | ledger-reader → rollforward → poster | 關帳文件包 `.xlsx` |
| `pitch-agent/` | researcher → modeler → deck-writer | 簡報 `.pptx` + 模型 |
| `statement-auditor/` | statement-reader → reconciler → flagger | 簽核文件 `.xlsx` |
| `valuation-reviewer/` | package-reader → valuation-runner → publisher | LP 報告 `.xlsx` |

---

## 台灣市場術語對照

| 英文術語 | 台灣用語 |
|----------|----------|
| SEC EDGAR | 公開資訊觀測站 |
| 10-K / 年報 | 年報 / 季報 |
| Ticker | 股票代號 |
| EBITDA | 稅前息前折舊攤銷前獲利 |
| IRR | 內部報酬率 |
| MOIC | 投資倍數 |
| S&P 500 | 台灣加權指數 |
| 401k | 勞退自提 |

### 股票代號格式

台灣股票使用 4 碼格式：
- **上市股**：2330（台積電）、2317（鴻海）、0050（元大台灣50）
- **上櫃股**：例如 6477（玉石）— 已上市股票代號前導為 2 或 6

---

## 資料來源

所有插件透過 **MCP 協定** 連接 **TWSEMCPServer**（基於台灣證交所 OpenAPI），提供 **143 個金融資料工具**，無需額外 API Key。

| 來源 | 用途 |
|------|------|
| 公開資訊觀測站 (MOPS) | 財務報表、重大訊息 |
| 台灣證券交易所 (TWSE) | 上市股票行情、交易資料 |
| 櫃買中心 (OTC) | 上櫃股票資料 |
| TWStock MCP Server | 即時報價、歷史資料 |

常用 MCP 工具：
```bash
# 即時報價
TWStockMCPServer_get_realtime_quote stock_nos: ["2330", "0050"]

# 歷史股價
TWStockMCPServer_get_stock_history stock_no: "2330", date: "20250101"

# 公司基本資料
TWStockMCPServer_get_company_profile code: "2330"

# 財務報表（自動辨識產業格式）
TWStockMCPServer_get_company_balance_sheet code: "2330"
TWStockMCPServer_get_company_income_statement code: "2330"

# 營收資料
TWStockMCPServer_get_company_monthly_revenue code: "2330"

# 三大法人買賣超
TWStockMCPServer_get_twse_institutional_investors_summary date: "20260505"
```

---

## 外掛結構

```
plugin-name/
├── .claude-plugin/plugin.json   # 外掛清單（名稱、描述、版本）
├── commands/                    # 斜線命令（.md 檔案）
│   └── command-name.md          # 每個檔案 = 一個斜線命令
├── skills/                      # 特定任務的知識文件
│   └── skill-name/SKILL.md      # 詳細工作流程指引
├── hooks/                       # 事件驅動自動化
└── .mcp.json                    # MCP 資料源設定（指向 TWSEMCPServer）
```

---

## 使用範例

### 範例 1：分析台積電 (2330) 股票

```
你：幫我分析 2330 的投資價值

AI：正在為您進行台積電投資分析...

1. 取得公司基本資料
2. 分析最近 8 季營收與獲利趨勢
3. 比較同業（半導體族群）
4. 計算 DCF 估值
5. 生成投資建議摘要
```

### 範例 2：建立財報預覽報告

```
你：幫我準備 2317 的 Q1 財報預覽

AI：正在為您準備鴻海財報預覽...

1. 取得最新財報數據
2. 分析市場共識預估
3. 比較去年同期表現
4. 產出 4-5 頁專業報告
```

---

## 開發工作流程

1. **直接編輯 markdown 檔案** — 改動立即生效
2. **用 `/<plugin>:command-name` 語法測試命令**
3. **當觸發條件匹配時，Skills 自動激活**
4. **執行測試計畫驗證結構完整性**

---

## 輸出格式

| 格式 | 用途 |
|------|------|
| Excel (.xlsx) | 可比公司分析、DCF/LBO 模型、三表模型、敏感性分析 |
| Word (.docx) | CIM 投資人簡報、公司概覽、IC 備忘錄 |
| PowerPoint (.pptx) | Pitch Deck、產業概覽簡報 |

---

## 故障排除

**Q：MCP 工具無法連線**
- 檢查網路連線
- 確認 MCP 伺服器運行正常

**Q：股票代號格式錯誤**
- 確認使用 4 碼格式（如 2330）
- 上市股票：2 碼或 6 碼開頭

**Q：分析結果與預期不符**
- 檢查輸入的股票代號是否正確
- 確認資料來源為最新

---

## 版本資訊

- **版本**：1.0.0
- **更新日期**：2026年6月
- **適用地區**：台灣
- **支援語言**：繁體中文 / English

---

## 授權

Apache License 2.0

**免責聲明**：本套件僅供輔助金融工作流程，不提供金融或投資建議。所有分析結論應由合格的金融專業人士驗證後再行使用。
