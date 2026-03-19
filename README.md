# Lemnos Cost Guard | Lemnos 成本卫士

Real-time API cost monitoring and budget enforcement for OpenClaw agents.
OpenClaw 智能体实时 API 成本监控与预算执行工具。

Built by [Lemnos AI](https://getlemnos.ai) — operations experts first, AI developers second.
由 [Lemnos AI](https://getlemnos.ai) 开发——运营专家优先，AI 开发者其次。

## Features | 功能

- auto_cost_report.py — Daily spend summary from session files | 每日支出摘要
- task_cost_report.py — Per-task cost breakdown (briefing, email, research) | 按任务类型分解成本
- task_logger.py — Logs every task with cost, API calls, token count | 记录成本、调用次数、token 数量
- Budget enforcement — Warning at 80%, hard stop at limit | 80% 预警，达到上限硬停止
- Zero config — Reads OpenClaw session files directly | 零配置，直接读取会话文件

## Quick Start | 快速开始

Install via ClawHub:

```
openclaw install lemnos-cost-guard
```

Or clone:

```
git clone https://github.com/getlemnos32/cost-guard.git
```

Configure your budget:

```json
{
  "daily_budget": 10.00,
  "warning_threshold": 0.8,
  "currency": "USD"
}
```

Run:

```
python auto_cost_report.py
python task_cost_report.py
```

## Why Cost Guard? | 为什么需要 Cost Guard？

Running an autonomous agent 24/7 without cost controls is dangerous. One bloated session can consume 9M+ tokens and blow your budget in hours. Cost Guard is battle-tested at Lemnos AI where our agent runs daily on a $10/day budget.

全天候运行自主智能体而没有成本控制非常危险。一个膨胀的会话可以消耗 900 万+ token，几小时内耗尽预算。Cost Guard 已在 Lemnos AI 生产环境中验证，我们的智能体每天以 10 美元预算运行。

## Use Cases | 使用场景

- One-Person Companies (一人公司) — Control costs while your agent runs your business | 智能体运营业务时控制成本
- Freelancers — Know what each AI task costs | 了解每个任务的成本
- Agency deployments — Monitor spend across client agents | 监控客户智能体支出
- Dev and testing — Catch runaway costs before production | 上线前捕获失控成本

## Links | 链接

- Web: https://getlemnos.ai
- Email: nick@getlemnos.ai
- ClawHub: lemnos-cost-guard

MIT License
