# 00 · Building Blocks Cheat Sheet

A quick reference of the components that show up in almost every design.

| Block | Reach for it when | Watch out for |
|-------|-------------------|---------------|
| Load balancer (L4/L7) | Spreading traffic over stateless servers | Becoming a single point of failure; sticky sessions |
| CDN | Static or cacheable content for global users | Cache invalidation, cost for low-traffic assets |
| Cache (Redis/Memcached) | Read-heavy data, hot keys, sessions | Stale data, thundering herd, eviction policy |
| Relational DB | Transactions, joins, strong consistency | Write scaling; needs sharding eventually |
| Wide-column / KV store | Huge write volume, simple access by key | No joins, modeling around queries |
| Document store | Flexible schema, nested objects | Cross-document transactions |
| Message queue / log | Decoupling, buffering spikes, async work | Ordering, duplicates, consumer lag |
| Object storage | Large blobs: images, video, backups | Not for small, frequently updated records |
| Search index | Full-text, fuzzy, faceted search | Index lag behind the source of truth |
| Time-series DB | Metrics, events keyed by time | Cardinality explosion |
| Stream processor | Real-time aggregation over events | State management, late events |
| Coordination (ZooKeeper/etcd) | Leader election, config, locks | Keep it off the hot path |

## Consistency vocabulary

- **Strong**: every read sees the latest committed write.
- **Eventual**: replicas converge if writes stop.
- **Read-your-writes**: a user always sees their own updates.
- **CAP**: during a network partition, choose consistency (reject some requests) or availability (serve possibly stale data).

## Patterns worth naming in interviews

- **Write-through / write-back / cache-aside** caching
- **Fan-out on write vs fan-out on read**
- **Idempotency keys** for safe retries
- **Outbox pattern** to publish events and update the DB atomically
- **Saga** for multi-step workflows without distributed locks
- **Backpressure** so slow consumers don't crash fast producers
- **Circuit breaker** to stop hammering a failing dependency
