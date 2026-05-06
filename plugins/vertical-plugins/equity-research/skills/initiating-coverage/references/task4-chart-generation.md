# Task 4: Chart Generation - Detailed Workflow

This document provides step-by-step instructions for executing Task 4 (Chart Generation) of the initiating-coverage skill.

## Task Overview

**Purpose**: Generate 25-35 professional financial charts for the report.

**Prerequisites**: ⚠️ Verify before starting
- **Required**: Company research from Task 1
  - Company history, milestones (for timeline charts)
  - Management team, org structure (for org charts)
  - Product portfolio (for product charts)
  - Customer segmentation (for customer charts)
  - Competitive landscape (for competitive positioning charts)
  - TAM analysis (for market size charts)
- **Required**: Financial model from Task 2
  - Revenue by product/geography data
  - Margin trends
  - Scenario comparison data
- **Required**: Valuation analysis from Task 3
  - DCF sensitivity table
  - Comparable companies data
  - Valuation ranges
- **Required**: 外部市场数据
  - A 股历史股价数据（AKShare `stock_zh_a_hist` / Tushare `daily` / 雪球 / 同花顺，前复权）
  - 历史估值倍数（PE-Band / PB-Band，AKShare `stock_a_pe` / Wind / 同花顺 iFinD）
  - 行业指数对比基准：沪深 300、申万一级行业指数（如电子、食品饮料、电力设备）、创业板指、科创 50
  - **A 股专属图表数据：** 北向资金持仓变动（AKShare `stock_hsgt_*`）、机构调研频次、龙虎榜上榜历史、限售解禁日历、申万行业相对强弱

**⚠️ CRITICAL: DO NOT START THIS TASK UNLESS TASKS 1, 2, AND 3 ARE COMPLETE**

This task requires outputs from all three previous tasks. Starting without them will result in incomplete charts.

**IF ANY OF TASKS 1, 2, OR 3 ARE NOT COMPLETE**: Stop immediately and inform the user which tasks need to be completed first. The specific requirements are:
- Task 1: Company research document (for 9 charts)
- Task 2: Financial model with all 6 tabs (for 8 charts)
- Task 3: Valuation tabs added to the model (for 6 charts)
- External data access (for 2 charts)

Do not attempt to create placeholder charts or skip charts due to missing data.

**Output**: 25-35 Professional Chart Files (PNG/JPG, 300 DPI)

---

## Input Verification

**BEFORE STARTING - CHECK ALL PREREQUISITES:**

### Task 1 Verification (Company Research)
- [ ] Task 1 complete? (Company research document exists)
- [ ] Company history and milestones documented? (for charts 05, 06)
- [ ] Management team and org structure described? (for chart 07)
- [ ] Product portfolio detailed? (for chart 08)
- [ ] Customer segmentation analyzed? (for chart 09)
- [ ] Competitive landscape mapped? (for charts 16, 17, 18)
- [ ] TAM sizing completed? (for chart 15)

### Task 2 Verification (Financial Model)
- [ ] Task 2 complete? (Financial model Excel file exists)
- [ ] Revenue by product breakdown available? (for chart 03 ⭐)
- [ ] Revenue by geography breakdown available? (for chart 04 ⭐)
- [ ] Historical + projected financials complete? (for charts 02, 10, 11, 12)
- [ ] Scenario analysis (Bull/Base/Bear) complete? (for chart 14)
- [ ] Operating metrics available? (for chart 13)

### Task 3 Verification (Valuation)
- [ ] Task 3 complete? (Valuation tabs added to model)
- [ ] DCF sensitivity matrix exists? (for chart 28 ⭐)
- [ ] DCF calculation details available? (for chart 29)
- [ ] Comparable companies data collected? (for charts 30, 31)
- [ ] Valuation ranges calculated? (for chart 32 ⭐)

### External Data Verification
- [ ] 能否访问 A 股历史股价数据？（AKShare / Tushare / 雪球，用于 chart 01）
- [ ] 能否访问历史估值数据？（PE-Band / PB-Band，用于 chart 34）
- [ ] 能否访问北向资金 / 机构调研 / 龙虎榜 / 解禁日历数据？（A 股专属图表）

**IF ANY VERIFICATION FAILS**:
- Missing Task 1? → Complete Task 1 (公司研究) first
- Missing Task 2? → Complete Task 2 (财务建模) first
- Missing Task 3? → Complete Task 3 (估值分析) first
- Missing external data? → 从 AKShare / Tushare / Wind / 同花顺 iFinD / 雪球获取

---

## Chart Requirements: 25 Required + 10 Optional

**IMPORTANT**: Task 5 (Report Assembly) will embed **ALL charts created** throughout the report. The report requires dense visual content (1 chart every 200-300 words), so create comprehensive chart coverage.

### 4 MANDATORY Charts (Non-Negotiable) ⭐

These 4 charts are critical visualizations that MUST be present:

1. **chart_03**: Revenue by Product/Segment - Stacked Area Chart ⭐
2. **chart_04**: Revenue by Geography - Stacked Bar Chart ⭐
3. **chart_28**: DCF Sensitivity Analysis - 2-Way Heatmap ⭐
4. **chart_32**: Valuation Football Field - Horizontal Bar Chart ⭐

### 25 REQUIRED Charts (Complete Set)

Create all 25 of these charts. Each has a specific purpose in Task 5:

**Investment Summary Section (1 chart):**
- chart_01: Stock Price Performance (12-24 months)

**Financial Performance Section (6 charts):**
- chart_02: Revenue Growth Trajectory
- chart_03: Revenue by Product - Stacked Area ⭐ MANDATORY
- chart_04: Revenue by Geography - Stacked Bar ⭐ MANDATORY
- chart_10: Gross Margin Evolution
- chart_11: EBITDA Margin Progression
- chart_12: Free Cash Flow Trend

**Company 101 Section (7 charts):**
- chart_05: Company Overview/Timeline
- chart_06: Key Milestones Timeline
- chart_07: Organizational Structure
- chart_08: Product Portfolio Overview
- chart_09: Customer Segmentation
- chart_15: Market Size Evolution (TAM)
- chart_16: Competitive Positioning Matrix

**Competitive & Market Section (2 charts):**
- chart_17: Market Share Breakdown
- chart_18: Competitive Benchmarking

**Scenario Analysis Section (2 charts):**
- chart_13: Operating Metrics Dashboard
- chart_14: Scenario Comparison (Bull/Base/Bear)

**Valuation Section (7 charts):**
- chart_28: DCF Sensitivity Heatmap ⭐ MANDATORY
- chart_29: DCF Valuation Waterfall
- chart_30: Trading Comps Scatter Plot
- chart_31: Peer Multiples Comparison
- chart_32: Valuation Football Field ⭐ MANDATORY
- chart_33: Price Target Scenarios
- chart_34: Historical Valuation Multiples

**Total: 25 Required Charts**

### 10 OPTIONAL Charts (For 30-35 Range)

Add these for greater visual density and storytelling (reach 26-35 total)。**A 股研究建议优先采用 A 股专属图表替代部分通用图：**

- chart_19: 客户获取趋势 / 经销商数量变动
- chart_20: 单位经济（如白酒吨价、半导体单晶圆价）演变
- chart_21: 产品路线图 / 产品矩阵迭代
- chart_22: 地理扩张 / 渠道分布（A 股按"华东 / 华南 / 华北 / 海外"）
- chart_23: 研发投入趋势（含资本化率，A 股专属）
- chart_24: 销售费用率 / 管理费用率趋势
- chart_25: 营运资本（应收 / 存货周转天数）
- chart_26: 债务到期结构 / 短期借款 vs 长期借款
- chart_27: 股权结构 / 实控人持股 / 大股东质押率（A 股专属）
- chart_35: 卖方分析师目标价分布（A 股 Wind / 同花顺一致预期）

### A 股专属推荐图表（替代或补充上述可选图）

- **北向资金持仓变动图**：日 / 周 / 月度北向持股变化（AKShare `stock_hsgt_individual_em`），反映外资态度
- **申万行业相对强弱图**：标的 vs 申万一级 / 二级行业指数 vs 沪深 300，过去 12-24 个月
- **机构调研频次图**：月度调研机构数量（AKShare `stock_jgdy_detail`），反映机构关注度
- **龙虎榜上榜历史图**：上榜次数与游资 / 机构席位占比（A 股短线情绪指标）
- **限售解禁日历图**：未来 12 个月解禁数量与占总股本比（A 股流动性冲击指标）
- **PE-Band / PB-Band 历史估值带**：标的 vs 行业中位数（A 股研报常见图）
- **股息率历史走势图**：高分红蓝筹必备
- **机构持仓集中度图**：基金 / 社保 / QFII / 险资持股变动

**Total Range: 25-35 Charts (25 required + 0-10 optional + A 股专属图)**

---

## Data Source Mapping for Required Charts

Understanding where each chart's data comes from:

### From Task 1 (Company Research) - 9 charts
- chart_05: Company Overview → Task 1: Company Overview section
- chart_06: Key Milestones → Task 1: Company History section
- chart_07: Org Structure → Task 1: Management Team section
- chart_08: Product Portfolio → Task 1: Products & Services section
- chart_09: Customer Segmentation → Task 1: Customers & Go-to-Market section
- chart_15: Market Size Evolution → Task 1: Market Opportunity (TAM) section
- chart_16: Competitive Positioning → Task 1: Competitive Landscape section
- chart_17: Market Share → Task 1: Competitive Landscape section
- chart_18: Competitive Benchmarking → Task 1: Competitive Landscape section

### From Task 2 (Financial Model) - 8 charts
- chart_02: Revenue Growth → Income Statement tab (Revenue row)
- chart_03: Revenue by Product ⭐ → Revenue Model tab (Product breakdown)
- chart_04: Revenue by Geography ⭐ → Revenue Model tab (Geography breakdown)
- chart_10: Gross Margin → Income Statement tab (Gross Profit / Revenue)
- chart_11: EBITDA Margin → Income Statement tab (EBITDA / Revenue)
- chart_12: Free Cash Flow → Cash Flow Statement tab (CFO - CapEx)
- chart_13: Operating Metrics → Multiple tabs (Income Statement, Cash Flow)
- chart_14: Scenario Comparison → Scenarios tab (Bull/Base/Bear)

### From Task 3 (Valuation) - 6 charts
- chart_28: DCF Sensitivity ⭐ → Sensitivity Analysis tab
- chart_29: DCF Waterfall → DCF tab (Enterprise Value components)
- chart_30: Trading Comps Scatter → Comparable Companies tab
- chart_31: Peer Multiples → Comparable Companies tab
- chart_32: Valuation Football Field ⭐ → Valuation Summary tab
- chart_33: Price Target Scenarios → Valuation Summary tab (or calculate from scenarios)

### From External Sources - 2 charts
- chart_01: 股价表现 → AKShare `stock_zh_a_hist`（前复权）/ Tushare `daily` / 雪球 / 同花顺，对比沪深 300 / 申万行业指数
- chart_34: 历史估值倍数（PE-Band / PB-Band）→ AKShare `stock_a_pe` / Wind / 同花顺 iFinD（历史 PE / PB / PEG）

**IMPORTANT**: Require ALL three tasks (1, 2, 3) complete PLUS external data access to create all 25 required charts.

---

## Step-by-Step Chart Generation Workflow

### Step 1: Set Up Environment

**Install required libraries:**
```bash
pip install matplotlib seaborn pandas numpy plotly akshare tushare
# matplotlib 中文字体支持：需配置 'SimHei' 或 'Microsoft YaHei' / 'PingFang SC'
```

**中文字体配置（A 股图表中文标签必备）：**
```python
import matplotlib.pyplot as plt
plt.rcParams['font.sans-serif'] = ['PingFang SC', 'Microsoft YaHei', 'SimHei']
plt.rcParams['axes.unicode_minus'] = False  # 避免负号显示为方块
```

**Create Python script header:**
```python
import matplotlib.pyplot as plt
import seaborn as sns
import pandas as pd
import numpy as np
from matplotlib.patches import Rectangle
import warnings
warnings.filterwarnings('ignore')

# Set global style
plt.style.use('seaborn-v0_8-darkgrid')
sns.set_palette("husl")

# Global settings
DPI = 300
FIGURE_WIDTH = 10
FIGURE_HEIGHT = 6
TITLE_FONT_SIZE = 14
AXIS_FONT_SIZE = 12
LABEL_FONT_SIZE = 10
```

### Step 2: Extract Data from Model and Valuation

#### A. Extract Revenue Data
```python
# Revenue by Product (from Task 2 model)
years = [2020, 2021, 2022, 2023, 2024, 2025, 2026, 2027, 2028, 2029]

# Extract from Excel or define manually from model
product_a = [100, 120, 145, 175, 210, 252, 302, 363, 435, 522]
product_b = [80, 95, 115, 138, 165, 198, 238, 285, 342, 411]
product_c = [50, 62, 78, 98, 122, 153, 191, 239, 299, 374]
product_d = [30, 38, 48, 61, 77, 97, 122, 153, 191, 239]

# 按地区营收（A 股年报披露口径，单位：百万元）
huadong = [150, 180, 220, 265, 320, 384, 461, 553, 664, 797]   # 华东
huanan = [80, 95, 115, 140, 170, 204, 245, 294, 353, 423]      # 华南
huabei = [40, 50, 63, 80, 101, 127, 159, 199, 249, 311]        # 华北
overseas = [20, 25, 32, 40, 51, 64, 80, 100, 125, 156]         # 境外
```

#### B. Extract Margin Data
```python
# Margin evolution
gross_margin = [58.0, 59.2, 60.5, 61.8, 63.0, 64.5, 66.0, 67.0, 67.5, 68.0]
ebitda_margin = [12.0, 15.5, 18.8, 22.0, 25.0, 28.0, 30.5, 32.0, 33.0, 34.0]
fcf_margin = [8.0, 11.0, 14.5, 18.0, 21.0, 24.0, 26.5, 28.0, 29.0, 30.0]
```

#### C. Extract DCF Sensitivity Data
```python
# DCF Sensitivity (from Task 3 valuation)
wacc_values = [7.0, 8.0, 9.0, 10.0, 11.0, 12.0]
terminal_growth = [1.5, 2.0, 2.5, 3.0, 3.5]

# Price per share matrix (rows = WACC, columns = terminal growth)
dcf_sensitivity = np.array([
    [66, 71, 76, 82, 89],
    [58, 62, 67, 72, 78],
    [52, 55, 59, 63, 68],
    [47, 50, 53, 56, 60],
    [42, 45, 48, 51, 54],
    [39, 41, 44, 46, 49]
])
```

#### D. Extract Valuation Ranges
```python
# 估值橄榄球图（来自 Task 3，A 股以 PE 为主）
valuation_methods = ['PE 可比公司法\n（主估值）', 'DCF\n（永续增长）', 'PB 可比公司法', 'A 股并购重组对标']
valuation_low = [147, 54, 130, 150]    # 单位：元 / 股
valuation_high = [166, 70, 160, 175]
current_price = 100  # 元
target_price = 127   # 元
```

### Step 3: Create Mandatory Charts

#### Chart 1: Revenue by Product - Stacked Area ⭐ MANDATORY

```python
def create_revenue_by_product_chart():
    """Create revenue by product stacked area chart"""

    fig, ax = plt.subplots(figsize=(10, 6))

    # Create stacked area chart
    ax.stackplot(years, product_a, product_b, product_c, product_d,
                 labels=['产品 A', '产品 B', '产品 C', '产品 D'],
                 colors=['#1f77b4', '#ff7f0e', '#2ca02c', '#d62728'],
                 alpha=0.8)

    # Formatting
    ax.set_xlabel('年度', fontsize=12, fontweight='bold')
    ax.set_ylabel('营业收入（百万元）', fontsize=12, fontweight='bold')
    ax.set_title('图 3 - 按产品 / 业务分部营收（2020-2029E）',
                 fontsize=14, fontweight='bold', pad=20)

    # Legend
    ax.legend(loc='upper left', frameon=False, fontsize=10)

    # Grid
    ax.grid(axis='y', alpha=0.3, linestyle='--')
    ax.set_axisbelow(True)

    # Remove top and right spines
    ax.spines['top'].set_visible(False)
    ax.spines['right'].set_visible(False)

    # Add vertical line to separate historical from projected
    ax.axvline(x=2024, color='gray', linestyle='--', linewidth=1, alpha=0.5)
    ax.text(2024.2, ax.get_ylim()[1]*0.95, '预测期 →',
            fontsize=9, color='gray', ha='left')

    # Source line
    fig.text(0.12, 0.02, '数据来源：公司年报（巨潮资讯网）、AKShare、[研究机构] 测算',
             fontsize=9, style='italic', color='gray')

    # Save
    plt.tight_layout()
    plt.savefig('chart_03_revenue_by_product_stacked_area.png',
                dpi=300, bbox_inches='tight', facecolor='white')
    plt.close()
    print("✓ Created: chart_03_revenue_by_product_stacked_area.png")

create_revenue_by_product_chart()
```

#### Chart 2: Revenue by Geography - Stacked Bar ⭐ MANDATORY

```python
def create_revenue_by_geography_chart():
    """Create revenue by geography stacked bar chart"""

    years_labels = ['2020', '2021', '2022', '2023', '2024',
                    '2025E', '2026E', '2027E', '2028E', '2029E']

    fig, ax = plt.subplots(figsize=(10, 6))

    # Create stacked bar chart
    width = 0.6
    x = np.arange(len(years_labels))

    p1 = ax.bar(x, huadong, width, label='华东', color='#1f77b4')
    p2 = ax.bar(x, huanan, width, bottom=huadong,
                label='华南', color='#ff7f0e')
    p3 = ax.bar(x, huabei, width,
                bottom=np.array(huadong) + np.array(huanan),
                label='华北', color='#2ca02c')
    p4 = ax.bar(x, overseas, width,
                bottom=np.array(huadong) + np.array(huanan) + np.array(huabei),
                label='境外', color='#d62728')

    # Formatting
    ax.set_xlabel('年度', fontsize=12, fontweight='bold')
    ax.set_ylabel('营业收入（百万元）', fontsize=12, fontweight='bold')
    ax.set_title('图 4 - 按地区营收（2020-2029E，年报披露口径）',
                 fontsize=14, fontweight='bold', pad=20)
    ax.set_xticks(x)
    ax.set_xticklabels(years_labels, rotation=45, ha='right')

    # Legend
    ax.legend(loc='upper left', frameon=False, fontsize=10)

    # Grid
    ax.grid(axis='y', alpha=0.3, linestyle='--')
    ax.set_axisbelow(True)

    # Remove top and right spines
    ax.spines['top'].set_visible(False)
    ax.spines['right'].set_visible(False)

    # Source line
    fig.text(0.12, 0.02, '数据来源：公司年报（巨潮资讯网）、AKShare、[研究机构] 测算',
             fontsize=9, style='italic', color='gray')

    # Save
    plt.tight_layout()
    plt.savefig('chart_04_revenue_by_geography_stacked_bar.png',
                dpi=300, bbox_inches='tight', facecolor='white')
    plt.close()
    print("✓ Created: chart_04_revenue_by_geography_stacked_bar.png")

create_revenue_by_geography_chart()
```

#### Chart 3: DCF Sensitivity - Heatmap ⭐ MANDATORY

```python
def create_dcf_sensitivity_heatmap():
    """Create DCF sensitivity analysis heatmap"""

    # Create DataFrame
    df = pd.DataFrame(dcf_sensitivity,
                      index=[f'{w}%' for w in wacc_values],
                      columns=[f'{g}%' for g in terminal_growth])

    fig, ax = plt.subplots(figsize=(8, 6))

    # Create heatmap
    sns.heatmap(df, annot=True, fmt='d', cmap='RdYlGn',
                cbar_kws={'label': '每股价值（元）'},
                linewidths=0.5, linecolor='white',
                ax=ax, vmin=35, vmax=95)

    # Formatting
    ax.set_xlabel('永续增长率 g', fontsize=12, fontweight='bold')
    ax.set_ylabel('WACC（A 股区间 7-11%）', fontsize=12, fontweight='bold')
    ax.set_title('图 28 - DCF 敏感性分析（元 / 股）',
                 fontsize=14, fontweight='bold', pad=20)

    # Rotate y-axis labels
    plt.yticks(rotation=0)

    # Source line
    fig.text(0.12, 0.02, '数据来源：[研究机构] 测算',
             fontsize=9, style='italic', color='gray')

    # Save
    plt.tight_layout()
    plt.savefig('chart_28_dcf_sensitivity_heatmap.png',
                dpi=300, bbox_inches='tight', facecolor='white')
    plt.close()
    print("✓ Created: chart_28_dcf_sensitivity_heatmap.png")

create_dcf_sensitivity_heatmap()
```

#### Chart 4: Valuation Football Field ⭐ MANDATORY

```python
def create_valuation_football_field():
    """Create valuation football field chart"""

    fig, ax = plt.subplots(figsize=(10, 5))

    # Create horizontal bars
    y_positions = np.arange(len(valuation_methods))
    colors = ['#1f77b4', '#ff7f0e', '#2ca02c']

    colors = ['#1f77b4', '#ff7f0e', '#2ca02c', '#d62728']  # 4 种估值方法

    for i, (method, low, high, color) in enumerate(
            zip(valuation_methods, valuation_low, valuation_high, colors)):
        ax.barh(i, high - low, left=low, height=0.6,
                color=color, alpha=0.7, label=method)

        # Add value labels at ends
        ax.text(low - 1, i, f'¥{low}', va='center', ha='right', fontsize=10)
        ax.text(high + 1, i, f'¥{high}', va='center', ha='left', fontsize=10)

    # Add current price line
    ax.axvline(x=current_price, color='red', linestyle='--', linewidth=2,
               label=f'当前股价：¥{current_price}', alpha=0.7)

    # Add target price line
    ax.axvline(x=target_price, color='black', linestyle='-', linewidth=2,
               label=f'目标价：¥{target_price}')

    # Formatting
    ax.set_yticks(y_positions)
    ax.set_yticklabels(valuation_methods, fontsize=11)
    ax.set_xlabel('每股价值（元）', fontsize=12, fontweight='bold')
    ax.set_title('图 32 - 估值橄榄球图',
                 fontsize=14, fontweight='bold', pad=20)

    # Set x-axis limits
    ax.set_xlim(40, 200)

    # Remove spines
    ax.spines['top'].set_visible(False)
    ax.spines['right'].set_visible(False)
    ax.spines['left'].set_visible(False)

    # Grid
    ax.grid(axis='x', alpha=0.3, linestyle='--')
    ax.set_axisbelow(True)

    # Legend
    ax.legend(loc='upper right', frameon=False, fontsize=9)

    # Source line
    fig.text(0.12, 0.02, '数据来源：AKShare / Wind 一致预期、申万行业可比公司、[研究机构] 测算',
             fontsize=9, style='italic', color='gray')

    # Save
    plt.tight_layout()
    plt.savefig('chart_32_valuation_football_field.png',
                dpi=300, bbox_inches='tight', facecolor='white')
    plt.close()
    print("✓ Created: chart_32_valuation_football_field.png")

create_valuation_football_field()
```

### Step 4: Create Remaining Required Charts (Charts 1-34)

**Complete the 25 REQUIRED charts** by creating all remaining charts from the required list. Each chart has a specific purpose in Task 5.

#### Investment Summary (1 chart)
```python
# chart_01: A 股股价表现（12-24 个月，前复权）
# - 折线图：标的股价 vs 沪深 300 vs 申万行业指数（如食品饮料 / 电子 / 电力设备）
# - 数据源：AKShare `stock_zh_a_hist` / Tushare `daily`
# - 用于报告封面页
```

#### Financial Performance (5 additional charts beyond chart_03 and chart_04)
```python
# chart_02: Revenue Growth Trajectory
# chart_10: Gross Margin Evolution
# chart_11: EBITDA Margin Progression
# chart_12: Free Cash Flow Trend
# chart_14: Scenario Comparison (Bull/Base/Bear)
```

#### Company 101 Section (7 charts)
```python
# chart_05: Company Overview/Timeline
# chart_06: Key Milestones Timeline
# chart_07: Organizational Structure
# chart_08: Product Portfolio Overview
# chart_09: Customer Segmentation
# chart_15: Market Size Evolution (TAM)
# chart_16: Competitive Positioning Matrix
```

#### Competitive & Market (2 charts)
```python
# chart_17: Market Share Breakdown
# chart_18: Competitive Benchmarking
```

#### Scenario Analysis (1 chart)
```python
# chart_13: Operating Metrics Dashboard
```

#### Valuation Section (6 additional charts beyond chart_28 and chart_32)
```python
# chart_29: DCF Valuation Waterfall
# chart_30: Trading Comps Scatter Plot
# chart_31: Peer Multiples Comparison
# chart_33: Price Target Scenarios
# chart_34: Historical Valuation Multiples
```

**Use consistent formatting across all charts:**
- 300 DPI resolution
- Professional color scheme
- Clear labels, legends, and titles
- Figure numbers (e.g., "Figure 5 - Company Timeline")
- Source citations at bottom

### Step 4B: Create Optional Charts (For 26-35 Total)

**Optional**: Add 1-10 additional charts from this list for greater visual density:

```python
# chart_19: Customer Acquisition Trends
# chart_20: Unit Economics Evolution
# chart_21: Product Roadmap Timeline
# chart_22: Geographic Expansion Map
# chart_23: R&D Investment Trends
# chart_24: Sales & Marketing Efficiency
# chart_25: Working Capital Trends
# chart_26: Debt Maturity Schedule
# chart_27: Ownership Structure
# chart_35: Analyst Price Target Distribution
```

These optional charts provide additional visual storytelling and help achieve the "1 chart per 200-300 words" density target in Task 5.

### Step 5: Create Chart Index

Create a text file documenting all charts:

```python
def create_chart_index():
    """Create index of all charts"""

    # 25 REQUIRED CHARTS
    required_charts = [
        "chart_01_stock_price_performance.png - Stock Price Performance (12-24M)",
        "chart_02_revenue_growth_trajectory.png - Revenue Growth Trajectory",
        "chart_03_revenue_by_product_stacked_area.png - Revenue by Product [MANDATORY]",
        "chart_04_revenue_by_geography_stacked_bar.png - Revenue by Geography [MANDATORY]",
        "chart_05_company_overview.png - Company Overview/Timeline",
        "chart_06_key_milestones_timeline.png - Key Milestones Timeline",
        "chart_07_organizational_structure.png - Organizational Structure",
        "chart_08_product_portfolio.png - Product Portfolio Overview",
        "chart_09_customer_segmentation.png - Customer Segmentation",
        "chart_10_gross_margin_evolution.png - Gross Margin Evolution",
        "chart_11_ebitda_margin_progression.png - EBITDA Margin Progression",
        "chart_12_free_cash_flow_trend.png - Free Cash Flow Trend",
        "chart_13_operating_metrics_dashboard.png - Operating Metrics Dashboard",
        "chart_14_scenario_comparison.png - Scenario Comparison (Bull/Base/Bear)",
        "chart_15_market_size_evolution.png - Market Size Evolution (TAM)",
        "chart_16_competitive_positioning.png - Competitive Positioning Matrix",
        "chart_17_market_share.png - Market Share Breakdown",
        "chart_18_competitive_benchmarking.png - Competitive Benchmarking",
        "chart_28_dcf_sensitivity_heatmap.png - DCF Sensitivity Heatmap [MANDATORY]",
        "chart_29_dcf_waterfall.png - DCF Valuation Waterfall",
        "chart_30_trading_comps_scatter.png - Trading Comps Scatter Plot",
        "chart_31_peer_multiples_comparison.png - Peer Multiples Comparison",
        "chart_32_valuation_football_field.png - Valuation Football Field [MANDATORY]",
        "chart_33_price_target_scenarios.png - Price Target Scenarios",
        "chart_34_historical_valuation_multiples.png - Historical Valuation Multiples",
    ]

    # 10 OPTIONAL CHARTS (for 26-35 range)
    optional_charts = [
        "chart_19_customer_acquisition_trends.png - Customer Acquisition Trends [OPTIONAL]",
        "chart_20_unit_economics_evolution.png - Unit Economics Evolution [OPTIONAL]",
        "chart_21_product_roadmap_timeline.png - Product Roadmap Timeline [OPTIONAL]",
        "chart_22_geographic_expansion_map.png - Geographic Expansion Map [OPTIONAL]",
        "chart_23_rd_investment_trends.png - R&D Investment Trends [OPTIONAL]",
        "chart_24_sales_marketing_efficiency.png - Sales & Marketing Efficiency [OPTIONAL]",
        "chart_25_working_capital_trends.png - Working Capital Trends [OPTIONAL]",
        "chart_26_debt_maturity_schedule.png - Debt Maturity Schedule [OPTIONAL]",
        "chart_27_ownership_structure.png - Ownership Structure [OPTIONAL]",
        "chart_35_analyst_price_targets.png - Analyst Price Target Distribution [OPTIONAL]",
    ]

    with open('chart_index.txt', 'w') as f:
        f.write("CHART INDEX FOR [COMPANY] EQUITY RESEARCH REPORT\n")
        f.write("=" * 60 + "\n\n")

        f.write("4 MANDATORY CHARTS (Must be present):\n")
        f.write("- chart_03: Revenue by Product (Stacked Area) ⭐\n")
        f.write("- chart_04: Revenue by Geography (Stacked Bar) ⭐\n")
        f.write("- chart_28: DCF Sensitivity (Heatmap) ⭐\n")
        f.write("- chart_32: Valuation Football Field ⭐\n\n")

        f.write("25 REQUIRED CHARTS:\n")
        for chart in required_charts:
            f.write(f"  {chart}\n")

        f.write("\n10 OPTIONAL CHARTS (for 26-35 total):\n")
        for chart in optional_charts:
            f.write(f"  {chart}\n")

        f.write("\n" + "=" * 60 + "\n")
        f.write("NOTE: Task 5 will embed ALL charts created (25-35) throughout\n")
        f.write("the report for visual density (1 chart every 200-300 words).\n")

    print("✓ Created: chart_index.txt")

create_chart_index()
```

### Step 6: Quality Check

**Run verification checks:**

```python
import os

def verify_charts():
    """Verify all charts were created successfully"""

    mandatory_charts = [
        'chart_03_revenue_by_product_stacked_area.png',
        'chart_04_revenue_by_geography_stacked_bar.png',
        'chart_28_dcf_sensitivity_heatmap.png',
        'chart_32_valuation_football_field.png'
    ]

    print("\n" + "="*60)
    print("CHART GENERATION VERIFICATION")
    print("="*60)

    # Check mandatory charts
    print("\n1. MANDATORY CHARTS:")
    all_mandatory_present = True
    for chart in mandatory_charts:
        if os.path.exists(chart):
            size = os.path.getsize(chart) / 1024  # KB
            print(f"   ✓ {chart} ({size:.1f} KB)")
        else:
            print(f"   ✗ MISSING: {chart}")
            all_mandatory_present = False

    # Count total charts
    chart_files = [f for f in os.listdir('.') if f.startswith('chart_') and f.endswith('.png')]
    print(f"\n2. TOTAL CHARTS: {len(chart_files)}")
    print(f"   Target: 25-35 charts")
    print(f"   Status: {'✓ PASS' if 25 <= len(chart_files) <= 35 else '⚠ WARNING'}")

    # Check file sizes (should be > 50KB for 300 DPI)
    print("\n3. FILE SIZE CHECK:")
    small_files = []
    for chart in chart_files[:5]:  # Sample first 5
        size = os.path.getsize(chart) / 1024
        if size < 50:
            small_files.append(chart)
        print(f"   {chart}: {size:.1f} KB")

    if small_files:
        print(f"   ⚠ WARNING: {len(small_files)} files may be low resolution")
    else:
        print(f"   ✓ All sampled files have adequate size")

    # Final verdict
    print("\n" + "="*60)
    if all_mandatory_present and 25 <= len(chart_files) <= 35:
        print("✓ VERIFICATION PASSED - Ready for Task 5")
    else:
        print("✗ VERIFICATION FAILED - Review missing charts")
    print("="*60 + "\n")

verify_charts()
```

---

## Quality Standards

### Visual Quality
- [ ] High resolution (300 DPI minimum)
- [ ] Professional color scheme (consistent across all charts)
- [ ] Clear, legible text (no fonts smaller than 9pt)
- [ ] Proper aspect ratio (no distortion)
- [ ] No pixelation or artifacts

### Data Accuracy
- [ ] Data matches source (financial model and valuation)
- [ ] Proper units and labels ($ millions, percentages, etc.)
- [ ] Appropriate scale and range
- [ ] Consistent time periods across charts
- [ ] Verified calculations

### Formatting Quality
- [ ] Consistent styling across all charts
- [ ] Proper figure numbering (sequential)
- [ ] Clear titles and captions
- [ ] Source citations on every chart
- [ ] Professional appearance

### Completeness
- [ ] All 4 mandatory charts created
- [ ] 25-35 total charts
- [ ] Proper file naming (chart_01, chart_02, etc.)
- [ ] Chart index created
- [ ] Ready for embedding in Word

---

## Chart Types Reference

### When to Use Each Chart Type

**Line Charts**: Time series trends (revenue, margins, stock price)

**Stacked Area**: Revenue by product ⭐, market size composition

**Stacked Bar**: Revenue by geography ⭐, quarterly breakdowns

**Heatmap**: DCF sensitivity ⭐, correlation matrices

**Horizontal Bar**: Valuation football field ⭐, peer rankings

**Waterfall**: Revenue bridges, margin analysis, DCF build-up

**Scatter/Bubble**: Growth vs. valuation, competitive positioning

**2×2 Matrix**: Competitive positioning, product portfolio

---

## File Naming Convention

**Always use this format:**
```
chart_[NUMBER]_[DESCRIPTION].png

Examples:
chart_01_stock_price_performance.png
chart_03_revenue_by_product_stacked_area.png
chart_28_dcf_sensitivity_heatmap.png
```

**Number charts sequentially** based on their position in the report, not creation order.

---

## Common Chart Generation Issues

### Issue 1: Low Resolution
**Problem**: Chart looks pixelated
**Solution**: Ensure `dpi=300` in `plt.savefig()`

### Issue 2: Text Cutoff
**Problem**: Labels or titles cut off at edges
**Solution**: Use `bbox_inches='tight'` in `plt.savefig()`

### Issue 3: Poor Colors
**Problem**: Colors don't look professional
**Solution**: Use established palettes like Tableau10 or define custom corporate colors

### Issue 4: Overlapping Labels
**Problem**: Axis labels overlap
**Solution**: Rotate labels (e.g., `rotation=45`) or reduce font size

### Issue 5: White Space
**Problem**: Too much white space around chart
**Solution**: Use `plt.tight_layout()` before saving

---

## Success Criteria

A successful chart package should:
1. **Include all 4 mandatory charts** (verified) ⭐
   - chart_03: Revenue by Product
   - chart_04: Revenue by Geography
   - chart_28: DCF Sensitivity
   - chart_32: Valuation Football Field
2. **Create 25 required charts minimum** (verified)
3. **Optional: 1-10 additional charts** for 26-35 total
4. Have consistent professional styling across all charts
5. Be high resolution (300 DPI) for print quality
6. Have clear labels, legends, and titles on every chart
7. Include proper figure numbers and source citations
8. Be ready for immediate embedding in Word
9. Cover all key financial metrics and analyses
10. Tell a visual story complementing the written analysis
11. Be accurate and auditable to source data (model/valuation)
12. All charts packaged in zip file with chart index

**Remember**: Task 5 will embed ALL charts created (25-35) throughout the report for visual density.

---

## Output Files

After completing Task 4, deliverables include:

**25 REQUIRED Chart Files (Minimum):**
1. chart_01_stock_price_performance.png
2. chart_02_revenue_growth_trajectory.png
3. chart_03_revenue_by_product_stacked_area.png ⭐ MANDATORY
4. chart_04_revenue_by_geography_stacked_bar.png ⭐ MANDATORY
5. chart_05_company_overview.png
6. chart_06_key_milestones_timeline.png
7. chart_07_organizational_structure.png
8. chart_08_product_portfolio.png
9. chart_09_customer_segmentation.png
10. chart_10_gross_margin_evolution.png
11. chart_11_ebitda_margin_progression.png
12. chart_12_free_cash_flow_trend.png
13. chart_13_operating_metrics_dashboard.png
14. chart_14_scenario_comparison.png
15. chart_15_market_size_evolution.png
16. chart_16_competitive_positioning.png
17. chart_17_market_share.png
18. chart_18_competitive_benchmarking.png
19-27. *Reserved for optional charts if created*
28. chart_28_dcf_sensitivity_heatmap.png ⭐ MANDATORY
29. chart_29_dcf_waterfall.png
30. chart_30_trading_comps_scatter.png
31. chart_31_peer_multiples_comparison.png
32. chart_32_valuation_football_field.png ⭐ MANDATORY
33. chart_33_price_target_scenarios.png
34. chart_34_historical_valuation_multiples.png
35. *Reserved for optional chart if created*

**10 OPTIONAL Chart Files (For 26-35 Total):**
- chart_19 through chart_27, chart_35 (if created)

**Chart Index** (1 text file):
- chart_index.txt (listing all charts with descriptions and categories)

**All chart files must be:**
- 300 DPI resolution (print quality)
- 6-10 inches wide (standard Word embedding size)
- White background (professional appearance)
- PNG format (lossless quality)
- Ready for immediate Word embedding

**Final Step: Package All Charts**

Create a zip file containing all chart files and the chart index:

```
[Company]_Charts_[Date].zip
├── chart_01_stock_price_performance.png
├── chart_02_revenue_growth_trajectory.png
├── chart_03_revenue_by_product_stacked_area.png ⭐
├── chart_04_revenue_by_geography_stacked_bar.png ⭐
├── chart_05_company_overview.png
├── ... (all 25-35 chart files)
├── chart_28_dcf_sensitivity_heatmap.png ⭐
├── chart_32_valuation_football_field.png ⭐
├── chart_34_historical_valuation_multiples.png
└── chart_index.txt
```

**Example**: `贵州茅台_600519.SH_Charts_2026-05-06.zip` 或 `宁德时代_300750.SZ_Charts_2026-05-06.zip`

**Why this matters**: Task 5 will embed ALL charts created (25-35) throughout the report. The report requires visual density (1 chart per 200-300 words), so all charts serve a purpose—either for specific analytical sections or for visual storytelling and page density.
- Verify all 25-35 charts are present
- Extract charts for Task 5 (Report Assembly)

---

## Next Steps

After completing Task 4, the zip file will be used for:
- **Task 5 (Report Assembly)**: Extract charts and embed all into the final DOCX report at appropriate locations throughout the document

The 4 mandatory charts are critical for the valuation and financial analysis sections of the report.
