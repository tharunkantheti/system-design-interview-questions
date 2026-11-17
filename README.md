# System Design Interview Questions

My personal notes for preparing system design interviews: the common problems, the
building blocks they share, and the trade-offs worth saying out loud in the room.

Every note follows the same shape so it doubles as an interview script:

1. **Clarify** – functional and non-functional requirements
2. **Estimate** – rough traffic, storage and bandwidth numbers
3. **Design** – a high-level diagram and the main APIs
4. **Deep dive** – the two or three components interviewers push on
5. **Trade-offs** – what you gave up and why
6. **Practice questions** – follow-ups to rehearse answers for

Diagrams are written in [Mermaid](https://mermaid.js.org/) so GitHub renders them inline.

## Foundations

| # | Topic | Core idea |
|---|-------|-----------|
| 01 | [Scaling from one server to millions](notes/01-scaling.md) | Stateless tiers, caching, replication, sharding |
| 02 | [Back-of-the-envelope estimation](notes/02-estimation.md) | Powers of two, latency numbers, QPS math |
| 03 | [Interview framework](notes/03-interview-framework.md) | How to run the 45 minutes |
| 04 | [Rate limiter](notes/04-rate-limiter.md) | Token bucket, sliding window, distributed counters |
| 05 | [Consistent hashing](notes/05-consistent-hashing.md) | Hash ring, virtual nodes |
| 06 | [Key-value store](notes/06-key-value-store.md) | Quorums, vector clocks, gossip, Merkle trees |
| 07 | [Unique ID generator](notes/07-unique-id-generator.md) | Snowflake-style IDs |

## Classic product designs

| # | Topic | Core idea |
|---|-------|-----------|
| 08 | [URL shortener](notes/08-url-shortener.md) | Base62, redirect caching |
| 09 | [Web crawler](notes/09-web-crawler.md) | URL frontier, politeness, dedup |
| 10 | [Notification system](notes/10-notification-system.md) | Fan-out queues, retries, providers |
| 11 | [News feed](notes/11-news-feed.md) | Fan-out on write vs read |
| 12 | [Chat system](notes/12-chat-system.md) | WebSockets, presence, message sync |
| 13 | [Search autocomplete](notes/13-search-autocomplete.md) | Tries, top-k caching |
| 14 | [Video streaming (YouTube-like)](notes/14-video-streaming.md) | Transcoding DAG, CDN |
| 15 | [Cloud file storage (Drive-like)](notes/15-cloud-file-storage.md) | Block sync, dedup, conflicts |

## Location, data and infrastructure

| # | Topic | Core idea |
|---|-------|-----------|
| 16 | [Proximity service](notes/16-proximity-service.md) | Geohash, quadtree |
| 17 | [Nearby friends](notes/17-nearby-friends.md) | Pub/sub location updates |
| 18 | [Maps and navigation](notes/18-maps-navigation.md) | Tiles, routing graph, ETA |
| 19 | [Distributed message queue](notes/19-message-queue.md) | Partitioned logs, consumer groups |
| 20 | [Metrics monitoring and alerting](notes/20-metrics-monitoring.md) | Time-series DB, downsampling |
| 21 | [Ad click aggregation](notes/21-ad-click-aggregation.md) | Stream windows, exactly-once |
| 22 | [Hotel reservation](notes/22-hotel-reservation.md) | Inventory, double-booking prevention |
| 23 | [Email service](notes/23-email-service.md) | SMTP, mailbox storage, search |
| 24 | [Object storage (S3-like)](notes/24-object-storage.md) | Metadata vs data, erasure coding |
| 25 | [Real-time leaderboard](notes/25-leaderboard.md) | Redis sorted sets |
| 26 | [Payment system](notes/26-payment-system.md) | Idempotency, ledger, reconciliation |
| 27 | [Digital wallet](notes/27-digital-wallet.md) | Distributed transactions, event sourcing |
| 28 | [Stock exchange](notes/28-stock-exchange.md) | Order book, matching engine, low latency |

## Cheat sheet

- [Building blocks and when to use them](notes/00-building-blocks.md)

## How I study with these

- Pick a note, close it, and design the system on a whiteboard in 35 minutes.
- Re-open it and compare: what did I miss in requirements, numbers, or trade-offs?
- Answer the practice questions out loud.
