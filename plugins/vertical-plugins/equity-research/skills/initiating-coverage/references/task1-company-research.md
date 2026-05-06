# Task 1: Company Research - Detailed Workflow

This document provides step-by-step instructions for executing Task 1 (Company Research) of the initiating-coverage skill.

## Task Overview

**Purpose**: Research company's business, management, competitive position, industry, and risks.

**Prerequisites**: ✅ None (fully independent)
- 公司名称或 A 股代码（如 600519.SH / 000858.SZ / 300750.SZ / 688981.SH）

**Output**: Company Research Document (6,000-8,000 words)

---

## Data Sources to Gather

### Primary Sources (Company)
- **巨潮资讯网（cninfo.com.cn）定期报告：**
  - 最新年报：业务描述、风险因素、管理层讨论与分析（MD&A）、财务报表
  - 最新半年报与季报（一季报 / 三季报）
  - 业绩预告 / 业绩快报（披露超预期或低预期信号）
  - 临时公告：重大事项、并购重组、高管变动、股东减持、回购、对外担保
  - 业绩说明会通稿 / 投资者关系活动记录表

- **公司官网与投资者关系（IR）：**
  - 路演 PPT / 业绩说明会材料
  - 业绩说明会通稿（最近 2-3 个季度）
  - 公司公告与新闻稿
  - 产品资料

- **数据接口（结构化数据优先）：**
  - AKShare MCP / Tushare MCP（首选，免费/低成本）
  - Wind / 同花顺 iFinD（付费，机构数据）
  - 上证 e 互动 / 深交所互动易（管理层公开问答）

### Secondary Sources (Industry/Competitive)
- 竞争对手官网与定期报告（巨潮资讯网）
- 行业研究报告（券商研报、艾瑞、易观、中商产业研究院、wind 行业数据库）
- 财经媒体（财联社、第一财经、证券时报、新浪财经、雪球大 V）
- 行业协会数据（如汽车工业协会、半导体行业协会、中国电力企业联合会）
- 高管背景：天眼查 / 企查查 / 公司公告中的董监高履历

### Key Information to Extract

**Key Information:**
- 公司成立日期、注册地、上市板块（沪主板 / 深主板 / 创业板 / 科创板 / 北交所）、员工人数
- 营业总收入规模与增长轨迹（最近 3-5 年）
- 产品矩阵与价格体系
- 客户结构与典型案例（前五大客户占比）
- 董监高背景与履历
- 竞争格局与市场份额（申万行业内排名）
- 行业趋势与增长驱动
- 政策与监管考量（行业新政、补贴、税收优惠）
- 高频财务指标（来自年报正文 MD&A，非详细数据提取，详细财务建模在 Task 2）
- 实控人与股权结构、大股东质押率、限售解禁日历

---

## Step-by-Step Research Workflow

### Step 1: Initial Data Collection

1. **Start with company website**
   - Read About/Company pages
   - Review product pages
   - Identify customer case studies
   - Note key metrics mentioned (employees, customers, etc.)

2. **抓取定期报告（巨潮资讯网 / AKShare / Tushare）**
   - 下载最新年报
   - 下载最新季报 / 半年报
   - 下载最近 12 个月的临时公告（重大事项 / 并购 / 担保 / 关联交易 / 高管减持）
   - 关注披露窗口：年报次年 4 月 30 日前、半年报当年 8 月 31 日前、一季报当年 4 月 30 日前、三季报当年 10 月 31 日前；业绩预告 1 月 31 日前（亏损 / 扭亏 / 大增 / 大减强制预告）

3. **阅读业绩材料**
   - 最近一次业绩说明会通稿 / 投资者关系活动记录表
   - 最新路演 PPT
   - 最近 12 个月的公司公告与新闻稿
   - 上证 e 互动 / 深交所互动易上的高频问答

4. **Document basic facts**
   - Founding date and story
   - Headquarters location
   - Employee count
   - Products/services
   - Key customers

### Step 2: Business Model Analysis

1. **Map revenue streams**
   - What does the company sell?
   - How is it priced? (subscription, transaction, license, etc.)
   - Who pays?
   - What are typical deal sizes?

2. **Understand customer segments**
   - 大客户（如车企 / 三大运营商 / 国央企）vs. 中小企业 vs. 终端消费者（C 端）
   - 服务行业（按申万行业分类）
   - 区域分布（境内 vs. 海外；华东 / 华南 / 华北等）
   - 客户集中度（前五大客户占比，年报"经营情况讨论与分析"或"重大销售合同"披露）

3. **Document go-to-market**
   - Direct sales vs. channel partners
   - Sales cycle length
   - Customer acquisition strategy
   - Distribution model

4. **Identify unit economics**
   - LTV/CAC if available
   - Gross margins
   - Net revenue retention
   - Payback periods

### Step 3: Management Research

**For each of 3-4 key executives:**

1. **Identify key leaders**
   - 董事长 / 实控人（必查）
   - 总经理（必查）
   - 财务总监 / 董秘 / 核心技术带头人 / 核心业务事业部负责人（2 位）

2. **Research each executive**
   - 年报"董监高及员工情况"章节披露的履历
   - 天眼查 / 企查查的关联企业与对外投资
   - 媒体专访与业绩说明会发言
   - 在公司任职年限、是否实控人或一致行动人

3. **Write 300-400 word bio including:**
   - 当前职务与分工
   - 过往任职经历（最近 2-3 段）
   - 主要业绩与履历亮点
   - 教育背景与专业资质（高级工程师 / CPA / 行业奖项）
   - 行业从业年限
   - 在本公司任职时间、持股数量与股权激励情况

4. **Assess governance**
   - 董事会结构（独立董事比例 ≥1/3，A 股强制要求）
   - 监事会构成（A 股特有，不同于美股审计委员会）
   - 实控人与一致行动人持股比例
   - 大股东质押率（>50% 重点风险）
   - 高管薪酬与股权激励（限制性股票 / 股票期权）
   - 业绩承诺与对赌（重大重组后 3-5 年承诺期）

### Step 4: Competitive Intelligence

1. **Identify 5-10 competitors**
   - Direct competitors (same products/markets)
   - Indirect competitors (substitute solutions)
   - Emerging competitors (disruptors)
   - 查阅年报"行业竞争格局"或"经营情况讨论与分析"章节中公司列出的竞争对手

2. **Research each competitor**
   - 访问竞争对手官网
   - 阅读其定期报告（A 股竞争对手用巨潮，港股用披露易，美股标的用 SEC EDGAR）
   - 关注核心产品与定位
   - 识别差异化要素
   - 估算市场份额（结合行业协会 / 券商研报 / wind 行业数据库）

3. **Create competitive framework**
   - Map on key dimensions (price, features, scale, etc.)
   - Identify company's competitive advantages
   - Note competitive vulnerabilities
   - Assess switching costs and network effects

4. **Document competitive insights**
   - Who are the market leaders?
   - Where does this company rank?
   - What are unique differentiators?
   - What are competitive threats?

### Step 5: Industry Analysis

1. **Define the industry**
   - 申万一级 / 二级 / 三级行业分类（A 股权威分类，共 31 个一级行业）
   - 中证 / 国证行业指数对应板块
   - 范围与边界
   - 相邻 / 关联行业（产业链上下游）

2. **Size the market**
   - 总体可触达市场（TAM，参考行业协会 / 券商研报 / 国家统计局）
   - 可服务市场（SAM）
   - 可获得市场（SOM）
   - 当前渗透率（如新能源车渗透率、SaaS 渗透率、国产替代率）

3. **Research growth drivers**
   - Historical market growth rate
   - Projected growth rate (next 3-5 years)
   - Key trends accelerating/decelerating growth
   - Technology changes impacting industry

4. **Understand industry structure**
   - Fragmented vs. consolidated
   - Barriers to entry
   - Supplier/buyer power
   - Threat of substitutes
   - Regulatory environment

### Step 6: Risk Assessment

Identify 8-12 risks across four categories. For each risk, write 50-100 words.

**Company-Specific Risks（公司层面，4-6 项）：**
- 经营执行风险（管理层能否兑现承诺）
- 客户集中度（前五大客户占比 >50% 重点关注）
- 核心人员依赖（创始人 / 核心技术带头人）
- 产品 / 技术迭代风险
- 区域集中度
- 并购整合风险（近 3 年完成的重大重组）
- **A 股专属：** 商誉减值风险（商誉 / 净资产 >30%）、大股东质押风险（质押率 >50%）、限售股解禁压力、关联交易占比偏高、业绩承诺到期风险（重组对赌期满）、实控人变更 / 高管减持密集、审计意见非标（保留 / 无法表示意见）、退市新规风险（连续亏损 / 财务造假 / 市值低于阈值）

**Industry/Market Risks（行业 / 市场层面，3-4 项）：**
- 行业竞争加剧（价格战、内卷）
- 政策与监管变化（行业新政、补贴退坡、税收优惠到期、双减 / 反垄断 / 数据合规）
- 技术替代风险
- 市场饱和

**Financial Risks（财务层面，2-3 项）：**
- 盈利时间表（仍处亏损期的科创板 / 创业板公司）
- 融资需求（再融资节奏、定增受限）
- 资产负债率与短债压力
- 经营性现金流转负
- 应收账款 / 存货占营收比偏高

**Macroeconomic Risks（宏观层面，2-3 项）：**
- 经济周期敏感性（顺周期 vs. 防御）
- 利率敏感性（10Y 中国国债走势）
- 汇率敞口（出口型企业 / 海外营收占比高）
- 地缘政治（中美关系、出口管制、产业链转移）

**For each risk:**
- Describe the risk clearly
- Quantify impact if possible
- Note likelihood/severity
- Identify mitigating factors

### Step 7: Synthesis and Writing

**Write document following this structure:**

1. **Company Overview** (800-1,200 words)
   - What does the company do? (plain English)
   - How do they make money? (business model)
   - Where do they operate? (geographic presence)
   - How large are they? (revenue, employees, customers)
   - Key metrics and scale indicators

2. **Company History** (800-1,200 words)
   - Founding story (who, when, why, where)
   - Timeline of major milestones
   - Strategic pivots or transformations
   - Key acquisitions
   - Recent developments (last 1-2 years)

3. **Management Team** (1,000-1,400 words)
   - 300-400 word bio for each of 3-4 executives
   - Board composition and governance
   - Insider ownership
   - Management track record assessment

4. **Products & Services** (700-1,000 words)
   - Detailed product portfolio
   - Key features and capabilities
   - Product differentiation
   - Target customers and use cases
   - Pricing models and typical deal sizes

5. **Customers & Go-to-Market** (500-700 words)
   - Customer segments and profiles
   - Distribution channels
   - Sales strategy and cycle
   - Key partnerships
   - Customer case studies

6. **Industry Overview** (800-1,200 words)
   - Industry definition and scope
   - Market size and structure
   - Growth rates (historical and projected)
   - Key trends and drivers
   - Regulatory environment
   - Industry dynamics

7. **Competitive Landscape** (700-1,000 words)
   - Analysis of 5-10 key competitors
   - Market positioning framework
   - Company's competitive advantages
   - Competitive vulnerabilities
   - Market share analysis

8. **Market Opportunity** (500-700 words)
   - TAM sizing and methodology
   - Market growth projections
   - Company's serviceable market
   - Market share opportunity
   - Penetration strategy

9. **Risk Assessment** (600-900 words)
   - Company-specific risks (4-6)
   - Industry/market risks (3-4)
   - Financial risks (2-3)
   - Macroeconomic risks (2-3)
   - Each risk: 50-100 word description

**Data Sources Section**
- List all sources used
- Include dates and URLs
- Organize by source type

---

## Quality Standards

### Content Depth
- Each section must meet minimum word count targets
- Analysis should be substantive, not just descriptive
- Use specific examples and quantitative data
- Cite sources throughout
- Maintain objectivity and balance

### Management Bios
- 300-400 words per executive for 3-4 key executives
- Must include: current role, prior experience, key accomplishments, education
- Provide enough detail to assess track record and capabilities

### Competitive Analysis
- Must analyze 5-10 specific competitors
- Include both direct and indirect competitors
- Assess relative positioning on key dimensions
- Identify company's competitive advantages and vulnerabilities
- Use specific data and examples

### Risk Assessment
- Must identify 8-12 distinct risks across all four categories
- Each risk needs 50-100 word description
- Quantify impact where possible
- Note mitigating factors
- Cover all four risk categories

### Writing Quality
- Professional, analytical tone
- Lead with key insights
- Use concrete examples and data
- Avoid generic statements
- Proper citations throughout

---

## Output Format

```
COMPANY RESEARCH REPORT: [Company Name]
Date: [Date]
Analyst: [Your name if applicable]

TABLE OF CONTENTS
1. Company Overview
2. Company History
3. Management Team
4. Products & Services
5. Customers & Go-to-Market
6. Industry Overview
7. Competitive Landscape
8. Market Opportunity (TAM)
9. Risk Assessment

======================================

1. COMPANY OVERVIEW (800-1,200 words)

[Content]

2. COMPANY HISTORY (800-1,200 words)

[Content]

3. MANAGEMENT TEAM (1,000-1,400 words)

[Name], [Title]
[300-400 word bio]

[Repeat for 3-4 key executives]

[Governance section]

4. PRODUCTS & SERVICES (700-1,000 words)

[Content]

5. CUSTOMERS & GO-TO-MARKET (500-700 words)

[Content]

6. INDUSTRY OVERVIEW (800-1,200 words)

[Content]

7. COMPETITIVE LANDSCAPE (700-1,000 words)

[Content]

8. MARKET OPPORTUNITY (500-700 words)

[Content]

9. RISK ASSESSMENT (600-900 words)

Company-Specific Risks:
[4-6 risks with descriptions]

Industry/Market Risks:
[3-4 risks with descriptions]

Financial Risks:
[2-3 risks with descriptions]

Macroeconomic Risks:
[2-3 risks with descriptions]

======================================

DATA SOURCES
[List all sources with dates and URLs]
```

---

## Success Criteria

A successful Task 1 completion should deliver:

1. Meet 6,000-8,000 word target (verify word count)
2. Include all 9 required sections with target word counts
3. Provide substantive analysis, not just description
4. Use specific examples and quantitative data
5. Cite all sources properly
6. Enable reader to understand:
   - What the company does and how it makes money
   - Quality and track record of management team
   - Company's competitive position
   - Market opportunity size
   - Key risks to consider

---

## File Naming Convention

Save the output as:

`[Company]_Research_Document_[Date].md`

Example: `贵州茅台_600519.SH_Research_Document_2026-05-06.md` 或 `宁德时代_300750.SZ_Research_Document_2026-05-06.md`

---

## Next Steps

After completing Task 1, the research document will be used:

- As standalone company analysis
- As input for Task 2 (Financial Modeling) - provides business context for projections
- As input for Task 4 (Chart Generation) - provides data for company/competitive charts
- As foundation for Task 5 (Report Assembly) - Company 101 sections copied verbatim
