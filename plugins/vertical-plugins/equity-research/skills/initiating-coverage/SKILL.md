---
name: initiating-coverage
description: Create institutional-quality A-share equity research initiation reports (首次覆盖报告) through a 5-task workflow. Tasks must be executed individually with verified prerequisites - (1) company research, (2) financial modeling, (3) valuation analysis, (4) chart generation, (5) final report assembly. Each task produces specific deliverables (markdown docs, Excel models, charts, or DOCX reports). Tasks 3-5 have dependencies on earlier tasks.
---

# Initiating Coverage（A股首次覆盖报告）

Create institutional-quality A-share equity research initiation reports (首次覆盖报告) through a structured 5-task workflow. Each task must be executed separately with verified inputs.

## Overview

This skill produces comprehensive first-time coverage reports for A-share listed companies following Chinese sell-side institutional standards (中信证券、中金公司、海通证券、招商证券 format). Tasks are executed individually, each verifying prerequisites before proceeding.

**Default Font**: 宋体 (SimSun) for body text and 黑体 (SimHei) for headings throughout all Chinese documents (unless user specifies otherwise). For mixed Chinese-English content, English text uses Times New Roman.

**目标市场**: 沪深 A 股（上交所主板/科创板、深交所主板/创业板、北交所），股票代码格式 `XXXXXX.SH` / `XXXXXX.SZ` / `XXXXXX.BJ`（例：贵州茅台 600519.SH，五粮液 000858.SZ，宁德时代 300750.SZ）。

---

## ⚠️ CRITICAL: One Task at a Time

**THIS SKILL OPERATES IN SINGLE-TASK MODE ONLY.**

### If User Requests Full Pipeline

When user requests:
- "Create a coverage initiation report for [Company]"
- "Write an initiation report for [Company]"
- "Do the entire equity research process for [Company]"
- "Complete all 5 tasks for [Company]"
- Any request that implies running multiple tasks or the entire workflow

**REQUIRED RESPONSE:**

1. **Ask which specific task to perform:**
   ```
   I can help you create an equity research initiation report for [Company].
   This involves 5 separate tasks that need to be completed individually:

   1. Company Research - Research business, management, industry
   2. Financial Modeling - Build projection model
   3. Valuation Analysis - DCF and comparable companies
   4. Chart Generation - Create 25-35 charts
   5. Report Assembly - Compile final report

   Which task would you like to start with?
   ```

2. **When user explicitly requests all tasks together:**
   ```
   I understand you'd like to complete the entire initiation report pipeline.
   Currently, this skill supports executing one task at a time, which allows
   for better quality control and review at each stage.

   We're working on a seamless end-to-end workflow that will make this process
   more automated, but for now, we'll need to complete each task separately.

   Would you like to start with Task 1 (Company Research)?
   ```

3. **Never automatically assume which task to start** - always ask user to confirm.

4. **Never execute multiple tasks in sequence** - complete one task, deliver outputs, then wait for next user request.

### Task Execution Rules

- ✅ Execute exactly ONE task per user request
- ✅ Always verify prerequisites before starting a task
- ✅ Deliver task outputs and confirm completion
- ✅ Wait for user to explicitly request the next task
- ❌ Never chain multiple tasks together automatically
- ❌ Never assume user wants to proceed to next task
- ❌ Never execute Tasks 3-5 without verifying required inputs exist

### ⚠️ Deliverables Policy: NO SHORTCUTS

**DELIVER ONLY THE SPECIFIED OUTPUTS. DO NOT CREATE EXTRA DOCUMENTS.**

Each task specifies exact deliverables. Do NOT create:
- ❌ "Completion summaries"
- ❌ "Executive summaries"
- ❌ "Quick reference guides"
- ❌ "Next steps documents"
- ❌ "Task completion reports"
- ❌ Any other "helpful" documentation not explicitly specified

**Why**: These extras waste context and are not part of the professional workflow.

**What TO deliver**:
- ✅ Task 1: Research document (.md) — **NOTHING ELSE**
- ✅ Task 2: Financial model (.xlsx) — **NOTHING ELSE**
- ✅ Task 3: Valuation analysis (.md) + Excel tabs added to Task 2 file — **NOTHING ELSE**
- ✅ Task 4: Charts zip file (.zip) — **NOTHING ELSE**
- ✅ Task 5: Final report (.docx) — **NOTHING ELSE**

**If a deliverable is not listed above, DO NOT CREATE IT.**

---

## Task Selection

Select which task to execute:

| Task | Name | Prerequisites | Output |
|------|------|--------------|--------|
| **1** | 公司研究 (Company Research) | 公司名称 / A股代码 | 6-8K 字研究文档 |
| **2** | 财务建模 (Financial Modeling) | 年度报告 / 财务数据 | Excel 模型（6 个标签页） |
| **3** | 估值分析 (Valuation Analysis) | 财务模型（Task 2） | 估值结果 + 目标价 |
| **4** | 图表生成 (Chart Generation) | Tasks 1, 2, 3 + 外部数据 | 25-35 张 PNG/JPG 图表 |
| **5** | 报告组装 (Report Assembly) | 前序所有任务 (1-4) | 30-50 页 DOCX 报告 |

---

## How to Use This Skill

### User Request Patterns and Responses

**Pattern 1: User specifies a specific task**
```
User: "Use initiating-coverage, Task 1 for 贵州茅台 (600519.SH)"
Response: ✅ Execute Task 1 immediately
```

**Pattern 2: User asks for "initiation report" or "full pipeline"**
```
User: "为宁德时代 (300750.SZ) 写一份首次覆盖报告"
Response: ❌ DO NOT start any task automatically
         ✅ Ask which task to start with (see template above)
```

**Pattern 3: User wants to do "all tasks" or "entire workflow"**
```
User: "把比亚迪 (002594.SZ) 的 5 个任务全部跑完"
Response: ❌ DO NOT chain tasks together
         ✅ Explain one-at-a-time limitation (see template above)
         ✅ Ask if they want to start with Task 1
```

### Correct Usage Examples

**Executing a single task:**
```
"Use initiating-coverage skill, Task 1 for 贵州茅台 (600519.SH)"
"Do Task 2 of initiating-coverage for 五粮液 (000858.SZ)"
"Run Task 3 for 宁德时代 (300750.SZ) using the initiating-coverage skill"
```

**Completing full report (requires 5 separate requests):**
```
Request 1: "Do Task 1 for 贵州茅台 (600519.SH)" → Complete → Deliver outputs
Request 2: "Do Task 2 for 贵州茅台 (600519.SH)" → Complete → Deliver outputs
Request 3: "Do Task 3 for 贵州茅台 (600519.SH)" → Complete → Deliver outputs
Request 4: "Do Task 4 for 贵州茅台 (600519.SH)" → Complete → Deliver outputs
Request 5: "Do Task 5 for 贵州茅台 (600519.SH)" → Complete → Deliver outputs
```

### Task Execution Order

For a complete initiation report, tasks must be executed in separate user requests following this order:

```
Request 1: Task 1 - Company Research (independent)
           ↓ [User reviews outputs and requests next task]
Request 2: Task 2 - Financial Modeling (independent)
           ↓ [User reviews outputs and requests next task]
Request 3: Task 3 - Valuation Analysis (requires Task 2 output)
           ↓ [User reviews outputs and requests next task]
Request 4: Task 4 - Chart Generation (requires Tasks 2 & 3 outputs)
           ↓ [User reviews outputs and requests next task]
Request 5: Task 5 - Report Assembly (requires ALL previous task outputs)
```

**Note**: Tasks 1 and 2 can be run in any order. Tasks 3-5 have strict dependencies and must verify inputs before proceeding.

---

## Task 1: Company Research

**Purpose**: Research A-share listed company's 业务、管理层、行业地位、竞争格局 and 风险。

**Prerequisites**: ✅ None (fully independent)
- 公司中文名称 + A 股代码（如：贵州茅台 600519.SH）

**核心数据源（A 股）**:
- **巨潮资讯网** (cninfo.com.cn) — 官方法定信息披露平台：年度报告、季度报告（一季报/三季报）、半年度报告、临时公告
- **沪深交易所官网** (sse.com.cn / szse.cn) — 公告、ESG 信息、问询函回复
- **AKShare MCP / Tushare MCP** — 行情、财务、股东、行业数据接口
- **Wind / 同花顺 iFinD / 东方财富 Choice** — 专业数据终端（如可用）
- **业绩说明会** / **投资者关系活动记录表** / **上证 e 互动** / **深交所互动易** — 替代美股 earnings call transcript
- **券商研报库**（慧博、Wind 研报、东方财富研报）— 同行研究参考
- **行业协会数据** — 中汽协、中钢协、中酒协、半导体协会等
- **国家统计局 / 工信部 / 发改委** — 宏观与行业政策

**披露窗口提示（A 股法定时点）**:
- 年度报告：次年 4 月 30 日前
- 半年度报告：当年 8 月 31 日前
- 一季报：当年 4 月 30 日前
- 三季报：当年 10 月 31 日前
- 业绩预告：报告期结束后（年报预告 1 月底前、半年报预告 7 月中旬前）

**Process**:
1. Verify 公司名称 / A 股代码 provided（XXXXXX.SH / XXXXXX.SZ / XXXXXX.BJ）
2. Load detailed instructions from references/task1-company-research.md
3. Execute qualitative research workflow（数据源以巨潮 + AKShare 为主）
4. Deliver research document

**Output**: 公司研究文档 (Company Research Document, 6,000-8,000 字)
- 公司概况与发展沿革
- 管理层简历（300-400 字 × 3-4 位高管，覆盖董事长 / 总经理 / 财务总监 / 核心技术 or 业务负责人）
- 主营业务与产品分析（按申万行业分类描述）
- 行业概况（申万一级 / 二级 / 三级行业分类）
- 竞争分析（5-10 家可比公司，含 A 股同业 + 港股/美股中概同业）
- 市场空间测算（国内市场 + 出海市场）
- 风险评估（8-12 项，含 A 股专属风险类别）

**File name**: `[公司名]([代码])_首次覆盖_[年月].md`（例：`贵州茅台(600519.SH)_首次覆盖_202605.md`）

**⚠️ DELIVER ONLY THIS 1 FILE. NO completion summaries, no extra documents.**

**⚠️ DO NOT TAKE SHORTCUTS:**
- ✅ Write full 6,000-8,000 字（中文 / not summaries）
- ✅ Complete 300-400 字 bios for ALL 3-4 高管
- ✅ Analyze ALL 5-10 可比公司 thoroughly
- ✅ Cover all 8-12 风险 across 4 categories（含 A 股专属风险）
- ❌ Do not abbreviate sections to save time
- ❌ Do not skip any required sections

**Verification before proceeding**: None required for this task.

---

## Task 2: Financial Modeling

**Purpose**: Extract historical financials (按 CAS 中国会计准则) and build comprehensive Excel financial model with projections and scenarios.

**会计准则**: 中国企业会计准则 (CAS)。报表项目使用 A 股标准中文科目（营业总收入、营业成本、销售费用、管理费用、研发费用、财务费用、营业利润、利润总额、净利润、归属于母公司股东的净利润 / **归母净利润**、扣除非经常性损益后的归母净利润 / **扣非归母净利润**、经营活动产生的现金流量净额 等）。

**货币与单位**: 人民币元，列示单位统一为 **人民币亿元**（大额）或 **人民币百万元**（细项）。涉及外币业务（出海占比高的公司）需注明汇率假设。

**Prerequisites**: ⚠️ Verify before starting
- **Required**: Access to company financial data
  - 上市公司：最新年度报告（年报）+ 最近一期半年度报告 / 季度报告，从巨潮资讯网下载
  - 数据接口：AKShare MCP / Tushare MCP 提取标准化财务三表
  - OR: 用户提供已整理好的历史财务数据
- **Optional**: Company research (Task 1) for business context

**Input Verification**:
```
BEFORE STARTING - Select approach:

Option A: Extract financials (most common)
- [ ] 是否能访问巨潮资讯网年度报告 / AKShare / Tushare？
- [ ] 是否准备提取 3-5 年的年报数据 + 最近一期季报 / 半年报？

Option B: User provided pre-extracted financials
- [ ] 是否收到历史财务数据文件？
- [ ] 是否包含三大报表（利润表 / 现金流量表 / 资产负债表）3-5 年完整数据？
- [ ] 是否区分了归母净利润与扣非归母净利润？

Optional:
- [ ] Company research (Task 1) complete for context?

披露窗口对齐:
- [ ] 当前日期是否已过最新年报披露窗口（4 月底）？如已过，必须使用最新年报
- [ ] 是否需要纳入最新季报 / 半年报数据增强时效性？
```

**Process**:
1. Verify access to financial data（巨潮 / AKShare / Tushare）
2. Load detailed instructions from references/task2-financial-modeling.md
3. **Step 1**: Extract historical financials（按 CAS 科目）
4. **Step 2+**: Build projection model with 6 essential tabs
5. Deliver Excel model

**Output**: Excel 财务模型 (.xlsx)
- 6 个核心标签页：
  1. **收入模型 (Revenue Model)** - 分产品 / 业务条线拆分（20-30 行）+ 分地区 / 国内外拆分（15-20 行）
  2. **利润表 (Income Statement)** - 完整 P&L，40-50 个科目（按 CAS：营业总收入 → 营业成本 → 销售/管理/研发/财务费用 → 营业利润 → 利润总额 → 净利润 → 归母净利润 → 扣非归母净利润），历史 3-5 年 + 预测 5 年
  3. **现金流量表 (Cash Flow Statement)** - 经营活动 / 投资活动 / 筹资活动现金流，历史 + 预测
  4. **资产负债表 (Balance Sheet)** - 资产 / 负债 / 所有者权益，历史 + 预测，重点列示商誉、应收账款、存货、有息负债
  5. **情景分析 (Scenarios)** - 乐观 / 中性 / 悲观三档对比表
  6. **DCF 输入 (DCF Inputs)** - 为 Task 3 估值准备无杠杆自由现金流 (UFCF)、WACC 输入

**File name**: `[公司名]([代码])_财务模型_[年月].xlsx`（例：`贵州茅台(600519.SH)_财务模型_202605.xlsx`）

**⚠️ DELIVER ONLY THIS 1 FILE. NO completion summaries, no extra documents.**

**⚠️ DO NOT TAKE SHORTCUTS:**
- ✅ 提取三大报表（CAS 准则）所有科目（3-5 年）
- ✅ 建立完整 6 个标签页（不简化）
- ✅ 收入模型必须区分主营业务 vs 其他业务，分产品（20-30 行）+ 分地区（含国内 / 海外，15-20 行）
- ✅ 利润表必须同时披露 净利润 / 归母净利润 / 扣非归母净利润 三档
- ✅ 资产负债表必须独立列示 商誉、应收账款、存货周转、有息负债（短期借款 + 长期借款 + 应付债券）
- ✅ 现金流量表必须区分 经营活动 / 投资活动 / 筹资活动 三档
- ✅ 三种情景（乐观 / 中性 / 悲观）必须使用差异化参数
- ❌ 不要使用 GAAP / IFRS 科目命名
- ❌ 不要使用美元单位
- ❌ Do not skip 历史财务数据提取 if needed

**Verification before proceeding to Task 3**:
- [ ] 历史财务数据已提取（按 CAS 准则）
- [ ] Excel 文件创建并可打开
- [ ] 6 个标签页齐备（收入模型 / 利润表 / 现金流量表 / 资产负债表 / 情景分析 / DCF 输入）
- [ ] 历史数据（3-5 年）已录入
- [ ] 预测（5 年）已完成
- [ ] 三种情景（乐观 / 中性 / 悲观）已完成
- [ ] 货币单位统一为人民币亿元 / 百万元

---

## Task 3: Valuation Analysis

**Purpose**: Perform comprehensive A 股估值，使用 A 股市场偏好的估值方法（PE / PB / PEG / DCF / 戈登增长模型），辅以可比公司分析。

**A 股估值方法选择（重要 — 不同于美股）**:

A 股市场估值偏好与美股有显著差异，**主估值方法按行业选择**：

| 行业类别 | 主估值方法 | 辅助方法 | 经验估值区间 |
|---------|----------|---------|------------|
| **白酒 / 高端消费** | PE | DCF、PEG | 25-40x PE（茅台 30-40x、其他 20-30x） |
| **银行** | PB | 戈登增长模型、ROE-PB 联动 | 0.5-1.2x PB |
| **保险** | PEV（内含价值倍数） | PB | 0.6-1.5x PEV |
| **券商** | PB | PE | 1-2x PB |
| **房地产** | PB / NAV | PE | 0.5-1.5x PB |
| **公用事业（电力、燃气、水务）** | DCF / 戈登增长模型 | PE、PB | 10-15x PE |
| **新能源（光伏、风电、锂电）** | PE / PEG | DCF | 15-30x PE（成长期） |
| **半导体 / 软件** | PE / PEG / PS | DCF | 30-60x PE（高成长） |
| **医药（创新药）** | DCF（管线 NPV） | PS | 视管线而定 |
| **医药（仿制药 / 原料药）** | PE | PEG | 15-25x PE |
| **传统制造 / 周期股** | PB（底部）/ PE（中部）| EV/EBITDA | 1-2x PB 或 8-15x PE |
| **互联网 / 平台** | PE / PS / DCF | EV/EBITDA | 视生命周期 |

**核心估值方法详解**:
1. **PE 估值**：A 股最常用，分行业 PE 倍数对标。需注意：(a) 用扣非归母净利润口径更稳健；(b) 警惕一次性损益带来的"PE 失真"
2. **PB 估值**：金融、地产、强周期行业首选。结合 ROE 判断（高 ROE 应享受 PB 溢价）
3. **PEG 估值**：成长股核心方法，PEG = PE / 利润增速。<1 低估，1-1.5 合理，>1.5 偏高
4. **DCF 估值**：长周期稳定现金流公司（公用、消费龙头）。WACC 选取需符合 A 股市场利率水平（通常 8-10%），永续增长率取 2-3%（与 GDP 长期增速对齐）
5. **戈登增长模型**：适用于稳定派息的银行、公用、高分红蓝筹。P = D₁ / (r - g)
6. **可比公司估值（同业对标）**：选择申万同行业 5-10 家 A 股公司 + 港股 / 美股中概同业（如适用）

**辅助方法**: EV/EBITDA 在 A 股仅作辅助参考（用于跨市场对比或并购场景），**不作为主估值**。

**Prerequisites**: ⚠️ Verify before starting
- **Required**: Financial model from Task 2
  - 预测利润表（含归母净利润 / 扣非归母净利润）
  - 预测现金流量表
  - 营业收入与净利润预测
  - DCF 输入（无杠杆自由现金流 UFCF）
  - 预测 ROE / ROA / 净资产 / 每股净资产 / EPS / BPS

**⚠️ CRITICAL: DO NOT START THIS TASK UNLESS TASK 2 IS COMPLETE**

This task requires the financial model from Task 2. Starting without it will result in incomplete work.

**IF TASK 2 IS NOT COMPLETE**: Stop immediately and inform the user that Task 2 (Financial Modeling) must be completed first. Do not attempt to proceed or create placeholder valuations.

**Input Verification**:
```
BEFORE STARTING:
- [ ] Task 2 complete? (财务模型已存在)
- [ ] 模型文件路径已知？
- [ ] 能访问预测财务数据？
- [ ] 已确认公司所属申万一级行业（决定主估值方法）？

Required from model:
- [ ] 预测无杠杆自由现金流 UFCF（5 年）
- [ ] 预测营业总收入
- [ ] 预测归母净利润 / 扣非归母净利润
- [ ] 预测每股收益 EPS / 每股净资产 BPS
- [ ] 永续期数据 / 终值假设
```

**Process**:
1. Verify financial model is accessible
2. Load detailed instructions from references/task3-valuation.md
3. **根据行业选择主估值方法**（按上表）
4. Execute valuation workflow
5. Deliver valuation analysis

**Output**: 估值分析 (Valuation Analysis, 4-6 页 + Excel 标签页)
- 主估值方法（PE / PB / PEG / DCF / 戈登增长 — 按行业）+ 敏感性分析
- 可比公司分析（5-10 家申万同行业 A 股 + 港股 / 美股同业）
- 历史估值带（PE Band / PB Band — 5 年滚动）
- 估值对比图（football field）
- **目标价**: ¥XX.XX 元
- **投资评级**: 买入 / 增持 / 中性 / 减持 / 卖出（A 股标准五档评级，**不使用美股 BUY/HOLD/SELL 三档**）
- **上行空间**: XX%
- **股价催化因素 (Catalysts)**: 3-5 项（业绩超预期、政策落地、新产品发布、产能投放、并购重组等）

**评级体系（A 股惯例 — 强制使用五档）**:
- **买入 (Buy)**: 未来 6-12 个月预期相对沪深 300 涨幅 > 20%
- **增持 (Overweight)**: 未来 6-12 个月预期相对沪深 300 涨幅 5-20%
- **中性 (Neutral)**: 未来 6-12 个月预期相对沪深 300 涨幅 -5% 至 +5%
- **减持 (Underweight)**: 未来 6-12 个月预期相对沪深 300 涨幅 -20% 至 -5%
- **卖出 (Sell)**: 未来 6-12 个月预期相对沪深 300 涨幅 < -20%

**Files**:
- `[公司名]([代码])_估值分析_[年月].md`（例：`贵州茅台(600519.SH)_估值分析_202605.md`）
- Excel 标签页 added to `[公司名]([代码])_财务模型_[年月].xlsx`（from Task 2）
  - 主估值标签页（PE / PB / PEG / DCF — 按行业选择）
  - 敏感性分析标签页（双因素：WACC × 永续增速 或 PE × EPS）
  - 可比公司标签页（同业对标）
  - 估值汇总标签页（football field）

**⚠️ DELIVER ONLY: 1 markdown 文件 + 4 个标签页 added to existing Excel. NO completion summaries, no extra documents.**

**⚠️ DO NOT TAKE SHORTCUTS:**
- ✅ 完成主估值方法 with 完整敏感性矩阵 (not simplified)
- ✅ 分析 5-10 家可比公司（申万同行业 A 股优先）with full data
- ✅ 在可比公司表中包含统计摘要（最大值 / 75 分位 / 中位数 / 25 分位 / 最小值）
- ✅ 历史估值带（PE Band / PB Band）必须给出 5 年滚动数据
- ✅ 完成完整的敏感性分析标签页（多档 WACC 与 永续增速 / 多档 PE 与 EPS）
- ✅ 写完整 4-6 页估值分析（不简化）
- ✅ 用具体方法论论证目标价（不能只给结论不给推导过程）
- ❌ 不要跳过可比公司分析
- ❌ 不要使用美元定价（必须人民币元）
- ❌ 不要使用 BUY/HOLD/SELL 三档评级（必须用 A 股五档）

**Verification before proceeding to Task 4**:
- [ ] 目标价（¥XX.XX 元）已确定
- [ ] 投资评级（买入 / 增持 / 中性 / 减持 / 卖出）已确定
- [ ] 估值采用多种方法（主估值 + 可比公司 minimum）
- [ ] 主估值方法符合行业惯例（按上表行业偏好选择）
- [ ] 敏感性分析表完整
- [ ] 可比公司表包含统计摘要

---

## Task 4: Chart Generation

**Purpose**: Generate 25-35 professional financial charts for the report.

**Prerequisites**: ⚠️ Verify before starting
- **Required**: Company research from Task 1
  - Company history and milestones (for timeline charts)
  - Management team and org structure (for org charts)
  - Product portfolio (for product charts)
  - Customer segmentation (for customer charts)
  - Competitive landscape (for competitive charts)
  - TAM analysis (for market size charts)
- **Required**: Financial model from Task 2 (with Task 3 valuation tabs added)
  - Revenue by product/geography data (Task 2 tabs)
  - Margin trends (Task 2 tabs)
  - Scenario comparison data (Task 2 tabs)
  - DCF sensitivity table (Task 3 tab in same Excel file)
  - Comparable companies data (Task 3 tab in same Excel file)
  - Valuation ranges (Task 3 tab in same Excel file)
- **Required**: 外部市场数据
  - 历史股价数据（AKShare MCP / Tushare MCP / 同花顺 / 东方财富）
  - 历史估值倍数（5 年 PE Band / PB Band，用于历史估值带图）
  - 行业指数对比（申万行业指数、沪深 300 / 中证 500 / 创业板指）

**⚠️ CRITICAL: DO NOT START THIS TASK UNLESS TASKS 1, 2, AND 3 ARE COMPLETE**

This task requires outputs from all three previous tasks. Starting without them will result in incomplete charts.

**IF ANY OF TASKS 1, 2, OR 3 ARE NOT COMPLETE**: Stop immediately and inform the user which tasks need to be completed first. The specific requirements are:
- Task 1: Company research document (for 9 charts)
- Task 2: Financial model with all 6 tabs (for 8 charts)
- Task 3: Valuation tabs added to the model (for 6 charts)
- External data access (for 2 charts)

Do not attempt to create placeholder charts or skip charts due to missing data.

**Input Verification**:
```
BEFORE STARTING:
- [ ] Task 1 complete? (Company research exists)
- [ ] Task 2 complete? (Financial model exists)
- [ ] Task 3 complete? (Valuation analysis exists)
- [ ] Can access external market data sources?

Required from Task 1:
- [ ] Company history and milestones (for charts 05, 06)
- [ ] Management team structure (for chart 07)
- [ ] Product portfolio details (for chart 08)
- [ ] Customer segmentation data (for chart 09)
- [ ] Competitive landscape analysis (for charts 16, 17, 18)
- [ ] TAM sizing and market data (for chart 15)

Required from Task 2:
- [ ] Revenue by product (historical + projected) - for chart 03 ⭐
- [ ] Revenue by geography (historical + projected) - for chart 04 ⭐
- [ ] Income statement with margins (for charts 02, 10, 11)
- [ ] Cash flow statement (for chart 12)
- [ ] Scenario comparison data (for chart 14)

Required from Task 3:
- [ ] 主估值敏感性矩阵 - for chart 28 ⭐（PE / PB / DCF 敏感性）
- [ ] 估值方法分解（for chart 29）
- [ ] 可比公司数据（for charts 30, 31 — 申万同业对标）
- [ ] 估值区间 - for chart 32 ⭐（football field）

Required from External Sources（A 股数据源）:
- [ ] 历史股价数据（for chart 01 — 含沪深 300 / 申万行业指数对比）
- [ ] 历史估值倍数 PE Band / PB Band（for chart 34 — 5 年滚动）
```

**Process**:
1. Verify model and valuation outputs are accessible
2. Load detailed instructions from references/task4-chart-generation.md
3. Execute chart generation workflow
4. Package all charts into a zip file
5. Deliver zip file

**Output**: 25-35 Professional Chart Files (PNG/JPG, 300 DPI) packaged in zip

**4 MANDATORY Charts** (must be present) ⭐:
- chart_03: 分产品 / 业务条线营业收入构成 (stacked area)
- chart_04: 分地区营业收入（国内 vs 出海，stacked bar）
- chart_28: 主估值敏感性热力图（2-way heatmap — PE×EPS 或 WACC×永续增速）
- chart_32: 估值对比 football field（多种估值方法目标价区间，horizontal bars）

**25 REQUIRED Charts** (specific list):
- Investment Summary: chart_01
- Financial Performance: charts 02, 03⭐, 04⭐, 10, 11, 12, 14
- Company 101: charts 05, 06, 07, 08, 09, 15, 16
- Competitive/Market: charts 17, 18
- Scenario Analysis: chart 13
- Valuation: charts 28⭐, 29, 30, 31, 32⭐, 33, 34

**10 OPTIONAL Charts** (for 26-35 range):
- charts 19-27, 35 (customer acquisition, unit economics, product roadmap, etc.)

**IMPORTANT**: Task 5 embeds ALL charts created (25-35) for visual density (1 chart per 200-300 words).

**File naming**: `chart_01_description.png`, `chart_02_description.png`, etc.

**Deliverable**: `[公司名]([代码])_图表_[年月].zip`（例：`贵州茅台(600519.SH)_图表_202605.zip`）containing all 25-35 chart files + chart_index.txt

**⚠️ DELIVER ONLY THIS 1 ZIP FILE. NO completion summaries, no separate chart lists, no extra documents.**

**⚠️ DO NOT TAKE SHORTCUTS:**
- ✅ 创建至少 25 张图表（specific list provided in task4-chart-generation.md）
- ✅ 必须包含全部 4 张强制图表：
  - chart_03: 分产品 / 业务营业收入构成 (stacked area) ⭐
  - chart_04: 分地区营业收入（国内 vs 出海，stacked bar）⭐
  - chart_28: 主估值敏感性热力图 (heatmap) ⭐
  - chart_32: 估值 football field ⭐
- ✅ Optional: 额外加 1-10 张图表达到 26-35 张以提升视觉密度
- ✅ Generate professional-quality charts at 300 DPI (not low-res placeholders)
- ✅ 图表标题、轴标签、图例使用中文（货币单位人民币亿元 / 百万元）
- ✅ Create unique, well-formatted charts for each visualization
- ✅ Package all charts in zip file with chart index
- ❌ Do not create only 10-15 charts (minimum is 25)
- ❌ Do not skip any of the 4 mandatory charts
- ❌ Do not use low-quality/placeholder images
- ❌ 不要使用美元单位
- ❌ 不要使用英文标题（除非中英对照）

**Verification before proceeding to Task 5**:
- [ ] 至少 25 张图表已创建
- [ ] 4 张强制图表齐备:
  - [ ] chart_03: 分产品 / 业务营业收入 ⭐
  - [ ] chart_04: 分地区营业收入（国内 vs 出海）⭐
  - [ ] chart_28: 主估值敏感性 ⭐
  - [ ] chart_32: 估值 football field ⭐
- [ ] All charts open and display correctly
- [ ] Charts saved at 300 DPI (print quality)
- [ ] 图表使用中文标签和人民币单位
- [ ] Chart index created listing all files with categories
- [ ] All charts packaged in zip file
- [ ] File naming follows convention: chart_##_description.png

---

## Task 5: Report Assembly

**Purpose**: Write and assemble the comprehensive final DOCX report.

**Prerequisites**: ⚠️ Verify before starting
- **Required**: 公司研究 from Task 1
  - 完整 6-8K 字内容
  - 管理层简历
  - 竞争分析
  - 风险评估（含 A 股专属风险）
- **Required**: 财务模型 from Task 2
  - Excel 工作簿（CAS 准则）
  - 所有预测与情景
- **Required**: 估值分析 from Task 3
  - 目标价（¥XX.XX 元）和评级（买入 / 增持 / 中性 / 减持 / 卖出）
  - 主估值方法（PE / PB / PEG / DCF / 戈登）+ 可比公司
  - 全部估值数据
- **Required**: 图表文件 from Task 4
  - Zip 文件包含 25-35 张 PNG/JPG 文件（中文标签）
  - chart_index.txt 包含在 zip 内

**⚠️ CRITICAL: DO NOT START THIS TASK UNLESS ALL TASKS 1-4 ARE COMPLETE**

This is the final assembly task. It cannot be completed without all previous work products.

**IF ANY OF TASKS 1, 2, 3, OR 4 ARE NOT COMPLETE**: Stop immediately and inform the user which tasks need to be completed first. The specific requirements are:
- Task 1: Company research document (6-8K words)
- Task 2: Financial model with all 6 tabs
- Task 3: Valuation analysis with price target and recommendation
- Task 4: Charts zip file with 25-35 charts

Do not attempt to create placeholder content, substitute missing sections, or assemble an incomplete report. The report requires ALL inputs to be publication-ready.

**Input Verification**:
```
BEFORE STARTING - ALL TASKS MUST BE COMPLETE:

Task 1 Verification:
- [ ] Company research document exists? (6-8K words)
- [ ] Management bios complete? (300-400 words × 3-4 execs)
- [ ] Competitive analysis complete? (5-10 competitors)
- [ ] Risk assessment complete? (8-12 risks)

Task 2 Verification:
- [ ] Financial model exists and can be opened?
- [ ] Model has projections (5 years)?
- [ ] Scenarios exist (Bull/Base/Bear)?

Task 3 Verification:
- [ ] 估值分析完成？
- [ ] 目标价（¥XX.XX 元）已确定？
- [ ] 评级已设置？（买入 / 增持 / 中性 / 减持 / 卖出）
- [ ] 主估值方法 + 可比公司分析完成？

Task 4 Verification:
- [ ] Chart zip file exists?
- [ ] Can extract/access all 25-35 chart files from zip?
- [ ] All 4 mandatory charts present?
  - [ ] 分产品 / 业务营业收入构成 (stacked area)
  - [ ] 分地区营业收入（国内 vs 出海，stacked bar）
  - [ ] 主估值敏感性 (heatmap)
  - [ ] 估值 football field
- [ ] Chart files accessible and can be opened?

IF ANY VERIFICATION FAILS: Stop and complete missing task first.
```

**Process**:
1. **CRITICAL**: Verify ALL prerequisites before starting
2. Load detailed instructions from references/task5-report-assembly.md
3. Execute report assembly workflow using Claude's built-in skills:
   - **Use DOCX skill** to create and manipulate the Word document
   - **Use XLSX skill** to read Excel data from Task 2/3
   - **Use Read tool** to read Task 1 and Task 3 markdown files
   - Read Task 1 .md file → Convert to Word formatting → Insert charts inline
   - Read Task 2 .xlsx file → Extract tables → Write quantitative analysis
   - Read Task 3 .md file + Excel tabs → Copy/adapt valuation analysis
   - Insert Task 4 .png chart files throughout using DOCX skill
   - Create text-dense report with charts interspersed every 200-300 words
4. Save and deliver final DOCX report

**Key Principles**:
- Use Claude's DOCX and XLSX skills (NOT Python libraries)
- Use actual file operations (read .md/.xlsx/.png files, write .docx file)
- Good equity research reports are text-dense with lots of illustrating images (60-80% page coverage, 1+ chart per page)

**🔥 CRITICAL: GO ALL OUT ON THIS TASK**

**THIS IS THE FINAL DELIVERABLE. DO NOT TAKE SHORTCUTS.**

- ✅ **Use full token budget** - This is the culmination of all previous work
- ✅ **Write every section completely** - Do not summarize or abbreviate
- ✅ **Hit ALL minimum requirements** - 30+ pages, 10,000+ words, 25+ charts, 12+ tables
- ✅ **Be thorough on projection assumptions** - 2,000-3,000 words with product-by-product detail
- ✅ **Be comprehensive on scenarios** - 1,500-2,000 words with specific Bull/Base/Bear parameters
- ✅ **Insert ALL charts from Task 4** - Not just a few, ALL 25-35 charts throughout
- ✅ **Create ALL tables from Task 2/3** - Extract every financial table, don't skip any
- ✅ **Use Task 1 content verbatim** - Copy/paste full Company 101 sections (6-8K words)
- ✅ **Professional quality only** - This must be indistinguishable from JPMorgan/Goldman Sachs research

**NEVER:**
- ❌ "This section would include..." - WRITE THE ACTUAL SECTION
- ❌ "Charts would be inserted here..." - INSERT THE ACTUAL CHARTS
- ❌ "See financial model for details..." - EXTRACT AND INCLUDE THE DETAILS
- ❌ Skip sections due to length - Every section MUST be complete
- ❌ Abbreviate for token conservation - Use whatever tokens are needed

**This is publication-ready institutional research. Spare no effort, tokens, or detail.**

**Output**: A 股首次覆盖研究报告 (.docx)

**Specifications**:
- **页数**: 30-50 页 (MINIMUM 30)
- **字数**: 15,000-25,000 字 (MINIMUM 15,000，中文报告字数比英文报告多)
- **图表**: 25-35 张内嵌图表（中文标签）
- **表格**: 12-20 张完整表格（CAS 准则科目）
- **格式**: 专业 DOCX，含可点击超链接
- **字体**: 正文宋体 / 标题黑体 / 数字 Times New Roman
- **语言**: 中文为主，专业术语可中英对照

**报告结构（A 股卖方研报标准章节）**:
- **第 1 页 — 投资要点 / 评级页（首次覆盖标识）**
  - 公司名称（股票代码）+ 行业
  - 投资评级（买入 / 增持 / 中性 / 减持 / 卖出）
  - 目标价：¥XX.XX 元
  - 当前价 + 上行空间
  - 核心数据（总市值、流通市值、52 周高低、PE、PB、ROE、股息率）
- **第 2-5 页 — 投资逻辑 (Investment Thesis) 与 风险提示 (Risks)**
- **第 6-17 页 — 公司基本面 (Company Overview)**
  - 公司概况与发展沿革
  - 主营业务与产品
  - 股权结构与实际控制人
  - 管理层简历
- **第 18-25 页 — 行业分析 (Industry Analysis) / 所处行业**
  - 申万行业分类与行业空间
  - 行业景气度（PMI、库存周期、产能利用率）
  - 政策环境与监管
  - 竞争格局（A 股同业 + 海外对标）
  - 国产替代 / 出海机会
- **第 26-35 页 — 盈利预测 (Financial Forecast)**
  - 历史财务回顾（CAS 科目，3-5 年）
  - 收入与利润预测（5 年）
  - 三种情景（乐观 / 中性 / 悲观）
- **第 36-43 页 — 估值与目标价 (Valuation)**
  - 估值方法选择理由（按行业）
  - 主估值（PE / PB / PEG / DCF / 戈登）
  - 可比公司估值（申万同业 + 港股 / 美股同业）
  - 历史估值带（PE Band / PB Band）
  - 估值对比（football field）
- **第 44-48 页 — 股价催化因素 (Catalysts) 与 风险提示 (Risks)**
- **第 49-50 页 — 附录**

**章节标题映射（美股 → A 股）**:
- "Investment Thesis" → **投资逻辑**
- "Company Overview" → **公司概况** / **公司基本面**
- "Industry Analysis" → **行业分析** / **所处行业**
- "Financial Forecast" → **盈利预测**
- "Valuation" → **估值与目标价**
- "Risks" → **风险提示**
- "Catalysts" → **股价催化因素** / **催化剂**

**File name**: `[公司名]([代码])_首次覆盖报告_[年月].docx`（例：`贵州茅台(600519.SH)_首次覆盖报告_202605.docx`）

**⚠️ DELIVER ONLY THIS 1 DOCX FILE. NO executive summaries, no "highlights" documents, no extra files.**

**Final Verification**:
- [ ] 报告 30-50 页
- [ ] 字数 15,000-25,000 字
- [ ] 25-35 张图表已内嵌（中文标签）
- [ ] 12-20 张表格已包含（CAS 科目）
- [ ] 所有引用链接可点击（巨潮 / 交易所公告链接）
- [ ] 数字与财务模型完全一致
- [ ] 评级使用 A 股五档（买入 / 增持 / 中性 / 减持 / 卖出）
- [ ] 货币单位统一为人民币元 / 亿元 / 百万元
- [ ] 报告封面含合规声明（"本报告仅供参考，不构成投资建议"）

---

## Input Verification Protocol

### Why Input Verification Matters

Each task has strict prerequisites. Running a task without required inputs will:
- Waste time with incomplete work
- Produce low-quality outputs
- Require rework

**Always verify inputs before starting a task.**

### Verification Checklist by Task

**Task 1**: ✅ No verification needed (independent)

**Task 2**: Check historical financials available

**Task 3**: Check financial model exists and is accessible

**Task 4**: Check both model (Task 2) AND valuation (Task 3) exist

**Task 5**: Check ALL previous tasks complete (1, 2, 3, 4)

### What to Do if Verification Fails

```
IF prerequisites are missing:
1. Stop the current task
2. Identify which prerequisite task(s) need to be completed
3. Execute the missing task(s) first
4. Return to current task once prerequisites are met
```

### Example Verification Dialogue

```
User: "Use initiating-coverage, Task 5 for 贵州茅台 (600519.SH)"

Claude: "Starting Task 5: 报告组装 for 贵州茅台 (600519.SH)

VERIFICATION - Checking prerequisites:
- Task 1 (公司研究)... ❌ NOT FOUND
- Task 2 (财务模型)... ❌ NOT FOUND
- Task 3 (估值分析)... ❌ NOT FOUND
- Task 4 (图表)... ❌ NOT FOUND

⚠️ VERIFICATION FAILED

Task 5 requires ALL previous tasks to be complete.

To proceed:
1. Complete Task 1: 公司研究
2. Complete Task 2: 财务建模（CAS 准则）
3. Complete Task 3: 估值分析（PE/PB/PEG/DCF/戈登 — 按行业选择）
4. Complete Task 4: 图表生成
5. Then return to Task 5

Would you like to start with Task 1 first?"
```

---

## Task Reference Files

Detailed instructions for each task are in separate reference files to keep this skill lean:

- **references/task1-company-research.md** - Company research workflow
- **references/task2-financial-modeling.md** - Financial modeling workflow
- **references/task3-valuation.md** - Valuation methodology
  - Also see: references/valuation-methodologies.md for DCF/comps deep dive
- **references/task4-chart-generation.md** - Chart generation workflow
- **references/task5-report-assembly.md** - Report writing workflow
  - Also see: assets/report-template.md for report structure
  - Also see: assets/quality-checklist.md for quality checks

**When to load reference files**: Load ONLY the reference file associated with the specific task being performed. These files are very large - do not load multiple reference files at once. Read the appropriate task reference file at the start of the task for detailed step-by-step instructions.

---

## Quality Standards

All outputs meet 中国卖方研究机构的机构级标准（中信证券、中金公司、海通证券、招商证券、申万宏源、国泰君安、华泰证券）：

- **全面 (Comprehensive)**: 满足所有最低要求
- **详尽 (Detailed)**: 给出具体数据和案例，避免泛泛之谈
- **量化 (Quantified)**: 用数字和指标说话（CAS 科目，人民币亿元 / 百万元）
- **引用规范 (Cited)**: 数据来源标注完整（巨潮链接、交易所公告号、Wind/AKShare 数据接口）
- **专业 (Professional)**: 机构级排版（中文宋体 / 黑体，专业图表）
- **准确 (Accurate)**: 所有数字交叉核对（与最新年报 / 季报一致）

## A 股行业分析维度（必须覆盖）

对照美股 GICS，A 股行业分类使用 **申万行业分类**（一级 / 二级 / 三级），同时关注以下 A 股特色分析维度：

1. **政策敏感度**：A 股政策市特征明显，必须分析所在行业的政策环境
   - 行业新政（半导体大基金、新能源补贴、医保集采、双减、房住不炒）
   - 税收优惠到期（高新技术企业认定、研发加计扣除、增值税即征即退）
   - 国家战略对应（"十四五"规划、双碳目标、新质生产力）

2. **行业景气度**：通过领先指标判断
   - 制造业 PMI / 非制造业 PMI
   - 库存周期（被动去库 → 主动补库 → 被动补库 → 主动去库）
   - 产能利用率
   - 行业集中度 CR3 / CR5 / CR10

3. **国产替代进度**：重点关注半导体、医疗器械、工业软件、高端机床、精密仪器等领域

4. **出海占比**：消费电子、汽车、工程机械、家电、新能源、医药等行业的海外收入占比与出海空间

5. **国企改革 / 民营经济信号**（视公司性质）

## A 股专属风险类别（风险提示章节必须覆盖）

除常规经营风险（市场需求、原材料、汇率、技术更迭）外，A 股研报必须评估以下专属风险：

1. **商誉减值风险** — 商誉 / 净资产 > 30% 需重点提示
2. **大股东质押风险** — 控股股东质押率 > 50% 需重点提示
3. **限售股解禁压力** — 列出未来 12 个月解禁时点和解禁市值
4. **关联交易占比** — 关联销售 / 关联采购占比过高的独立性风险
5. **退市新规风险** — 财务造假退市、连续亏损退市（净利润 + 营收双指标）、市值低于 3 亿元、股价低于 1 元、信息披露重大违法
6. **政策风险** — 行业新政、税收优惠到期、监管政策收紧
7. **公司治理风险** — 实控人变更、董监高减持、审计意见非标（保留意见 / 无法表示意见 / 否定意见）
8. **应收账款 / 存货减值风险** — 应收账款周转天数显著恶化、存货跌价准备激增
9. **业绩承诺无法兑现风险** — 涉及并购对赌的需逐项评估

---

## Important Notes

### Task Independence

- **Task 1** can run anytime (no dependencies)
- **Task 2** can run anytime (just needs historical data)
- **Tasks 1 & 2** can run in parallel
- **Task 3** requires Task 2
- **Task 4** requires Tasks 2 & 3
- **Task 5** requires Tasks 1, 2, 3, & 4

### Session Management

**Same session**: Outputs automatically available to subsequent tasks

**Different sessions**: Reference previous task outputs explicitly
```
"Use Task 3 with the model from yesterday at [path]"
"Use Task 5 with the research document at [path]"
```

### File Organization

Recommended structure during workflow（以贵州茅台为例）:
```
贵州茅台(600519.SH)_首次覆盖/
├── Task1_公司研究/
│   └── 贵州茅台(600519.SH)_首次覆盖_202605.md
├── Task2_财务模型/
│   └── 贵州茅台(600519.SH)_财务模型_202605.xlsx
├── Task3_估值分析/
│   └── 贵州茅台(600519.SH)_估值分析_202605.md
├── Task4_图表/
│   ├── chart_01_股价走势.png
│   └── ... (25-35 files)
└── Task5_最终报告/
    └── 贵州茅台(600519.SH)_首次覆盖报告_202605.docx
```

### No End-to-End Execution

This skill does **NOT** support running all tasks automatically in sequence. Each task must be explicitly requested and verified.

**Why**: This ensures:
- Quality control at each stage
- Ability to review outputs before proceeding
- Flexibility to pause/resume workflow
- Clear verification of prerequisites

---

## Success Criteria

A successful initiation report workflow should:
1. Complete all 5 tasks in order
2. Pass all input verifications
3. Meet all quality standards
4. Produce all required deliverables
5. Numbers cross-check between outputs
6. Final report is publication-ready

**Output quality**: 机构级（中信证券 / 中金公司 / 海通证券 / 招商证券 / 申万宏源 / 国泰君安 / 华泰证券 level）
**Use case**: A 股上市公司首次覆盖综合研究报告
