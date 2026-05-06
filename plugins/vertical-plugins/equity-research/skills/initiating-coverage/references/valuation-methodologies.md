# Valuation Methodologies for A 股 Equity Research

This reference document provides comprehensive guidance on A 股市场常用估值方法：PE / PB / PEG（A 股主估值），DCF（永续增长法 / 退出倍数法），戈登增长模型（高分红蓝筹 / 银行 / 公用类），EV/EBITDA（辅助），以及 A 股并购重组对标。

## Table of Contents

1. [A 股主估值方法：PE / PB / PEG](#a-股主估值方法pe-pb-peg)
2. [Discounted Cash Flow (DCF) Analysis](#discounted-cash-flow-dcf-analysis)
3. [Gordon 戈登增长模型（高分红蓝筹 / 银行 / 公用类）](#gordon-戈登增长模型)
4. [可比公司分析（Trading Comparables）](#trading-comparables-analysis)
5. [A 股并购重组对标（Precedent Transactions）](#precedent-transactions-analysis)
6. [估值汇总（Valuation Reconciliation）](#valuation-reconciliation)
7. [A 股行业 PE/PB 经验区间](#a-股行业-pepb-经验区间)

---

## A 股主估值方法：PE / PB / PEG

### Overview

A 股市场以 PE / PB / PEG 为主流估值方法，与美股以 EV/EBITDA 与 DCF 为主显著不同。原因：
- A 股投资者结构以散户和公募基金为主，对 PE / PB 接受度高
- 卖方研报（中信 / 中金 / 招商 / 国君等）目标价大多由 PE × 预测 EPS 推导
- A 股利息税盾、研发资本化、商誉减值等会计特殊性，使 EV/EBITDA 失真

### A 股估值方法适用矩阵

| 公司类型 | 主估值 | 辅助估值 | 备注 |
|---------|-------|---------|------|
| 成熟稳定盈利（消费 / 医药）| PE | DCF, PEG | 卖方惯用 PE × EPS |
| 高成长（30%+ 增速，半导体 / 创新药）| PEG | PE, PS | PEG < 1 通常被认为低估 |
| 银行 / 保险 / 房地产 / 重资产周期 | PB | ROE-PB | 关注 PB-ROE 匹配度 |
| 高分红蓝筹 / 公用 / 高速 | 戈登模型 | PE | 看股息率与永续增长 |
| 亏损 / 低利润率（科创板早期）| PS | EV/Revenue | 关注收入质量 |
| 周期股（化工 / 钢铁 / 有色）| PB（周期低位）| PE（周期高位）| PB 抗周期 |

### PE 估值法

```
目标市值 = 当年 / 次年一致预期归母净利润 × 行业可比 PE 中位数
目标股价 = 目标市值 / 总股本
```

**A 股 PE 倍数选择：**
- 用申万二级 / 三级行业可比公司 PE 中位数（5-10 家可比）
- 给予溢价 / 折价（龙头 +10-30%、国央企 +5-15%、高质押 -10-25%、解禁压力 -5-15%）
- 当年 PE 优于 TTM PE（一致预期更前瞻）

### PB 估值法

```
目标市值 = 最新归母净资产 × 行业可比 PB 中位数
```

**适用：**
- 银行（PB 0.5-1.2x）
- 保险（PEV 内含价值倍数 + PB）
- 房地产（NAV 净资产价值法 + PB）
- 周期股低点（PB < 1 抄底信号）

### PEG 估值法

```
PEG = PE / 归母净利润年复合增速 × 100

PEG < 1：相对低估
PEG = 1：合理
PEG > 1：相对高估
```

**适用：高成长股（25%+ 增速），如半导体、创新药、SaaS。**

---

---

## Discounted Cash Flow (DCF) Analysis

### Overview

DCF analysis values a company based on the present value of its projected future cash flows. This is considered the most theoretically sound valuation method as it's based on fundamental value creation.

### Step-by-Step DCF Process

#### 1. Historical Financial Analysis
- Collect 3-5 years of historical financials
- Calculate historical FCF = EBIT(1-Tax Rate) + D&A - CapEx - Change in NWC
- Analyze historical growth rates and margins
- Identify trends and cyclicality

#### 2. Build Revenue Projections (5-10 years)
**Approaches:**
- **Top-down**: Start with market size (TAM) → Market share → Revenue
- **Bottom-up**: Units sold × Price per unit
- **Hybrid**: Combine multiple drivers

**Key Considerations:**
- Management guidance and historical growth
- Industry growth rates and market trends
- Competitive dynamics and market share evolution
- Product pipeline and new market opportunities
- Macroeconomic factors

#### 3. Project Operating Expenses
- **COGS**: As % of revenue (analyze historical margins)
- **SG&A**: Often semi-fixed; model as % of revenue with scale effects
- **R&D**: Critical for tech/pharma; model as % of revenue
- **D&A**: Based on CapEx assumptions

**Calculate EBIT** = Revenue - COGS - Operating Expenses

#### 4. Calculate Unlevered Free Cash Flow
```
EBIT
× (1 - Tax Rate)
= NOPAT (Net Operating Profit After Tax)
+ Depreciation & Amortization
- Capital Expenditures
- Increase in Net Working Capital
= Unlevered Free Cash Flow (UFCF)
```

**CapEx Assumptions:**
- Maintenance CapEx: Required to maintain current operations (typically 2-4% of revenue)
- Growth CapEx: Required for expansion
- Consider industry benchmarks and company guidance

**Net Working Capital:**
- NWC = (Accounts Receivable + Inventory) - Accounts Payable
- Model as % of revenue or days (DSO, DIO, DPO)
- An increase in NWC is a use of cash

#### 5. Determine Terminal Value

**Method A: 永续增长法**
```
Terminal Value = FCF(final year) × (1 + g) / (WACC - g)
```
- g = 永续增长率（建议 2-3%，不超过中国长期 GDP 潜在增速 3-4%）
- 中性建议 2.5%；高分红蓝筹与公用股 1.5-2%；高景气赛道 3%
- 适用于成熟稳定盈利公司

**Method B: 退出倍数法**
```
Terminal Value = 净利润 / EBITDA(final year) × Exit Multiple
```
- A 股偏好用 PE 退出（10-25x 区间），EBITDA 倍数（8-15x）作为辅助
- 退出倍数基于当前申万行业可比公司中位数
- 更适合周期股

#### 6. Calculate Weighted Average Cost of Capital (WACC)

```
WACC = (E/V × Cost of Equity) + (D/V × Cost of Debt × (1 - Tax Rate))
```

**Cost of Equity (using CAPM)：**
```
Cost of Equity = Risk-Free Rate + Beta × Equity Risk Premium
```
- Risk-Free Rate：10 年期中国国债收益率（当前约 2.0-2.5%，AKShare / Wind / 中债登）
- Beta：标的股票回归沪深 300 或申万一级 / 二级行业指数（60 个月）
- Equity Risk Premium（A 股 ERP）：5.5-7%（高于美股 4.5-5.5%，反映新兴市场风险溢价）

**Cost of Debt（A 股口径）：**
```
Cost of Debt = LPR（贷款基础利率，1Y / 5Y）+ 信用利差
或 = 公司年报附注披露的实际借款利率
或 = 公司债 / 中票到期收益率
```
- A 股主体评级参考：
  - AAA 级央国企：4.0-4.8%
  - AA+ 级地方国企 / 龙头民企：5.0-6.0%
  - AA 级民企：6.5-8.0%

**Capital Structure（A 股口径）：**
- E/V = 总市值 / (总市值 + 有息负债)
- D/V = 有息负债 / (总市值 + 有息负债)；有息负债 = 短期借款 + 应付债券 + 长期借款 + 一年内到期非流动负债
- 使用目标资本结构（如非当前）

**A 股 WACC 经验区间：**
- 银行 / 公用：6-8%
- 消费 / 医药：8-10%
- 科技 / 周期：9-12%
- 整体显著低于美股（10-14%），主因无风险利率偏低

#### 7. Discount Cash Flows to Present Value

```
PV = Σ [FCFt / (1 + WACC)^t] + [Terminal Value / (1 + WACC)^n]
```

#### 8. Calculate Enterprise Value and Equity Value

```
Enterprise Value = PV of Projected FCF + PV of Terminal Value
Less: Net Debt (Total Debt - Cash)
Plus: Non-operating Assets
Less: Minority Interest
Less: Preferred Stock
= Equity Value

Price Per Share = Equity Value / Diluted Shares Outstanding
```

### DCF Sensitivity Analysis

Always perform sensitivity analysis on key variables:

1. **Two-way sensitivity table**: WACC vs. Terminal Growth Rate
2. **Revenue growth scenarios**: Base / Bull / Bear cases
3. **Margin assumptions**: Operating leverage scenarios
4. **Terminal multiple sensitivity**: If using exit multiple method

**Example Sensitivity Table（A 股 WACC 区间）：**
```
           永续增长率 g
WACC      2.0%    2.5%    3.0%
8.0%      ¥67     ¥72     ¥77
9.0%      ¥57     ¥61     ¥65
10.0%     ¥50     ¥52     ¥56
```

### Common DCF Pitfalls to Avoid

1. **重复计入增长**：高增长须对应资本开支与营运资本投入
2. **永续增长率过高**：不应超过中国长期 GDP 潜在增速 3-4%
3. **忽视周期性**：周期股需用正常化盈利建模（PB 估值优于 PE）
4. **现金流口径错误**：必须用 FCFF（无杠杆 FCF），不要用净利润
5. **假设不一致**：贴现率应与现金流口径匹配（FCFF → WACC）
6. **A 股专属陷阱：** 营业利润含投资收益与公允价值变动，不等同于美股 EBIT；建模时应"营业利润 - 投资收益 - 公允价值变动"还原至经营性 EBIT
7. **税率混淆**：A 股标准税率 25%，高新技术企业 15%，西部大开发 / 海南自贸 15%，需按公司实际有效税率建模

---

## Gordon 戈登增长模型

### Overview

戈登增长模型适用于稳定现金流 + 稳定分红 + 永续经营的公司。A 股典型适用对象：

- 国有大行（工建中农、招商银行）
- 公用事业（长江电力、华能水电）
- 高速公路（招商公路、宁沪高速）
- 港口（上港集团）
- 高分红消费蓝筹（美的集团、格力电器）

### 公式

```
P = D₁ / (r - g)

其中：
- P = 每股内在价值
- D₁ = 下一年股息（每股）
- r = 权益成本（A 股 8-10% 区间）
- g = 永续增长率（1-3%，不超过 GDP 潜在增速）
```

### 与 PB-ROE 框架结合（银行 / 保险常用）

```
合理 PB = (ROE - g) / (r - g)

例：
ROE = 12%, r = 9%, g = 3%
合理 PB = (0.12 - 0.03) / (0.09 - 0.03) = 1.5x
```

**示例（A 股银行股）：**
- 工商银行：ROE 11%, 股息率 5.5%, 永续增长 2%
- r = 8%（保守估计 A 股银行权益成本）
- 合理 PB = (0.11 - 0.02) / (0.08 - 0.02) = 1.5x
- 当前 PB ~0.6x，估值显著低估（但市场长期压制，慎做反转）

---

## Trading Comparables Analysis

### Overview

Trading comps values a company based on how similar companies are valued in the public markets. This reflects current market sentiment and relative valuation.

### Step-by-Step Comps Process

#### 1. Select Comparable Companies

**Selection Criteria（A 股可比公司选择）：**
- 同申万二级 / 三级行业（首要标准）
- 相似业务模式
- 可比规模（市值、营收）
- 相似增长曲线（营收 CAGR、ROE）
- 上市板块尽量匹配（主板 / 创业板 / 科创板，板块估值差异显著）
- 国央企 / 民企属性匹配

**Typical Universe：**
- Start with 8-15 A 股 / 港股可比
- Remove 特殊情况公司（重大重组中、被 ST、停牌）
- Final set of 5-10 公司

#### 2. Gather Financial Information

**Required Data（A 股口径）：**
- 当前 A 股收盘价（前复权）与总股本 / 流通股本
- 最新定期报告（年报 / 半年报）财务数据
- 当年 / 次年一致预期（Wind / 同花顺 iFinD）
- 历史增长率（最近 3-5 年）

**Calculate Market Metrics：**
- 总市值 = A 股股价 × 总股本
- 企业价值 = 总市值 + 有息负债 + 少数股东权益 + 优先股 - 货币资金
- 净负债 = 有息负债 - 货币资金（A 股有息负债 = 短期借款 + 应付债券 + 长期借款 + 一年内到期非流动负债）

#### 3. Calculate Valuation Multiples（A 股偏好倍数）

**A 股核心倍数（PE / PB / PEG 为主）：**
- **PE (TTM / 当年E / 次年E)**：A 股最常用，卖方研报标准
- **PB (LF 最新一期)**：银行 / 保险 / 房地产 / 周期股核心
- **PEG**：高成长股（30%+ 增速）
- **股息率 (TTM)**：高分红蓝筹核心指标
- **ROE (TTM)**：杜邦三要素拆解必查

**辅助倍数（EV 类，用于交叉验证）：**
- **EV/Revenue**：早期 / 高增长 / 亏损公司
- **EV/EBITDA**：辅助验证（注意 A 股营业利润含投资收益与公允价值变动，需还原经营性 EBITDA）
- **PS (Price/Sales)**：亏损 / 低利润率公司

**计算口径：**
- TTM（最近四个季度滚动）：通过最新季报或半年报推算
- 当年 E：Wind / 同花顺一致预期
- 次年 E：Wind / 同花顺一致预期

#### 4. Analyze and Select Multiples

**A 股可比公司表（PE / PB / PEG 为主）：**

| 公司 | 股票代码 | 总市值（亿元）| PE TTM | PE 2025E | PB LF | PEG | 股息率 TTM | ROE TTM | 营收增速 |
|------|---------|--------------|--------|----------|-------|-----|-----------|---------|---------|
| 可比 A | 600XXX.SH | 100 | 35.2x | 28.5x | 8.2x | 1.2x | 1.5% | 22% | 18% |
| 可比 B | 000XXX.SZ | 80  | 32.5x | 26.8x | 7.5x | 1.1x | 2.0% | 21% | 15% |
| ...    | ...      | ... | ...   | ...   | ...  | ...  | ...  | ...  | ...  |
| 中位数 |          | -   | **35.0x** | **28.0x** | **7.8x** | **1.2x** | **1.8%** | **22%** | **17%** |

**数据源：AKShare / Tushare / Wind / 同花顺 iFinD。**

**Adjustments:**
- Remove outliers (typically >2 standard deviations)
- Consider using median instead of mean (less affected by outliers)
- Weight multiples if some comps are more comparable
- Adjust for differences in growth, margins, risk

#### 5. Apply Multiples to Target Company

**Example Calculation（A 股 PE 法）：**
```
标的 2025E 归母净利润 = ¥5.5 亿
申万行业可比公司 PE (2025E) 中位数 = 28.0x
隐含总市值 = ¥5.5 亿 × 28.0x = ¥154 亿

总股本 = 1.00 亿股
隐含每股价值 = ¥154.00 / 股
```

#### 6. Select Appropriate Multiple

**A 股选择标准：**
- **PE (当年/次年 E)**：成熟稳定盈利公司（消费 / 医药 / 龙头制造）
- **PB**：银行、保险（PEV）、房地产（NAV）、周期股低位
- **PEG**：高成长股（25%+ 增速，半导体 / 创新药 / SaaS）
- **PS**：亏损 / 低利润率公司（科创板早期、未盈利上市）
- **戈登模型 / 股息贴现**：高分红蓝筹（公用 / 高速 / 银行）
- **EV/EBITDA**：辅助验证（注意 A 股营业利润口径差异）

### 给予溢价 / 折价分析（A 股专属因子）

**A 股估值溢价 / 折价因子：**
- 龙头溢价（行业第一）：+10-30%
- 国央企背景（资金成本低 / 政策红利）：+5-15%
- 高成长 / 高 ROE（ROE > 行业 1.5x）：+10-20%
- 大股东高质押（>50%）/ 商誉占净资产高（>30%）：-10-25%
- 限售股密集解禁（未来 6-12 个月 >总股本 15%）：-5-15%
- 流通市值偏小（< 50 亿，流动性折价）：-10-20%
- 实控人变更 / 高管减持密集：-5-15%
- 业绩承诺到期临近（重组对赌期满）：-10-20%
- 高分红 + 低估值 + 高 ROE 三高：+10-20%
- 板块估值差异（科创板 > 创业板 > 主板）

**示例：**
- 增速 25% vs 行业中位数 18%：成长溢价 +15%
- 国央企 + 龙头：+10%
- 大股东质押率 60%：-15%
- 综合溢价：+10%

---

## A 股并购重组对标（Precedent Transactions Analysis）

### Overview

A 股并购重组活跃度低于美股，但仍有重要参考价值。A 股并购特点：
- 重大资产重组需经证监会并购重组委（注册制下交易所）审核
- 配套业绩承诺 + 对赌（通常 3-5 年承诺净利润 CAGR 15-30%）
- 商誉风险（并购溢价计入商誉，承诺期满后高发减值）
- 借壳上市预期（小市值公司）会扭曲倍数

### Step-by-Step Process

#### 1. Identify Relevant A 股 Transactions

**Selection Criteria：**
- 同申万二级行业
- 相似规模（标的 0.5x 至 2x）
- 相似业务特征
- 近 3-5 年已完成的重组
- 已通过证监会 / 交易所审核的交易（剔除终止 / 失败案例）

**Typical Universe：**
- A 股并购案例 5-10 个
- 重视近期案例（最近 1-2 年权重更高）

#### 2. Gather Transaction Details（A 股口径）

**Required Information：**
- 公告日期（首次披露 / 通过审核 / 完成过户）
- 交易对价（现金 / 股份 / 现金+股份）
- 标的资产截至基准日的财务数据（评估报告披露）
- 业绩承诺与补偿方案
- 配套募集资金用途
- 控制权溢价（以二级市场未受影响价为基准）

**Sources：**
- 巨潮资讯网"重大资产重组"专栏
- 上市公司重组报告书 / 评估报告
- Wind 并购数据库
- 交易所审核问询函

#### 3. Calculate Transaction Multiples（A 股口径）

**与可比公司倍数相同，但基于交易对价（A 股偏好 PE / PB）：**

```
交易总对价 = 现金对价 + 股份对价（按发行价折算）+ 承担债务 - 标的现金

并购 PE = 交易对价 / 标的 LTM 归母净利润
并购 PB = 交易对价 / 标的最新归母净资产
EV/EBITDA（辅助）= 交易企业价值 / 标的 LTM EBITDA
```

**计算控制权溢价：**
```
控制权溢价 = (并购对价 - 未受影响股价对应市值) / 未受影响市值
```
- 未受影响股价 = 重组首次披露前 20-60 个交易日均价（A 股证监会规定）
- A 股并购控制权溢价典型区间：10-30%（低于美股 20-40%，因 A 股流通股权较分散）

#### 4. Analyze A 股 Precedent Transactions

**A 股并购案例对标表：**

| 公告日期 | 标的 | 收购方 | 交易对价 | 并购 PE | 并购 PB | 溢价 | 备注 |
|---------|------|-------|---------|---------|---------|------|------|
| 2024Q1 | A 公司 | 上市公司 A | ¥52 亿 | 35.0x | 6.5x | 25% | 横向并购 |
| 2023Q3 | B 公司 | 产业基金 | ¥38 亿 | 30.5x | 5.8x | 18% | 平台型并购 |
| 中位数 | - | - | - | **32.5x** | **6.0x** | **22%** | - |

#### 5. Apply to Target Company

**Important Considerations（A 股专属）：**
- 并购倍数通常比二级市场可比公司溢价 10-30%（含控制权溢价 + 协同效应）
- 配套业绩承诺会人为抬高估值（承诺期内的"虚高利润"）
- 注意小市值公司的"借壳上市预期"溢价（剔除壳价值）
- 政策环境影响（证监会并购重组政策周期）
- 权重最近案例（最近 1-2 年）

**Example Calculation：**
```
标的 LTM 归母净利润 = ¥4.5 亿
A 股并购中位数 PE = 32.5x（含控制权溢价）
申万行业可比 PE 中位数 = 28.0x

并购法隐含市值 = ¥4.5 亿 × 32.5x = ¥146.3 亿
PE 法隐含市值 = ¥4.5 亿 × 28.0x = ¥126.0 亿

隐含控制权溢价 = ¥146.3 亿 / ¥126.0 亿 - 1 = 16%
```

### Adjustments to Transaction Multiples（A 股专属考量）

**Consider adjusting for：**
- **市场环境**：A 股牛市 / 熊市并购活跃度差异显著
- **买方类型**：产业方（战略协同）vs 财务投资者（PE / VC）
- **协同效应**：横向整合 vs 纵向延伸 vs 多元化
- **竞争格局**：单一竞标 vs 多家竞标
- **时间价值**：A 股 2018 年前并购倍数显著偏高（杠杆并购泡沫期），需大幅折价
- **业绩承诺剔除**：承诺期内的协议价应还原至自然增长口径
- **借壳预期剔除**：小市值标的（< 30 亿）的并购倍数含壳价值，需扣除

---

## Valuation Reconciliation

### Creating a Valuation Bridge

Present all three methods in a single framework:

**A 股估值汇总示例（PE 法主导）：**

| 方法 | 隐含市值（亿元）| 每股价值（元）| 权重 | 加权值（元）|
|------|----------------|--------------|------|------------|
| PE 可比公司法（主估值）| ¥154 | ¥154.00 | 50% | ¥77.00 |
| DCF 永续增长法 | ¥66  | ¥61.00 | 30% | ¥18.30 |
| PB 可比公司法 | ¥130 | ¥130.00 | 10% | ¥13.00 |
| A 股并购重组对标 | ¥146 | ¥146.00 | 10% | ¥14.60 |
| **加权平均目标价** | - | **¥122.90** | - | **¥122.90** |

### Weighting the Methods（A 股典型权重）

**A 股权重分配（与美股不同，主估值是 PE 而非 DCF）：**
- **PE 法（主估值）**：40-60%（A 股市场最常用，与卖方研报一致）
- **DCF**：20-40%（成熟稳定盈利公司高，高成长 / 周期股低）
- **PB 法**：10-30%（重资产 / 周期股高，轻资产消费股低）
- **戈登模型**：高分红蓝筹 / 银行 / 公用事业 30-50%
- **并购重组对标**：5-20%（A 股并购重组活跃度有限，仅作为补充）

**Adjust weights based on：**
- **预测置信度**：可见度高 → DCF / 戈登模型权重高
- **市场环境**：牛市 → 可比公司法权重高；熊市 → DCF 权重高
- **并购可能性**：行业整合期 → 并购对标权重高
- **公司类型**：
  - 成熟稳定盈利：PE 50% + DCF 30% + PB 10% + 并购 10%
  - 高成长（30%+）：PEG 40% + PE 30% + DCF 20% + PS 10%
  - 银行 / 公用：PB 40% + 戈登模型 40% + PE 20%
  - 周期股：PB 50% + PE（周期高位除外）30% + DCF（正常化）20%
  - 房地产：NAV 50% + PB 30% + 其他 20%

### Valuation Range

Always present a valuation range, not a point estimate:

**Approach:**
- **Base Case**: Most likely scenario
- **Bull Case**: Optimistic assumptions (revenue growth, margins)
- **Bear Case**: Conservative assumptions

**Example（A 股口径）：**
```
悲观情景：¥95 - ¥105
中性情景：¥120 - ¥130
乐观情景：¥150 - ¥165

评级：买入（A 股五档评级）
12 个月目标价：¥125（中性情景中点）
当前股价 ¥100，预期收益率 +25%（跑赢申万行业指数 15% 以上）
```

### Sanity Checks

**Cross-check valuation with:**
1. **Historical multiples**: Is current valuation in line with history?
2. **Peer comparison**: Justified premium/discount vs. peers?
3. **Implied growth**: What growth is market pricing in?
4. **Implied returns**: IRR from current price to target price
5. **Market cap analysis**: Does total market cap make sense?

---

## A 股行业 PE/PB 经验区间

A 股不同申万行业估值差异巨大，建立"合理估值锚"是研究第一步。下表为典型行业历史中位数（仅供参考，需结合当前市场环境与公司基本面调整）：

| 申万行业 | PE 中性区间 | PB 中性区间 | 备注 |
|---------|------------|------------|------|
| 食品饮料 - 白酒 | 25-40x | 6-10x | 龙头溢价显著 |
| 食品饮料 - 大众品 | 20-30x | 3-6x | |
| 银行 | 4-7x | 0.5-1.2x | 估值长期压制，重在分红 |
| 非银金融 - 保险 | 8-15x | 1-2.5x | PEV 内含价值更准 |
| 非银金融 - 券商 | 10-20x | 1-2x | 强周期 |
| 房地产 | 5-10x | 0.5-1.5x | NAV 优于 PE |
| 电力设备 - 新能源 | 15-30x | 2-5x | 周期性增强 |
| 电子 - 半导体 | 30-60x | 4-8x | 国产替代叙事 |
| 医药生物 - 创新药 | 30-80x | 4-10x | 管线驱动，亏损用 PS |
| 医药生物 - CXO | 20-40x | 4-8x | 周期回落 |
| 计算机 - 软件 | 30-60x | 6-12x | PS 辅助 |
| 计算机 - SaaS | 30-80x（盈利后）| - | 早期用 PS / EV/Sales |
| 通信 | 15-25x | 2-4x | 成熟期 |
| 传媒 - 游戏 | 15-25x | 2-5x | |
| 传媒 - 影视 | 20-35x | 1.5-3x | |
| 钢铁 / 化工（强周期）| 5-12x（周期低位）| 0.8-2x | PB 优于 PE |
| 有色金属 | 10-20x | 1.5-3x | 商品价格驱动 |
| 公用事业 - 电力 | 10-15x | 1-2x | 戈登模型适用 |
| 公用事业 - 水务 / 燃气 | 12-18x | 1.5-2.5x | |
| 交通运输 - 高速公路 | 8-12x | 1-2x | 高分红 + 戈登模型 |
| 交通运输 - 港口 / 机场 | 15-25x | 1.5-3x | |
| 汽车 - 整车（合资）| 8-15x | 1-2x | |
| 汽车 - 新能源车 | 20-40x | 3-6x | |
| 汽车 - 零部件 | 15-25x | 2-4x | |
| 家用电器 - 白电 | 12-18x | 2-3.5x | 龙头高分红 |
| 家用电器 - 黑电 / 小家电 | 15-25x | 2-4x | |
| 农林牧渔 - 养殖（周期）| 10-15x（周期低位）| 1-3x | PB 优于 PE |
| 国防军工 | 30-60x | 3-6x | 估值偏高 |
| 机械 - 工程机械 | 8-15x | 1-2.5x | 强周期 |
| 机械 - 通用机械 | 15-25x | 1.5-3x | |
| 商业贸易 / 零售 | 15-25x | 1.5-3x | |
| 纺织服装 | 10-18x | 1.5-3x | |
| 建筑装饰 - 央企基建 | 5-10x | 0.6-1x | 估值长期压制 |
| 建筑材料 - 水泥 | 6-12x（周期低位）| 0.8-1.5x | 强周期 |

**注：**
1. 上述区间为历史中位数，需结合当前市场无风险利率环境调整。利率下行时整体估值中枢上移
2. 龙头公司可在区间上沿，腰部 / 尾部在区间下沿
3. 政策驱动行业（如新能源 / 半导体 / 创新药）短期估值会大幅偏离历史中位数
4. 强周期行业（钢铁 / 化工 / 养殖）慎用 PE，应用 PB-ROE 框架

---

## Conclusion

A 股估值需综合运用 PE / PB / PEG（主估值）、DCF / 戈登模型（理论估值）、可比公司法（市场比较）、并购重组对标（控制权溢价）多种方法：

- **PE / PB / PEG**：A 股市场最常用，与卖方研报一致
- **DCF**：基于基本面的内在价值，成熟稳定盈利公司适用
- **戈登增长模型**：高分红蓝筹 / 银行 / 公用类
- **可比公司法**：反映当前市场情绪与相对估值
- **并购重组对标**：M&A 价值与控制权溢价

关键是理解每种方法背后的假设，并基于多情景给出合理估值区间。**A 股研究的差异化能力体现在：（1）申万行业经验区间锚定；（2）A 股专属溢价 / 折价因子识别；（3）政策与监管环境理解；（4）流动性与解禁压力评估。**
