<p align="center"> <img src="https://img.shields.io/badge/🦞_TRACTION-253_Deployments_and_Counting-ff4d4d?style=for-the-badge&labelColor=0a0a0f" alt="Traction Badge"/> <img src="https://img.shields.io/badge/ClawHub-v1.1.0-00e68a?style=for-the-badge&labelColor=0a0a0f" alt="ClawHub Version"/> <img src="https://img.shields.io/badge/License-MIT-4d9fff?style=for-the-badge&labelColor=0a0a0f" alt="License"/> <img src="https://img.shields.io/badge/Lang-EN_|_中文-ffd700?style=for-the-badge&labelColor=0a0a0f" alt="Languages"/> </p>

# 🦞 Cost Guard

The autonomous cost monitoring skill for OpenClaw agents. Cost Guard watches your AI agent's API spend in real-time, catches runaway costs before they hit your wallet, and delivers daily spend reports — all without human intervention.

Built by [Lemnos AI](https://getlemnos.ai), the operations-first AI company.

---

## Why Cost Guard Exists

Every OpenClaw operator has the same nightmare: you deploy an agent, go to sleep, and wake up to a $200 API bill from a single hallucination loop. Cost Guard kills that problem.

It runs silently alongside your agent, monitors token consumption across providers, and triggers alerts + automatic throttling when spend exceeds your thresholds. No dashboards to check. No spreadsheets to update. It just works.

---

## Traction

| Metric | Value |
|--------|-------|
| Organic Downloads | 253 in first 14 days |
| Active Deployments | Growing daily across US, EU, and Asia |
| ClawHub Rating | Published v1.1.0 |
| GitHub | Open source, MIT licensed |
| Languages | English + 中文 (Mandarin) |

> *"If DeepSeek marked a milestone for open-source LLMs, then OpenClaw represents a similar turning point for open-source agents."* — Counterpoint Research

---

## Features

🔍 Real-Time Spend Tracking — Monitors Anthropic API costs per session, per day, and per task. No manual logging.

🚨 Threshold Alerts — Set daily/weekly/monthly spend caps. Get notified via your agent's messaging channel (Telegram, Slack, Discord) the moment you approach a limit.

🛑 Auto-Throttle — When spend hits your hard cap, Cost Guard gracefully throttles agent activity instead of letting it burn cash on repeat failures.

📊 Daily Spend Reports — Automatic end-of-day summaries: total spend, cost per task, model breakdown, anomaly flags.

🌐 Multi-Provider Ready — Architected for Anthropic today, extensible to DeepSeek, OpenAI, and domestic Chinese LLM providers (Qwen, Doubao, Kimi) in v2.

📱 Zero-Config Deployment — Install as an OpenClaw skill. No API keys to configure beyond what your agent already uses. Running in under 60 seconds.

---

## Quick Start

```bash
# Install via ClawHub (recommended)
openclaw skill install cost-guard

# Or clone from GitHub
git clone https://github.com/getlemnos32/cost-guard.git
cd cost-guard
```

### Configuration

Edit `config.yaml` in the skill directory:

```yaml
# Cost Guard Configuration
monitoring:
  provider: anthropic        # Primary provider to monitor
  daily_budget: 15.00        # Daily spend cap in USD
  alert_threshold: 0.80      # Alert at 80% of budget
  hard_cap: true             # Auto-throttle at 100%

alerts:
  channel: telegram          # telegram | slack | discord
  frequency: realtime        # realtime | hourly | daily

reporting:
  daily_summary: true        # End-of-day spend report
  weekly_rollup: true        # Weekly trend analysis
  cost_per_task: true        # Per-task cost attribution
```

### Verify Installation

```bash
openclaw skill status cost-guard
# Output: ✅ Cost Guard v1.1.0 — Monitoring active — $0.00 today
```

---

## How It Works

```
┌─────────────────────────────────────────────────┐
│                YOUR OPENCLAW AGENT               │
│                                                  │
│  Task Request ──► LLM API Call ──► Response      │
│                                                  │
│                        │                         │
│                        │                         │
└────────────────────────┼────────────────────────┘
                         │
              ┌──────────▼──────────┐
              │                     │
              │      COST GUARD     │
              │                     │
              │  • Token counter    │
              │  • Spend calculator │
              │  • Threshold check  │
              │  • Alert dispatcher │
              │  • Report generator │
              └──────────┬──────────┘
                         │
              ┌──────────▼──────────┐
              │   IF over budget:   │
              │   → Alert owner     │
              │   → Throttle agent  │
              │   → Log anomaly     │
              └─────────────────────┘
```

---

## Real-World Performance

We run Cost Guard on our own production agents at [Lemnos AI](https://getlemnos.ai). Here's what it looks like in practice:

- Daily agent budget: $15.00
- Actual daily spend: $0.48 average (97% under budget)
- Alerts triggered: 0 hard-cap events in 30+ days
- Cost per lead generated: < $0.03
- Agent uptime: 24/7, autonomous, zero human monitoring

Cost Guard isn't a concept — it's running in production, protecting real revenue-generating agents, every day.

---

## About Lemnos AI

Operators first. AI developers second.

Lemnos AI builds autonomous agents that replace $80K/year administrative overhead for $12K/year. We specialize in property management, real estate operations, and B2B workflow automation on the OpenClaw stack.

Cost Guard is our first open-source skill — a proof point that AI operations tooling should be free, reliable, and built by people who actually run agents in production.

🌐 [getlemnos.ai](https://getlemnos.ai) · 🦞 [ClawHub](https://clawhub.com/lemnos/cost-guard) · 𝕏 [@GetLemnosAI](https://x.com/GetLemnosAI) · [LinkedIn](https://linkedin.com/company/lemnos-ai)

---

## Roadmap

- [x] v1.0 — Anthropic API spend tracking + daily reports
- [x] v1.1 — Threshold alerts + auto-throttle + Mandarin README
- [ ] v2.0 — Multi-provider support (DeepSeek, OpenAI, Qwen, Doubao)
- [ ] v2.1 — Cost-per-task attribution with ROI tracking
- [ ] v2.2 — Team/multi-agent fleet monitoring dashboard
- [ ] v3.0 — Predictive spend forecasting with anomaly detection

---

## Contributing

We welcome contributions. If you're running OpenClaw agents in production and want to help make Cost Guard better, open an issue or submit a PR.

Priority areas:
- Multi-provider API adapters (DeepSeek, OpenAI, etc.)
- Additional messaging channel integrations
- Internationalization (language packs beyond EN/中文)

---

## 中文说明

Cost Guard 是一个用于 OpenClaw 代理的自主成本监控技能。它可以实时跟踪 AI 代理的 API 支出，在成本失控之前捕获问题，并自动生成每日支出报告。由 [Lemnos AI](https://getlemnos.ai) 构建 — 运营优先的 AI 公司。

安装:
```bash
openclaw skill install cost-guard
```

详细中文文档请参阅 [README_ZH.md](./README_ZH.md)

---

## License

MIT License. Use it, fork it, build on it. Just don't let your agents burn cash. 🦞

---

<p align="center">
  <strong>Built with 🦞 by <a href="https://getlemnos.ai">Lemnos AI</a></strong><br>
  <em>253 operators trust Cost Guard to protect their AI agents.</em>
</p>
