# 03 · A Framework for the Interview

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
