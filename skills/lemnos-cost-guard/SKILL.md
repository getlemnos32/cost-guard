---
name: lemnos-cost-guard
description: "Real-time API cost tracking, context bloat detection, and budget enforcement for OpenClaw agents. Use when setting up cost guardrails, checking daily spend, logging token usage after a task, analyzing context bloat, generating cost reports (daily/weekly/monthly), getting model routing recommendations, or when a user asks about API costs, budget status, or why costs are high."
---

# Lemnos Cost Guard

**Zero-config API cost tracking for OpenClaw agents. Reads your session files directly — no manual logging required.**

Built by [Lemnos AI](https://getlemnos.ai) — the AI operations company.  
GitHub: [getlemnos32/cost-guard](https://github.com/getlemnos32/cost-guard)

---

## Scripts

| Script | Purpose |
|--------|---------|
| `scripts/auto_cost_report.py` | **Zero-config** — reads OpenClaw session JSONL files directly. No setup. |
| `scripts/task_logger.py` | Log cost by task type for granular attribution |
| `scripts/task_cost_report.py` | Breakdown by task type |
| `scripts/cost_report.py` | Report from manually logged entries |
| `scripts/context_analyzer.py` | Scan workspace for context bloat |
| `scripts/track_cost.py` | Log a single cost entry manually |

Model pricing and routing rules: `references/model_pricing.md`

---

## Quickstart (30 seconds)

```bash
# Daily cost check — no setup required
python3 skills/lemnos-cost-guard/scripts/auto_cost_report.py --budget 10.00 --format brief
```

Output:
```
💰 COST (today 09:14 UTC): $3.42 / $10.00 (34%) ✅ OK
   47 calls | 1,243,800 in + 18,400 out + 892,100 cached
```

---

## Daily Workflow

### Morning Briefing — Cost Section
Run both reports before sending briefing:

```bash
# Auto report (reads sessions directly)
python3 skills/lemnos-cost-guard/scripts/auto_cost_report.py --budget 10.00 --format brief

# Task-level breakdown
python3 skills/lemnos-cost-guard/scripts/task_cost_report.py --format brief
```

Include output verbatim. Flag anything over 80% of budget.

### Log Per-Task Costs
```bash
python3 skills/lemnos-cost-guard/scripts/task_logger.py log "briefing" "Daily briefing 2026-03-16" --cost 2.14 --calls 38
```

Logs to: `task-log.jsonl` (readable by `task_cost_report.py`)

### Context Bloat Check (weekly or when costs spike)
```bash
python3 skills/lemnos-cost-guard/scripts/context_analyzer.py --workspace /root/.openclaw/workspace
```

---

## Budget Rules

| Threshold | Action |
|-----------|--------|
| ≥80% of daily budget | Warn user, flag in briefing |
| ≥100% of daily budget | Hard stop all non-revenue tasks. Notify immediately. |
| Single call >500K input tokens | Immediate alert — context bloat risk |
| I/O ratio >50:1 on any call | Context bloat warning — recommend compaction |

**Recommended budgets:**
- Scrape days (Mon/Wed/Fri): $15/day
- Standard days: $10/day

---

## Context Loading Rules

Load ONLY what the current task requires. Never load all files by default.

| Task | Load |
|------|------|
| Morning briefing | SOUL.md, USER.md, MEMORY.md, HEARTBEAT.md, today's memory |
| Email outreach | MEMORY.md (relevant section), sent-log.md |
| Research task | Reference files for that vertical only |
| Heartbeat (nothing to do) | HEARTBEAT.md only |

---

## Model Routing

See `references/model_pricing.md` for full pricing table.

| Task Type | Model | Cost |
|-----------|-------|------|
| Format, classify, status check | Haiku | $0.80/M input |
| Research, drafting, analysis | Sonnet | $3.00/M input |
| Complex reasoning | Sonnet + thinking | ~$3.00/M input |
| Opus | Never (unless explicitly requested) | $15/M input |

---

## Auto Report: How It Works

`auto_cost_report.py` reads OpenClaw's native session JSONL files at:
```
/root/.openclaw/agents/main/sessions/*.jsonl
```

Each API call writes `message.usage.cost.total` to the session file automatically. This script aggregates by date, model, and session — no manual tracking needed.

```bash
# Today's cost
python3 auto_cost_report.py --budget 10.00

# Specific date
python3 auto_cost_report.py --date 2026-03-15 --budget 10.00

# Last 7 days, full breakdown
python3 auto_cost_report.py --days 7 --budget 70.00 --format full
```

---

## Cost Log Format (manual entries)

```json
{
  "ts": "2026-03-16T14:00:00Z",
  "task": "email_send",
  "model": "claude-sonnet-4-6",
  "input_tokens": 45000,
  "output_tokens": 1200,
  "ratio": 37.5,
  "cost_usd": 0.153,
  "notes": "Day 7 breakup batch — 7 emails"
}
```

---

## ⭐ If This Saves You Money
Star it on ClawHub — it helps others find it.

192+ downloads. Built for production. Zero marketing.

---

*By [Lemnos AI](https://getlemnos.ai) — we deploy AI employees that cut admin overhead by 85%.*  
*GitHub: [getlemnos32/cost-guard](https://github.com/getlemnos32/cost-guard)*
