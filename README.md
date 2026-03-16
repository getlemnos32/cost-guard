# 🛡️ Cost Guard — OpenClaw Skill

**Real-time API cost tracking, context bloat detection, and budget enforcement for OpenClaw agents.**

Built by [Lemnos AI](https://getlemnos.ai) — the AI operations company that deploys agents that handle admin work for $12K/year instead of an $80K hire.

---

## What It Does

Cost Guard gives your OpenClaw agent a financial brain. It watches every token, flags budget overruns before they happen, catches context bloat that quietly inflates your API bill, and routes tasks to cheaper models when appropriate.

**Without Cost Guard:** You find out you blew your budget after the bill arrives.  
**With Cost Guard:** Your agent warns you at 80%, stops non-revenue tasks at 100%, and tells you exactly which session or task is burning money.

### Features

- 📊 **Auto cost reporting** — reads directly from OpenClaw session JSONL files, no manual logging required
- 🚨 **Budget alerts** — warns at 80%, hard stops at 100%
- 🔍 **Context bloat detection** — flags sessions with high token ratios before they spiral
- 🧭 **Model routing rules** — built-in guidance to route simple tasks to Haiku ($0.80/M) instead of Sonnet ($3/M)
- 📋 **Per-task cost logging** — log cost by task type for granular reporting
- 📈 **Daily/weekly/monthly rollups** — full cost breakdown by date, model, and session

---

## Install

### Via ClawHub (recommended)
```bash
clawhub install lemnos-cost-guard
```
Find it at: **https://clawhub.com** → search "cost-guard"

### Manual
```bash
git clone https://github.com/getlemnos32/cost-guard.git
cp -r cost-guard/skills/lemnos-cost-guard ~/.openclaw/workspace/skills/
```

---

## Quick Start

### Daily cost check (run in morning briefing)
```bash
python3 skills/lemnos-cost-guard/scripts/auto_cost_report.py --budget 10.00 --format brief
```

**Example output:**
```
💰 COST (today 09:14 UTC): $3.42 / $10.00 (34%) ✅ OK
   47 calls | 1,243,800 in + 18,400 out + 892,100 cached
```

### Log a task's cost
```bash
python3 skills/lemnos-cost-guard/scripts/task_logger.py log "email_send" "Day 3 FU batch" --cost 0.18 --calls 6
```

### Check for context bloat
```bash
python3 skills/lemnos-cost-guard/scripts/context_analyzer.py --workspace /root/.openclaw/workspace
```

---

## Scripts Reference

| Script | What It Does |
|--------|-------------|
| `auto_cost_report.py` | Reads OpenClaw session files directly — no manual input needed. Supports `--days`, `--date`, `--budget`, `--format` |
| `cost_report.py` | Manual cost report from logged entries |
| `task_cost_report.py` | Cost breakdown by task type |
| `task_logger.py` | Log per-task costs to `task-log.jsonl` |
| `context_analyzer.py` | Scan workspace files for bloat signals |
| `track_cost.py` | Log a single cost entry manually |

---

## Budget Rules (Recommended Defaults)

```
Daily budget:    $10.00 (non-scrape days) / $15.00 (scrape days)
Warning at:      80% of daily budget
Hard stop at:    100% — pause all non-revenue tasks, notify user
Context alert:   I/O ratio > 50:1 on any single call
Single-call cap: > 500K input tokens = immediate alert
```

---

## Model Routing

| Task Type | Recommended Model | Cost |
|-----------|------------------|------|
| Format, classify, status check | Haiku | $0.80/M input |
| Research, drafting, analysis | Sonnet | $3.00/M input |
| Complex reasoning (rare) | Sonnet with thinking | ~$3.00/M input |
| Opus | Never, unless explicitly requested | $15/M input |

---

## Why We Built This

We run Max — an AI operations agent deployed for Lemnos AI's own business. Max runs 24/7 executing lead generation, email sequencing, campaign management, and reporting.

Early on, we had sessions run to $40–60/day with zero visibility. Cost Guard was built out of necessity. It's now standard on every Lemnos deployment.

**192+ downloads on ClawHub. Zero marketing.**

---

## About Lemnos AI

We deploy AI employees for businesses that are tired of paying $60–80K/year for admin roles.

- 🌐 [getlemnos.ai](https://getlemnos.ai)
- 📧 nick@getlemnos.ai
- 📞 917-275-7123

---

## License

MIT — use it, fork it, deploy it.

---

*Part of the Lemnos AI CRE Admin Automation Suite — coming to ClawHub Q3 2026.*
