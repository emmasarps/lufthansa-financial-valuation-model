# Lufthansa Group — Integrated Financial Valuation & Forecasting Model

**Built by:** Emmanuel Sarpong  
**Company:** Lufthansa Group  
**Date:** July 2026  
**Tools:** Microsoft Excel • DCF Valuation • Comparable Company Analysis • Financial Forecasting  

---

## What this project is

An integrated financial forecasting and valuation model developed in Microsoft Excel to evaluate Lufthansa Group's financial performance and estimate intrinsic enterprise value using Discounted Cash Flow (DCF) and Comparable Company Analysis. The model links the Income Statement, Balance Sheet, and Cash Flow Statement across a six-year forecast horizon (2025E–2030E), anchored to five years of verified historical data (2020A–2024A), and summarises key valuation outputs in an executive dashboard.

This project was built to demonstrate applied FMVA-level skills in a real-world context — not a template, but a from-scratch model built to professional financial modelling standards using public primary sources.

---

## Key outputs

| Metric | Value |
|---|---|
| WACC (CAPM build-up) | ≈ 7.16% |
| Terminal Growth Rate | 2.0% |
| DCF Implied Share Price | See Dashboard |
| Comps-Implied Price (EV/EBITDA) | See Dashboard |
| Reference Market Price (2024 year-end) | €6.18 |
| Sensitivity range (WACC 6.5–8.5% × TGR 1.5–3.5%) | See Sensitivity sheet |

---

## Model structure

| Sheet | Contents |
|---|---|
| **Sources** | Data sources and verification status (VERIFIED / APPROXIMATE / ESTIMATED) for every input |
| **Cover** | Navigation index |
| **Assumptions** | All forecast drivers (revenue growth, EBIT margins, D&A, CapEx, WACC inputs, DPS), with rationale column |
| **Income Statement** | 2020A–2030E; EBIT, EBITDA, Net Income; historical inputs verified from LH Annual Reports |
| **Balance Sheet** | Independently modelled current liabilities (no plug); Cash driven from CF waterfall; Equity roll-forward includes dividends |
| **Cash Flow** | Section A: FCFF (for DCF); Section B: indirect-method cash waterfall (drives BS cash — genuine 3-statement link) |
| **DCF Valuation** | FCFF-based, Gordon Growth terminal value; full equity bridge (EV → Net Debt → Equity Value → Implied Price) |
| **Comparables** | EV/EBITDA peer benchmarking: Ryanair, IAG, Air France-KLM, easyJet; median multiple → implied price |
| **Sensitivity** | 7×7 WACC × TGR table; implied share price at every combination |
| **Dashboard** | One-page summary: 6 KPI tiles, 11-year performance table, DCF & Comps side-by-side, mini sensitivity |

---

## Technical highlights

**3-statement integration (genuine, not cosmetic)**

- Cash Flow Section B uses an indirect method: Net Income → +D&A → ±Working Capital → Operating CF → −CapEx → ±Debt Changes → Ending Cash
- The Balance Sheet cash line for forecast years is a live link to CF ending cash (not an input)
- Equity roll-forward: `Prior Equity + Net Income − (DPS × Shares Outstanding)` — dividends explicitly modelled
- Balance check (`Total Assets − Total E&L`) is a real test; it is non-zero for historical years where inputs are estimated, and ~0 for forecast years confirming 3-statement consistency

**Balance Sheet design**

- Current liabilities are independently modelled (no plug):
  - Trade Payables = Revenue × 4.5%
  - Deferred Revenue (advance ticket sales) = Revenue × 9.0%
  - Other Current Liabilities = Revenue × 8.0%
- Non-current liabilities: Long-Term Borrowings decline via a debt repayment formula; Pension Obligations projected forward at −3%/yr (consistent with LH's IAS 19 OCI trend)

**WACC build-up from first principles**

```
Rf  = 2.50%   (10Y German Bund yield avg 2024, Deutsche Bundesbank)
β   = 1.20    (LHA.DE 5Y monthly vs STOXX 600, Bloomberg proxy)
ERP = 5.50%   (Damodaran Western Europe, Jan 2024)
Ke  = Rf + β × ERP = 9.10%

Kd  = 3.50%   (LH bond yields 2024; Baa3/BBB- rated)
t   = 25.0%
Kd(AT) = 2.625%

We  = 70%,  Wd = 30%
WACC = 70% × 9.10% + 30% × 2.625% ≈ 7.16%
```

**Financial Modelling Standards**

The model follows professional financial modelling best practices and industry conventions throughout.

Highlights include:
- Integrated Income Statement, Balance Sheet, and Cash Flow Statement with genuine 3-statement links
- Dynamic assumptions sheet driving all forecast schedules — change one input, the whole model updates
- DCF valuation using FCFF methodology with full equity bridge (EV → Net Debt → Equity → Implied Price)
- Comparable Company Analysis (EV/EBITDA) across four European airline peers
- WACC and Terminal Value calculated from first principles
- Sensitivity analysis across 49 WACC × TGR combinations
- Executive dashboard summarising financial performance and valuation outputs
- Industry colour coding: Blue = inputs, Black = formulas, Green = cross-sheet links, Orange = estimated

**Roadmap**

Planned enhancements include automated financial data refresh and continuous model validation via CI/CD (GitHub Actions).

---

## Data sources and verification

All inputs are tagged with a verification status on the Sources sheet. Key verified figures:

| Figure | Value | Source |
|---|---|---|
| Revenue 2022 | €32,770M | LH 2022 FY Press Release, 03-Mar-2023 (exact) |
| Revenue 2023 | €35,442M | LH IR key data page |
| Revenue 2024 | €37,581M | LH IR key data page |
| EBIT 2024 | €1,731M | LH IR key data page (Reported EBIT) |
| Net Income 2024 | €1,380M | LH IR key data page |
| Total Assets 2021 | €42,538M | LH 2022 FY Press Release comparative |
| Total Assets 2022 | €43,335M | LH Annual Report 2022 |
| Total Assets 2024 | €47,052M | LH Annual Report 2024 |
| Equity 2024 | €11,594M | LH Annual Report 2024 |
| Net Debt 2024 | €5,744M | LH IR net indebtedness figure |
| CapEx 2024 | €3,743M (gross) | LH IR key data page |
| D&A 2022 | €2,199M | LH 2023 AR comparative CF statement |

Figures tagged ESTIMATED or APPROXIMATE are documented with explanations on the Sources sheet. Notably:

- **2022 Equity (€8,500M):** The jump from ~€4.5bn (2021) to ~€8.5bn (2022) is driven by OCI pension remeasurement under IAS 19 — net pension obligations fell from ~€6.5bn to ~€2.0bn, flowing through Other Comprehensive Income, not the P&L. A simplified IS-based model cannot replicate this via Net Income alone; the cell is correctly kept as an estimate pending page-level verification against the LH AR 2022.

---

## Forecast assumptions

| Driver | 2025E | 2026E | 2027E | 2028E | 2029E | 2030E |
|---|---|---|---|---|---|---|
| Revenue growth | +5.0% | +4.0% | +4.0% | +3.0% | +3.0% | +2.5% |
| EBIT margin | 5.5% | 6.0% | 6.5% | 6.8% | 7.0% | 7.0% |
| D&A (€M) | 2,380 | 2,430 | 2,480 | 2,530 | 2,580 | 2,630 |
| CapEx (€M) | 3,600 | 3,500 | 3,400 | 3,300 | 3,200 | 3,100 |
| DPS (€) | 0.33 | 0.36 | 0.40 | 0.44 | 0.48 | 0.50 |

Rationale: LH management targets 8%+ Adjusted EBIT margin by 2028 (reported margin typically lags ~2–3pp). 2025E reflects partial recovery from industrial action costs (~€450M impact in 2024). Revenue growth assumes ITA Airways full-year consolidation adding ~€1.5B in 2025, then normalization toward terminal rate.

---

## Limitations (honest assessment)

This is an integrated financial forecasting and valuation model — not a fully detailed investment-banking-grade three-statement model.

- Historical 2020–2021 figures on the BS rely partly on estimated/interpolated data (documented on Sources sheet)
- The equity roll-forward uses `Prior + NI − Dividends`; it cannot capture OCI movements (pension remeasurement, FX translation) that were material for LH in 2022
- Comparables multiples are approximate (Q4 2024); market caps fluctuate daily — re-verify before use
- WACC weights (70/30) are target-capital-structure estimates, not market-value-weighted from live data

---

## How to use

Download `Lufthansa_Valuation_Model.xlsx` and open in Microsoft Excel (2016 or later recommended). All sheets are formula-linked — changing an assumption on the **Assumptions** sheet will flow through to the Income Statement, Balance Sheet, Cash Flow, DCF, and Dashboard automatically.

---

## Author

**Emmanuel Sarpong**  
FMVA® — Financial Modeling & Valuation Analyst, CFI (June 2026)  
[linkedin.com/in/e-sarpong](https://linkedin.com/in/e-sarpong) · [github.com/emmasarps](https://github.com/emmasarps)

> *Portfolio project. Not investment advice.*
