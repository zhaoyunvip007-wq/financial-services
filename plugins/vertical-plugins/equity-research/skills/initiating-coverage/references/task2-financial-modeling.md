# Task 2: Financial Modeling - Detailed Workflow

This document provides step-by-step instructions for executing Task 2 (Financial Modeling) of the initiating-coverage skill.

## Task Overview

**Purpose**: Extract historical financials and build comprehensive Excel financial model with projections and scenarios.

**Prerequisites**: ⚠️ Verify before starting
- **Required**: 公司财务数据来源
  - A 股上市公司：最新年报、半年报、季报（巨潮资讯网 cninfo.com.cn）
  - 结构化数据：AKShare MCP / Tushare MCP / Wind / 同花顺 iFinD
  - 或：用户提供的预提取历史财务数据
- **Optional**: 公司研究文档（Task 1）作为业务背景

**Output**: Excel 财务模型（.xlsx），包含 6 个核心 tab（按 CAS 中国会计准则口径）：
1. 收入模型（Revenue Model）
2. 利润表（Income Statement，对应"合并利润表"）
3. 现金流量表（Cash Flow Statement，对应"合并现金流量表"）
4. 资产负债表（Balance Sheet，对应"合并资产负债表"）
5. 情景分析（Scenarios，乐观 / 中性 / 悲观）
6. DCF 输入（DCF Inputs）

---

## Input Verification

**BEFORE STARTING - CHECK:**

**Option A: 直接抓取财务数据（最常用）**
- [ ] 是否能从巨潮资讯网获取最新年报、半年报、季报？
- [ ] 或能通过 AKShare MCP / Tushare MCP / Wind / 同花顺拉取结构化财务数据？
- [ ] 是否准备好创建 Excel 历史财务文件？

**Option B: 用户已提供预提取财务数据**
- [ ] 是否提供历史财务文件？（.xlsx 或其他格式）
- [ ] 是否包含 3-5 年利润表、现金流量表、资产负债表？
- [ ] 数据是否干净可用？

**Optional Context:**
- [ ] 公司研究（Task 1）是否已完成业务理解？

**IF VERIFICATION FAILS**: 暂停并获取定期报告（年报 / 半年报 / 季报）后再继续。

---

## Model Structure and Formatting

### Color Coding (Industry Standard)
- **Blue text**: Hardcoded inputs (user can change)
- **Black text**: Formulas and calculations
- **Green text**: Links to other sheets
- **Red text**: Errors or flags (should be resolved)

### Formatting Standards
- Professional borders and shading
- Clear section headers
- Grouped rows for collapsibility
- Named ranges for key inputs/outputs
- No hardcoded numbers in formulas (except constants like 12 months)
- 单位统一标注（人民币万元 / 百万元 / 亿元，A 股年报默认"元"或"万元"，建模时建议统一为"百万元"或"亿元"）

### Formula Best Practices
- All numbers should flow from assumptions
- Change an assumption → entire model updates
- No circular references
- Use named ranges for key cells
- Keep formulas simple and auditable
- Add comments for complex calculations

---

## Step-by-Step Modeling Workflow

### Step 1: Extract Historical Financials

**If historical financials are already extracted, skip to Step 2.**

**For A 股上市公司：**

1. **抓取定期报告**
   - 访问巨潮资讯网（https://www.cninfo.com.cn）搜索公司代码 / 名称
   - 下载最新年报（次年 4 月 30 日前披露）、半年报（当年 8 月 31 日前）、一季报（4 月 30 日前）、三季报（10 月 31 日前）
   - 关注业绩预告（1 月 31 日前对亏损 / 扭亏 / 大增 / 大减强制披露）和业绩快报
   - 优先用 AKShare / Tushare 接口直接拉结构化数据（节省提取时间）

2. **Create Historical Financials Excel File**
   - File name: `[公司名]_[股票代码]_Historical_Financials_[Date].xlsx`
   - This file will be the foundation for the model

3. **提取利润表（3-5 年，CAS 科目）**
   - Create Sheet 1: "Historical Income Statement"
   - 提取全部科目（A 股利润表标准科目）：
     - 营业总收入（含主营业务收入 / 其他业务收入）、营业收入分部数据（如年报"分行业 / 分产品 / 分地区"披露）
     - 营业成本（主营业务成本 + 其他业务成本）
     - 毛利（营业收入 - 营业成本）
     - 营业税金及附加（消费税 / 城建税 / 教育费附加等）
     - 销售费用、管理费用、研发费用（2018 年起单列）、财务费用（A 股 P&L 四费分列）
     - 信用减值损失、资产减值损失（A 股专属，含商誉减值）
     - 投资收益、公允价值变动损益、其他收益（政府补助）
     - **营业利润**（A 股口径含投资收益与公允价值变动，与美股 EBIT 不同！）
     - 营业外收入 / 营业外支出
     - 利润总额、所得税费用、有效税率
     - 净利润、归母净利润、扣非归母净利润（A 股核心利润口径）
     - EPS（基本 / 稀释）、加权平均股本

4. **提取现金流量表（3-5 年，CAS 科目）**
   - Create Sheet 2: "Historical Cash Flow"
   - Extract ALL line items（A 股现金流量表标准科目）：
     - 经营活动（从净利润开始的间接法附注）
     - 销售商品 / 提供劳务收到的现金、收到的税费返还、购买商品 / 接受劳务支付的现金、支付给职工的现金、支付的各项税费
     - 折旧与摊销、股份支付（A 股股权激励）
     - 经营性应收 / 应付项目变动（应收账款、存货、应付账款）
     - **经营活动产生的现金流量净额**（A 股核心指标）
     - 投资活动：购建固定资产 / 无形资产支付的现金（CapEx）、取得子公司支付的现金（并购）、收回投资 / 处置长期资产收到的现金
     - 投资活动产生的现金流量净额
     - 筹资活动：取得借款 / 偿还债务、吸收投资 / 分配股利（A 股分红普遍较低，注意 ROE 与分红率匹配）、回购股份
     - 筹资活动产生的现金流量净额
     - 汇率变动对现金的影响、现金及现金等价物净增加额、期初 / 期末现金及现金等价物余额

5. **提取资产负债表（3-5 年，CAS 科目）**
   - Create Sheet 3: "Historical Balance Sheet"
   - Extract ALL line items（A 股资产负债表标准科目）：
     - 流动资产：货币资金、交易性金融资产、应收票据、应收账款、应收账款融资、预付款项、其他应收款、存货、合同资产、其他流动资产
     - 非流动资产：长期股权投资、其他权益工具投资、固定资产（含累计折旧）、在建工程、使用权资产（新租赁准则）、无形资产、开发支出、商誉（A 股专属重点关注科目）、长期待摊费用、递延所得税资产
     - 资产总计
     - 流动负债：短期借款、应付票据、应付账款、合同负债（替代预收账款，新收入准则）、应付职工薪酬、应交税费、其他应付款、一年内到期的非流动负债
     - 非流动负债：长期借款、应付债券、租赁负债、长期应付款、递延所得税负债
     - 负债合计
     - 所有者权益：实收资本（或股本）、资本公积、盈余公积、未分配利润、其他综合收益、少数股东权益（合并报表必有）
     - 所有者权益（或股东权益）合计、负债和所有者权益合计

6. **Calculate Historical Metrics（A 股核心指标）**
   - Create Sheet 4: "Historical Metrics"
   - Calculate from statements:
     - 营业总收入增长率（YoY）
     - 毛利率（毛利 / 营业总收入）
     - 营业利润率、净利率、归母净利率、扣非归母净利率
     - 经营活动现金流净额 / 净利润（现金含金量，A 股重点）
     - 自由现金流（经营活动现金流净额 - CapEx）
     - ROE（归母净利润 / 期初期末净资产平均；杜邦三要素拆解）
     - ROIC（NOPAT / 投入资本）
     - 资产负债率（总负债 / 总资产）
     - 流动比率、速动比率
     - **A 股专属指标：** 商誉占净资产比、应收账款 / 营收、存货周转天数、有息负债率、大股东质押率、扣非净利率与净利率差（识别非经常性损益占比）

7. **Document Sources and Notes**
   - Create Sheet 5: "Notes"
   - Document:
     - 年报披露日期与会计年度（A 股一律 12 月 31 日年末）
     - 任何非经常性损益项目（A 股扣非利润口径）
     - CAS 与 IFRS 差异（A 股 H 股双重上市公司需关注）
     - 分部数据（按产品 / 地区 / 行业披露）
     - 数据质量与披露限制
     - 审计意见类型（标准无保留 / 保留 / 无法表示意见 / 否定，非标审计意见为重大红旗）

**For 拟上市 / 未上市公司：**

1. **Gather Available Data**
   - 招股说明书 / 公开转让说明书（新三板）
   - 媒体披露的营收数据
   - 融资公告
   - 行业估算或可比公司数据（用申万行业内 A 股可比公司）

2. **Create Simplified Historical File**
   - 估算营业总收入（如可获得）
   - 估算毛利率 / 净利率（从可比公司）
   - 关键比率与指标
   - 全部假设与来源备注

**Verification:**
- [ ] All 3 financial statements extracted (3-5 years)
- [ ] Numbers reconcile across statements（净利润 → 现金流量表 → 资产负债表未分配利润勾稽）
- [ ] Key metrics calculated correctly
- [ ] Excel file saved and can be opened
- [ ] 数据来源已记录（年报披露日期、巨潮 URL、AKShare 拉取时间戳）

**Foundation for projection model is now complete. Proceed to Step 2.**
   - Capital expenditures
   - Working capital items
   - Debt and interest expense
   - Share count (basic and diluted)

3. **Organize historical data for entry**
   - Prepare 3-5 years of actuals
   - Will be entered directly into Income Statement, Cash Flow Statement, and Balance Sheet tabs
   - Historical years in columns, projected years following

4. **Calculate historical trends**
   - Revenue CAGR
   - Margin progression
   - OpEx leverage
   - Working capital patterns
   - CapEx as % of revenue
   - These trends will inform projection assumptions

**Note**: Assumptions will be documented directly in each tab as blue text inputs, not in a separate tab.

### Step 2: Model Revenue

**CRITICAL: This is the most important and detailed part of the model.**

#### A. Revenue by Product/Category (20-30 rows)

Create detailed table:
```
                        2021A   2022A   2023A   2024A   2025E   2026E   2027E   2028E   2029E
Product Category A
  Sub-product A1        XX      XX      XX      XX      XX      XX      XX      XX      XX
  Sub-product A2        XX      XX      XX      XX      XX      XX      XX      XX      XX
  Sub-product A3        XX      XX      XX      XX      XX      XX      XX      XX      XX
  Category A Total      XX      XX      XX      XX      XX      XX      XX      XX      XX
  % of Total Rev        X%      X%      X%      X%      X%      X%      X%      X%      X%
  YoY Growth %          -       X%      X%      X%      X%      X%      X%      X%      X%

Product Category B
  [Similar structure]

[Continue for all product categories]

Services Revenue        XX      XX      XX      XX      XX      XX      XX      XX      XX
Other Revenue           XX      XX      XX      XX      XX      XX      XX      XX      XX

TOTAL REVENUE           XX      XX      XX      XX      XX      XX      XX      XX      XX
Total Revenue Growth %  -       X%      X%      X%      X%      X%      X%      X%      X%
```

**Key Requirements:**
- Show absolute revenue ($M) for each category
- Calculate % of total revenue for each category
- Show YoY growth % for each category
- Must have granular sub-categories (not just 3-5 top-level categories)
- Show mix shift over time
- Link all projections to Assumptions tab

#### B. Revenue by Geography (15-20 rows，A 股年报"按地区"分类口径)

Create detailed table:
```
                        2021A   2022A   2023A   2024A   2025E   2026E   2027E   2028E   2029E
境内
  华东                  XX      XX      XX      XX      XX      XX      XX      XX      XX
  华南                  XX      XX      XX      XX      XX      XX      XX      XX      XX
  华北                  XX      XX      XX      XX      XX      XX      XX      XX      XX
  华中 / 西部           XX      XX      XX      XX      XX      XX      XX      XX      XX
  境内合计              XX      XX      XX      XX      XX      XX      XX      XX      XX
  占比 %                X%      X%      X%      X%      X%      X%      X%      X%      X%
  YoY 增速 %            -       X%      X%      X%      X%      X%      X%      X%      X%

境外
  亚洲（除中国）        XX      XX      XX      XX      XX      XX      XX      XX      XX
  欧洲                  XX      XX      XX      XX      XX      XX      XX      XX      XX
  美洲                  XX      XX      XX      XX      XX      XX      XX      XX      XX
  其他                  XX      XX      XX      XX      XX      XX      XX      XX      XX
  境外合计              XX      XX      XX      XX      XX      XX      XX      XX      XX
  占比 %                X%      X%      X%      X%      X%      X%      X%      X%      X%
  YoY 增速 %            -       X%      X%      X%      X%      X%      X%      X%      X%

营业总收入合计           XX      XX      XX      XX      XX      XX      XX      XX      XX
```

**注：A 股年报披露的地区分布粒度通常为"境内 / 境外"或"华东 / 华南 / 华北等"，部分公司按国家或省份披露。出口型企业（如家电、消费电子、机械）需特别关注境外营收占比与汇率敏感性。

**Verification:**
- Revenue by product total = Revenue by geography total = Total revenue
- All percentages sum to 100%
- Growth rates calculated correctly

#### C. Revenue by Channel (if applicable)

```
                        2021A   2022A   2023A   2024A   2025E   2026E   2027E   2028E   2029E
Direct Sales            XX      XX      XX      XX      XX      XX      XX      XX      XX
E-commerce/Online       XX      XX      XX      XX      XX      XX      XX      XX      XX
Wholesale/Partner       XX      XX      XX      XX      XX      XX      XX      XX      XX
Retail Stores
  Company-owned stores  XX      XX      XX      XX      XX      XX      XX      XX      XX
  Store count           XX      XX      XX      XX      XX      XX      XX      XX      XX
  Sales per store       XX      XX      XX      XX      XX      XX      XX      XX      XX
Other Channels          XX      XX      XX      XX      XX      XX      XX      XX      XX

TOTAL REVENUE           XX      XX      XX      XX      XX      XX      XX      XX      XX
```

### Step 3: Model Operating Expenses（A 股四费 + 营业成本结构）

#### A. 营业成本（Cost of Revenue）
1. **拆解营业成本构成**
   - 直接材料（原材料 / 大宗商品价格敏感）
   - 直接人工
   - 制造费用（折旧 / 能源 / 辅料）
   - 物流与运输（新收入准则下，运输费可计入合同履约成本或销售费用）

2. **Link to revenue**
   - 计算营业成本占营收比
   - 按年度建模毛利率
   - 链接到假设 tab

#### B. 销售费用（Selling Expenses，A 股科目）
```
销售费用                2021A   2022A   2023A   2024A   2025E   2026E   2027E   2028E   2029E
销售人员人数             XX      XX      XX      XX      XX      XX      XX      XX      XX
人均薪酬                 XX      XX      XX      XX      XX      XX      XX      XX      XX
职工薪酬                 XX      XX      XX      XX      XX      XX      XX      XX      XX
广告与市场推广费         XX      XX      XX      XX      XX      XX      XX      XX      XX
其他销售费用             XX      XX      XX      XX      XX      XX      XX      XX      XX
销售费用合计             XX      XX      XX      XX      XX      XX      XX      XX      XX
占营业总收入 %           X%      X%      X%      X%      X%      X%      X%      X%      X%
```

#### C. 管理费用（Administrative Expenses，A 股科目）
```
管理费用                2021A   2022A   2023A   2024A   2025E   2026E   2027E   2028E   2029E
管理人员人数             XX      XX      XX      XX      XX      XX      XX      XX      XX
人均薪酬                 XX      XX      XX      XX      XX      XX      XX      XX      XX
职工薪酬                 XX      XX      XX      XX      XX      XX      XX      XX      XX
中介机构费 / 折旧摊销     XX      XX      XX      XX      XX      XX      XX      XX      XX
其他管理费用             XX      XX      XX      XX      XX      XX      XX      XX      XX
管理费用合计             XX      XX      XX      XX      XX      XX      XX      XX      XX
占营业总收入 %           X%      X%      X%      X%      X%      X%      X%      X%      X%
```

#### D. 研发费用（R&D Expenses，A 股 2018 年起单列）
```
研发费用                2021A   2022A   2023A   2024A   2025E   2026E   2027E   2028E   2029E
研发人员人数             XX      XX      XX      XX      XX      XX      XX      XX      XX
人均薪酬                 XX      XX      XX      XX      XX      XX      XX      XX      XX
研发人员薪酬             XX      XX      XX      XX      XX      XX      XX      XX      XX
研发投入资本化金额        XX      XX      XX      XX      XX      XX      XX      XX      XX
研发投入费用化金额        XX      XX      XX      XX      XX      XX      XX      XX      XX
研发投入合计             XX      XX      XX      XX      XX      XX      XX      XX      XX
占营业总收入 %           X%      X%      X%      X%      X%      X%      X%      X%      X%
研发资本化率             X%      X%      X%      X%      X%      X%      X%      X%      X%
```

**注：A 股研发投入分"资本化"（计入开发支出 / 无形资产）和"费用化"（计入研发费用），资本化率过高需警惕利润操纵嫌疑（行业惯例：硬件企业 10-30%、纯软件企业 0-10%、创新药企较高）。

#### E. 财务费用（Financial Expenses，A 股科目，含利息净支出 + 汇兑损益 + 手续费）
```
财务费用                2021A   2022A   2023A   2024A   2025E   2026E   2027E   2028E   2029E
利息支出                 XX      XX      XX      XX      XX      XX      XX      XX      XX
减：利息收入             (XX)    (XX)    (XX)    (XX)    (XX)    (XX)    (XX)    (XX)    (XX)
汇兑损益                 XX      XX      XX      XX      XX      XX      XX      XX      XX
手续费                   XX      XX      XX      XX      XX      XX      XX      XX      XX
财务费用合计             XX      XX      XX      XX      XX      XX      XX      XX      XX
占营业总收入 %           X%      X%      X%      X%      X%      X%      X%      X%      X%
```

#### F. Depreciation & Amortization
- Link to CapEx schedule
- Apply depreciation rates from 假设 tab（A 股年报披露固定资产折旧年限：房屋 20-50 年、机器 5-15 年、运输工具 4-10 年、电子设备 3-5 年）
- Calculate annual D&A
- 注：A 股折旧摊销分散在营业成本（生产用设备）、销售 / 管理 / 研发费用（办公设备）多个科目，需穿透还原

### Step 4: Build Income Statement

**Create 完整利润表（CAS 中国会计准则口径，40-50 行科目）：**

```
合并利润表（单位：百万元）   2021A   2022A   2023A   2024A   2025E   2026E   2027E   2028E   2029E

营业总收入
[Link to Revenue Model tab]
营业总收入              XX      XX      XX      XX      XX      XX      XX      XX      XX
  YoY 增速 %            -       X%      X%      X%      X%      X%      X%      X%      X%

营业总成本
营业成本                XX      XX      XX      XX      XX      XX      XX      XX      XX
营业税金及附加          XX      XX      XX      XX      XX      XX      XX      XX      XX
销售费用                XX      XX      XX      XX      XX      XX      XX      XX      XX
管理费用                XX      XX      XX      XX      XX      XX      XX      XX      XX
研发费用                XX      XX      XX      XX      XX      XX      XX      XX      XX
财务费用                XX      XX      XX      XX      XX      XX      XX      XX      XX
信用减值损失            (XX)    (XX)    (XX)    (XX)    (XX)    (XX)    (XX)    (XX)    (XX)
资产减值损失（含商誉减值） (XX)    (XX)    (XX)    (XX)    (XX)    (XX)    (XX)    (XX)    (XX)

毛利                    XX      XX      XX      XX      XX      XX      XX      XX      XX
  毛利率 %              X%      X%      X%      X%      X%      X%      X%      X%      X%

加：投资收益            XX      XX      XX      XX      XX      XX      XX      XX      XX
加：公允价值变动损益    XX      XX      XX      XX      XX      XX      XX      XX      XX
加：其他收益（政府补助） XX      XX      XX      XX      XX      XX      XX      XX      XX

营业利润                XX      XX      XX      XX      XX      XX      XX      XX      XX
  营业利润率 %          X%      X%      X%      X%      X%      X%      X%      X%      X%

加：营业外收入          XX      XX      XX      XX      XX      XX      XX      XX      XX
减：营业外支出          (XX)    (XX)    (XX)    (XX)    (XX)    (XX)    (XX)    (XX)    (XX)

利润总额                XX      XX      XX      XX      XX      XX      XX      XX      XX
减：所得税费用          (XX)    (XX)    (XX)    (XX)    (XX)    (XX)    (XX)    (XX)    (XX)
  有效税率 %            X%      X%      X%      X%      X%      X%      X%      X%      X%
                       （A 股标准 25%；高新技术企业 15%；西部大开发 / 海南自贸 15%；小微企业减免）

净利润                  XX      XX      XX      XX      XX      XX      XX      XX      XX
减：少数股东损益        XX      XX      XX      XX      XX      XX      XX      XX      XX
归属于母公司净利润      XX      XX      XX      XX      XX      XX      XX      XX      XX
  归母净利率 %          X%      X%      X%      X%      X%      X%      X%      X%      X%
扣非归母净利润          XX      XX      XX      XX      XX      XX      XX      XX      XX
  扣非净利率 %          X%      X%      X%      X%      X%      X%      X%      X%      X%

EBITDA（计算项）        XX      XX      XX      XX      XX      XX      XX      XX      XX
  EBITDA 利润率 %       X%      X%      X%      X%      X%      X%      X%      X%      X%

股本（亿股）
基本股数（亿股）         XX      XX      XX      XX      XX      XX      XX      XX      XX
稀释股数（亿股）         XX      XX      XX      XX      XX      XX      XX      XX      XX

每股收益
基本 EPS（元）           ¥X.XX   ¥X.XX   ¥X.XX   ¥X.XX   ¥X.XX   ¥X.XX   ¥X.XX   ¥X.XX   ¥X.XX
稀释 EPS（元）           ¥X.XX   ¥X.XX   ¥X.XX   ¥X.XX   ¥X.XX   ¥X.XX   ¥X.XX   ¥X.XX   ¥X.XX
扣非 EPS（元）           ¥X.XX   ¥X.XX   ¥X.XX   ¥X.XX   ¥X.XX   ¥X.XX   ¥X.XX   ¥X.XX   ¥X.XX
```

### Step 5: Build Cash Flow Statement（合并现金流量表，CAS 口径）

```
合并现金流量表（百万元）  2021A   2022A   2023A   2024A   2025E   2026E   2027E   2028E   2029E

经营活动产生的现金流量
销售商品提供劳务收到现金   XX      XX      XX      XX      XX      XX      XX      XX      XX
收到的税费返还             XX      XX      XX      XX      XX      XX      XX      XX      XX
收到其他经营活动现金       XX      XX      XX      XX      XX      XX      XX      XX      XX
经营活动现金流入小计       XX      XX      XX      XX      XX      XX      XX      XX      XX

购买商品接受劳务支付现金   (XX)    (XX)    (XX)    (XX)    (XX)    (XX)    (XX)    (XX)    (XX)
支付给职工以及为职工支付   (XX)    (XX)    (XX)    (XX)    (XX)    (XX)    (XX)    (XX)    (XX)
支付的各项税费             (XX)    (XX)    (XX)    (XX)    (XX)    (XX)    (XX)    (XX)    (XX)
支付其他经营活动现金       (XX)    (XX)    (XX)    (XX)    (XX)    (XX)    (XX)    (XX)    (XX)
经营活动现金流出小计       (XX)    (XX)    (XX)    (XX)    (XX)    (XX)    (XX)    (XX)    (XX)

经营活动产生的现金流量净额  XX     XX      XX      XX      XX      XX      XX      XX      XX
（间接法附注核对：净利润 + 折旧摊销 + 减值损失 + 信用损失 + 经营性应收应付变动）

投资活动产生的现金流量
收回投资收到的现金         XX      XX      XX      XX      XX      XX      XX      XX      XX
取得投资收益收到的现金     XX      XX      XX      XX      XX      XX      XX      XX      XX
处置长期资产收回的现金     XX      XX      XX      XX      XX      XX      XX      XX      XX
投资活动现金流入小计       XX      XX      XX      XX      XX      XX      XX      XX      XX

购建固定资产无形资产支付   (XX)    (XX)    (XX)    (XX)    (XX)    (XX)    (XX)    (XX)    (XX)
（即 CapEx，A 股核心科目）
投资支付的现金             (XX)    (XX)    (XX)    (XX)    (XX)    (XX)    (XX)    (XX)    (XX)
取得子公司支付的现金净额   (XX)    (XX)    (XX)    (XX)    (XX)    (XX)    (XX)    (XX)    (XX)
投资活动现金流出小计       (XX)    (XX)    (XX)    (XX)    (XX)    (XX)    (XX)    (XX)    (XX)

投资活动产生的现金流量净额 (XX)    (XX)    (XX)    (XX)    (XX)    (XX)    (XX)    (XX)    (XX)

自由现金流（经营 - CapEx）  XX     XX      XX      XX      XX      XX      XX      XX      XX
  FCF / 营业总收入 %        X%      X%      X%      X%      X%      X%      X%      X%      X%

筹资活动产生的现金流量
吸收投资收到的现金         XX      XX      XX      XX      XX      XX      XX      XX      XX
（A 股 IPO / 定增 / 配股）
取得借款收到的现金         XX      XX      XX      XX      XX      XX      XX      XX      XX
筹资活动现金流入小计       XX      XX      XX      XX      XX      XX      XX      XX      XX

偿还债务支付的现金         (XX)    (XX)    (XX)    (XX)    (XX)    (XX)    (XX)    (XX)    (XX)
分配股利利润支付现金       (XX)    (XX)    (XX)    (XX)    (XX)    (XX)    (XX)    (XX)    (XX)
（A 股股息率普遍偏低，高股息蓝筹另当别论）
回购股份支付的现金         (XX)    (XX)    (XX)    (XX)    (XX)    (XX)    (XX)    (XX)    (XX)
筹资活动现金流出小计       (XX)    (XX)    (XX)    (XX)    (XX)    (XX)    (XX)    (XX)    (XX)

筹资活动产生的现金流量净额  XX     XX      XX      XX      XX      XX      XX      XX      XX

汇率变动对现金的影响        XX     XX      XX      XX      XX      XX      XX      XX      XX
现金及现金等价物净增加额    XX     XX      XX      XX      XX      XX      XX      XX      XX

期初现金及等价物            XX     XX      XX      XX      XX      XX      XX      XX      XX
期末现金及等价物            XX     XX      XX      XX      XX      XX      XX      XX      XX
```

### Step 6: Build Balance Sheet（合并资产负债表，CAS 口径）

Create full 资产负债表 with 35-45 行科目：

```
合并资产负债表（百万元）    2021A   2022A   2023A   2024A   2025E   2026E   2027E   2028E   2029E

资产
流动资产：
  货币资金                 XX      XX      XX      XX      XX      XX      XX      XX      XX
  交易性金融资产           XX      XX      XX      XX      XX      XX      XX      XX      XX
  应收票据及应收账款       XX      XX      XX      XX      XX      XX      XX      XX      XX
  应收账款融资             XX      XX      XX      XX      XX      XX      XX      XX      XX
  预付款项                 XX      XX      XX      XX      XX      XX      XX      XX      XX
  其他应收款               XX      XX      XX      XX      XX      XX      XX      XX      XX
  存货                     XX      XX      XX      XX      XX      XX      XX      XX      XX
  合同资产                 XX      XX      XX      XX      XX      XX      XX      XX      XX
  其他流动资产             XX      XX      XX      XX      XX      XX      XX      XX      XX
流动资产合计                XX      XX      XX      XX      XX      XX      XX      XX      XX

非流动资产：
  长期股权投资             XX      XX      XX      XX      XX      XX      XX      XX      XX
  其他权益工具投资         XX      XX      XX      XX      XX      XX      XX      XX      XX
  固定资产（原值）         XX      XX      XX      XX      XX      XX      XX      XX      XX
  减：累计折旧             (XX)    (XX)    (XX)    (XX)    (XX)    (XX)    (XX)    (XX)    (XX)
  固定资产净值             XX      XX      XX      XX      XX      XX      XX      XX      XX
  在建工程                 XX      XX      XX      XX      XX      XX      XX      XX      XX
  使用权资产（新租赁准则） XX      XX      XX      XX      XX      XX      XX      XX      XX
  无形资产（土地 / 软件）  XX      XX      XX      XX      XX      XX      XX      XX      XX
  开发支出（资本化研发）   XX      XX      XX      XX      XX      XX      XX      XX      XX
  商誉                     XX      XX      XX      XX      XX      XX      XX      XX      XX
  （A 股专属重点关注：商誉 / 净资产 >30% 即重大减值风险）
  长期待摊费用             XX      XX      XX      XX      XX      XX      XX      XX      XX
  递延所得税资产           XX      XX      XX      XX      XX      XX      XX      XX      XX
  其他非流动资产           XX      XX      XX      XX      XX      XX      XX      XX      XX
非流动资产合计              XX      XX      XX      XX      XX      XX      XX      XX      XX

资产总计                    XX      XX      XX      XX      XX      XX      XX      XX      XX

负债
流动负债：
  短期借款                 XX      XX      XX      XX      XX      XX      XX      XX      XX
  应付票据及应付账款       XX      XX      XX      XX      XX      XX      XX      XX      XX
  合同负债（替代预收账款） XX      XX      XX      XX      XX      XX      XX      XX      XX
  应付职工薪酬             XX      XX      XX      XX      XX      XX      XX      XX      XX
  应交税费                 XX      XX      XX      XX      XX      XX      XX      XX      XX
  其他应付款               XX      XX      XX      XX      XX      XX      XX      XX      XX
  一年内到期的非流动负债   XX      XX      XX      XX      XX      XX      XX      XX      XX
  其他流动负债             XX      XX      XX      XX      XX      XX      XX      XX      XX
流动负债合计                XX      XX      XX      XX      XX      XX      XX      XX      XX

非流动负债：
  长期借款                 XX      XX      XX      XX      XX      XX      XX      XX      XX
  应付债券                 XX      XX      XX      XX      XX      XX      XX      XX      XX
  租赁负债                 XX      XX      XX      XX      XX      XX      XX      XX      XX
  长期应付款               XX      XX      XX      XX      XX      XX      XX      XX      XX
  递延所得税负债           XX      XX      XX      XX      XX      XX      XX      XX      XX
  其他非流动负债           XX      XX      XX      XX      XX      XX      XX      XX      XX
非流动负债合计              XX      XX      XX      XX      XX      XX      XX      XX      XX

负债合计                    XX      XX      XX      XX      XX      XX      XX      XX      XX

所有者权益
  实收资本（或股本）       XX      XX      XX      XX      XX      XX      XX      XX      XX
  资本公积                 XX      XX      XX      XX      XX      XX      XX      XX      XX
  减：库存股               (XX)    (XX)    (XX)    (XX)    (XX)    (XX)    (XX)    (XX)    (XX)
  其他综合收益             XX      XX      XX      XX      XX      XX      XX      XX      XX
  盈余公积                 XX      XX      XX      XX      XX      XX      XX      XX      XX
  未分配利润               XX      XX      XX      XX      XX      XX      XX      XX      XX
  归属母公司股东权益       XX      XX      XX      XX      XX      XX      XX      XX      XX
  少数股东权益             XX      XX      XX      XX      XX      XX      XX      XX      XX
所有者权益合计              XX      XX      XX      XX      XX      XX      XX      XX      XX

负债与所有者权益总计        XX      XX      XX      XX      XX      XX      XX      XX      XX

平衡校验                    OK      OK      OK      OK      OK      OK      OK      OK      OK
```

**Balance Check Formula:**
- Total Assets must equal Total Liabilities + Equity for each year
- Flag any imbalances in red

### Step 7: Build DCF Inputs Tab

Prepare inputs for valuation (Task 3):

```
DCF 输入（百万元）       2025E   2026E   2027E   2028E   2029E

营业利润（CAS 口径，含投资收益与公允价值变动）
                        XX      XX      XX      XX      XX
（注：A 股 DCF 建议用"营业利润 - 投资收益 - 公允价值变动"还原至经营性 EBIT，避免重复计算非经常项目）
经营性 EBIT             XX      XX      XX      XX      XX
有效税率                X%      X%      X%      X%      X%
（A 股标准 25%；高新技术企业 15%；西部大开发 / 海南自贸 15%）
NOPAT                   XX      XX      XX      XX      XX

加：折旧摊销             XX      XX      XX      XX      XX
减：CapEx               (XX)    (XX)    (XX)    (XX)    (XX)
减：营运资本变动         (XX)    (XX)    (XX)    (XX)    (XX)

无杠杆自由现金流（FCFF） XX      XX      XX      XX      XX

终值年指标:
  2029E 营业总收入       ¥X,XXX
  2029E EBITDA          ¥XXX
  2029E 经营性 EBIT     ¥XXX
  2029E FCFF            ¥XXX
```

### Step 8: Build Scenarios Tab

Create three scenarios with different assumptions:

#### Scenario Assumptions Table
```
Assumption                      Bull        Base        Bear
Revenue CAGR (2025-2029)        XX%         XX%         XX%
Gross Margin 2029E              XX%         XX%         XX%
EBITDA Margin 2029E             XX%         XX%         XX%
CapEx as % of Revenue           X%          X%          X%
[Add other key assumptions]
```

#### Scenario Output Table
```
Metric                          Bull        Base        Bear
2029E Revenue ($M)              $X,XXX      $X,XXX      $X,XXX
2029E EBITDA ($M)               $XXX        $XXX        $XXX
2029E EBITDA Margin             XX%         XX%         XX%
2029E Net Income ($M)           $XXX        $XXX        $XXX
2029E EPS                       $X.XX       $X.XX       $X.XX
2029E FCF ($M)                  $XXX        $XXX        $XXX
2029E FCF Margin                XX%         XX%         XX%

Cumulative FCF 2025-2029 ($M)   $XXX        $XXX        $XXX
```

**Document scenario rationale:**
- Bull case: [Describe optimistic but achievable assumptions]
- Base case: [Describe most likely scenario]
- Bear case: [Describe downside risks and triggers]

### Step 9: Quality Check

**Verify model integrity:**
1. [ ] Test all formulas (spot check calculations)
2. [ ] Change assumption → verify model updates correctly
3. [ ] Test scenario switching
4. [ ] Verify color coding (blue/black/green)
5. [ ] Check balance sheet balances for all years
6. [ ] Verify no circular references (Excel will flag)
7. [ ] Check for hardcoded numbers in projections
8. [ ] Verify all cross-sheet links work
9. [ ] Test that revenue totals tie across all tabs
10. [ ] Review formatting and presentation

---

## Quality Standards

### Model Integrity
- All formulas link properly across sheets
- No hardcoded numbers in projections (except in Assumptions tab)
- No circular references
- Balance sheet balances for all years
- Scenario switching works properly

### Completeness
- All 6 essential tabs: Revenue Model, Income Statement, Cash Flow Statement, Balance Sheet, Scenarios, DCF Inputs
- 40-50 line items in Income Statement
- 20-30 rows in Revenue Model (product breakdown)
- 15-20 rows in Revenue Model (geography breakdown)
- Full cash flow and balance sheet with all line items
- Bull/Base/Bear scenarios complete

### Professional Formatting
- Consistent color coding (blue/black/green)
- Clear headers and labels
- Proper borders and shading
- Named ranges for key cells
- Grouped rows for collapsibility
- Units clearly labeled ($ thousands vs. $ millions)

### Documentation
- Assumptions documented with rationale (blue text cells with comments)
- Data sources noted in cell comments or notes section within tabs
- Complex calculations explained with comments
- Methodology described

---

## File Naming Convention

Save the financial model as:
`[Company]_Financial_Model_[Date].xlsx`

Example: `贵州茅台_600519.SH_Financial_Model_2026-05-06.xlsx` 或 `宁德时代_300750.SZ_Financial_Model_2026-05-06.xlsx`

---

## Success Criteria

A successful financial model should:
1. Have all 6 essential tabs (Revenue Model, Income Statement, Cash Flow Statement, Balance Sheet, Scenarios, DCF Inputs)
2. Be fully dynamic (change assumption → model updates)
3. Have no hardcoded numbers in projections
4. Include detailed revenue breakdowns (20-30 rows by product, 15-20 rows by geography)
5. Contain 40-50 line items in Income Statement
6. Include Bull/Base/Bear scenarios
7. Be professionally formatted with color coding
8. Balance properly (balance sheet, cash flows)
9. Be auditable and easy to follow
10. Support valuation analysis with proper FCF calculations

---

## Common Model Types - Special Considerations

### 高成长科创板 / 创业板（半导体 / 创新药 / SaaS）
- 关注 ARR 增长与续费率（SaaS）、新管线进度（创新药）、订单 / 出货数据（半导体）
- 按产品线 / 客户分类建模
- 研发费用率与销售费用率高（科创板研发资本化率上限关注）
- 盈利时间表（科创板第五套标准允许未盈利上市）
- 单位经济（LTV/CAC、客户净留存）

### 消费 / 零售（家电 / 白酒 / 食品饮料 / 服装）
- 按产品大类与渠道（线上 / 线下 / 经销 / 直营）拆分
- 门店数量与同店增长（连锁零售）
- 存货周转天数与营运资金（白酒囤货周期长，存货周转慢但毛利高）
- 物流与履约成本
- 经销商体系与渠道库存（高端白酒重点跟踪）

### 制造业 / 周期股（化工 / 钢铁 / 有色 / 工程机械）
- 产能利用率与产能扩张周期
- 原材料价格与产品价格（周期股 PB 估值优于 PE）
- 毛利率桥接分析（销量 / 价格 / 产品组合 / 成本）
- 重资产高 CapEx 模式（关注资本开支节奏与折旧拐点）
- 营运资金周期与应收账款管理

### 银行 / 非银金融 / 房地产
- 银行：关注净息差、不良率、拨备覆盖率、ROE，PB 为主估值（0.5-1.2x PB）
- 非银金融（保险 / 券商）：内含价值（EV）、新业务价值（NBV）
- 房地产：销售金额、销售面积、土储、债务结构（三道红线）、NAV 估值优于 PE

### 公用 / 高分红蓝筹（电力 / 高速 / 港口 / 银行）
- 长期稳定现金流，戈登增长模型适用
- 关注分红率与股息率
- 资产负债率较高但现金流稳定
- WACC 下行受益（低利率环境估值修复）

---

## Next Steps

After completing Task 2, the financial model will be used for:
- **Task 3 (Valuation)**: DCF inputs, projected financials
- **Task 4 (Charts)**: Data for revenue trends, margin charts, scenario comparisons
- **Task 5 (Report Assembly)**: Financial data for report tables and analysis
