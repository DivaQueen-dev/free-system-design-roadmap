# System Design Interview Guide

A step-by-step framework you can follow in every system design interview, with timing, example phrases, and the mistakes to avoid.

## Contents

1. [What interviewers are evaluating](#what-interviewers-are-evaluating)
2. [The 6-step framework](#the-6-step-framework)
3. [A 45-minute timeline](#a-45-minute-timeline)
4. [Checklists](#checklists)
5. [How to talk about trade-offs](#how-to-talk-about-trade-offs)
6. [Phrases that help](#phrases-that-help)
7. [What changes by level](#what-changes-by-level)
8. [Common mistakes](#common-mistakes)
9. [A short worked example](#a-short-worked-example)
10. [How to practise](#how-to-practise)

---

## What interviewers are evaluating

The interview is open-ended on purpose. There is no single correct design. Interviewers look for:

| Signal | What it looks like |
| ------ | ------------------ |
| **Problem exploration** | You ask clarifying questions and define scope before designing. |
| **Structured thinking** | You follow a clear process instead of jumping around. |
| **Technical breadth** | You know the building blocks and can combine them. |
| **Technical depth** | When asked, you can go deep on one or two components. |
| **Trade-off reasoning** | You explain why you chose something and what you gave up. |
| **Use of numbers** | You estimate scale and let it drive decisions. |
| **Communication** | You explain clearly, draw clean diagrams, and respond well to hints. |
| **Collaboration** | You treat the interviewer as a teammate, not an examiner. |

You are expected to drive. Don't wait for the interviewer to tell you what to do next.

---

## The 6-step framework

### Step 1: Clarify requirements (about 5 minutes)

Never start designing right away. Ask questions to pin down what you're building.

**Functional requirements**: what the system does.
- What are the core features? (Pick 2 to 4 and agree to defer the rest.)
- Who are the users? Are there different roles?
- What are the inputs and outputs?
- Any platform constraints (mobile, web, API)?

**Non-functional requirements**: how well it must do it.
- Scale: how many users, how many requests per second?
- Latency: what response time is acceptable?
- Availability: how critical is uptime?
- Consistency: is stale data acceptable, or must it be exact?
- Durability: can we ever lose data?
- Geography: single region or global?

**Out of scope**: say what you won't cover. "I'll leave authentication and analytics out unless you'd like me to cover them."

Write the agreed requirements on the board. You'll refer back to them.

### Step 2: Estimate scale (about 3 to 5 minutes)

Use quick numbers to find the bottlenecks. Estimate:
- Requests per second (average and peak)
- Read to write ratio
- Storage needed (per day and over the retention period)
- Bandwidth, if media is involved

Then state what the numbers imply: "This is read-heavy at about 50,000 reads per second, so caching is essential. Storage is around 5 TB per year, which fits on a sharded database or object storage."

Don't spend too long on arithmetic. Round aggressively. The goal is to inform decisions, not to be exact. See [estimation in FUNDAMENTALS.md](FUNDAMENTALS.md#3-back-of-envelope-estimation).

### Step 3: Define the API and data model (about 5 minutes)

**API**: list the main endpoints with parameters and responses.

```
POST /v1/urls            body: { long_url, custom_alias?, expires_at? }   -> { short_url }
GET  /{short_code}                                                         -> 302 redirect
```

**Data model**: list the main entities, their key fields, and relationships. Say which database type you'd choose and why. Note the primary access patterns, since they drive your indexes and shard key.

### Step 4: High-level design (about 10 minutes)

Draw a simple diagram with the main components and the flow of a request through them: clients, load balancer, services, caches, databases, queues, object storage, CDN.

Walk through the main use cases end to end. Keep it simple at first. A correct simple design beats an impressive complicated one.

Start with the straightforward version, then evolve it as requirements and numbers demand.

### Step 5: Deep dive (about 15 minutes)

This is where you differentiate yourself. The interviewer may pick areas to explore, or you can propose them: "The hardest parts here are generating unique short codes and handling the read load. Which would you like me to go into?"

Typical deep-dive topics:
- Data partitioning and the shard key
- Caching strategy and invalidation
- Handling hot keys or celebrity users
- Consistency and failure scenarios
- Fan-out strategy (write vs read)
- Queue design, retries, and idempotency
- Algorithm choice (for example, rate limiting algorithm, ranking, ID generation)

For each, explain options, pick one, and justify it.

### Step 6: Wrap up (about 5 minutes)

- Identify bottlenecks and single points of failure, and say how you'd address them.
- Discuss failure scenarios: what if a database, a cache node, or a region goes down?
- Mention monitoring: what you'd track and alert on.
- Mention how you'd evolve the system: what changes at 10 times the scale?
- Note what you'd do with more time (security, analytics, cost optimisation).

Summarise your design in two or three sentences.

---

## A 45-minute timeline

| Minutes | Step |
| ------- | ---- |
| 0 - 5 | Clarify requirements and scope |
| 5 - 10 | Estimate scale, define API and data model |
| 10 - 20 | High-level design and main flows |
| 20 - 40 | Deep dives on 2 or 3 components |
| 40 - 45 | Bottlenecks, failures, monitoring, questions |

For 60-minute interviews, extend the deep dive. For 30-minute ones, shorten estimation and deep dives, and skip the full data model.

---

## Checklists

### Clarifying question checklist

- Who are the users and how many?
- What are the 2 to 4 core features?
- Read-heavy or write-heavy? What is the ratio?
- Expected scale: DAU, QPS, data size?
- Latency target? Real-time or eventual?
- Strict consistency, or is stale data okay?
- Availability target?
- Global or single region?
- Mobile, web, or both?
- Any special constraints (compliance, budget, existing systems)?

### Non-functional requirements checklist

| Area | Question to ask yourself |
| ---- | ------------------------ |
| Scalability | What happens at 10x traffic? |
| Latency | What is the p99 target for key operations? |
| Availability | Which components can't fail? |
| Consistency | Where do we need strong consistency, and where is eventual fine? |
| Durability | What data can never be lost? |
| Security | Authentication, authorisation, encryption, abuse? |
| Cost | What dominates the bill: storage, compute, bandwidth? |
| Operability | How do we monitor, deploy, and debug? |

### Final review checklist

- Did I address every functional requirement we agreed on?
- Do the estimates support my choices?
- Where are the single points of failure?
- What happens when each component fails?
- Where are the hot spots (hot keys, hot shards)?
- Is the data model matched to the access patterns?
- Can I explain every technology choice and its alternative?

---

## How to talk about trade-offs

Every decision has a cost. Interviewers love to hear you name it. A simple template:

> "I'll use **X** because **reason tied to requirement**. The trade-off is **cost of X**. If **condition changes**, I'd switch to **Y**."

Examples:

- "I'll use a cache-aside Redis cache because this is read-heavy and users tolerate a few seconds of staleness. The trade-off is occasional stale data and extra operational complexity. If we needed strict freshness, I'd use write-through or invalidate on every update."
- "I'll use asynchronous replication for lower write latency. The trade-off is that a failover could lose the last few writes. If this were payments, I'd use synchronous replication to at least one replica."
- "I'll fan out on write for most users so feed reads are fast. The trade-off is heavy write amplification for users with millions of followers, so for those accounts I'll fetch their posts at read time and merge."

### Common trade-off pairs

| Choose... | Over... | When |
| --------- | ------- | ---- |
| Consistency | Availability | Money, inventory, bookings |
| Availability | Consistency | Feeds, likes, carts, DNS |
| Latency | Throughput | Interactive requests |
| Throughput | Latency | Batch jobs, analytics |
| SQL | NoSQL | Complex queries, transactions, moderate scale |
| NoSQL | SQL | Huge scale, simple access patterns, flexible schema |
| Push (fan-out on write) | Pull (fan-out on read) | Many reads, few followers per writer |
| Pull | Push | Celebrity accounts, rarely read content |
| Monolith | Microservices | Small team, early product |
| Strong consistency | Performance | Correctness-critical data |
| Denormalisation | Normalisation | Read-heavy paths |

---

## Phrases that help

**Starting**
- "Before I design, I'd like to clarify the requirements."
- "Let me confirm the scope. I'll focus on X and Y, and treat Z as out of scope for now."

**Estimating**
- "Let me do a quick back-of-envelope calculation to see where the bottlenecks are."
- "Assuming 100 million daily users with 10 requests each, that's about 10,000 requests per second on average."

**Designing**
- "I'll start simple and then scale it."
- "Let me walk through the main flow end to end."
- "The key challenge here is..."

**Trade-offs**
- "There are two options here. A gives us..., but costs us... B gives us..."
- "I'm choosing X because of requirement Y. If that changes, I'd reconsider."

**When you're unsure**
- "I haven't used that exact system, but the underlying idea is..."
- "I'd want to benchmark this, but my expectation is..."
- "Can I make an assumption here and revisit it later?"

**Wrapping up**
- "The main bottlenecks I see are... and I'd address them by..."
- "If we had 10 times the traffic, the first thing to break would be... so I'd..."

---

## What changes by level

| Level | What is expected |
| ----- | ---------------- |
| **Fresher / junior** | Good fundamentals: how a web app works, SQL vs NoSQL, caching, load balancing, basic schema and API design. Usually paired with an LLD round. Clear thinking matters more than depth. |
| **Mid-level (about 2 to 5 years)** | Solid command of the building blocks. Complete designs with sensible estimates and trade-offs. Can handle a few deep-dive questions on one or two areas. |
| **Senior** | Drives the whole interview. Goes deep on multiple areas. Brings real-world experience, failure scenarios, operational concerns, cost, and evolution over time. Challenges ambiguous requirements. |
| **Staff and above** | Broader scope: cross-system impact, organisational constraints, migration strategies, build vs buy, long-term evolution. |

---

## Common mistakes

| Mistake | Why it hurts | What to do instead |
| ------- | ------------ | ------------------ |
| Jumping straight into boxes and arrows | You may solve the wrong problem | Clarify requirements first |
| Skipping estimation | Choices look arbitrary | Use quick numbers to justify decisions |
| Over-engineering | Shows poor judgement | Start simple, add complexity when numbers demand it |
| Name-dropping tools | Signals memorisation | Explain why each tool fits |
| Never mentioning failure | Misses a core part of the job | Discuss what breaks and how you recover |
| Ignoring the interviewer's hints | Looks rigid | Treat hints as direction and adapt |
| Going silent | Interviewer can't grade your thinking | Narrate your reasoning |
| One giant diagram from the start | Hard to follow | Build up in layers |
| Going deep on irrelevant parts | Wastes time | Prioritise the riskiest or hardest components |
| Claiming a perfect design | Unrealistic | Acknowledge limitations and alternatives |
| Memorising "Design X" answers | Falls apart when requirements change | Learn the building blocks and practise adapting |

---

## A short worked example

**Prompt:** "Design a URL shortener."

**Step 1: Requirements.**
Functional: create a short link from a long URL; redirect from short to long. Optional: custom alias, expiry. Out of scope: analytics, user accounts.
Non-functional: highly available redirects, low latency (under 100 ms), links shouldn't be guessable in sequence, durable. Scale: 100 million new links per month.

**Step 2: Estimates.**
Writes: 100M per month is about 40 per second. If reads are 100 times writes, that's about 4,000 redirects per second. Storage: 1.2 billion links per year, at about 500 bytes each is roughly 600 GB per year. That fits easily with sharding. A 7-character base62 code gives about 3.5 trillion combinations, plenty.
Conclusion: read-heavy, small data. Caching will handle most reads.

**Step 3: API and data model.**
`POST /v1/urls` and `GET /{code}`. Table: `code (PK), long_url, created_at, expires_at, user_id`. A key-value lookup by code is the main access pattern, so a key-value store or a sharded SQL table keyed by code works.

**Step 4: High-level design.**
Client, load balancer, stateless app servers, Redis cache, database. On redirect: check cache, fall back to DB, populate cache, return 302.

**Step 5: Deep dive.**
Code generation: compare hashing with collision handling, random codes with a uniqueness check, and a counter encoded in base62. Pick counters handed out in ranges to each app server (no coordination per request). Discuss 301 vs 302: 301 reduces load but browsers cache it and you lose analytics.

**Step 6: Wrap-up.**
SPOFs: database (replicate and fail over), cache (cluster, and the DB can absorb a cold start with rate limits). Monitor redirect latency, cache hit rate, and error rate. At 10x, shard by code and add more cache nodes.

Full version: [CASE_STUDIES.md: URL shortener](CASE_STUDIES.md#1-design-a-url-shortener).

---

## How to practise

1. **Solve alone first.** Set a 40-minute timer, draw on paper or Excalidraw, and speak aloud.
2. **Compare with a good solution** and note what you missed. See [CASE_STUDIES.md](CASE_STUDIES.md).
3. **Do mock interviews.** Take turns with a partner (our [Discord](https://discord.gg/ETCSm74A59) has study groups). Giving feedback teaches as much as receiving it.
4. **Record yourself** and watch it back. Look for silent gaps, rambling, and unexplained choices.
5. **Change the requirements** on problems you've solved: 100 times the traffic, strict consistency, a new region. Redesign.
6. **Keep a design journal** with a one-page summary of each problem: requirements, estimates, diagram, and top three trade-offs.
7. **Read real architectures** from engineering blogs and ask: what problem did they solve, and what did they trade off?

Consistency beats cramming. Two problems a week for two months is better than twenty in one weekend.
