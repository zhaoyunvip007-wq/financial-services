---
name: comps-analysis
description: |
  Build institutional-grade comparable company analyses with operating metrics, valuation multiples, and statistical benchmarking in Excel/spreadsheet format.

  **Perfect for:**
  - Public company valuation (M&A, investment analysis)
  - Benchmarking performance vs. industry peers
  - Pricing IPOs or funding rounds
  - Identifying valuation outliers (over/under-valued)
  - Supporting investment committee presentations
  - Creating sector overview reports

  **Not ideal for:**
  - Private companies without comparable public peers
  - Highly diversified conglomerates
  - Distressed/bankrupt companies
  - Pre-revenue startups
  - Companies with unique business models
---

# Comparable Company Analysis

## ⚠️ CRITICAL: 数据源优先级（先读这段）

**A 股数据源层级（必须按此顺序）：**

1. **首选：AKShare MCP / Tushare MCP** — 行情、财报、北向资金、龙虎榜、申万行业、机构持仓
2. **公告原文：巨潮资讯网（cninfo.com.cn）** — 上市公司年报/季报/重大事项公告，是法定披露源
3. **市场情绪与大V观点：雪球（用户账号 cookie）** — 当雪球 MCP 部署后启用
4. **机构付费数据（可选）：Wind / 同花顺 iFinD** — 团队/机构场景才考虑
5. **不要用 Google/百度搜索做主数据源** — 财经媒体二手转述常有口径错误，必须回到原始公告

**Why this matters：** A 股财报和公告以 CAS 中国会计准则披露，自带 Wind/同花顺/AKShare 这些渠道做了清洗，比海外数据库（Daloopa/FactSet/S&P Capital IQ）覆盖更全。优先用 MCP 拿结构化数据，公告原文做交叉验证。

---

## Overview
This skill teaches Claude to build institutional-grade comparable company analyses that combine operating metrics, valuation multiples, and statistical benchmarking. The output is a structured Excel/spreadsheet that enables informed investment decisions through peer comparison.

**Reference Material & Contextualization:**

An example comparable company analysis is provided in `examples/comps_example.xlsx`. When using this or other example files in this skill directory, use them intelligently:

**DO use examples for:**
- Understanding structural hierarchy (how sections flow)
- Grasping the level of rigor expected (statistical depth, documentation standards)
- Learning principles (clear headers, transparent formulas, audit trails)

**DO NOT use examples for:**
- Exact reproduction of format or metrics
- Copying layout without considering context
- Applying the same visual style regardless of audience

**ALWAYS ask yourself first:**
1. **"Do you have a preferred format or should I adapt the template style?"**
2. **"Who is the audience?"** (Investment committee, board presentation, quick reference, detailed memo)
3. **"What's the key question?"** (Valuation, growth analysis, competitive positioning, efficiency)
4. **"What's the context?"** (M&A evaluation, investment decision, sector benchmarking, performance review)

**Adapt based on specifics:**
- **Industry context**: Big tech mega-caps need different metrics than emerging SaaS startups
- **Sector-specific needs**: Add relevant metrics early (e.g., cloud ARR, enterprise customers, developer ecosystem for tech)
- **Company familiarity**: Well-known companies may need less background, more focus on delta analysis
- **Decision type**: M&A requires different emphasis than ongoing portfolio monitoring

**Core principle:** Use template principles (clear structure, statistical rigor, transparent formulas) but vary execution based on context. The goal is institutional-quality analysis, not institutional-looking templates.

User-provided examples and explicit preferences always take precedence over defaults.

## Core Philosophy
**"Build the right structure first, then let the data tell the story."**

Start with headers that force strategic thinking about what matters, input clean data, build transparent formulas, and let statistics emerge automatically. A good comp should be immediately readable by someone who didn't build it.

---

## ⚠️ CRITICAL: Formulas Over Hardcodes + Step-by-Step Verification

**Environment — Office JS vs Python:**
- **If running inside Excel (Office Add-in / Office JS):** Use Office JS directly (`Excel.run(async (context) => {...})`). Write formulas via `range.formulas = [["=E7/C7"]]`, not `range.values`. No separate recalc step — Excel handles it natively. Use `range.format.*` for colors/fonts.
- **If generating a standalone .xlsx file:** Use Python/openpyxl. Write `cell.value = "=E7/C7"` (formula string).
- Same principles either way — just translate the API calls.
- **Office JS merged cell pitfall:** Do NOT call `.merge()` then set `.values` on the merged range (throws `InvalidArgument` — range still reports its pre-merge dimensions). Instead write the value to the top-left cell alone, then merge + format the full range:
  ```js
  ws.getRange("A1").values = [["TECHNOLOGY — COMPARABLE COMPANY ANALYSIS"]];
  const hdr = ws.getRange("A1:H1");
  hdr.merge();
  hdr.format.fill.color = "#1F4E79";
  hdr.format.font.color = "#FFFFFF";
  hdr.format.font.bold = true;
  ```

**Formulas, not hardcodes:**
- Every derived value (margin, multiple, statistic) MUST be an Excel formula referencing input cells — never a pre-computed number pasted in
- When using Python/openpyxl to build the sheet: write `cell.value = "=E7/C7"` (formula string), NOT `cell.value = 0.687` (computed result)
- The only hardcoded values should be raw input data (revenue, EBITDA, share price, etc.) — and every one of those gets a cell comment with its source
- Why: the model must update automatically when an input changes. A hardcoded margin is a silent bug waiting to happen.

**Verify step-by-step with the user:**
- After setting up the structure → show the user the header layout before filling data
- After entering raw inputs → show the user the input block and confirm sources/periods before building formulas
- After building operating metrics formulas → show the calculated margins and sanity-check with the user before moving to valuation
- After building valuation multiples → show the multiples and confirm they look reasonable before adding statistics
- Do NOT build the entire sheet end-to-end and then present it — catch errors early by confirming each section

---

## Section 1: Document Structure & Setup

### Header Block (Rows 1-3) — A 股版本

```
Row 1: [行业] - A 股可比公司分析
Row 2: [公司列表带代码] • 公司一 (600519.SH) • 公司二 (000858.SZ) • 公司三 (000568.SZ)
Row 3: 截至 [报告期] | 单位：人民币百万元（除每股数据和比率外）| 行业分类：申万一级/二级
```

**A 股证券代码规则：**
- 沪市主板：60xxxx.SH（如贵州茅台 600519.SH）
- 沪市科创板：688xxx.SH
- 深市主板：000xxx.SZ / 001xxx.SZ
- 深市创业板：300xxx.SZ
- 北交所：8xxxxx.BJ

**Why this matters:** Establishes context immediately. Anyone opening this file knows what they're looking at, when it was created, and how to interpret the numbers.

### Visual Convention Standards (OPTIONAL - User preferences and uploaded templates always override)

**IMPORTANT: These are suggested defaults only. Always prioritize:**
1. User's explicit formatting preferences
2. Formatting from any uploaded template files
3. Company/team style guides
4. These defaults (only if no other guidance provided)

**Suggested Font & Typography:**
- **Font family**: Times New Roman (professional, readable, industry standard)
- **Font size**: 11pt for data cells, 12pt for headers
- **Bold text**: Section headers, company names, statistic labels

**Default Color & Shading — Professional Blue/Grey Palette (minimal is better):**
- **Keep it restrained** — only blues and greys. Do NOT introduce greens, oranges, reds, or multiple accent colors. A clean comps sheet uses 3-4 colors total.
- **Section headers** (e.g., "OPERATING STATISTICS & FINANCIAL METRICS"):
  - Dark blue background (`#1F4E79` or `#17365D` navy)
  - White bold text
  - Full row shading across all columns
- **Column headers** (e.g., "Company", "Revenue", "Margin"):
  - Light blue background (`#D9E1F2` or similar pale blue)
  - Black bold text
  - Centered alignment
- **Data rows**:
  - White background for company data
  - Black text for formulas; blue text for hardcoded inputs
- **Statistics rows** (Maximum, 75th Percentile, etc.):
  - Light grey background (`#F2F2F2`)
  - Black text, left-aligned labels
- **That's the whole palette**: dark blue + light blue + light grey + white. Nothing else unless the user's template says otherwise.

**Suggested Formatting Conventions:**
- **Decimal precision**:
  - Percentages: 1 decimal (12.3%)
  - Multiples: 1 decimal (13.5x)
  - Dollar amounts: No decimals, thousands separator (69,632)
  - Margins shown as percentages: 1 decimal (68.7%)
- **Borders**: No borders (clean, minimal appearance)
- **Alignment**: All metrics center-aligned for clean, uniform appearance
- **Cell dimensions**: All column widths should be uniform/even, all row heights should be consistent (creates clean, professional grid)

**Note:** If the user provides a template file or specifies different formatting, use that instead.

---

## Section 2: Operating Statistics & Financial Metrics

### Core Columns (Start with these)
1. **Company** - Names with consistent formatting
2. **Revenue** - Size metric (can be LTM, quarterly, or annual depending on context)
3. **Revenue Growth** - Year-over-year percentage change
4. **Gross Profit** - Revenue minus cost of goods sold
5. **Gross Margin** - GP/Revenue (fundamental profitability)
6. **EBITDA** - Earnings before interest, tax, depreciation, amortization
7. **EBITDA Margin** - EBITDA/Revenue (operating efficiency)

### Optional Additions (Choose based on industry/purpose)
- **Quarterly vs LTM** - Include both if seasonality matters
- **Free Cash Flow** - For capital-intensive or SaaS businesses
- **FCF Margin** - FCF/Revenue (cash generation efficiency)
- **Net Income** - For mature, profitable companies
- **Operating Income** - For businesses with varying D&A
- **CapEx metrics** - For asset-heavy industries
- **Rule of 40** - Specifically for SaaS (Growth % + Margin %)
- **FCF Conversion** - For quality of earnings analysis (advanced)

### Formula Examples (Using Row 7 as example)
```excel
// Core ratios - these are always calculated
Gross Margin (F7): =E7/C7
EBITDA Margin (H7): =G7/C7

// Optional ratios - include if relevant
FCF Margin: =[FCF]/[Revenue]
Net Margin: =[Net Income]/[Revenue]
Rule of 40: =[Growth %]+[FCF Margin %]
```

**Golden Rule:** Every ratio should be [Something] / [Revenue] or [Something] / [Something from this sheet]. Keep it simple.

### Statistics Block (After company data)

**CRITICAL: Add statistics formulas for all comparable metrics (ratios, margins, growth rates, multiples).**

```
[Leave one blank row for visual separation]
- Maximum: =MAX(B7:B9)
- 75th Percentile: =QUARTILE(B7:B9,3)
- Median: =MEDIAN(B7:B9)
- 25th Percentile: =QUARTILE(B7:B9,1)
- Minimum: =MIN(B7:B9)
```

**Columns that NEED statistics (comparable metrics):**
- Revenue Growth %, Gross Margin %, EBITDA Margin %, EPS
- EV/Revenue, EV/EBITDA, P/E, Dividend Yield %, Beta

**Columns that DON'T need statistics (size metrics):**
- Revenue, EBITDA, Net Income (absolute size varies by company scale)
- Market Cap, Enterprise Value (not comparable across different-sized companies)

**Note:** Add one blank row between company data and statistics rows for visual separation. Do NOT add a "SECTOR STATISTICS" or "VALUATION STATISTICS" header row.

**Why quartiles matter:** They show distribution, not just average. A 75th percentile multiple tells you what "premium" companies trade at.

---

## Section 3: Valuation Multiples & Investment Metrics

### Core Valuation Columns (Start with these)
1. **Company** - Same order as operating section
2. **Market Cap** - Current market valuation
3. **Enterprise Value** - Market Cap ± Net Debt/Cash
4. **EV/Revenue** - How much market pays per dollar of sales
5. **EV/EBITDA** - How much market pays per dollar of earnings
6. **P/E Ratio** - Price relative to net earnings

### Optional Valuation Metrics (Choose based on context)
- **FCF Yield** - FCF/Market Cap (for cash-focused analysis)
- **PEG Ratio** - P/E/Growth Rate (for growth companies)
- **Price/Book** - Market value vs. book value (for asset-heavy businesses)
- **ROE/ROA** - Return metrics (for profitability comparison)
- **Revenue/EBITDA CAGR** - Historical growth rates (for trend analysis)
- **Asset Turnover** - Revenue/Assets (for operational efficiency)
- **Debt/Equity** - Leverage (for capital structure analysis)

**Key Principle:** Include 3-5 core multiples that matter for your industry. Don't include every possible metric just because you can.

### Formula Examples
```excel
// Core multiples - always include these
EV/Revenue: =[Enterprise Value]/[LTM Revenue]
EV/EBITDA: =[Enterprise Value]/[LTM EBITDA]
P/E Ratio: =[Market Cap]/[Net Income]

// Optional multiples - include if data available
FCF Yield: =[LTM FCF]/[Market Cap]
PEG Ratio: =[P/E]/[Growth Rate %]
```

### Cross-Reference Rule
**CRITICAL:** Valuation multiples MUST reference the operating metrics section. Never input the same raw data twice. If revenue is in C7, then EV/Revenue formula should reference C7.

### Statistics Block
Same structure as operating section: Max, 75th, Median, 25th, Min for every metric. Add one blank row for visual separation between company data and statistics. Do NOT add a "VALUATION STATISTICS" header row.

---

## Section 4: Notes & Methodology Documentation

### Required Components

**Data Sources & Quality:**
- Where did the data come from? (S&P Kensho MCP, FactSet MCP, Daloopa MCP, Bloomberg, SEC filings)
- What period does it cover? (Q4 2024, audited figures)
- How was it verified? (Cross-checked against 10-K/10-Q)
- Note: Prioritize MCP data sources (S&P Kensho, FactSet, Daloopa) if available for better accuracy and traceability

**Key Definitions:**
- EBITDA calculation method (Gross Profit + D&A, or Operating Income + D&A)
- Free Cash Flow formula (Operating CF - CapEx)
- Special metrics explained (Rule of 40, FCF Conversion)
- Time period definitions (LTM, CAGR calculation periods)

**Valuation Methodology:**
- How was Enterprise Value calculated? (Market Cap + Net Debt)
- What growth rates were used? (Historical CAGR, forward estimates)
- Any adjustments made? (One-time items excluded, normalized margins)

**Analysis Framework:**
- What's the investment thesis? (Cloud/SaaS efficiency)
- What metrics matter most? (Cash generation, capital efficiency)
- How should readers interpret the statistics? (Quartiles provide context)

---

## Section 5: Choosing the Right Metrics (Decision Framework)

### Start with "What question am I answering?"

**"Which company is undervalued?"**
→ Focus on: EV/Revenue, EV/EBITDA, P/E, Market Cap
→ Skip: Operational details, growth metrics

**"Which company is most efficient?"**
→ Focus on: Gross Margin, EBITDA Margin, FCF Margin, Asset Turnover
→ Skip: Size metrics, absolute dollar amounts

**"Which company is growing fastest?"**
→ Focus on: Revenue Growth %, EBITDA CAGR, User/Customer Growth
→ Skip: Margin metrics, leverage ratios

**"Which is the best cash generator?"**
→ Focus on: FCF, FCF Margin, FCF Conversion, CapEx intensity
→ Skip: EBITDA, P/E ratios

### A 股行业指标选择（按申万一级分类）

**白酒（食品饮料-白酒）：**
必备：营收增速、销售毛利率（70%+ 是行业基线）、净利率、预收账款（合同负债）、ROE
可选：吨价、产能利用率、经销商数量
不要：CapEx 强度、研发费用率（占比极低）

**新能源（电力设备-电池/光伏/风电）：**
必备：营收增速、毛利率、海外营收占比、产能（GWh/GW）、研发费用率
可选：单位投资强度、库存周转、现金循环天数
不要：仅看 PE（周期股需结合景气位置看 PB+ROE）

**银行（银行）：**
必备：ROE、净息差（NIM）、不良率、拨备覆盖率、PB（A 股银行核心估值锚）
可选：核心一级资本充足率、零售贷款占比、中收占比
不要：毛利率、EBITDA（银行不适用）

**券商（非银金融-证券）：**
必备：ROE、PB、自营投资收益占比、经纪业务市占率、两融余额
可选：投行储备项目、资管 AUM
不要：毛利率（券商不披露此口径）

**医药（医药生物）：**
必备：营收增速、毛利率、研发费用率、销售费用率、PE（成长性强）
可选：管线进度、获批品种数、集采影响
注意：仿制药 vs 创新药估值逻辑完全不同

**消费电子/半导体（电子）：**
必备：营收增速、毛利率、研发费用率、客户集中度、ROE
可选：晶圆产能、设备国产化率、产品代际
不要：单看 PE（半导体周期波动大，参考 PB 和景气）

**军工（国防军工）：**
必备：营收增速、订单（中报/年报披露）、应收账款周转、毛利率
可选：合同负债、关联交易占比（军工集团内部）
注意：业绩季节性强，Q4 集中确认收入

**地产（房地产）：**
必备：销售额、毛利率、负债率、净负债率（"三道红线"指标）、PB
可选：土储面积、存货周转、回款率
不要：单看 PE（地产 PE 失真严重，PB-NAV 更合适）

### The "5-10 Rule"

**5 operating metrics** - Revenue, Growth, 2-3 margins/efficiency metrics
**5 valuation metrics** - Market Cap, EV, 3 multiples
**= 10 total columns** - Enough to tell the story, not so many you lose the thread

If you have more than 15 metrics, you're probably including noise. Edit ruthlessly.

---

## Section 6: Best Practices & Quality Checks

### Before You Start
1. **Define the peer group** - Companies must be truly comparable (similar business model, scale, geography)
2. **Choose the right period** - LTM smooths seasonality; quarterly shows trends
3. **Standardize units upfront** - Millions vs. billions decision affects everything
4. **Map data sources** - Know where each number comes from

### As You Build
1. **Input all raw data first** - Complete the blue text before writing formulas
2. **Add cell comments to ALL hard-coded inputs** - Right-click cell → Insert Comment → Document source OR assumption

   **For sourced data, cite exactly where it came from:**
   - Example: "Bloomberg Terminal - MSFT Equity DES, accessed 2024-10-02"
   - Example: "Q4 2024 10-K filing, page 42, line item 'Total Revenue'"
   - Example: "FactSet consensus estimate as of 2024-10-02"
   - **Include hyperlinks when possible**: Right-click cell → Link → paste URL to SEC filing, data source, or report

   **For assumptions, explain the reasoning:**
   - Example: "Assumed 15% EBITDA margin based on peer median, company does not disclose"
   - Example: "Estimated Enterprise Value as Market Cap + $50M net debt (from Q3 balance sheet, Q4 not yet available)"
   - Example: "Forward P/E based on street consensus EPS of $3.45 (average of 12 analyst estimates)"

   **Why this matters**: Enables audit trails, data verification, assumption transparency, and future updates
3. **Build formulas row by row** - Test each calculation before moving on
4. **Use absolute references for headers** - $C$6 locks the header row
5. **Format consistently** - Percentages as percentages, not decimals
6. **Add conditional formatting** - Highlight outliers automatically

### Sanity Checks
- **Margin test**: Gross margin > EBITDA margin > Net margin (always true by definition)
- **A 股估值合理范围（按申万行业经验）：**
  - PE：白酒 25-40x、新能源 15-30x、银行 4-8x、券商 10-25x、医药创新 30-80x、传统制造 10-25x
  - PB：银行 0.5-1.2x、券商 1-2x、白酒 8-15x、地产 0.5-1.5x、消费电子 2-5x
  - PS：科创板/创业板成长股 5-20x，传统消费 1-5x
  - PEG：< 1 偏低估、1-2 合理、> 2 偏高估（仅适用稳定增长公司）
  - ROE：消费龙头 > 20% 是常态，工业 10-15%，银行 10-13%，公用 5-10%
- **A 股估值经验法则：** 同行业内龙头给 1.2-1.5x 估值溢价，二线给 0.7-0.9x 折价
- **成长 vs 估值匹配**：高增长（>30%）通常给高 PE，但要看是否有可持续性（白酒、消费电子常被周期错杀）

### Common Mistakes to Avoid
❌ Mixing market cap and enterprise value in formulas
❌ Using different time periods for numerator and denominator (LTM vs quarterly)
❌ Hardcoding numbers into formulas instead of cell references
❌ **Hard-coded inputs without cell comments citing the source OR explaining the assumption**
❌ Missing hyperlinks to SEC filings or data sources when available
❌ Including too many metrics without clear purpose
❌ Including non-comparable companies (different business models)
❌ Using outdated data without disclosure
❌ Calculating averages of percentages incorrectly (should be median)

---

## Section 6: Advanced Features

### Dynamic Headers
For columns showing calculations, use clear unit labels:
```
Revenue Growth (YoY) % | EBITDA Margin | FCF Margin | Rule of 40
```

### Quartile Analysis Benefits
Instead of just mean/median, quartiles show:
- **75th percentile** = "Premium" companies trade here
- **Median** = Typical market valuation
- **25th percentile** = "Discount" territory

This helps answer: "Is our target company trading rich or cheap vs. peers?"

### Industry-Specific Modifications

**Software/SaaS:**
- Add: ARR, Net Dollar Retention, CAC Payback Period
- Emphasize: Rule of 40, FCF margins, gross margins >70%

**Healthcare:**
- Add: R&D/Revenue, Pipeline value, Regulatory status
- Emphasize: EBITDA margins, growth rates, reimbursement risk

**Industrials:**
- Add: Backlog, Order book trends, Geographic mix
- Emphasize: ROIC, asset turnover, cyclical adjustments

**Consumer:**
- Add: Same-store sales, Customer acquisition cost, Brand value
- Emphasize: Revenue growth, gross margins, inventory turns

---

## Section 7: Workflow & Practical Tips

### Step-by-Step Process
1. **Set up structure** (30 minutes)
   - Create all headers
   - Format cells (blue for inputs, black for formulas)
   - Lock in units and date references

2. **Gather data** (60-90 minutes)
   - Pull from primary sources (S&P Kensho MCP, FactSet MCP, Daloopa MCP if available; otherwise Bloomberg, SEC)
   - Input all raw numbers in blue
   - Document sources in notes section

3. **Build formulas** (30 minutes)
   - Start with simple ratios (margins)
   - Progress to multiples (EV/Revenue)
   - Add cross-checks (do margins make sense?)

4. **Add statistics** (15 minutes)
   - Copy formula structure for all columns
   - Verify ranges are correct (B7:B9, not B7:B10)
   - Check quartile logic

5. **Quality control** (30 minutes)
   - Run sanity checks
   - Verify formula references
   - Check for #DIV/0! or #REF! errors
   - Compare against known benchmarks

6. **Documentation** (15 minutes)
   - Complete notes section
   - Add data sources
   - Define methodologies
   - Date-stamp the analysis

### Pro Tips
- **Save templates**: Build once, reuse forever
- **Color-code outliers**: Conditional formatting for values >2 standard deviations
- **Link to source files**: Hyperlink to Bloomberg screenshots or SEC filings
- **Version control**: Save as "Comps_v1_2024-12-15" with clear dating
- **Collaborative reviews**: Have someone else check your formulas

### Excel Formatting Checklist (Optional - adapt to user preferences)
- [ ] Font set to user's preferred style (default: Times New Roman, 11pt data, 12pt headers)
- [ ] Section headers formatted per user's template (default: dark blue #17365D with white bold text)
- [ ] Column headers formatted per user's template (default: light blue/gray #D9E2F3 with black bold text)
- [ ] Statistics rows formatted per user's template (default: light gray #F2F2F2)
- [ ] No borders applied (clean, minimal appearance)
- [ ] **Column widths set to uniform/even width** (creates clean, professional appearance)
- [ ] **Row heights set to consistent height** (typically 20-25pt for data rows)
- [ ] Numbers formatted with proper decimal precision and thousands separators
- [ ] **All metrics center-aligned** for clean, uniform appearance
- [ ] **One blank row for separation between company data and statistics rows**
- [ ] **No separate "SECTOR STATISTICS" or "VALUATION STATISTICS" header rows**
- [ ] **Every hard-coded input cell has a comment with either: (1) exact data source, OR (2) assumption explanation**
- [ ] **Hyperlinks added to cells where applicable** (SEC filings, data provider pages, reports)

---

## Section 8: Example Template Layout

**Simple Version (从这里开始) — A 股白酒行业示例：**
```
┌─────────────────────────────────────────────────────────────┐
│ 白酒 - A 股可比公司分析（申万：食品饮料-白酒Ⅱ）              │
│ 贵州茅台 (600519.SH) • 五粮液 (000858.SZ) • 泸州老窖 (000568.SZ) │
│ 截至 2025Q4 | 单位：人民币亿元                                │
├─────────────────────────────────────────────────────────────┤
│ 经营指标                                                      │
├──────────┬─────────┬─────────┬──────────┬─────────┬────────┤
│ 公司     │ 营收    │ 营收增速 │ 销售毛利 │ 归母净利│ 净利率  │
│          │ (LTM)   │ (YoY)   │ 率       │ (LTM)   │        │
├──────────┼─────────┼─────────┼──────────┼─────────┼────────┤
│ 贵州茅台 │ 1,693   │ 15.7%   │ 91.9%    │ 826     │ 48.8%  │
│ 五粮液   │   832   │  9.2%   │ 75.3%    │ 304     │ 36.5%  │
│ 泸州老窖 │   311   │ 10.8%   │ 88.4%    │ 132     │ 42.5%  │
│          │         │         │          │         │        │ [blank row]
│ Median   │ =MEDIAN │ =MEDIAN │ =MEDIAN  │ =MEDIAN │=MEDIAN │
│ 75th %   │ =QUART  │ =QUART  │ =QUART   │ =QUART  │=QUART  │
│ 25th %   │ =QUART  │ =QUART  │ =QUART   │ =QUART  │=QUART  │
├─────────────────────────────────────────────────────────────┤
│ VALUATION MULTIPLES                                         │
├──────────┬──────────┬──────────┬──────────┬────────────────┤
│ Company  │ Mkt Cap  │ EV       │ EV/Rev   │ EV/EBITDA │ P/E│
├──────────┼──────────┼──────────┼──────────┼───────────┼────┤
│ MSFT     │3,550,000 │3,530,000 │ 13.5x    │ 17.2x     │36.0│
│ GOOGL    │2,030,000 │1,960,000 │  5.6x    │  8.2x     │24.5│
│ AMZN     │2,226,000 │2,320,000 │  3.6x    │ 15.2x     │58.3│
│          │          │          │          │           │    │ [blank row]
│ Median   │ =MEDIAN  │ =MEDIAN  │ =MEDIAN  │ =MEDIAN   │=MED│
│ 75th %   │ =QUART   │ =QUART   │ =QUART   │ =QUART    │=QRT│
│ 25th %   │ =QUART   │ =QUART   │ =QUART   │ =QUART    │=QRT│
└──────────┴──────────┴──────────┴──────────┴───────────┴────┘
```

**Add complexity only when needed:**
- Include quarterly AND LTM if seasonality matters
- Add FCF metrics if cash generation is key story
- Include industry-specific metrics (Rule of 40 for SaaS, etc.)
- Add more statistics rows if you have >5 companies

---

## Section 9: Industry-Specific Additions (Optional)

Only add these if they're critical to your analysis. Most comps work fine with just core metrics.

**Software/SaaS:**
Add if relevant: ARR, Net Dollar Retention, Rule of 40

**Financial Services:**
Add if relevant: ROE, Net Interest Margin, Efficiency Ratio

**E-commerce:**
Add if relevant: GMV, Take Rate, Active Buyers

**Healthcare:**
Add if relevant: R&D/Revenue, Pipeline Value, Patent Timeline

**Manufacturing:**
Add if relevant: Asset Turnover, Inventory Turns, Backlog

---

## Section 10: Red Flags & Warning Signs

### Data Quality Issues
🚩 Inconsistent time periods (mixing quarterly and annual)  
🚩 Missing data without explanation  
🚩 Significant differences between data sources (>10% variance)

### Valuation Red Flags
🚩 Negative EBITDA companies being valued on EBITDA multiples (use revenue multiples instead)  
🚩 P/E ratios >100x without hypergrowth story  
🚩 Margins that don't make sense for the industry

### Comparability Issues
🚩 不同财年末（A 股统一 12 月 31 日，但港股/美股可能不同）
🚩 把纯主业公司和多元集团混为一谈
🚩 主营完全不同的公司被标为"可比"

### A 股专属红旗（必查）
🚩 **ST / *ST 股票** — 财务异常或退市风险，估值逻辑完全不同
🚩 **商誉占净资产 > 30%** — 减值风险，每年报会爆雷
🚩 **大股东质押比例 > 70%** — 平仓风险传导到股价
🚩 **应收账款增速 > 营收增速 2 倍** — 收入质量存疑
🚩 **关联交易占营收 > 30%** — 利润可能被关联方调节
🚩 **限售股近期解禁占流通盘 > 10%** — 短期抛压
🚩 **审计意见非"标准无保留"** — 保留意见/否定意见/无法表示意见都是危险信号
🚩 **频繁更换审计机构** — 治理问题征兆
🚩 **次新股（上市 < 1 年）** — 估值不稳定，业绩变脸高发期

**有疑问就剔除。** 3 个干净的可比公司，好过 6 个有问题的。

---

## Section 11: Formulas Reference Guide

### Essential Excel Formulas
```excel
// Statistical Functions
=AVERAGE(range)          // Simple mean
=MEDIAN(range)           // Middle value
=QUARTILE(range, 1)      // 25th percentile
=QUARTILE(range, 3)      // 75th percentile
=MAX(range)              // Maximum value
=MIN(range)              // Minimum value
=STDEV.P(range)          // Standard deviation

// Financial Calculations
=B7/C7                   // Simple ratio (Margin)
=SUM(B7:B9)/3            // Average of multiple companies
=IF(B7>0, C7/B7, "N/A")  // Conditional calculation
=IFERROR(C7/D7, 0)       // Handle divide by zero

// Cross-Sheet References
='Sheet1'!B7             // Reference another sheet
=VLOOKUP(A7, Table1, 2)  // Lookup from data table
=INDEX(MATCH())          // Advanced lookup

// Formatting
=TEXT(B7, "0.0%")        // Format as percentage
=TEXT(C7, "#,##0")       // Thousands separator
```

### Common Ratio Formulas
```excel
Gross Margin = Gross Profit / Revenue
EBITDA Margin = EBITDA / Revenue
FCF Margin = Free Cash Flow / Revenue
FCF Conversion = FCF / Operating Cash Flow
ROE = Net Income / Shareholders' Equity
ROA = Net Income / Total Assets
Asset Turnover = Revenue / Total Assets
Debt/Equity = Total Debt / Shareholders' Equity
```

---

## Key Principles Summary

1. **Structure drives insight** - Right headers force right thinking
2. **Less is more** - 5-10 metrics that matter beat 20 that don't
3. **Choose metrics for your question** - Valuation analysis ≠ efficiency analysis
4. **Statistics show patterns** - Median/quartiles reveal more than average
5. **Transparency beats complexity** - Simple formulas everyone understands
6. **Comparability is king** - Better to exclude than force a bad comp
7. **Document your choices** - Explain which metrics and why in notes section

---

## Output Checklist

Before delivering a comp analysis, verify:
- [ ] All companies are truly comparable
- [ ] Data is from consistent time periods
- [ ] Units are clearly labeled (millions/billions)
- [ ] Formulas reference cells, not hardcoded values
- [ ] **All hard-coded input cells have comments with either: (1) exact data source with citation, OR (2) clear assumption with explanation**
- [ ] **Hyperlinks added where relevant** (SEC EDGAR filings, Bloomberg pages, research reports)
- [ ] Statistics include at least 5 metrics (Max, 75th, Med, 25th, Min)
- [ ] Notes section documents sources and methodology
- [ ] Visual formatting follows conventions (blue = input, black = formula)
- [ ] Sanity checks pass (margins logical, multiples reasonable)
- [ ] Date stamp is current ("As of [Date]")
- [ ] Formula auditing shows no errors (#DIV/0!, #REF!, #N/A)

---

## Continuous Improvement

After completing a comp analysis, ask:
1. Did the statistics reveal unexpected insights?
2. Were there any data gaps that limited analysis?
3. Did stakeholders ask for metrics you didn't include?
4. How long did it take vs. how long should it take?
5. What would make this more useful next time?

The best comp analyses evolve with each iteration. Save templates, learn from feedback, and refine the structure based on what decision-makers actually use.
