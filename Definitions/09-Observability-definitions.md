# 📖 Observability & CloudWatch — Definitions & Examples ⭐

> Roadmap: [`../Roadmap/09-Observability-CloudWatch.md`](../Roadmap/09-Observability-CloudWatch.md)

### 📚 Reference docs
- [Amazon CloudWatch docs](https://docs.aws.amazon.com/cloudwatch/) · [Logs Insights query syntax](https://docs.aws.amazon.com/AmazonCloudWatch/latest/logs/CWL_QuerySyntax.html)
- [CloudWatch Alarms](https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/AlarmThatSendsEmail.html) · [CloudTrail](https://docs.aws.amazon.com/cloudtrail/) · [AWS X-Ray](https://docs.aws.amazon.com/xray/)
- [Google SRE Book (free)](https://sre.google/books/) · [SRE Workbook](https://sre.google/workbook/table-of-contents/)
- [Golden Signals](https://sre.google/sre-book/monitoring-distributed-systems/) · [RED method](https://grafana.com/blog/2018/08/02/the-red-method-how-to-instrument-your-services/) · [USE method](https://www.brendangregg.com/usemethod.html)
- [OpenTelemetry](https://opentelemetry.io/docs/) · [Prometheus](https://prometheus.io/docs/) · [Grafana](https://grafana.com/docs/)

---

## Three pillars 🔥
- **Logs** — discrete events (what happened, with detail).
- **Metrics** — numeric time-series (CPU %, request count, latency).
- **Traces** — a request's path across services (find the slow hop).
**Monitoring vs Observability** — monitoring = watch known dashboards/alarms; observability = ability to ask *new* questions about unknown problems from your telemetry.

## CloudWatch 🔥🔥
**CloudWatch Logs** — Log **Groups** (per app) → Log **Streams** (per source). Collected via CloudWatch Agent (EC2) or `awslogs`/FireLens (ECS/EKS). Query with **Logs Insights**.
```
fields @timestamp, @message | filter @message like /ERROR/ | sort @timestamp desc | limit 20
```
**CloudWatch Metrics** — namespaces + dimensions; built-in (CPU, NetworkIn, RequestCount, Latency) + custom (`put-metric-data`). Statistics: avg, sum, p99.
**CloudWatch Alarm** 🔥 — watches a metric vs threshold over periods; states **OK / ALARM / INSUFFICIENT_DATA**; action → **SNS** (email/Slack/PagerDuty) or Auto Scaling.
**Dashboard** — widgets = single pane of glass per service/env.
**Composite alarm** — combine alarms to cut noise.

**CloudWatch vs CloudTrail** 🔥 — CloudWatch = performance/logs/metrics; **CloudTrail** = API audit (who called what, when). **X-Ray** = distributed tracing. **VPC Flow Logs** = network traffic.

## Alarm → SNS flow (your resume story) 🔥
`CPU > 80% for 5 min → CloudWatch Alarm → SNS topic → email/Slack → on-call` (and Auto Scaling adds capacity). This is how you cut detection time ~50%.

## SRE concepts 🔥
- **SLI** — a measured indicator (e.g. % successful requests).
- **SLO** — your internal target (e.g. 99.9% success).
- **SLA** — contractual promise to customers (with penalties); looser than SLO.
- **Error budget** — allowed failure = `1 − SLO`; spend it on releases, freeze when exhausted.
- **MTTR** — mean time to recover. **MTBF** — mean time between failures.
- **RED** (Rate, Errors, Duration) for services; **USE** (Utilization, Saturation, Errors) for resources.
- **p50 vs p99** — median vs tail latency (p99 = what your unhappiest users feel).
- **Alert fatigue** — too many noisy alerts; alert on **symptoms/SLO burn**, not every blip.

## Golden signals (Google SRE) — Latency, Traffic, Errors, Saturation.

---

## 🎯 Likely interview Qs
- Logs vs metrics vs traces. Monitoring vs observability.
- Explain your CloudWatch setup (logs→metrics→alarms→SNS→dashboard).
- CloudWatch vs CloudTrail.
- SLI vs SLO vs SLA; what is an error budget?
- How did you reduce MTTR / detection time?
- Which metrics matter for an API? (latency p99, error rate, throughput, saturation)
- How do you avoid alert fatigue?
