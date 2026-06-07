# TW Financial Services Plugins

A comprehensive suite of Claude AI plugins adapted for the **Taiwan financial market**.  
7 vertical plugins + 10 specialized agent plugins covering equity research, investment banking, private equity, wealth management, fund administration, and operations — all using Taiwan market data sources.

## Repository Layout

```
├── plugins/
│   ├── vertical-plugins/
│   │   ├── tw-financial-analysis/    # Core financial analysis (required)
│   │   ├── tw-equity-research/       # Taiwan equity research
│   │   ├── tw-investment-banking/    # Taiwan investment banking
│   │   ├── tw-private-equity/        # Taiwan private equity
│   │   ├── tw-wealth-management/     # Taiwan wealth management
│   │   ├── tw-fund-admin/            # Taiwan fund administration
│   │   └── tw-operations/            # Taiwan operations
│   └── agent-plugins/                # 10 specialized agents
├── managed-agent-cookbooks/          # 10 managed agent deployments
├── marketplace.json                  # Plugin registry
└── README.zh-TW.md                   # 繁體中文說明
```

## Installation

```bash
# 1. Add the local marketplace source
claude plugin marketplace add ./marketplace.json

# 2. Install core plugin (required)
claude plugin install tw-financial-analysis

# 3. Install additional plugins as needed
claude plugin install tw-equity-research
claude plugin install tw-investment-banking
claude plugin install tw-private-equity
claude plugin install tw-wealth-management
claude plugin install tw-fund-admin
claude plugin install tw-operations
```

For agent plugins, see each plugin under `plugins/agent-plugins/` for installation instructions.

## Vertical Plugins

| Plugin | Display Name | Commands | Skills | Description |
|--------|-------------|----------|--------|-------------|
| `tw-financial-analysis` | 台股財務分析 | 7 | 13 | DCF, comps, LBO, 3-statement models |
| `tw-equity-research` | 台股研究 | 9 | 9 | Earnings analysis, coverage, sector overviews |
| `tw-investment-banking` | 台灣投資銀行 | 7 | 9 | CIM, teaser, M&A models, deal tracking |
| `tw-private-equity` | 台灣私募股權 | 10 | 10 | Deal sourcing, DD, IC memos, portfolio |
| `tw-wealth-management` | 台灣財富管理 | 6 | 6 | Client reviews, financial planning, TLH |
| `tw-fund-admin` | 台灣基金行政管理 | 0 | 6 | GL recon, NAV tie-out, accruals |
| `tw-operations` | 台灣營運作業 | 0 | 2 | KYC document parsing, AML screening |

**Commands reference** — call with `/plugin:command-name`:
```
/tw-financial-analysis:dcf        /tw-equity-research:earnings
/tw-financial-analysis:comps      /tw-equity-research:initiate
/tw-financial-analysis:lbo        /tw-equity-research:sector
/tw-financial-analysis:3-statement-model  /tw-equity-research:screen
/tw-financial-analysis:competitive-analysis  /tw-equity-research:morning-note

/tw-investment-banking:cim        /tw-private-equity:source
/tw-investment-banking:teaser     /tw-private-equity:dd-checklist
/tw-investment-banking:merger-model  /tw-private-equity:ic-memo
/tw-investment-banking:buyer-list /tw-private-equity:returns

/tw-wealth-management:client-review  /tw-wealth-management:financial-plan
/tw-wealth-management:rebalance   /tw-wealth-management:tlh
/tw-wealth-management:proposal    /tw-wealth-management:client-report
```

## Agent Plugins

Each agent plugin has specialized skills and a managed-agent cookbook for automated multi-worker workflows.

| Agent | Display Name | Purpose |
|-------|-------------|---------|
| `tw-earnings-reviewer` | 財報審閱助手 | Process earnings calls → update models → publish notes |
| `tw-gl-reconciler` | 總帳調節助手 | GL/subledger break tracing and exception reporting |
| `tw-kyc-screener` | KYC審查助手 | Document parsing, AML rules, sanctions/PEP screening |
| `tw-market-researcher` | 市場研究助手 | Industry research, comps spread, thematic reports |
| `tw-meeting-prep-agent` | 會議準備助手 | Client briefing packs with holdings, news, agenda |
| `tw-model-builder` | 模型建構助手 | DCF/LBO/3-stmt/comps in Excel from a ticker |
| `tw-month-end-closer` | 月結關帳助手 | Accruals, roll-forwards, close package generation |
| `tw-pitch-agent` | 簡報提案助手 | Comps → model → branded deck pipeline |
| `tw-statement-auditor` | 對帳單審計助手 | LP statement audit against NAV packs |
| `tw-valuation-reviewer` | 估值審閱助手 | GP valuation review, waterfall, LP reporting |

## Managed Agent Cookbooks

Each cookbook defines a 3-worker pipeline (reader → critic → writer) for production-grade automation:

| Cookbook | Subagents | Output |
|----------|-----------|--------|
| `earnings-reviewer/` | transcript-reader → model-updater → note-writer | Research note + model `.xlsx` |
| `gl-reconciler/` | reader → critic → resolver | Exception report |
| `kyc-screener/` | doc-reader → rules-engine → escalator | Compliance escalation `.xlsx` |
| `market-researcher/` | sector-reader → comps-spreader → note-writer | Primer `.docx` + optional `.pptx` |
| `meeting-prep-agent/` | profiler → news-reader → pack-writer | Client briefing `.pptx` |
| `model-builder/` | data-puller → builder → auditor | Financial model `.xlsx` |
| `month-end-closer/` | ledger-reader → rollforward → poster | Close package `.xlsx` |
| `pitch-agent/` | researcher → modeler → deck-writer | Pitch deck `.pptx` + model |
| `statement-auditor/` | statement-reader → reconciler → flagger | Sign-off `.xlsx` |
| `valuation-reviewer/` | package-reader → valuation-runner → publisher | LP report `.xlsx` |

## Data Sources

All plugins connect to **TWSEMCPServer** via the MCP protocol, based on the Taiwan Stock Exchange (TWSE) OpenAPI.  
This provides **143 financial data tools** — real-time quotes, historical prices, financial statements, industry data, macro indicators, and more — with no external API key required.

Key MCP tools:
| Tool | Description |
|------|-------------|
| `TWStockMCPServer_get_realtime_quote` | Real-time intraday quotes (supports multiple stocks) |
| `TWStockMCPServer_get_stock_history` | Daily OHLCV history by month |
| `TWStockMCPServer_get_company_profile` | Company basic info, industry, capital |
| `TWStockMCPServer_get_company_balance_sheet` | Balance sheet (auto-detects industry format) |
| `TWStockMCPServer_get_company_income_statement` | Income statement (auto-detects industry format) |
| `TWStockMCPServer_get_company_monthly_revenue` | Monthly revenue reports |
| `TWStockMCPServer_get_margin_balance` | Margin lending and short selling balance |
| `TWStockMCPServer_get_twse_institutional_investors_summary` | Institutional buy/sell by stock |
| `TWStockMCPServer_get_daily_futures_market_report` | Futures daily trading |
| `TWStockMCPServer_get_futures_institutional` | Three major institutional futures positions |

## Plugin Structure

Every plugin follows this layout:
```
plugin-name/
├── .claude-plugin/plugin.json   # Manifest (name, displayName, description, version)
├── commands/                    # Slash commands (.md files)
│   └── command-name.md          # Each file = one slash command
├── skills/                      # Task-specific knowledge files
│   └── skill-name/SKILL.md      # Detailed workflow instructions
├── hooks/                       # Event-driven automations
└── .mcp.json                    # MCP data source config (points to TWSEMCPServer)
```

## Development Workflow

1. **Edit markdown files** — changes take effect immediately
2. **Test commands** with `/<plugin>:` syntax
3. **Skills activate automatically** when trigger conditions match
4. **Run the test plan** to validate structural integrity:
   ```
   # Phase 1: Structural tests (96 checks)
   # Phase 2: Content audit (8 checks)
   # Phase 3: Cross-plugin consistency (5 checks)
   # Phase 4: Functional CLI checks
   # Phase 5: Edge cases (4 checks)
   ```

## Terminology Mapping

| US Term | Taiwan Equivalent |
|---------|------------------|
| SEC EDGAR | 公開資訊觀測站 (MOPS) |
| 10-K / 10-Q | Annual / Quarterly Report |
| Ticker | Stock Code (4-digit) |
| S&P 500 | TAIEX (Taiwan Weighted Index) |
| 401(k) | Labor Pension (勞退) |
| Bloomberg Terminal | TWSE OpenAPI / MCP |

Stock codes are 4 digits: `2330` (TSMC), `2317` (Hon Hai), `0050` (Yuanta Taiwan 50).

## License

Apache License 2.0

**Disclaimer**: This suite is designed to assist financial workflows only and does not provide financial or investment advice. All outputs should be verified by qualified financial professionals.
