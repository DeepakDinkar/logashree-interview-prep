# 9. OBSERVABILITY — CloudWatch ⭐ — Roadmap

> Resume: *"Implemented CloudWatch monitoring + alerting, reduced incident detection 50%; built dashboards, cut issue identification 40%."* Strong, quantified — own it.

```
OBSERVABILITY (AWS)
│
├── 1. THREE PILLARS
│   ├── Logs — what happened
│   ├── Metrics — numeric time-series
│   └── Traces — request path across services
│
├── 2. CLOUDWATCH LOGS ⭐
│   ├── Log Groups / Log Streams
│   ├── agent (CloudWatch Agent) on EC2
│   ├── container logs (ECS/EKS → awslogs / FireLens)
│   ├── Logs Insights (query language)
│   └── retention + export to S3
│
├── 3. CLOUDWATCH METRICS ⭐
│   ├── namespaces, dimensions
│   ├── built-in (CPU, memory, requests, latency)
│   ├── custom metrics (put-metric-data)
│   └── statistics (avg, p99, sum)
│
├── 4. ALARMS ⭐
│   ├── threshold + period + evaluation
│   ├── states — OK / ALARM / INSUFFICIENT_DATA
│   ├── actions → SNS → email/Slack/PagerDuty
│   ├── composite alarms
│   └── Auto Scaling trigger
│
├── 5. DASHBOARDS ⭐
│   ├── widgets (graphs, numbers, logs)
│   ├── per-service / per-env boards
│   └── single pane of glass
│
├── 6. EVENTS & AUTOMATION
│   ├── EventBridge rules
│   ├── auto-remediation (Lambda)
│   └── scheduled jobs
│
├── 7. AUDIT & TRACE
│   ├── CloudTrail — API audit (who did what)
│   ├── X-Ray — distributed tracing
│   └── VPC Flow Logs — network traffic
│
└── 8. SRE CONCEPTS
    ├── SLI / SLO / SLA, error budget
    ├── MTTR / MTBF
    ├── RED (Rate, Errors, Duration) / USE
    └── alert fatigue — alert on symptoms, not noise
```

## 🔑 CloudWatch Logs Insights (interview-handy)
```
fields @timestamp, @message
| filter @message like /ERROR/
| sort @timestamp desc
| limit 20
```

## 🏗️ Alarm → SNS flow (your resume story)
CPU > 80% for 5 min → **CloudWatch Alarm** → **SNS topic** → email/Slack → on-call responds (and/or Auto Scaling adds capacity). Detection time dropped because alarms catch it before users do.

## 🔑 Decision reflexes
| Question | Answer |
|----------|--------|
| Logs vs Metrics vs Traces | events / numbers-over-time / request journey |
| CloudWatch vs CloudTrail | performance/logs vs API audit (who/when) |
| How alarms notify | Alarm → SNS → subscribers |
| Reduce alert fatigue | alert on symptoms/SLO burn, use composite alarms |
| p50 vs p99 latency | median vs tail (worst-case users feel) |

## 🎯 Interview focus
- Explain your monitoring/alerting setup (logs→metrics→alarms→SNS→dashboard).
- SLI vs SLO vs SLA; error budget.
- How you reduced MTTR / detection time (your 50% / 40% numbers).
- How to debug a production incident with CloudWatch.
- Metrics that matter for an API (latency, error rate, throughput, saturation).

→ Definitions: [`../Definitions/09-Observability-definitions.md`](../Definitions/09-Observability-definitions.md)
