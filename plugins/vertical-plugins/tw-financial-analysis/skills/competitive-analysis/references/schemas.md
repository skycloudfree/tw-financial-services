# Schemas Reference

Additional table formats not shown in main SKILL.md.

All monetary values in TWD unless otherwise noted. Use TWSEMCPServer tools (`get_company_profile`, `get_company_balance_sheet`, `get_company_income_statement`) for financial data.

## M&A Transaction Table

| Acquirer | Target | Date | Deal Value | Multiple | Rationale |
|----------|--------|------|------------|----------|-----------|
| Company A | Company B | MMM YYYY | NT$X.XB | X.Xx EV/Rev | [Strategic logic] |

State multiple methodology: "X.Xx EV/Revenue" or "X.Xx EV/EBITDA"

## Scenario Analysis Table

| Scenario | Probability | Valuation | Key Assumptions |
|----------|-------------|-----------|-----------------|
| Bull | XX% | NT$XXB | [Specific, quantified] |
| Base | XX% | NT$XXB | [Specific, quantified] |
| Bear | XX% | NT$XXB | [Specific, quantified] |

## Slide Structure

```
┌─────────────────────────────────────────────────────────────┐
│ [Insight headline, not topic]                               │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│                     [Main Content]                          │
│                                                             │
├─────────────────────────────────────────────────────────────┤
│ Source: [Citation] ([Date])                                 │
└─────────────────────────────────────────────────────────────┘
```
