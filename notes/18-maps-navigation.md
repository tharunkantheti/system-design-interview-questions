# 18 · Maps and Navigation (Google Maps-like)

Render maps, find routes, estimate travel time, and give turn-by-turn navigation.

## Requirements

- Location updates from users, navigation with ETA, map rendering on mobile.
- 1B DAU; ETA accurate and responsive to traffic; reroute on changes.
- Mobile-friendly: low data and battery usage.

## Key concepts

- **Map projection**: the sphere is drawn flat (Web Mercator).
- **Tiles**: the world is split into square image (or vector) tiles at each **zoom level**; zoom 0 = 1 tile, each level ×4.
- **Routing graph**: roads as nodes and edges. The whole world is too big for one graph, so split it into **routing tiles** (by geohash-like grid) at multiple levels of detail (local streets, arterials, highways).

## Design

```mermaid
flowchart LR
    M[Mobile client] -- tiles --> CDN[CDN: precomputed map tiles]
    M -- batched location updates --> LS[Location service] --> KQ[[Kafka]]
    KQ --> TR[Traffic updater] & ML[ML: ETA, new roads] & AN[Analytics]
    LS --> LDB[(User location DB: wide-column)]
    M -- route request --> NS[Navigation service]
    NS --> GEO[Geocoding service] --> GDB[(Geocoding DB)]
    NS --> RP[Route planner]
    RP --> SP[Shortest path service] --> RT[(Routing tiles in object storage)]
    RP --> ETA[ETA service]
    RP --> RANK[Ranker: tolls, highways filter]
    TR --> ETA
    NS -. reroute push .-> ANS[Adaptive ETA + rerouting] -.-> M
```

## Component notes

- **Tiles**: precomputed, static, served by CDN. Vector tiles cut bandwidth and render smoothly.
- **Location updates**: buffer on the device and send batches (e.g. every 15 s) to save battery. Write-heavy → Cassandra-style DB.
- **Shortest path**: A* / Dijkstra variants over routing tiles loaded on demand; hierarchical tiles keep long routes tractable.
- **ETA**: combine historical speeds and live traffic with ML predictions.
- **Rerouting**: track active navigations by tile; when traffic changes in a tile, recompute ETA for affected users and push updates over a WebSocket.

## Practice questions

- How many tiles exist at zoom 21? Why precompute and CDN them?
- Why split the routing graph into tiles with different levels?
- How do you detect a traffic jam from user location data?
- How do you know which users to reroute when an accident happens?
