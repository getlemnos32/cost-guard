# Changelog

All notable changes to Cost Guard will be documented in this file.
The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/).

---

## [v1.1.0] — 2026-03-14

### Added
- 🌐 Mandarin (中文) README and metadata for Chinese OpenClaw community
- 🚨 Configurable threshold alerts with soft/hard cap system
- 🛑 Auto-throttle: gracefully reduces agent activity at hard budget cap
- 📊 Weekly spend rollup report alongside daily summaries
- 🔗 ClawHub v1.1.0 published with updated keywords and description
- 📦 GitHub mirror live at github.com/getlemnos32/cost-guard

### Changed
- Improved cost calculation accuracy for streaming API responses
- Reduced alert latency from ~30s to <5s
- Updated config schema with `alert_threshold` and `hard_cap` options

### Fixed
- Edge case where token counts were double-counted on retried API calls
- Timezone handling in daily report generation for non-UTC agents

---

## [v1.0.0] — 2026-02-28

### Added
- 🔍 Real-time Anthropic API spend tracking per session, per day, per task
- 📊 Automated daily spend summary reports
- 📱 Telegram, Slack, and Discord notification channel support
- ⚙️ Zero-config deployment as OpenClaw skill
- 🧮 Per-model cost breakdown (Claude Opus, Sonnet, Haiku)
- 📄 MIT license
- 📖 Comprehensive README with architecture diagram

### Technical
- Built as native OpenClaw skill (SKILL.md + config.yaml)
- Token counting via Anthropic API response headers
- Local SQLite storage for spend history (no cloud dependency)
- Sub-1MB skill footprint

---

## [v0.1.0] — 2026-02-15 (Internal)

### Added
- Initial prototype: basic token counting for Anthropic API
- Daily cost logging to local file
- Manual threshold check (no auto-alerts)

### Notes
- Internal testing only at Lemnos AI
- Used to monitor our own production agent "Max" running on DigitalOcean
- Validated $0.48/day average spend on 24/7 autonomous operations

---

## Upcoming

### v2.0.0 (Planned — Q2 2026)
- Multi-provider support: DeepSeek, OpenAI, Qwen (Alibaba), Doubao (ByteDance)
- Universal cost monitoring for the entire OpenClaw ecosystem
- WeChat/Feishu alert channel integration for Chinese operators

### v2.1.0 (Planned — Q2 2026)
- Cost-per-task attribution with ROI tracking
- "Was this task worth the tokens?" analysis

### v3.0.0 (Planned — Q3 2026)
- Predictive spend forecasting
- Anomaly detection (catch hallucination loops before they drain budget)
- Multi-agent fleet monitoring for teams running 5+ agents

---

<p align="center">
  <strong>🦞 Built by <a href="https://getlemnos.ai">Lemnos AI</a></strong>
</p>
