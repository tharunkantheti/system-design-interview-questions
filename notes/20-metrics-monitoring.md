# 20 · Metrics Monitoring and Alerting

**Difficulty:** 🟡 Medium &nbsp;|&nbsp; **Topics:** time-series DB · alerting

> [!TIP]
> **30-second answer**
> - Collectors (pull or push) → Kafka → time-series DB with compression and downsampling.
> - Query service powers dashboards and an alert manager that dedupes and routes alerts.

<details><summary><b>Contents</b></summary>

- [Requirements](#requirements)
- [Data model](#data-model)
- [Design](#design)
- [Pull vs push](#pull-vs-push)
- [Storage](#storage)
- [Alerting](#alerting)
- [Common mistakes](#common-mistakes)
- [Practice questions](#practice-questions)

</details>

Collect infrastructure and app metrics (CPU, latency, error rates), visualize them, and alert on problems.

## Requirements

- 100M DAU-scale company; ~1,000 server pools × 100 machines × ~100 metrics → **~10M metrics**.
- Retention: raw for 7 days, 1-minute rollups for 30 days, 1-hour rollups for a year.
- Alerts via email, phone, PagerDuty, webhooks.
- Write-heavy; reads are bursty (dashboards, alert queries).

## Data model

A **time series** = metric name + labels/tags + a list of (timestamp, value).

```
http_requests_total{host="web-12", region="us-east", status="500"}  1700000000  42
```

**Cardinality** (unique label combinations) is the thing that explodes; avoid user IDs as labels.

## Design

```mermaid
flowchart LR
    SRC[Servers, apps, DBs] --> COL[Metrics collectors: pull or push agents]
    COL --> K[[Kafka]]
    K --> CON[Consumers / stream processors]
    CON --> TSDB[(Time-series DB)]
    TSDB --> QS[Query service + cache]
    QS --> VIS[Dashboards]
    QS --> AL[Alerting service]
    AL --> CH[Email, SMS, PagerDuty, webhooks]
```

## Pull vs push

| Pull (Prometheus-style) | Push (agent-based) |
|---|---|
| Collector scrapes `/metrics` endpoints found via service discovery | Agents on each host send metrics to collectors |
| Easy to tell if a target is down | Works behind firewalls and for short-lived jobs |
| Needs network reachability | Collector must handle bursts; aggregation can happen on the agent |

Both are fine; say which and why.

## Storage

- Use a purpose-built **TSDB** (InfluxDB, Prometheus TSDB, M3, etc.) over a general DB.
- **Delta-of-delta** and XOR-style compression shrink timestamps and values dramatically.
- **Downsampling** jobs roll raw data into coarser buckets; move old data to cold storage.
- Kafka in front decouples ingestion from storage outages.

## Alerting

- Rules in config files (YAML): `if p99_latency > 500ms for 5m → page`.
- Alert manager **dedupes, groups, silences**, and routes; retries delivery until acknowledged.
- Store alert state to avoid duplicate pages.

## Common mistakes

- ❌ Using a generic relational DB for metrics.
- ❌ High-cardinality labels such as user IDs.
- ❌ No plan for when monitoring itself fails.

## Practice questions

- Why is cardinality the main scaling risk?
- How do you alert when the monitoring system itself is down?
- Explain how delta-of-delta encoding saves space.
- How long does a "last 30 days, p99 by region" dashboard query take, and how do you make it fast?

---

[← Distributed Message Queue](19-message-queue.md) &nbsp;·&nbsp; [🏠 All notes](../README.md) &nbsp;·&nbsp; [Ad Click Aggregation →](21-ad-click-aggregation.md)
