# Task 3: Valuation Analysis - Detailed Workflow

This document provides step-by-step instructions for executing Task 3 (Valuation Analysis) of the initiating-coverage skill.

## Task Overview

**Purpose**: 综合运用 PE / PB / PEG / DCF / EV/EBITDA 完成估值分析（A 股偏好 PE / PB，EV/EBITDA 仅辅助，DCF 用于成熟期与公用类）。

**Prerequisites**: ⚠️ Verify before starting
- **Required**: Financial model from Task 2
  - Projected income statements
  - Projected cash flows
  - Revenue and EBITDA forecasts
  - DCF inputs (unlevered FCF)

**⚠️ CRITICAL: DO NOT START THIS TASK UNLESS TASK 2 IS COMPLETE**

This task requires the financial model from Task 2. Starting without it will result in incomplete work.

**IF TASK 2 IS NOT COMPLETE**: Stop immediately and inform the user that Task 2 (Financial Modeling) must be completed first. Do not attempt to proceed or create placeholder valuations.

**Output**: Valuation Analysis (4-6 pages + Excel tabs)
- 主估值（PE / PB / PEG，A 股核心方法）含申万行业可比公司
- DCF 分析与敏感性表（成熟稳定期 / 公用类首选；高成长股辅助）
- 戈登增长模型（高分红蓝筹 / 银行 / 公用类适用）
- EV/EBITDA（重资产周期股辅助验证）
- 估值橄榄球图（Football Field）
- 目标价与五档评级（买入 / 增持 / 中性 / 减持 / 卖出）

---

## Input Verification

**BEFORE STARTING - CHECK:**
- [ ] Task 2 complete? (Financial model exists)
- [ ] Model file path/location known?
- [ ] Can access projected financials from model?

**Required from model:**
- [ ] Projected FCF (5 years)
- [ ] Revenue projections
- [ ] EBITDA projections
- [ ] Terminal year metrics
- [ ] Balance sheet data (debt, cash, shares)

**IF VERIFICATION FAILS**: Stop and complete Task 2 (Financial Modeling) before proceeding.

---

## Detailed Methodology Reference

For deep dive on valuation methodologies, formulas, and theory, see:
**[valuation-methodologies.md](valuation-methodologies.md)**

This workflow document focuses on execution steps. Reference the methodology file for:
- DCF theory and formulas
- WACC calculation details
- Terminal value methods
- Comparable companies theory
- Precedent transactions theory

---

## Step-by-Step Valuation Workflow

### Step 1: Extract Data from Financial Model

**From Task 2's financial model, extract:**

1. **Projected Financials (5 years)**
   - Revenue by year (2025E-2029E)
   - EBITDA by year
   - EBIT by year
   - Tax rate
   - D&A by year
   - CapEx by year
   - Change in NWC by year

2. **Unlevered Free Cash Flow**
   ```
   Extract from DCF Inputs tab in financial model:

                   2025E   2026E   2027E   2028E   2029E
   EBIT            $XXX    $XXX    $XXX    $XXX    $XXX
   × (1 - Tax Rate)
   = NOPAT         $XXX    $XXX    $XXX    $XXX    $XXX
   + D&A           $XXX    $XXX    $XXX    $XXX    $XXX
   - CapEx         ($XX)   ($XX)   ($XX)   ($XX)   ($XX)
   - Chg in NWC    ($XX)   ($XX)   ($XX)   ($XX)   ($XX)
   = Unlevered FCF $XXX    $XXX    $XXX    $XXX    $XXX
   ```

3. **Balance Sheet Data (current)**
   - Total debt
   - Cash & equivalents
   - Net debt (Debt - Cash)
   - Diluted shares outstanding

4. **Scenario Data**
   - Bull case revenue CAGR and terminal margin
   - Base case revenue CAGR and terminal margin
   - Bear case revenue CAGR and terminal margin

### Step 2: Build DCF Analysis

#### A. Calculate WACC

**1. 确定无风险利率（Risk-Free Rate）**
   - 使用 10 年期中国国债收益率（中国央行 / Wind 数据）
   - 当前参考区间：约 2.0-2.5%（2024-2026 年低利率环境）
   - 数据源：AKShare `bond_zh_us_rate` / Wind / 中债登

**2. 计算权益成本（CAPM）**
   ```
   Cost of Equity = Risk-Free Rate + Beta × Equity Risk Premium

   Inputs:
   - Risk-Free Rate: 当前 10Y 中国国债收益率（如 2.3%）
   - Beta: 沪深 300 或申万一级 / 二级行业指数 60 个月回归（AKShare / Tushare 可拉取）
   - Equity Risk Premium（A 股 ERP）: 5.5-7%（高于美股 4.5-5.5%，反映新兴市场风险溢价）

   Example:
   Cost of Equity = 2.3% + 1.2 × 6.0% = 9.5%
   ```

**3. 确定债务成本（Cost of Debt）**
   ```
   Cost of Debt = 公司当前借款利率（年报附注披露）或公司债到期收益率

   或参考行业基准：
   Cost of Debt = LPR（贷款基础利率，1Y / 5Y）+ 信用利差（按主体评级 AAA/AA+/AA）

   A 股参考：
   - AAA 级央国企：4.0-4.8%
   - AA+ 级地方国企 / 龙头民企：5.0-6.0%
   - AA 级民企：6.5-8.0%

   Example（高新技术企业，税率 15%）:
   Cost of Debt (pre-tax) = 5.0%
   Cost of Debt (after-tax) = 5.0% × (1 - 15%) = 4.25%

   Example（标准企业，税率 25%）:
   Cost of Debt (after-tax) = 5.0% × (1 - 25%) = 3.75%
   ```

**4. 确定资本结构**
   ```
   使用市场价值（而非账面价值）：

   股权市值 (E) = A 股收盘价 × 总股本
   债务市值 (D) = 短期借款 + 应付债券 + 长期借款 + 一年内到期非流动负债（年报口径，无可交易债券时用账面）
   总价值 (V) = E + D

   股权权重 = E / V
   债务权重 = D / V

   Example（典型 A 股消费股）:
   E = ¥50 亿（90.9%）
   D = ¥5 亿（9.1%）
   V = ¥55 亿（100%）
   ```

**5. Calculate WACC**
   ```
   WACC = (E/V × Cost of Equity) + (D/V × Cost of Debt × (1 - Tax Rate))

   Example（A 股标准企业，税率 25%）:
   WACC = (90.9% × 9.5%) + (9.1% × 5.0% × (1 - 25%))
   WACC = 8.64% + 0.34% = 8.98%

   Round to: 9.0% for base case

   注：A 股 WACC 经验区间约 7-11%，低于美股（10-14%），主因无风险利率偏低。
   - 银行 / 公用：6-8%
   - 消费 / 医药：8-10%
   - 科技 / 周期：9-12%
   ```

#### B. Calculate Terminal Value

**Method 1: 永续增长法（优先）**
```
Terminal Value = FCF(2029) × (1 + g) / (WACC - g)

Where:
- FCF(2029) = 模型末年 FCFF
- g = 永续增长率（建议 2.0-3.0%）
  - 不应超过长期中国 GDP 增长（当前约 4-5%，潜在增长率下行至 3-4%）
  - 中性建议 2.5%；高分红蓝筹与公用股 1.5-2%；高景气赛道 3%

Example:
FCF(2029) = ¥5 亿
g = 2.5%
WACC = 9.0%

Terminal Value = ¥5 亿 × (1.025) / (0.09 - 0.025)
Terminal Value = ¥5.125 亿 / 0.065 = ¥78.85 亿
```

**Method 2: 退出倍数法（备选）**
```
Terminal Value = EBITDA(2029) × Exit Multiple

Where:
- Exit Multiple = 申万行业内 A 股可比公司当前 EV/EBITDA 中位数（A 股偏好用 PE 退出，10-25x 区间）

Example:
EBITDA(2029) = ¥8 亿
Exit Multiple = 12x（消费类）

Terminal Value = ¥8 亿 × 12x = ¥96 亿
```

**Method 3: 戈登增长模型（高分红蓝筹 / 银行 / 公用类）**
```
P = D₁ / (r - g)

适用条件：稳定现金流 + 稳定分红率 + 永续经营
- 银行 / 高速 / 港口 / 电力 / 高分红蓝筹
- D₁ = 下一年股息
- r = 权益成本（无杠杆，因银行 / 保险口径）
- g = 永续增长率
```

**A 股建议优先级：消费 / 医药首选永续增长法；周期 / 制造首选退出倍数法；银行 / 公用首选戈登模型。**

#### C. Discount Cash Flows to Present Value

```
PV of Projected FCF = Σ [FCFt / (1 + WACC)^t] for t = 1 to 5

Example（WACC=9.0%）:
Year    FCF      Discount    PV of FCF
        (亿元)   Factor      (亿元)
2025    ¥2.5     1/(1.09)^1 = 0.917      ¥2.29
2026    ¥3.2     1/(1.09)^2 = 0.842      ¥2.69
2027    ¥3.9     1/(1.09)^3 = 0.772      ¥3.01
2028    ¥4.5     1/(1.09)^4 = 0.708      ¥3.19
2029    ¥5.0     1/(1.09)^5 = 0.650      ¥3.25
                              Total PV:  ¥14.43 亿

PV of Terminal Value = Terminal Value / (1 + WACC)^5
PV of Terminal Value = ¥78.85 亿 / (1.09)^5 = ¥78.85 亿 × 0.650 = ¥51.25 亿

Enterprise Value = ¥14.43 亿 + ¥51.25 亿 = ¥65.68 亿
```

#### D. Calculate Equity Value and Price Per Share

```
Enterprise Value                 ¥65.68 亿
- 净债务（有息负债 - 货币资金）   (¥4.5 亿)
+ 非经营性资产（交易性金融资产 / 长期股权投资可变现部分）  ¥0 亿
- 少数股东权益                    ¥0 亿
- 优先股 / 永续债                 ¥0 亿
= 股权价值                        ¥61.18 亿

总股本（亿股）                     1.00 亿股

每股价值 = ¥61.18 亿 / 1.00 亿股 = ¥61.18

当前股价：                         ¥42.00
隐含上行空间：                     45.7%
```

#### E. DCF Sensitivity Analysis **CRITICAL**

**Table 1: WACC vs. 永续增长率（A 股 WACC 区间 7-11%）**

Create 2-way sensitivity table:
```
每股价值 (¥)            永续增长率 g
WACC        1.5%    2.0%    2.5%    3.0%    3.5%
7.5%        ¥68     ¥73     ¥78     ¥84     ¥91
8.0%        ¥63     ¥67     ¥72     ¥77     ¥83
8.5%        ¥58     ¥62     ¥66     ¥70     ¥75
9.0%        ¥54     ¥57     ¥61     ¥65     ¥70
9.5%        ¥50     ¥53     ¥56     ¥60     ¥64
10.0%       ¥47     ¥50     ¥52     ¥56     ¥60
10.5%       ¥44     ¥46     ¥49     ¥52     ¥55

中性基准：WACC = 9.0%, g = 2.5% → ¥61
热力图：绿色（高值）→ 黄色 → 红色（低值）
```

**Table 2: 营收 CAGR vs. 终值年归母净利率（A 股偏好用净利率而非 EBITDA 利润率）**
```
每股价值 (¥)            归母净利率（2029E）
营收 CAGR       12%     15%     18%     21%     24%
10%             ¥42     ¥48     ¥54     ¥60     ¥66
15%             ¥48     ¥56     ¥63     ¥71     ¥78
20%             ¥56     ¥65     ¥74     ¥83     ¥92
25%             ¥65     ¥75     ¥86     ¥97     ¥108
30%             ¥75     ¥87     ¥99     ¥112    ¥125

中性基准：营收 CAGR = 20%, 归母净利率 = 18% → ¥74
```

### Step 3: Comparable Companies Analysis

#### A. Select Comparable Companies

**Selection Criteria:**
- Same industry/sector (primary requirement)
- Similar business model
- Comparable size (market cap, revenue)
- Similar growth profile
- Similar geographies

**Identify 5-10 peer companies:**
1. [Peer 1] - Direct competitor
2. [Peer 2] - Direct competitor
3. [Peer 3] - Adjacent player
4. [Peer 4] - Similar business model
5. [Peer 5] - Regional competitor
6. [Add 3-5 more]

**Document rationale for each peer selected.**

#### B. Gather Peer Financial Data

**For each comparable, gather:**
- Current stock price
- Shares outstanding (diluted)
- Market capitalization
- Total debt and cash (for EV calculation)
- Enterprise value
- LTM (Last Twelve Months) financials:
  - Revenue
  - EBITDA
  - EBIT
  - Net Income
- NTM (Next Twelve Months) consensus estimates
- Revenue growth rate
- EBITDA margin

**Data sources:**
- FactSet, CapitalIQ, Bloomberg (preferred)
- Company 10-Ks/10-Qs for actuals
- Consensus estimates from Yahoo Finance, Seeking Alpha (if pro tools unavailable)

#### C. Calculate Valuation Multiples

**For each peer, calculate:**
```
EV/Revenue (LTM) = Enterprise Value / LTM Revenue
EV/Revenue (NTM) = Enterprise Value / NTM Revenue (est.)
EV/EBITDA (LTM) = Enterprise Value / LTM EBITDA
EV/EBITDA (NTM) = Enterprise Value / NTM EBITDA (est.)
P/E (NTM) = Market Cap / NTM Net Income (est.)
```

#### D. Create Comparable Companies Table (MANDATORY FORMAT)

```
COMPARABLE COMPANIES ANALYSIS

Company      Ticker  Mkt Cap  EV/Rev  EV/Rev  EV/EBITDA  EV/EBITDA  P/E   Rev     EBITDA
                     ($B)     LTM     NTM     LTM        NTM        NTM   Growth  Margin
Peer A       PRA     45.2     3.5x    3.2x    15.2x      13.8x      25x   18%     23%
Peer B       PRB     32.8     3.2x    2.9x    14.1x      12.5x      22x   15%     23%
Peer C       PRC     28.5     2.8x    2.6x    12.8x      11.2x      20x   12%     22%
Peer D       PRD     52.1     4.1x    3.7x    17.5x      15.2x      29x   22%     23%
Peer E       PRE     38.9     3.6x    3.3x    15.8x      14.1x      25x   17%     23%
Peer F       PRF     41.2     3.7x    3.4x    16.1x      13.9x      26x   19%     23%
Peer G       PRG     35.5     3.3x    3.0x    14.5x      12.8x      23x   16%     22%

[Target]     TRGT    38.0     3.4x    3.1x    14.8x      13.0x      24x   17%     23%

STATISTICAL SUMMARY
Maximum              52.1     4.1x    3.7x    17.5x      15.2x      29x   22%     23%
75th Percentile      45.2     3.7x    3.4x    16.1x      14.1x      26x   19%     23%
Median               38.9     3.5x    3.2x    15.2x      13.8x      25x   17%     23%
25th Percentile      32.8     3.2x    2.9x    14.1x      12.5x      22x   15%     22%
Minimum              28.5     2.8x    2.6x    12.8x      11.2x      20x   12%     22%

Note: Market data as of [Date]. LTM = Last Twelve Months. NTM = Next Twelve Months.
Source: FactSet, company filings, [Analyst] estimates.
```

**CRITICAL**: The statistical summary (max/75th/median/25th/min) is MANDATORY.

#### E. Apply Multiples to Target Company

**Choose primary multiple (typically EV/EBITDA for mature companies):**

```
Target Company NTM EBITDA = $550M (from financial model)

Apply Median Peer Multiple:
Peer Median EV/EBITDA (NTM) = 13.8x
Implied EV = $550M × 13.8x = $7,590M

Apply 25th Percentile (Conservative):
25th Percentile EV/EBITDA (NTM) = 12.5x
Implied EV = $550M × 12.5x = $6,875M

Apply 75th Percentile (Optimistic):
75th Percentile EV/EBITDA (NTM) = 14.1x
Implied EV = $550M × 14.1x = $7,755M

Valuation Range (Comps): $6,875M - $7,755M
Midpoint: $7,315M

Convert to Equity Value:
Implied EV (Median)        $7,590M
- Net Debt                 ($450M)
= Implied Equity Value     $7,140M

Shares Outstanding         100M
Implied Price/Share        $71.40
```

**Justify Premium/Discount:**
- Target is growing 17% vs. peer median 17% → In-line
- Target EBITDA margin 23% vs. peer median 23% → In-line
- Target market position → [Justify premium/discount]
- **Conclusion**: Apply median multiple (no adjustment)

### Step 4: Precedent Transactions (Optional)

**Note**: Only if M&A is relevant for this sector/company.

#### A. Identify Relevant Transactions

**Search for 5-10 M&A deals:**
- Same industry, last 3-5 years
- Similar size (0.5x to 2x target's size)
- Announced and closed deals

**Example:**
```
PRECEDENT TRANSACTIONS ANALYSIS

Date     Target        Acquirer      Deal     EV/Rev  EV/EBITDA  Premium  Rationale
                                    Value($B)  LTM     LTM
Q1 2024  Comp A       Strategic      $5.2B    4.2x    16.5x      35%      Consolidation
Q3 2023  Comp B       PE Firm        $3.8B    3.8x    14.2x      28%      Platform
Q4 2023  Comp C       Strategic      $4.5B    4.0x    15.8x      32%      Geographic
Q2 2023  Comp D       Strategic      $6.1B    4.5x    17.2x      38%      Strategic fit
Q1 2023  Comp E       PE Firm        $3.2B    3.5x    13.5x      25%      Carve-out

Median                                        4.0x    15.8x      32%

Source: CapitalIQ, company filings, press releases.
```

#### B. Apply to Target Company

```
Target Company LTM EBITDA = $500M
Precedent Median EV/EBITDA (LTM) = 15.8x

Implied EV (Precedent) = $500M × 15.8x = $7,900M

Note: Precedent multiples typically 10-20% higher than trading comps
due to control premium and synergies.
```

### Step 5: Valuation Reconciliation

#### A. Create Valuation Summary Table

```
VALUATION SUMMARY

Method                  Low     Base    High    Weight  Weighted Value
DCF Analysis            $42     $46     $51     50%     $23.00
Trading Comps (NTM)     $64     $71     $78     40%     $28.40
Precedent Trans.        $70     $79     $88     10%     $7.90
                                                        -------
Weighted Average Target                         100%    $59.30

Rounded Price Target: $59.00

Current Price (as of [Date]):    $42.00
Upside to Target:                40% ($59.00 / $42.00 - 1)
```

#### B. Determine Weighting Rationale

**Typical Weighting:**
- DCF: 40-60% (higher when forecasts reliable)
- Trading Comps: 25-40% (reflects market sentiment)
- Precedent Trans: 10-25% (lower unless M&A likely)

**For this example:**
- DCF 50%: High confidence in projections
- Comps 40%: Robust peer set
- Precedent 10%: M&A unlikely near-term

#### C. Create Valuation Football Field Chart

```
VALUATION FOOTBALL FIELD

Method                  Low ◄────────── Range ──────────► High

DCF Analysis            $42 ▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓ $51

Trading Comps (NTM)     $64 ▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓ $78

Precedent Trans.        $70 ▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓ $88
                                          ↑
                                    Current: $42
─────────────────────────────────────────────────────────
Valuation Range         $42                          $88
Price Target: $59 (weighted average)

Color code:
- DCF: Blue
- Trading Comps: Green
- Precedent Trans: Orange
- Vertical line at current price: Red dashed
- Vertical line at target: Black solid
```

#### D. Scenario-Based Valuations

```
VALUATION BY SCENARIO

Scenario    Probability  Revenue  EBITDA    DCF      Comps    Weighted
                        CAGR     Margin    Value    Multiple  Avg
Bear Case   20%         18%      28%       $38      11.5x     $42
Base Case   60%         25%      32%       $46      13.8x     $59
Bull Case   20%         32%      36%       $58      16.0x     $82

Expected Value (probability-weighted): $59
```

### Step 6: Final Price Target & Recommendation

```
═══════════════════════════════════════════════════════════
INVESTMENT RECOMMENDATION
═══════════════════════════════════════════════════════════

Current Price:          $42.00 (as of [Date])
Price Target:           $59.00 (12-month)
Upside/(Downside):      +40.5%

Rating:                 BUY / OUTPERFORM

Valuation Methodology:  Based on weighted average of DCF (50%),
                       trading comparables (40%), and precedent
                       transactions (10%).

Time Horizon:          12 months

───────────────────────────────────────────────────────────
KEY INVESTMENT CATALYSTS
───────────────────────────────────────────────────────────

1. New Product Launch (Q2 2025)
   - Expected to drive 15-20% revenue acceleration
   - Already seeing strong pre-orders

2. Margin Expansion (FY2025-2026)
   - Operating leverage from scale
   - Path to 35% EBITDA margin (from current 28%)

3. Market Share Gains (Ongoing)
   - Taking share from legacy competitors
   - Net Promoter Score improvement

4. International Expansion (H2 2025)
   - Entry into European markets
   - Potential $200M incremental revenue opportunity

5. Potential M&A Target (12-18 months)
   - Strategic fit for larger players
   - Precedent transactions suggest 30-40% premium

───────────────────────────────────────────────────────────
KEY RISKS TO PRICE TARGET
───────────────────────────────────────────────────────────

Downside Risks:
1. Competitive Pressure (High probability, -15% impact)
   - New entrant launched competing product
   - Could pressure pricing and market share

2. Execution Risk (Medium probability, -10% impact)
   - New product launch delays or underperformance
   - Management turnover

3. Macro Slowdown (Medium probability, -20% impact)
   - Economic recession would impact customer spending
   - Operating leverage would reverse

4. Regulatory Risk (Low probability, -25% impact)
   - Potential new regulations in key market
   - Would increase compliance costs

Upside Risks:
1. M&A Bid (Low probability, +35% impact)
   - Strategic acquirer pays control premium

2. Beat-and-Raise (Medium probability, +10% impact)
   - Consistent outperformance vs. estimates

═══════════════════════════════════════════════════════════
```

---

## Quality Standards

### DCF Quality Checks
- [ ] WACC properly calculated with documented components
- [ ] Terminal value reasonable (< 70% of total enterprise value)
- [ ] Sensitivity analysis covers realistic ranges (±200-300bps for WACC, ±100bps for terminal growth)
- [ ] Unlevered FCF properly calculated from EBIT
- [ ] Enterprise to equity value bridge correct
- [ ] Share count is diluted shares, not basic

### Comparables Quality Checks
- [ ] 5-10 comparable companies selected
- [ ] Peer selection defensible (document why each peer was chosen)
- [ ] Statistical summary included (max/75th/median/25th/min) - MANDATORY
- [ ] Multiple selection appropriate (EV/EBITDA for mature, EV/Revenue for high-growth)
- [ ] Premium/discount justified with specific factors
- [ ] Data sourced properly with dates noted

### Overall Valuation Quality Checks
- [ ] At least 2 valuation methods used (DCF + Comps minimum)
- [ ] Weighting explained and appropriate
- [ ] Valuation range provided (low/base/high), not just point estimate
- [ ] Scenarios analyzed (Bull/Base/Bear)
- [ ] Sanity checks performed (see below)
- [ ] All assumptions documented with rationale

---

## Sanity Checks

**Always perform these validation checks:**

1. **Historical Multiple Check**
   - Is implied multiple in line with company's historical trading range?
   - If not, explain why

2. **Peer Comparison**
   - Is premium/discount vs. peers justified by fundamentals?
   - Check: growth, margins, market position

3. **Implied Growth Check**
   - What growth is market pricing in at current price?
   - Is that reasonable given company trajectory?

4. **Market Cap Reasonableness**
   - Does total market cap make sense given company size and peers?
   - Would company be too large/small relative to industry?

5. **Terminal Value Check**
   - Is terminal value < 60-70% of total enterprise value?
   - If > 70%, projections may not be long enough

6. **WACC Reasonableness**
   - Is WACC 8-14% range for typical companies?
   - Tech/high-growth: 10-14%
   - Mature/stable: 7-10%

7. **Implied Returns Check**
   - What IRR from current price to target over 12 months?
   - Is that consistent with recommendation rating?

---

## Output Files

Create the following deliverables:

### 1. Valuation Analysis Document
**File**: `[Company]_Valuation_Analysis_[Date].md` (written analysis)

**Contents** (4-6 pages):
- Executive summary with price target
- DCF analysis (1 page) with sensitivity table
- Comparable companies analysis (1 page) with statistical summary
- Precedent transactions (0.5 page) if applicable
- Valuation summary and football field (0.5 page)
- Investment recommendation (1 page)
- Key catalysts and risks (1 page)

### 2. Excel Valuation Tabs
**Add to Task 2's financial model file:** `[Company]_Financial_Model_[Date].xlsx`

**IMPORTANT**: Do NOT create a separate Excel file. Add these tabs to the existing financial model from Task 2. This keeps all quantitative data in one place.

**Tabs to add:**
- DCF tab with full calculations
- Sensitivity analysis tab
- Comps tab with peer data
- Precedent transactions tab (if applicable)
- Valuation summary tab

---

## Success Criteria

A successful valuation analysis should:
1. Use at least 2 methods (DCF + Comps minimum)
2. Include comprehensive DCF sensitivity analysis (2-way tables)
3. Include statistical summary in comps (max/75th/median/25th/min)
4. Provide valuation range (low/base/high), not point estimate
5. Document all key assumptions with clear rationale
6. Perform sanity checks
7. Arrive at defensible price target
8. Provide clear buy/hold/sell recommendation
9. Identify 3-5 key catalysts
10. Identify 3-5 key risks
11. Be auditable and transparent

---

## Next Steps

After completing Task 3, the valuation analysis will be used for:
- **Task 4 (Charts)**: Create DCF sensitivity heatmaps, valuation football field, scenario comparison charts
- **Task 5 (Report Assembly)**: Integrate valuation analysis into final report

The price target and recommendation are the foundation of the final investment recommendation in the equity research report.
