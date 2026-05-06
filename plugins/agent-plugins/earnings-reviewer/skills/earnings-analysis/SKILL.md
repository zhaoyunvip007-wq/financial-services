---
name: earnings-analysis
description: 撰写 A 股财报点评报告（8-12 页、3000-5000 字），针对已覆盖公司的季报/半年报/年报。快速周转格式，聚焦超预期/低于预期分析、核心指标、盈利预测调整、投资逻辑变化。包含 1-3 张汇总表 + 8-12 张图。触发：用户请求"财报点评""季报点评""年报点评""半年报""Q1/Q2/Q3 业绩点评""业绩快报点评"。
---

# A 股财报点评报告

撰写专业的 **A 股财报点评报告**，分析已覆盖公司的季报/半年报/年报，对标卖方研究所（中信、中金、招商、海通）的研报格式。

## A 股披露窗口（重要）

- **年报**：次年 4 月 30 日前披露完毕（多数公司 3-4 月集中披露）
- **半年报**：当年 8 月 31 日前披露完毕（多数公司 7-8 月披露）
- **一季报**：当年 4 月 30 日前披露
- **三季报**：当年 10 月 31 日前披露
- **业绩预告**：年报需在 1 月 31 日前披露（亏损/扭亏/大增/大减必须预告）
- **业绩快报**：可选披露，比正式财报早 1-2 月（提供未经审计的核心数据）

**Key Characteristics:**
- **Length**: 8-12 pages
- **Word Count**: 3,000-5,000 words
- **Tables**: 1-3 summary tables (NOT comprehensive)
- **Figures**: 8-12 charts
- **Turnaround**: 1-2 days (within 24-48 hours of earnings)
- **Audience**: Clients already familiar with the company
- **Focus**: What's NEW - beat/miss, updated estimates, thesis impact
- **Font**: Times New Roman throughout (unless user specifies otherwise)

## When to Use

Use when the user requests:
- "Create an earnings update for [Company] Q3 2024"
- "Analyze [Company]'s quarterly results"
- "Post-earnings report for [Company]"
- "Q1/Q2/Q3/Q4 update for [Company]"

**Do NOT use if:**
- User requests "initiation report" → Use different skill
- User requests "flash note" or "quick take" → Different format
- Company is not already covered → Need initiation first

## Critical Requirements

### 1. Speed & Timeliness
- Publish within 24-48 hours of earnings release
- Focus on NEW information only
- Don't rehash company background extensively

### 2. Beat/Miss Analysis
- Lead with whether company beat or missed estimates
- Quantify variances (e.g., "Revenue beat by $120M or 3%")
- Explain WHY results differed from expectations

### 3. Summary Format
- Keep tables to 1-3 (summary only, not comprehensive)
- No full P&L/Cash Flow/Balance Sheet (just key metrics)
- Assume reader has seen initiation report

### 4. A 股核心财务科目（CAS 中国会计准则）

**关键科目对照（不要用美股 GAAP 术语）：**

| A 股科目（CAS） | 美股近似科目（GAAP） | 备注 |
|---|---|---|
| 营业总收入 | Total Revenue | 包含主营 + 其他业务 |
| 营业收入 | Revenue / Net Sales | 主营业务收入 |
| 营业成本 | Cost of Revenue | A 股直接列示 |
| 销售费用 | Selling Expenses | 含市场推广、销售人员薪酬 |
| 管理费用 | G&A Expenses | 含办公、董秘费 |
| 研发费用 | R&D Expenses | 2018 年起独立列示 |
| 财务费用 | Net Interest Expense | 利息支出-利息收入 |
| 投资收益 | Investment Income | 含联营企业 + 处置收益 |
| 公允价值变动损益 | Fair Value Change | 金融资产持有期变动 |
| 营业利润 | Operating Income | A 股口径含投资收益（与美股不同） |
| 利润总额 | Pre-tax Income | 营业利润+营业外收支 |
| 归母净利润 | Net Income to Parent | 扣除少数股东损益 |
| **扣非归母净利润** | Adjusted Net Income | **核心业绩指标**，剔除非经常性损益 |
| 经营活动现金流净额 | Operating Cash Flow | 现金流量表第一项 |
| 自由现金流 | Free Cash Flow | A 股不直接披露，需自算（OCF-CapEx）|

**A 股关注的"业绩质量"指标：**
- **扣非归母净利润 vs 归母净利润差额**：差距大说明利润含较多非经常性损益（如政府补贴、资产处置、公允价值变动）
- **经营活动现金流 / 净利润 比率**：> 1 是健康，< 0.5 警惕利润质量
- **应收账款增速 vs 营收增速**：应收增速明显快于营收 = 收入确认激进
- **存货增速 vs 营收增速**：存货大增可能预示需求疲软
- **预收账款（合同负债）变化**：白酒、消费品行业的领先指标

### 5. Citations & Source Attribution ⭐⭐⭐ MANDATORY

**CRITICAL**: Properly cite all data with SPECIFIC sources and CLICKABLE HYPERLINKS.

**每张图表必须有 A 股标准引用源（带可点击链接）：**

```
资料来源：[公司名]2025 年三季度报告（披露日期 2025-10-30），公司投资者关系活动记录表
         [超链接"三季度报告"到：http://www.cninfo.com.cn/new/disclosure/detail?...]
         [超链接"投关活动记录"到：http://www.cninfo.com.cn/new/disclosure/detail?...]
```

**HOW HYPERLINKS SHOULD APPEAR IN WORD:**
- Document names appear as blue, underlined clickable links
- Reader can Ctrl+Click to open source directly
- Not plain text URLs - formatted hyperlinks with display text

**必备引用源（A 股版本）：**

每篇财报点评必须引用：
- ✅ 季报/半年报/年报全文（巨潮资讯 cninfo.com.cn 官方披露链接）
- ✅ 业绩预告/业绩快报（如已披露）
- ✅ 业绩说明会会议纪要 / 投资者关系活动记录表（巨潮披露）
- ✅ 公司公告（重大合同、定增、回购、关联交易等同期公告）
- ✅ 一致预期来源（Wind / 同花顺 iFinD / 雪球 / 东方财富 Choice，注明日期）
- ✅ 上期公告的业绩展望（如有）
- ✅ 行业数据：申万行业指数 / 国家统计局月度数据（如汽车销量、PMI、CPI）

**REFERENCE SECTION WITH CLICKABLE HYPERLINKS:**

Include "Sources" section at end of report:

```
资料来源与参考文献

财报材料（2025 年三季报）：
• 2025 年第三季度报告（披露日期 2025-10-30）
  [超链接：http://www.cninfo.com.cn/new/disclosure/detail?stockCode=600519&...]

• 投资者关系活动记录表（2025-10-31）
  [超链接：http://www.cninfo.com.cn/new/disclosure/detail?...]

• 业绩说明会通稿（如适用，公司官网或上证 e 互动）
  [超链接：上证 e 互动或公司投资者关系页面]

• 同期重大公告（如关联交易、回购、限制性股票激励等）
  [超链接：巨潮资讯网公告页面]
```

**VERIFICATION CHECKLIST:**
- [ ] Every figure has source with specific document and date
- [ ] Every table has source with document reference
- [ ] Beat/miss analysis cites consensus source with date
- [ ] Guidance changes cite current and prior guidance sources
- [ ] Key statistics have footnotes
- [ ] Sources section lists all materials with URLs
- [ ] ALL URLs are CLICKABLE HYPERLINKS (not plain text)
- [ ] All SEC filings hyperlinked to EDGAR viewer

### 5. Updated Estimates
- Update forward estimates based on results
- Show old vs. new estimates clearly
- Explain what changed and why

## High-Level Workflow

The earnings update process follows 5 phases:

### Phase 1: Data Collection (30-60 minutes)

**🚨🚨🚨 CRITICAL: TRAINING DATA IS OUTDATED 🚨🚨🚨**

**BEFORE STARTING - COMPLETE THESE 4 STEPS IN ORDER:**
1. **CHECK TODAY'S DATE** - Write down the current date
2. **SEARCH FOR LATEST** - Use web search: "[Company] latest earnings results"
3. **VERIFY THE DATE** - Confirm earnings release is within last 3 months
4. **CHECK TRANSCRIPT DATE** - Verify transcript date matches release date

**COMMON MISTAKE**: Using outdated earnings calls from training data instead of searching for the latest.

**REQUIREMENTS:**
- ✅ Search for latest earnings - do NOT rely on training data
- ✅ Write down today's date and the release date found
- ✅ Verify release date is within 3 months of today
- ✅ Verify transcript date matches release date
- ✅ If dates don't match or are old (>3 months), search again

**See [references/workflow.md](references/workflow.md)** for detailed search procedures and verification steps.

### Phase 2: Analysis (2-3 hours)
- Beat/miss analysis for each key metric
- Segment/geographic/product breakdown
- Margin and guidance analysis
- Update financial model and estimates

**See [references/workflow.md](references/workflow.md)** for detailed analysis framework.

### Phase 3: Chart Generation (1-2 hours)
Create 8-12 charts focusing on quarterly trends and what's new:
- Quarterly revenue progression
- Quarterly EPS progression
- Quarterly margin trends
- Revenue by segment/geography
- Key operating metrics
- Beat/miss summary
- Estimate revisions
- Valuation charts

**See [references/workflow.md](references/workflow.md)** for chart specifications.

### Phase 4: Report Creation (2-3 hours)
Create 8-12 page DOCX report with specific structure.

**See [references/report-structure.md](references/report-structure.md)** for complete page-by-page templates and formatting requirements.

**High-level structure:**
- Page 1: Earnings summary with rating and price target
- Pages 2-3: Detailed results analysis
- Pages 4-5: Key metrics & guidance
- Pages 6-7: Updated investment thesis
- Pages 8-10: Valuation & estimates
- Pages 11-12: Appendix (optional)

### Phase 5: Quality Check & Delivery (30 minutes)
Verify content, formatting, accuracy, and timeliness before delivery.

**See [references/best-practices.md](references/best-practices.md)** for quality checklist and common mistakes to avoid.

## Output Specification

**Primary Deliverable**: DOCX report (8-12 pages)
**文件命名**：`[公司名]_[年份]Q[季度]_财报点评.docx`
**示例**：`贵州茅台_2025Q3_财报点评.docx`、`宁德时代_2025年报_点评.docx`

**Contents:**
- Page 1: Summary with rating, price target, key takeaways
- Pages 2-3: Detailed results analysis
- Pages 4-5: Key metrics and guidance
- Pages 6-7: Updated thesis assessment
- Pages 8-10: Valuation and estimates
- Pages 11-12: Appendix (optional)
- 8-12 embedded charts
- 1-3 summary tables
- Complete sources section with clickable hyperlinks

**Optional Deliverable**: XLS model update (optional for earnings updates)

## Key Differences from Initiation Report

| Aspect | Earnings Update | Initiation Report |
|--------|----------------|-------------------|
| **Length** | 8-12 pages | 30-50 pages |
| **Words** | 3,000-5,000 | 10,000-15,000 |
| **Tables** | 1-3 summary | 12-20 comprehensive |
| **Figures** | 8-12 | 25-35 |
| **Turnaround** | 1-2 days | 3-6 weeks |
| **Scope** | Quarterly results | Complete company |
| **Focus** | What's NEW | Everything |
| **Company Background** | Brief mention | 6-10 pages |
| **XLS Model** | Optional | Required |

## Resources

### references/workflow.md
Detailed Phase 1-5 instructions with step-by-step procedures for data collection, analysis, chart generation, and report creation.

### references/report-structure.md
Complete page-by-page templates, table formats, and formatting requirements for the DOCX report.

### references/best-practices.md
Examples of good/bad headlines, tips for success, common mistakes to avoid, and comprehensive quality checklist.

## Dependencies

**Required:**
- Python (matplotlib, pandas, seaborn) for chart generation
- DOCX skill for report creation

**Optional:**
- XLS skill for model updates (not required for earnings updates)
