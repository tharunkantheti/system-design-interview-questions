# 03 · A Framework for the Interview

**Difficulty:** 🟢 Easy &nbsp;|&nbsp; **Topics:** process · communication

> [!TIP]
> **30-second answer**
> - Clarify (5–10 min) → high-level design (10–15) → deep dive (10–20) → wrap up (3–5).
> - Get the interviewer to agree on the high-level design before going deep.

<details><summary><b>Contents</b></summary>

- [Time plan](#time-plan)
- [Phase 1: clarify](#phase-1-clarify)
- [Phase 2: high-level design](#phase-2-high-level-design)
- [Phase 3: deep dive](#phase-3-deep-dive)
- [Phase 4: wrap up](#phase-4-wrap-up)
- [Do / don't](#do--dont)
- [Common mistakes](#common-mistakes)

</details>

A 45-minute system design interview rewards structure and communication more than a "perfect" design.

## Time plan

| Phase | Time | What to do |
|-------|------|------------|
| 1. Understand the problem | 5–10 min | Ask questions, agree on scope |
| 2. High-level design | 10–15 min | Draw boxes, define APIs, get buy-in |
| 3. Deep dive | 10–20 min | Go deep on 2–3 components the interviewer cares about |
| 4. Wrap up | 3–5 min | Bottlenecks, failure modes, what you'd do next |

## Phase 1: clarify

- Who are the users? What are the **core features** (pick 2–4)?
- How many users? Read-heavy or write-heavy?
- Latency, consistency and availability expectations?
- Mobile, web, or both? Global or one region?
- Write the requirements on the board so you can point back at them.

## Phase 2: high-level design

- Sketch the request path: client → LB → services → storage.
- Define the main **APIs** (`POST /v1/messages`, etc.) and the **data model**.
- Do quick estimates only if they change a decision.
- Ask: "Does this look like the right direction before I go deeper?"

## Phase 3: deep dive

- Let the interviewer steer; otherwise pick the hardest part (the hot path, consistency, scaling the write path).
- Discuss **trade-offs explicitly**: "I chose X over Y because…, the cost is…".

## Phase 4: wrap up

- Single points of failure and how to remove them.
- Monitoring, alerting, and how you'd roll this out.
- How the design changes at 10× scale.

## Do / don't

- ✅ Think out loud, ask for hints, keep it collaborative.
- ✅ Start simple and iterate.
- ❌ Don't jump into a solution before clarifying.
- ❌ Don't go deep on one box early and run out of time.
- ❌ Don't name-drop technologies without explaining why.

## Common mistakes

- ❌ Designing before asking a single question.
- ❌ Going silent while thinking.
- ❌ Spending 20 minutes on one component and never finishing the big picture.

---

[← Estimation](02-estimation.md) &nbsp;·&nbsp; [🏠 All notes](../README.md) &nbsp;·&nbsp; [Rate Limiter →](04-rate-limiter.md)
