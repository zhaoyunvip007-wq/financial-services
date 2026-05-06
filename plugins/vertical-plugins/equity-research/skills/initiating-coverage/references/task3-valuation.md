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

**Selection Criteria（A 股可比公司选择）：**
- 同申万二级 / 三级行业（首要标准）
- 相似业务模式
- 可比规模（市值、营收）
- 相似增长曲线（营收 CAGR、ROE）
- 上市板块尽量匹配（主板 / 创业板 / 科创板，板块估值差异显著）
- 国央企 / 民企属性匹配（国资背景估值结构不同）

**Identify 5-10 A 股 / 港股可比公司：**
1. [Peer 1] - 申万行业内直接竞争对手（同三级行业）
2. [Peer 2] - 直接竞争对手
3. [Peer 3] - 同二级行业的相邻细分
4. [Peer 4] - 同业务模式
5. [Peer 5] - 区域龙头
6. [新增 3-5 家，覆盖龙头 / 中游 / 长尾，必要时纳入港股 H 股或行业龙头中概股做交叉验证]

**为每家可比公司说明选择理由。**

#### B. Gather Peer Financial Data

**For each comparable, gather:**
- 最新 A 股收盘价（前复权）
- 总股本与流通股本（亿股）
- 总市值（亿元）、流通市值
- 有息负债与货币资金（用于 EV 计算）
- 企业价值（EV = 市值 + 净债务 + 少数股东权益）
- TTM（最近四个季度）财务：
  - 营业总收入
  - 归母净利润、扣非归母净利润
  - 净资产、ROE、ROIC
  - EBITDA（计算项，年报附注核对）
- 当年 / 次年一致预期（券商研报均值）
- 营收 YoY 增速、归母净利润 YoY 增速
- 销售净利率、毛利率、ROE

**Data sources:**
- AKShare MCP / Tushare MCP（A 股结构化数据，免费 / 低成本，首选）
- Wind / 同花顺 iFinD / 东方财富 Choice（机构付费，含一致预期）
- 巨潮资讯网（年报 / 季报原始数据）
- 雪球 / 同花顺 / 东方财富（个股快速对标）
- 行业券商研报（中信 / 中金 / 招商等的行业组深度报告，含一致预期）

#### C. Calculate Valuation Multiples（A 股偏好倍数）

**For each peer, calculate（A 股核心倍数 PE / PB / PEG，EV/EBITDA 仅辅助）：**
```
PE (TTM) = 总市值 / TTM 归母净利润
PE (当年E) = 总市值 / 当年一致预期归母净利润
PE (次年E) = 总市值 / 次年一致预期归母净利润
PB (LF) = 总市值 / 最新一期归母净资产
PEG = PE (当年E) / 当年归母净利润同比增速 × 100
EV/EBITDA = 企业价值 / TTM EBITDA（辅助）
EV/Revenue = 企业价值 / TTM 营业总收入（辅助，亏损或低利润率公司用）
股息率 (TTM) = TTM 现金分红 / 总市值（高分红蓝筹核心指标）
ROE (TTM) = TTM 归母净利润 / 平均归母净资产
```

**A 股行业 PE/PB 经验区间（合理估值锚）：**
| 申万行业 | PE 中性区间 | PB 中性区间 | 备注 |
|---------|------------|------------|------|
| 白酒（食品饮料二级）| 25-40x | 6-10x | 龙头溢价显著 |
| 银行 | 4-7x | 0.5-1.2x | 估值压制，重在分红 |
| 新能源（电力设备）| 15-30x | 2-5x | 周期性强 |
| 医药创新（生物科技）| 30-80x | 4-10x | 管线驱动 |
| 半导体（电子）| 30-60x | 4-8x | 国产替代叙事 |
| 房地产 | 5-10x | 0.5-1.5x | NAV 优于 PE |
| 钢铁 / 化工（周期股） | 5-12x（周期低位） | 0.8-2x | PB 优于 PE |
| 公用事业 / 高速 | 10-15x | 1-2x | 戈登模型适用 |
| 消费电子 | 15-25x | 2-4x | 苹果链溢价 |
| 软件 / SaaS | 30-60x | - | PS 辅助 |

#### D. Create Comparable Companies Table (MANDATORY FORMAT)

```
申万行业可比公司估值表（数据截至 YYYY-MM-DD）

公司         股票代码    总市值    PE      PE      PB      PEG    股息率   ROE     营收增速
                       (亿元)    TTM     2025E   LF              TTM     TTM     YoY
可比公司 A   600XXX.SH   452     35.2x   28.5x    8.2x   1.2x   1.5%    22%     18%
可比公司 B   000XXX.SZ   328     32.5x   26.8x    7.5x   1.1x   2.0%    21%     15%
可比公司 C   002XXX.SZ   285     28.8x   24.2x    6.8x   1.0x   2.5%    19%     12%
可比公司 D   300XXX.SZ   521     41.5x   33.2x    9.5x   1.5x   1.0%    24%     22%
可比公司 E   600XXX.SH   389     36.6x   29.8x    8.5x   1.3x   1.8%    22%     17%
可比公司 F   688XXX.SH   412     37.4x   30.2x    8.8x   1.4x   1.2%    23%     19%
可比公司 G   002XXX.SZ   355     33.5x   27.4x    7.9x   1.2x   2.2%    20%     16%

[标的]       XXXXXX.XX   380     34.8x   28.0x    8.0x   1.2x   1.8%    21%     17%

统计摘要
最大值                    521     41.5x   33.2x    9.5x   1.5x   2.5%    24%     22%
75 分位                   452     37.4x   30.2x    8.8x   1.4x   2.2%    23%     19%
中位数                    389     35.2x   28.5x    8.2x   1.2x   1.8%    22%     17%
25 分位                   328     32.5x   26.8x    7.5x   1.1x   1.2%    20%     15%
最小值                    285     28.8x   24.2x    6.8x   1.0x   1.0%    19%     12%

注：市场数据截至 [日期]。TTM = 最近四个季度。LF = 最新一期（年报或半年报披露）。2025E = 当年一致预期。
来源：AKShare / Tushare、巨潮资讯网、Wind 一致预期。
```

**CRITICAL**: 统计摘要（max/75 分位 / 中位数 / 25 分位 / min）必须呈现。

#### E. Apply Multiples to Target Company

**A 股建议主估值倍数选择：**
- 成熟稳定盈利公司：PE（当年 E 或次年 E）
- 银行 / 房地产 / 重资产周期股：PB
- 高成长（30%+ 增速）：PEG
- 亏损或低利润率：PS（市销率）或 EV/Revenue
- 高分红蓝筹：股息贴现 / 戈登模型

**示例（消费股，主估值用 PE）：**
```
标的公司 2025E 归母净利润 = ¥5.5 亿（来自财务模型）

应用申万行业可比公司中位数倍数：
可比中位数 PE (2025E) = 28.5x
隐含市值 = ¥5.5 亿 × 28.5x = ¥156.75 亿

应用 25 分位（保守）：
25 分位 PE (2025E) = 26.8x
隐含市值 = ¥5.5 亿 × 26.8x = ¥147.4 亿

应用 75 分位（乐观）：
75 分位 PE (2025E) = 30.2x
隐含市值 = ¥5.5 亿 × 30.2x = ¥166.1 亿

估值区间（PE 法）：¥147.4 亿 - ¥166.1 亿
中点：¥156.8 亿

转换为每股价值：
隐含市值（中位数）     ¥156.75 亿
÷ 总股本                1.00 亿股
= 每股价值              ¥156.75 / 股
```

**给予溢价 / 折价的理由（A 股估值差异化考量）：**
- 标的营收增速 17% vs. 可比中位数 17% → 持平
- 标的 ROE 21% vs. 可比中位数 22% → 略低
- 标的市场地位 / 国央企背景 / 龙头溢价 → [说明溢价 / 折价]
- **A 股专属溢价 / 折价因子：**
  - 龙头溢价（行业第一）：+10-30%
  - 国央企背景（资金成本低 / 政策红利）：+5-15%
  - 大股东高质押 / 商誉占净资产高 / 业绩承诺到期临近：-10-25%
  - 限售股密集解禁（未来 6-12 个月）：-5-15%
  - 流通市值偏小（< 50 亿，流动性折价）：-10-20%
  - 高分红 + 低估值 + 高 ROE 三高：+10-20%
- **结论：** 给予中位数估值（无调整）/ 溢价 X% / 折价 X%

### Step 4: A 股并购重组案例对标（Optional）

**Note**: A 股并购重组活跃度低于美股，仅当目标行业近 3-5 年有可比 A 股重大重组（重大资产重组 / 借壳上市 / 产业整合）时使用。

#### A. Identify Relevant Transactions（A 股并购数据源）

**Search for 5-10 A 股 M&A 重组案例：**
- 同申万二级行业，最近 3-5 年
- 相似规模（0.5x 至 2x 标的规模）
- 已完成的重组（已通过证监会并购重组委审核 / 注册制下交易所审核）
- 数据源：巨潮资讯网"重大资产重组"专栏、Wind 并购数据库、上市公司公告

**Example（A 股并购重组案例对标）：**
```
A 股并购重组案例分析

公告日期    标的             收购方         交易     PE          PB     备注
                                          对价(亿元) (LTM)
2024Q1      A 公司           上市公司 A     ¥52     35.0x       6.5x   产业整合 / 横向并购
2023Q3      B 公司           产业基金       ¥38     30.5x       5.8x   平台型并购
2023Q4      C 公司           上市公司 C     ¥45     32.0x       6.2x   区域扩张
2023Q2      D 公司           上市公司 D     ¥61     38.5x       7.0x   战略协同
2023Q1      E 公司           上市公司 E     ¥32     28.5x       5.5x   分拆收购

中位数                                              32.0x       6.2x

来源：巨潮资讯网、Wind 并购数据库、上市公司重组报告书。
```

**注：A 股并购重组特殊考量：**
- 重组配套业绩承诺（通常 3-5 年承诺净利润 CAGR 15-30%）
- 商誉风险（并购溢价计入商誉，承诺期满后高发减值）
- 注册制下重组审核效率提升，但仍需关注交易所问询函

#### B. Apply to Target Company

```
标的 LTM 归母净利润 = ¥5.0 亿
A 股可比并购中位数 PE = 32.0x

隐含市值（并购对标）= ¥5.0 亿 × 32.0x = ¥160 亿

注：A 股并购倍数通常比二级市场可比公司溢价 10-30%（控制权溢价 + 协同效应）。
但 A 股并购对小市值公司（< 50 亿）有更明显的"借壳预期"溢价，需剔除壳价值因素。
```

### Step 5: Valuation Reconciliation

#### A. Create Valuation Summary Table

```
估值汇总（A 股以 PE 法为主，DCF 与 EV/EBITDA 辅助）

方法                       低     中性     高      权重    加权值
PE 可比公司法（主估值）    ¥147   ¥157   ¥166    50%     ¥78.50
DCF（永续增长）            ¥54    ¥61    ¥70     30%     ¥18.30
PB 可比公司法              ¥130   ¥145   ¥160    10%     ¥14.50
A 股并购重组对标           ¥150   ¥160   ¥175    10%     ¥16.00
                                                        -------
加权平均目标价                                  100%    ¥127.30

四舍五入目标价：¥127.00

当前股价（截至 [日期]）：           ¥100.00
目标空间：                          27%（¥127.00 / ¥100.00 - 1）
```

#### B. 权重分配理由

**A 股典型权重分配（与美股不同，主估值是 PE 而非 DCF）：**
- PE 法（主估值）：40-60%（A 股市场最常用，与卖方研报一致）
- DCF：20-40%（成熟稳定盈利公司高，高成长 / 周期股低）
- PB 法：10-30%（重资产 / 周期股高，轻资产消费股低）
- 戈登模型：高分红蓝筹 / 银行 / 公用事业 30-50%
- 并购重组对标：5-20%（A 股并购重组活跃度有限，仅作为补充）

**For this example（消费股）：**
- PE 法 50%：A 股市场主流估值锚
- DCF 30%：业绩稳定性较高
- PB 法 10%：辅助下限验证
- 并购对标 10%：补充验证

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
投资建议
═══════════════════════════════════════════════════════════

当前股价：                ¥100.00（截至 [日期]）
12 个月目标价：           ¥127.00
预期收益率：              +27%

评级：                    买入 / 增持 / 中性 / 减持 / 卖出（A 股五档评级）

估值方法：                以申万行业可比公司 PE 法为主（50%），
                          DCF 永续增长法（30%），PB 法（10%），
                          A 股并购重组对标（10%）综合加权。

时间窗口：                12 个月

A 股评级标准（参考券商研报惯例）：
- 买入：未来 12 个月跑赢行业指数 15% 以上
- 增持：跑赢行业指数 5-15%
- 中性：跑输行业指数 5% 至跑赢 5% 之间
- 减持：跑输行业指数 5-15%
- 卖出：跑输行业指数 15% 以上

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

6. **WACC Reasonableness（A 股区间）**
   - A 股 WACC 7-11% 区间合理（低于美股 8-14%，因无风险利率低）
   - 银行 / 公用：6-8%
   - 消费 / 医药：8-10%
   - 科技 / 周期：9-12%

7. **Implied Returns Check**
   - What IRR from current price to target over 12 months?
   - Is that consistent with recommendation rating?

---

## Output Files

Create the following deliverables:

### 1. Valuation Analysis Document
**File**: `[公司名]_[股票代码]_Valuation_Analysis_[Date].md` (written analysis)
示例：`贵州茅台_600519.SH_Valuation_Analysis_2026-05-06.md`

**Contents** (4-6 pages):
- Executive summary with price target
- DCF analysis (1 page) with sensitivity table
- Comparable companies analysis (1 page) with statistical summary
- Precedent transactions (0.5 page) if applicable
- Valuation summary and football field (0.5 page)
- Investment recommendation (1 page)
- Key catalysts and risks (1 page)

### 2. Excel Valuation Tabs
**追加到 Task 2 财务模型文件中：** `[公司名]_[股票代码]_Financial_Model_[Date].xlsx`

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
