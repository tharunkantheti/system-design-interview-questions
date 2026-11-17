# 02 · Back-of-the-Envelope Estimation

**Difficulty:** 🟢 Easy &nbsp;|&nbsp; **Topics:** QPS · storage · bandwidth

> [!TIP]
> **30-second answer**
> - 1 day ≈ 10^5 seconds; 1M requests/day ≈ 12 QPS; peak ≈ 2–3× average.
> - Estimate QPS, storage over N years, and bandwidth, then say what each number changes in the design.

<details><summary><b>Contents</b></summary>

- [Numbers to keep in your head](#numbers-to-keep-in-your-head)
- [Handy shortcuts](#handy-shortcuts)
- [Worked example: photo-sharing app](#worked-example-photo-sharing-app)
- [Tips](#tips)
- [Common mistakes](#common-mistakes)
- [Practice questions](#practice-questions)

</details>

The goal is to get within an order of magnitude quickly, then use the number to justify design choices.

## Numbers to keep in your head

**Data sizes**

| Power | Approx | Name |
|-------|--------|------|
| 2^10 | 1 thousand | KB |
| 2^20 | 1 million | MB |
| 2^30 | 1 billion | GB |
| 2^40 | 1 trillion | TB |
| 2^50 | 1 quadrillion | PB |

**Latency (rough, order of magnitude)**

| Operation | Time |
|-----------|------|
| L1 cache reference | ~1 ns |
| Main memory reference | ~100 ns |
| Read 1 MB sequentially from memory | ~10 µs |
| SSD random read | ~100 µs |
| Round trip inside a data center | ~0.5 ms |
| Read 1 MB sequentially from SSD | ~1 ms |
| Disk seek (HDD) | ~10 ms |
| Round trip across continents | ~150 ms |

Takeaways: memory is fast, disk seeks are slow, network across regions is slowest. Compress before sending, and cache aggressively.

**Availability**

| SLA | Downtime per year |
|-----|-------------------|
| 99% | ~3.65 days |
| 99.9% | ~8.8 hours |
| 99.99% | ~53 minutes |
| 99.999% | ~5 minutes |

## Handy shortcuts

- 1 day ≈ 86,400 s ≈ **10^5 s** (round to 100k for mental math).
- 1 million requests/day ≈ **12 QPS**.
- **Peak QPS** ≈ 2–3× average.
- 1 billion requests/day ≈ ~12,000 QPS.

## Worked example: photo-sharing app

Assumptions: 100M daily active users, each uploads 1 photo per day on average, 500 KB per photo, 10 views per upload.

- Write QPS: 100M / 10^5 ≈ **1,000 QPS**, peak ~2,500.
- Read QPS: ~10× writes ≈ **10,000 QPS**.
- Storage per day: 100M × 500 KB = **50 TB/day**.
- Storage over 5 years: 50 TB × 365 × 5 ≈ **~90 PB** (before replication; ×3 for copies).
- Egress bandwidth: 10,000 × 500 KB ≈ **5 GB/s** → a CDN is mandatory.

## Tips

- Write down assumptions and label units.
- Round aggressively; precision isn't the point.
- Finish with what the number means: "~90 PB means object storage plus a CDN, not a database."

## Common mistakes

- ❌ Chasing precision instead of the order of magnitude.
- ❌ Producing numbers that never influence a design decision.
- ❌ Mixing up bits and bytes, or forgetting replication when sizing storage.

## Practice questions

- Estimate storage for 5 years of tweets (text only, then with media).
- How many servers to handle 50k QPS if one server handles ~2k?
- How much RAM does it take to cache the top 20% of daily reads?

---

[← Scaling](01-scaling.md) &nbsp;·&nbsp; [🏠 All notes](../README.md) &nbsp;·&nbsp; [Interview Framework →](03-interview-framework.md)
