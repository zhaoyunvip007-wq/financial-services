# A 股研究 Agent（Fork from Anthropic Financial Services）

> 本仓库 fork 自 anthropics/financial-services，已本地化为 A 股研究专用 Agent 套件。
> 详见 README-ASHARE.md。原 README.md 保留作为美股版参考。

## 当前分支

工作分支：`ashare-localization`（默认 main 保持与上游同步，A 股改造在此分支）

## 开发纪律（本项目内）

### 必跑的验证步骤（改 plugin 后）

光跑 `scripts/check.py` lint 不够，必须按以下顺序验证：

1. **Lint**：`python3 scripts/check.py` — 验证文件引用合规
2. **Sync**：`python3 scripts/sync-agent-skills.py` — 把 vertical-plugins/ 的改动传播到 agent-plugins/ bundles
3. **MCP 启动**：`uvx <mcp-name> --help` — 验证 MCP 依赖能装能起
4. **Plugin Install（必做）**：
   ```bash
   claude plugin marketplace update claude-for-financial-services
   claude plugin uninstall <name>@claude-for-financial-services
   claude plugin install <name>@claude-for-financial-services
   claude plugin list | grep <name>   # 看 Status: enabled
   ```
   不能只看安装成功消息，必须看 list 状态。`Status: ✘ failed to load` 才是失败的真信号
5. **Slash 命令实测**：在新 Claude Code session 跑一个 slash 命令看是否触发 skill

### 已知陷阱

- `hooks/hooks.json` 上游用 `[]`，但 Claude Code 加载器要求 `{"hooks": {}}`（object）。新增 plugin 时手动检查，否则 enabled 失败
- `scripts/check.py` 不验证 hooks.json schema，只验证 manifest 引用
- subagent 改子目录时容易漏改 references/，主 SKILL.md 改完后要确认子文档同步

### 工具使用纪律

- **Edit 工具要求 Read 工具读过的文件**：用 `cat`/`grep` 在 Bash 里看文件不算。批量改文件时，先 Read 再 Edit/Write，否则全部失败但报错可能被忽略
- **TaskUpdate completed 必须有真实证据**：不能基于"我以为 Edit 成功了"标记完成。每个改造文件后要 grep 验证关键词消失，或者读改后的几行看效果
- **真实失败信号**：lint 通过 ≠ 改造成功。lint 不验证内容含义，只验证语法 / 引用。语义层面的改造（如 CapIQ → AKShare）必须用 grep 关键词验证

## 关键改造文件清单

### 已改造的 skill（核心 6 个）
- `plugins/vertical-plugins/financial-analysis/skills/comps-analysis/SKILL.md` — 申万行业 + A 股估值范围 + 专属红旗
- `plugins/vertical-plugins/financial-analysis/skills/dcf-model/SKILL.md` — 中国 10Y 国债 + ERP + CAS 税率
- `plugins/vertical-plugins/equity-research/skills/earnings-analysis/SKILL.md` — CAS 科目 + 巨潮 + 披露窗口
- `plugins/vertical-plugins/equity-research/skills/initiating-coverage/SKILL.md` — 22 处改造（subagent 完成，质量自评 85 分）
- `plugins/vertical-plugins/equity-research/skills/idea-generation/SKILL.md` — A 股选股逻辑全重写
- `plugins/vertical-plugins/equity-research/skills/model-update/SKILL.md` — A 股财报科目全重写

### 新增 A 股专属 skill（6 个）
- `plugins/vertical-plugins/equity-research/skills/dragon-tiger-list/` — 龙虎榜
- `plugins/vertical-plugins/equity-research/skills/north-bound-flow/` — 北向资金
- `plugins/vertical-plugins/equity-research/skills/sw-industry-comp/` — 申万行业对比
- `plugins/vertical-plugins/equity-research/skills/restricted-stock-unlock/` — 限售解禁
- `plugins/vertical-plugins/equity-research/skills/block-trade/` — 大宗交易
- `plugins/vertical-plugins/equity-research/skills/china-macro/` — 中国宏观

### MCP 配置
- `plugins/vertical-plugins/financial-analysis/.mcp.json` — 替换 11 个海外 MCP 为 AKShare + Tushare

## 原版结构（参考）

# Financial Services Plugins

Cowork plugins and Claude Managed Agent templates for financial services. Each named agent ships two ways from one source.

## Repository Structure

```
├── plugins/
│   ├── agent-plugins/               #   named agents — one self-contained plugin each
│   │   └── <slug>/
│   │       ├── .claude-plugin/plugin.json
│   │       ├── agents/<slug>.md     #   ← canonical system prompt (one source, two wrappers)
│   │       └── skills/              #   ← bundled copies, synced from vertical-plugins/
│   ├── vertical-plugins/            #   FSI verticals — skill sources, commands, MCPs
│   │   └── <vertical>/
│   │       ├── .claude-plugin/plugin.json
│   │       ├── commands/
│   │       ├── skills/
│   │       └── .mcp.json
│   └── partner-built/               #   partner plugins (LSEG, S&P Global)
├── managed-agent-cookbooks/         # CMA cookbooks (one dir per named agent)
│   └── <slug>/
│       ├── agent.yaml               #   system + skills → ../../plugins/agent-plugins/<slug>/...
│       ├── subagents/*.yaml         #   depth-1 leaf workers
│       ├── steering-examples.json
│       └── README.md                #   security tier + handoff notes
├── claude-for-msft-365-install/     # admin tooling for the Microsoft 365 add-in (separate from FSI plugins)
└── scripts/                         # deploy-managed-agent.sh, check.py, validate.py, orchestrate.py, sync-agent-skills.py
```

Run `python3 scripts/check.py` before committing — it lints every manifest, verifies all `system.file` / `skills.path` / `callable_agents.manifest` references resolve, and fails if any `agent-plugins/<slug>/skills/` copy has drifted from its `vertical-plugins/` source. **Edit skills in `vertical-plugins/`**, then run `python3 scripts/sync-agent-skills.py` to propagate into the agent bundles.

## Key Files

- `marketplace.json`: Marketplace manifest - registers all plugins with source paths
- `plugin.json`: Plugin metadata - name, description, version, and component discovery settings
- `commands/*.md`: Slash commands invoked as `/plugin:command-name`
- `skills/*/SKILL.md`: Detailed knowledge and workflows for specific tasks
- `*.local.md`: User-specific configuration (gitignored)
- `mcp-categories.json`: Canonical MCP category definitions shared across plugins

## Development Workflow

1. Edit markdown files directly - changes take effect immediately
2. Test commands with `/plugin:command-name` syntax
3. Skills are invoked automatically when their trigger conditions match
