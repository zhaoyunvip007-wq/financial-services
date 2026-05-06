# A 股研究 Agent

> Fork 自 [anthropics/financial-services](https://github.com/anthropics/financial-services)，本地化为 A 股研究专用 Agent 套件。
> 维护人：赵一舟（zhaoyunvip007-wq）| 启动日期：2026-05-06

## 与原版的区别

| 维度 | Anthropic 原版 | A 股版本 |
|---|---|---|
| **数据源** | 11 个海外 MCP（Daloopa / Morningstar / FactSet / S&P 等） | AKShare MCP + Tushare MCP（A 股核心数据） |
| **会计准则** | GAAP / IFRS | CAS（中国会计准则）|
| **行业分类** | GICS | 申万一/二/三级 |
| **货币单位** | USD millions | 人民币亿元 / 百万元 |
| **估值惯例** | EV/EBITDA + DCF 优先 | PE / PB / PEG 优先，DCF 长期 |
| **风险维度** | 美股标准（10-K Item 1A） | A 股专属（商誉减值 / 大股东质押 / 限售解禁 / 关联交易 / 退市新规 / 政策风险） |
| **报告格式** | 卖方研报美股标准 | 中文卖方研报标准（中信 / 中金 / 海通 / 招商） |
| **评级体系** | Buy / Hold / Sell | 买入 / 增持 / 中性 / 减持 / 卖出（五档） |

## 新增 A 股专属 Skill

原版未覆盖、A 股特色的工作流：

| Skill | 命令 | 功能 |
|---|---|---|
| `dragon-tiger-list` | `/dragon-tiger` | 龙虎榜：机构 / 游资席位拆解、资金流向 |
| `north-bound-flow` | `/north-bound` | 北向资金：净流入、行业偏好、个股增减仓 |
| `sw-industry-comp` | `/sw-industry` | 申万行业成分股横向对比（多维度排序）|
| `restricted-stock-unlock` | `/unlock-calendar` | 限售股解禁日历 + 压力测试 |
| `block-trade` | `/block-trade` | 大宗交易：折溢价 / 机构接盘判断 |
| `china-macro` | `/macro` | PMI/CPI/PPI/社融/LPR + 板块影响 |

## 安装

### 前置依赖

```bash
# 安装 uvx（如未安装）
curl -LsSf https://astral.sh/uv/install.sh | sh

# 可选：申请 Tushare Pro Token（200 元/年）
# 注册：https://tushare.pro/register
# 设置环境变量
export TUSHARE_TOKEN="你的 token"
```

### 在 Claude Code 中安装本 plugin（本地路径方式）

```bash
# 方式 A：本地路径直接安装（推荐开发阶段）
claude plugin install ~/projects/a-share-research-agent/plugins/vertical-plugins/financial-analysis
claude plugin install ~/projects/a-share-research-agent/plugins/vertical-plugins/equity-research

# 方式 B：从 GitHub fork 安装（推送后可用）
claude plugin marketplace add zhaoyunvip007-wq/financial-services
claude plugin install financial-analysis-ashare@financial-services
claude plugin install equity-research-ashare@financial-services
```

### 验证安装

启动 Claude Code，输入：
```
/sw-industry 白酒
```

应触发 `sw-industry-comp` skill，输出申万白酒行业对比。

## 改造的核心 skill 清单

### financial-analysis（核心建模）
- `comps-analysis`：可比公司分析（GICS → 申万；EV/EBITDA → PE/PB；加 A 股专属红旗）
- `dcf-model`：DCF 估值（10Y UST → 10Y 国债；ERP 5-7%；CapEx 等假设按 A 股行业惯例）
- 其他建模 skill（lbo-model, 3-statement-model, audit-xls 等）：方法论通用，未改造，可直接用

### equity-research（卖方研究流程）
- `earnings-analysis`：财报点评（10-Q → 季报；SEC → 巨潮；GAAP → CAS；加扣非归母 / 合同负债等中文科目）
- `initiating-coverage`：首次覆盖报告（22 处改造，加 A 股估值方法对照表 / A 股专属风险章节 / 五档评级）
- `idea-generation`：选股筛选（重写为 A 股，加北向 / 龙虎榜 / 解禁等 A 股信号）
- `model-update`：模型更新（CAS 科目、扣非归母、A 股估值惯例）

## 待补 / 后续计划

### Phase 2（短期）
- [ ] 补 `initiating-coverage` 的 references/ 子文档（task1-5 详情）
- [ ] 端到端测试：用茅台 / 招行 / 宁德时代跑全流程
- [ ] 推送到 GitHub fork

### Phase 3（中期）
- [ ] 写雪球 MCP（用户账号 9107316608 + cookie 鉴权）
- [ ] 写巨潮公告 MCP（公告原文检索 + 解读）
- [ ] 改造 wealth-management 为中国财富管理（公募 / 私募 / 信托 / 银行理财）

### Phase 4（长期）
- [ ] 写东方财富资金流向 MCP
- [ ] 加港股通 / 美股 ADR 联动分析
- [ ] 加 A 股商业架构师工具包（私募研究 SOP、IC memo 中文模板）

## 数据源说明

### 必装（基础数据）
- **AKShare**：免费、覆盖全面（行情 / 财报 / 北向 / 龙虎榜 / 申万 / 宏观）
- **Tushare Pro**：财务数据更稳定（200 元/年订阅）

### 推荐补充（按需）
- **巨潮资讯网**（cninfo.com.cn）：公告原文（公开 API）
- **东方财富 Choice**：研报库 / 一致预期（订阅）
- **Wind / 同花顺 iFinD**：机构级（年费数万，团队场景）

### 用户账号资源
- 雪球账号 9107316608：未来雪球 MCP 使用 cookie 鉴权
- 关注 250+ 大 V，可作为雪球 MCP 数据池

## 双轨视角

本套工具同时服务两个场景：

**个人投资视角**：把研究 A 股的"找数据 → 整理 → 出研报模板"流程从 2 小时压到 10 分钟，沉淀 9 年正收益的研究方法论到系统中

**商业架构师视角**：可发展为面向私募 / 卖方分析师 / 买方研究员的 A 股研究 Agent 模板。Wind 终端 7 万/年、iFinD 4 万/年，本套工具的"开源版 + 订阅版"组合在 3000-1 万/年订阅价位有市场空间

## 风险声明

本仓库不构成投资 / 法律 / 税务建议。Agent 输出为研究草稿，需要合格专业人员复核。任何投资决策、交易执行、风险承担、合规判断均由用户负责。
