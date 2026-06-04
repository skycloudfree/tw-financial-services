---
name: tax-loss-harvesting
description: Identify tax-loss harvesting opportunities across taxable accounts. Finds positions with unrealized losses and suggests replacement securities. Triggers on "tax-loss harvesting", "TLH", "harvest losses", "tax losses", "unrealized losses", or "year-end tax planning".
---

# Tax-Loss Harvesting

## Workflow

### Step 1: Identify Candidates

Scan taxable accounts for positions with unrealized losses:

| Security | Asset Class | Cost Basis | Current Value | Unrealized Loss | Holding Period | % Loss |
|----------|-----------|-----------|---------------|-----------------|---------------|--------|
| | | | | | ST / LT | |

**Prioritize by:**
1. Largest absolute loss (biggest tax benefit)
2. Short-term losses first (offset short-term gains); under Taiwan tax rules, securities transaction gains are tax-exempt for individual investors (證所稅停徵), but losses can offset gains within the same tax year for specific circumstances
3. Positions with the largest % loss (less likely to recover quickly)

### Step 2: Gain/Loss Budget

Calculate the client's tax situation:

| Category | Amount |
|----------|--------|
| Realized short-term gains YTD | |
| Realized long-term gains YTD | |
| Realized losses YTD | |
| Net gain/(loss) position | |
| Carryforward losses from prior years | |
| **Target harvesting amount** | |

**Tax savings estimate:**
- Under current Taiwan tax framework: 證券交易所得稅 (securities transaction gains tax) is suspended for individual investors
- Securities transaction tax (證交稅) is paid on each trade — harvesting does not create a 證交稅 credit
- For corporate/CTA investors: losses can offset gains under 營利事業所得稅 rules
- Consult with a Taiwan tax advisor on the latest 最低稅負制 (AMT) implications

### Step 3: Replacement Securities

For each harvest candidate, suggest a replacement that:
- Maintains similar market exposure (same asset class, sector, geography)
- Has similar risk/return characteristics

| Sell | Replace With | Reason | Tracking Error Risk |
|------|-------------|--------|-------------------|
| 元大台灣50 (0050) | 富邦台50 (006208) | Same index, different fund family | Minimal |
| 元大高股息 (0056) | 國泰永續高股息 (00878) | Similar yield focus, different index | Low |
| Individual stock ABC | Sector ETF | Broader exposure | Moderate |

### Step 4: Taiwan Tax Note — No Wash Sale Rule

Unlike the US wash sale rule, Taiwan's tax framework does not have a "substantially identical" restriction. You may sell a security at a loss and repurchase it immediately without triggering a wash sale disallowance. However:

- Maintain proper documentation of realized losses for tax filings
- For corporate/CTA clients, consult with a Taiwan tax advisor on loss utilization rules

### Step 5: Execution Plan

| Trade # | Account | Action | Security | Shares | Est. Proceeds | Est. Loss | Replacement | Notes |
|---------|---------|--------|----------|--------|--------------|-----------|-------------|-------|
| | | Sell | | | | | | |
| | | Buy | | | | | | |

**Summary:**
- Total estimated losses harvested: $
- Estimated tax savings: $ (at marginal rate of %)
- Net portfolio impact: minimal (replacement securities maintain exposure)
- Loss documentation for tax filing

### Step 6: Post-Harvest Tracking

After 30+ days, optionally:
- Swap back to original securities (if preferred)
- Maintain replacement securities (if no reason to switch back)
- Update cost basis records
- Document for tax reporting

### Step 7: Output

- Harvest opportunity list (Excel)
- Trade execution sheet
- Loss tracking log
- Tax savings estimate summary
- Replacement security rationale

## Important Notes

- Taiwan currently has no wash sale rule — no restrictions on repurchasing the same security after selling at a loss
- However, maintain clear records of realized losses for annual tax filings
- For corporate/CTA clients, consult with a Taiwan tax advisor on loss utilization rules
- Under 最低稅負制 (AMT), certain high-income scenarios may still trigger alternative minimum tax on securities transactions
- Consider the long-term cost basis step-down — harvesting resets cost basis, which means more gains later
- Year-end is prime harvesting season but opportunities exist throughout the year
- Mutual fund capital gains distributions in December can create additional harvesting urgency
- Document everything for tax reporting and compliance
- Not all losses are worth harvesting — transaction costs and tracking error have real costs
