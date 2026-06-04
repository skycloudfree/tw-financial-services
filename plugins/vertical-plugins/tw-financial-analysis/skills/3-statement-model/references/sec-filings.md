# MOPS / TWSE Data Extraction Reference

**When to Use:** Only reference this file when a model template specifically requires pulling data from Taiwan public company financial reports. Use TWSEMCPServer tools as the primary data source, falling back to 公開資訊觀測站 (MOPS) for supplementary detail.

---

## Extracting Data from TWSE / MOPS for Taiwan Stocks

When populating a model template with Taiwan public company data, extract financials from TWSEMCPServer tools and 公開資訊觀測站 (MOPS).

### Step 1: Pull Primary Financial Data via TWSEMCPServer

Use the following MCP tools as the primary data source:

| Data Needed | TWSEMCPServer Tool |
|-------------|-------------------|
| Balance Sheet | `get_company_balance_sheet(code="STOCK_NO")` |
| Income Statement | `get_company_income_statement(code="STOCK_NO")` |
| Company Profile | `get_company_profile(code="STOCK_NO")` |
| Monthly Revenue | `get_company_monthly_revenue(code="STOCK_NO")` |
| Dividend Info | `get_company_dividend(code="STOCK_NO")` |
| EPS Statistics | `get_company_eps_statistics(code="STOCK_NO")` |
| Profitability Analysis | `get_company_profitability_analysis(code="STOCK_NO")` |

These tools automatically detect the company's industry and use the appropriate IFRS financial statement format (一般業, 金融業, 證券期貨業, 金控業, 保險業, 異業).

### Step 2: Identify Reporting Currency

Taiwan publicly traded companies report in **New Taiwan Dollars (TWD)** under **Taiwan-IFRS** (Taiwan International Financial Reporting Standards).

- Primary financial statements are in TWD
- Scale is typically in "thousands" or "millions" of TWD — check the statement header
- Document the currency and scale in the Assumptions tab

### Step 3: Access MOPS for Supplementary Detail

For additional detail beyond the TWSEMCPServer tools, access **公開資訊觀測站 (MOPS)**:

| Data | MOPS Section |
|------|-------------|
| 年度財務報告 (Annual Financial Report) | 基本資料 → 財務報表 → 年度財務報告 |
| 季度財務報告 (Quarterly Financial Report) | 基本資料 → 財務報表 → 季度財務報告 |
| 財務報告附註 (Notes to Financial Statements) | Included in each financial report PDF |
| 股東會年報 (Shareholder Meeting Annual Report) | 股東會及股利 → 股東會相關資料 |
| 重大訊息 (Major News/Announcements) | 重大訊息查詢 |

Also available via TWSEMCPServer: `get_company_major_news(code="STOCK_NO")`

### Step 4: Data Extraction Mapping

**Income Statement (綜合損益表)**

| MOPS / TWSE Line Item | Model Line Item |
|----------------------|-----------------|
| 營業收入 / 銷貨收入淨額 | Revenue |
| 營業成本 | COGS |
| 營業毛利 | Gross Profit |
| 推銷費用 + 管理費用 + 研究發展費用 | SG&A (combined) |
| 折舊與攤銷 | D&A (check cash flow statement for detail) |
| 利息費用 | Interest Expense |
| 所得稅費用 | Taxes |
| 本期淨利 / 歸屬於母公司業主淨利 | Net Income |

**Balance Sheet (資產負債表)**

| MOPS / TWSE Line Item | Model Line Item |
|----------------------|-----------------|
| 現金及約當現金 | Cash |
| 應收帳款淨額 | AR |
| 存貨 | Inventory |
| 不動產、廠房及設備淨額 | PP&E (Net) |
| 資產總計 | Total Assets |
| 應付帳款 | AP |
| 短期借款 / 一年內到期長期負債 | Current Debt |
| 長期借款 | LT Debt |
| 保留盈餘 | Retained Earnings |
| 權益總計 | Total Equity |

**Cash Flow Statement (現金流量表)**

| MOPS / TWSE Line Item | Model Line Item |
|----------------------|-----------------|
| 本期淨利 | Net Income |
| 折舊與攤銷 | D&A |
| 應收帳款變動 | ΔAR |
| 存貨變動 | ΔInventory |
| 應付帳款變動 | ΔAP |
| 資本支出 | CapEx |
| 現金增資 | Equity Issuance |
| 舉借債務 / 償還債務 | Debt activity |
| 發放現金股利 | Dividends |

### Step 5: Extract Supporting Detail from Financial Report Notes

For schedules, pull from the financial report notes (財務報告附註) available on MOPS:
- **附註：負債** → 到期分析、利率、合約條款
- **附註：不動產、廠房及設備** → 原始成本、累計折舊、耐用年限
- **附註：收入** → 部門別收入、地區別收入
- **附註：租賃** → 營業租賃與融資租賃義務

### Step 6: Historical Data Requirements

Extract minimum data via TWSEMCPServer tools:
- Annual reports provide the current year's financial statements with prior year comparatives
- Use `get_stock_daily_trading` / `get_stock_monthly_trading` for detailed market data
- Pull from MOPS for earlier years if needed

### Data Extraction Checklist

- Identify reporting currency (TWD) and scale (thousands/millions)
- 3+ years historical Income Statement
- 3+ years historical Cash Flow Statement
- 3+ years historical Balance Sheet
- Verify IS Net Income = CF starting Net Income (each year)
- Verify BS Cash = CF Ending Cash (each year)
- Extract debt maturity schedule from financial report notes
- Extract D&A detail or useful life assumptions
- Note any non-recurring / one-time items to normalize

### Handling Common Filing Variations

| Variation | How to Handle |
|-----------|---------------|
| D&A embedded in COGS/SG&A | Pull D&A from Cash Flow Statement (現金流量表) |
| "Other" line items are material | Check financial report notes for breakdown |
| Restatements | Use restated figures, note in assumptions |
| Fiscal year ≠ calendar year | Taiwan companies generally follow calendar year; label exceptions explicitly |
| Non-TWD reporting currency | Some Taiwan companies report in foreign currency; adapt model to match |
