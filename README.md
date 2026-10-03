# Free System Design Roadmap

### A complete, clear path from "what is a load balancer?" to designing large-scale systems. Free resources only.

[![Discord](https://img.shields.io/badge/Join%20Community-Discord-7289da?style=for-the-badge&logo=discord)](https://discord.gg/ETCSm74A59)
[![Stars](https://img.shields.io/github/stars/DivaQueen-dev/free-system-design-roadmap?style=for-the-badge)](https://github.com/DivaQueen-dev/free-system-design-roadmap)
[![PRs Welcome](https://img.shields.io/badge/PRs-Welcome-orange?style=for-the-badge)](CONTRIBUTING.md)

Part of the [Free Tech Roadmap](https://github.com/DivaQueen-dev/free-cs-roadmap) series.

---

> System design is not about memorising the architecture of Netflix. It is about learning a small set of building blocks, understanding the trade-offs of each, and combining them to meet requirements. This repo teaches the building blocks first, then shows how to combine them.

No paid courses. No affiliate links.

---

## What's in this repo

| File | What it has | Read it when |
| ---- | ----------- | ------------ |
| **README.md** (you are here) | Roadmap, resources, study plans, progress tracker | You want to know what to learn and in what order |
| **[FUNDAMENTALS.md](FUNDAMENTALS.md)** | Every core concept explained clearly: scaling, caching, databases, sharding, replication, queues, CAP, reliability, and more | You want to understand the building blocks |
| **[INTERVIEW_GUIDE.md](INTERVIEW_GUIDE.md)** | A step-by-step framework for the system design interview, with timing, phrases, and common mistakes | You are preparing for interviews |
| **[CASE_STUDIES.md](CASE_STUDIES.md)** | Worked designs (URL shortener, rate limiter, news feed, chat, RAG chatbot) plus 15 more problem summaries | You want to practise real problems |

---

## Table of Contents

1. [What system design is](#what-system-design-is)
2. [Prerequisites](#prerequisites)
3. [The roadmap in 6 stages](#the-roadmap-in-6-stages)
4. [Best free resources](#best-free-resources)
5. [Engineering blogs worth reading](#engineering-blogs-worth-reading)
6. [Papers that shaped the field](#papers-that-shaped-the-field)
7. [Tools for drawing diagrams](#tools-for-drawing-diagrams)
8. [Build to learn: hands-on projects](#build-to-learn-hands-on-projects)
9. [Low-level design (LLD)](#low-level-design-lld)
10. [Study plans](#study-plans)
11. [How to practise a design problem](#how-to-practise-a-design-problem)
12. [Progress tracker](#progress-tracker)
13. [Common mistakes](#common-mistakes)
14. [FAQ](#faq)
15. [Contributing](#contributing)

---

## What system design is

System design is the process of deciding how the parts of a software system fit together so that it meets its requirements: how many users it serves, how fast it responds, how reliable it is, and how much it costs.

There are two flavours, and people often mix them up:

| | High-level design (HLD) | Low-level design (LLD) |
| - | ----------------------- | ---------------------- |
| Question | What services, databases, and queues do we need? | What classes, interfaces, and methods do we need? |
| Example | Design Instagram | Design a parking lot, an elevator, or a chess game |
| Skills | Scaling, storage, networking, trade-offs | OOP, design patterns, clean code |
| Where asked | Mid and senior interviews, real architecture work | Most interviews, including freshers and Indian product companies |

This repo is mainly HLD. The [LLD section](#low-level-design-lld) points you to resources for the other half.

---

## Prerequisites

You don't need to be an expert, but you should be comfortable with:

- One programming language and how a web request works (client, server, HTTP, JSON)
- Basic SQL and what a database index is
- The basics of data structures (hash maps, queues, trees). See the [DSA roadmap](https://github.com/DivaQueen-dev/free-dsa-roadmap)
- Basic Linux and networking ideas (IP, ports, DNS)

If you are a complete beginner, build one small full-stack project first. System design makes far more sense once you have felt the pain of a slow query or a server that fell over.

---

## The roadmap in 6 stages

Work through the stages in order. Each stage lists what to learn and where to find it in this repo.

### Stage 1: The basics of how systems work

Learn: client-server model, HTTP and REST, DNS, what happens when you type a URL, latency vs throughput, vertical vs horizontal scaling, stateless vs stateful servers.

Read: [FUNDAMENTALS.md: Core vocabulary, Scaling, Networking](FUNDAMENTALS.md)

Goal: you can explain how a request travels from a browser to a database and back.

### Stage 2: Building blocks, part 1 (serving traffic)

Learn: load balancers, reverse proxies, API gateways, caching, CDNs.

Read: [FUNDAMENTALS.md: Load balancing, Caching, CDN](FUNDAMENTALS.md)

Goal: you can add caching and load balancing to a simple app and explain the problems each introduces (stale data, cache stampede).

### Stage 3: Building blocks, part 2 (storing data)

Learn: SQL vs NoSQL, indexes, replication, partitioning and sharding, consistent hashing, transactions, CAP theorem and consistency models, object storage, search, vector databases.

Read: [FUNDAMENTALS.md: Databases, Replication, Sharding, CAP, Storage](FUNDAMENTALS.md)

Goal: you can pick a database for a given workload and explain how it scales.

### Stage 4: Building blocks, part 3 (communication and reliability)

Learn: message queues, pub/sub, Kafka-style logs, delivery guarantees, idempotency, retries, circuit breakers, rate limiting, observability, security basics.

Read: [FUNDAMENTALS.md: Messaging, API design, Reliability, Observability](FUNDAMENTALS.md)

Goal: you can design asynchronous workflows and explain what happens when something fails.

### Stage 5: Putting it together

Learn: the interview framework, back-of-envelope estimation, and how to apply the building blocks to real problems.

Read: [INTERVIEW_GUIDE.md](INTERVIEW_GUIDE.md), then [CASE_STUDIES.md](CASE_STUDIES.md). Solve each problem yourself before reading the answer.

Goal: you can design a URL shortener, a chat app, and a news feed end to end in 45 minutes, and defend your choices.

### Stage 6: Going deeper

Learn: distributed systems theory (consensus, replication logs, clocks), architecture patterns (event sourcing, CQRS, sagas), data pipelines, and how real companies solved real scale problems.

Read: the [papers](#papers-that-shaped-the-field), the [engineering blogs](#engineering-blogs-worth-reading), and the advanced resources below.

Goal: you understand why systems like Kafka, Cassandra, and Spanner are built the way they are.

---

## Best free resources

### Start here (beginner)

| Resource | What it is | Why it's good |
| -------- | ---------- | ------------- |
| [System Design Primer](https://github.com/donnemartin/system-design-primer) | A huge GitHub guide covering all the core concepts with diagrams and links, plus Anki flashcards. | The most widely used free system design resource. Great as a reference. |
| [HelloInterview: System Design in a Hurry](https://www.hellointerview.com/learn/system-design/in-a-hurry/introduction) | A structured introduction to the interview format and core concepts. | Clear, modern, and focused on what interviewers actually ask. |
| [Tech Interview Handbook: System Design](https://www.techinterviewhandbook.org/system-design/) | Concise overview of how to approach system design interviews. | Short and practical. Good first read. |
| [ByteByteGo on YouTube](https://www.youtube.com/@ByteByteGo) | Short animated videos explaining concepts and how real systems work. | Excellent visuals. Makes abstract ideas concrete. |
| [System Design 101 (GitHub)](https://github.com/ByteByteGoHq/system-design-101) | Visual explanations of many concepts and technologies in one repo. | Quick, diagram-based revision. |
| [Gaurav Sen: System Design playlist](https://www.youtube.com/playlist?list=PLMCXHnjXnTnvo6alSjVkgxV-VH6EPyvoX) | Long-running playlist covering concepts and designs. | Clear explanations, good for building intuition. |

### Intermediate

| Resource | What it is | Why it's good |
| -------- | ---------- | ------------- |
| [Alex Xu book notes (Preslav Mihaylov)](https://github.com/preslavmihaylov/booknotes/tree/master/system-design/system-design-interview) | Detailed chapter notes for the popular System Design Interview book. | Lets you see the standard approach to the classic problems for free. |
| [Awesome Scalability](https://github.com/binhnguyennus/awesome-scalability) | A curated list of articles on how real companies scale their systems. | A goldmine of real-world case studies, organised by topic. |
| [High Scalability](http://highscalability.com) | Blog with architecture breakdowns of well-known systems. | Good for seeing how pieces are combined in production. |
| [Microservices.io patterns](https://microservices.io/patterns/index.html) | Catalogue of microservice patterns (saga, outbox, CQRS, API gateway). | The standard reference for these patterns. |
| [Martin Fowler: Microservices](https://martinfowler.com/articles/microservices.html) | The classic article defining the microservices style. | Explains both benefits and costs honestly. |
| [Hussein Nasser (YouTube)](https://www.youtube.com/@hnasr) | Deep dives on databases, proxies, networking, and protocols. | Strong on the "how does it actually work" questions. |

### Advanced

| Resource | What it is | Why it's good |
| -------- | ---------- | ------------- |
| [Jordan Has No Life (YouTube)](https://www.youtube.com/@jordanhasnolife5163) | Deep system design walkthroughs with detailed trade-off discussions. | Goes well beyond standard interview answers. |
| [MIT 6.824: Distributed Systems](https://pdos.csail.mit.edu/6.824/) | University course with lectures, readings, and labs (Raft, sharded KV store). Now numbered 6.5840. | The best free way to learn distributed systems properly. |
| Martin Kleppmann's distributed systems lectures | Free lecture series on YouTube covering time, replication, consensus, and consistency. Search for "Kleppmann distributed systems lecture series". | Rigorous and very clear. |
| [Raft visualisation](https://thesecretlivesofdata.com/raft/) and [raft.github.io](https://raft.github.io) | Interactive explanation of the Raft consensus algorithm, plus the paper and implementations. | Makes consensus understandable. |
| [AWS Well-Architected Framework](https://aws.amazon.com/architecture/well-architected/) | Best practices for building reliable, secure, efficient, cost-effective systems. | Vocabulary and principles used across the industry. |
| [Google SRE Book](https://sre.google/sre-book/table-of-contents/) | How Google runs reliable systems: SLOs, monitoring, incident response. | The foundation of reliability engineering. |

### Cloud architecture references

| Resource | What it is |
| -------- | ---------- |
| [AWS Architecture Center](https://aws.amazon.com/architecture/) | Reference architectures and diagrams for common workloads. |
| [Azure Architecture Center](https://learn.microsoft.com/en-us/azure/architecture/) | Design patterns, reference architectures, and guidance. |
| [Google Cloud Architecture Center](https://cloud.google.com/architecture) | Reference architectures and best practices. |

### Technology documentation worth skimming

You don't need to master these, but reading the "overview" or "architecture" page of each makes you far more concrete in interviews.

| Technology | Why look at it | Docs |
| ---------- | -------------- | ---- |
| Redis | Caching, rate limiting, leaderboards, pub/sub | [redis.io/docs](https://redis.io/docs) |
| Kafka | Event streaming, logs, partitions | [kafka.apache.org/documentation](https://kafka.apache.org/documentation/) |
| PostgreSQL | The default relational database choice | [postgresql.org/docs](https://www.postgresql.org/docs/) |
| Cassandra | Wide-column, leaderless, high write throughput | [cassandra.apache.org](https://cassandra.apache.org/doc/latest/) |
| Elasticsearch / OpenSearch | Full-text search | [elastic.co/guide](https://www.elastic.co/guide/index.html) |
| Nginx | Reverse proxy and load balancer | [nginx.org/en/docs](https://nginx.org/en/docs/) |

---

## Engineering blogs worth reading

Reading how real companies solved real problems is the fastest way to learn trade-offs. Pick one post a week and write a short summary: the problem, the solution, and the trade-offs.

| Blog | Typical topics |
| ---- | -------------- |
| [Netflix Tech Blog](https://netflixtechblog.com) | Streaming, resilience, microservices, data |
| [Uber Engineering](https://www.uber.com/blog/engineering/) | Real-time systems, geospatial, large-scale data |
| [Meta Engineering](https://engineering.fb.com) | Social graph, caching, infrastructure |
| [Cloudflare Blog](https://blog.cloudflare.com) | Networking, CDN, edge computing, outages explained |
| [Stripe Engineering](https://stripe.com/blog/engineering) | Payments, idempotency, reliability, APIs |
| [Airbnb Engineering](https://medium.com/airbnb-engineering) | Search, data platforms, service architecture |
| [LinkedIn Engineering](https://engineering.linkedin.com/blog) | Feeds, Kafka, data infrastructure |
| [Discord Blog](https://discord.com/blog) | Chat at scale, databases, real-time messaging |
| [Awesome Scalability](https://github.com/binhnguyennus/awesome-scalability) | Curated index of many more |

---

## Papers that shaped the field

You don't need to read these to pass interviews, but they explain where many modern systems came from. Search the title to find free PDFs on the authors' or publishers' sites. [Papers We Love](https://paperswelove.org) is a good community hub.

| Paper | Why it matters |
| ----- | -------------- |
| The Google File System | Distributed file storage at scale. The ancestor of HDFS. |
| MapReduce: Simplified Data Processing on Large Clusters | Batch processing model behind Hadoop. |
| Bigtable: A Distributed Storage System for Structured Data | Wide-column storage. Inspired HBase and Cassandra. |
| Dynamo: Amazon's Highly Available Key-value Store | Consistent hashing, quorums, eventual consistency. Inspired Cassandra and DynamoDB. |
| Kafka: a Distributed Messaging System for Log Processing | The log as a core abstraction. |
| In Search of an Understandable Consensus Algorithm (Raft) | Consensus explained in a way that people can implement. |
| Spanner: Google's Globally-Distributed Database | Global consistency using synchronised clocks. |
| The Chubby Lock Service | Distributed locking and coordination. Ancestor of ZooKeeper and etcd. |
| Scaling Memcache at Facebook | Practical lessons on caching at huge scale. |

---

## Tools for drawing diagrams

You will draw diagrams constantly. Get comfortable with one tool.

| Tool | Notes |
| ---- | ----- |
| [Excalidraw](https://excalidraw.com) | Free whiteboard-style drawing in the browser. Great for practice and interviews. |
| [draw.io / diagrams.net](https://app.diagrams.net) | Free, feature-rich, works offline. Good for polished diagrams. |
| [Mermaid](https://mermaid.js.org) | Write diagrams as text. GitHub renders Mermaid in markdown, which is how the diagrams in this repo are made. |
| [Lucidchart](https://www.lucidchart.com) | Free tier available. |

In interviews, simple boxes and arrows are enough. Label every arrow with what flows through it.

---

## Build to learn: hands-on projects

Reading is not enough. Each of these projects teaches several building blocks. Use Docker Compose to run everything locally for free.

| Project | What you practise | Stack idea |
| ------- | ----------------- | ---------- |
| URL shortener | Hashing, key-value storage, caching, read-heavy scaling | App server, PostgreSQL or Redis, Nginx |
| Rate limiter middleware | Token bucket, Redis, atomic operations | Any web framework, Redis |
| Chat application | WebSockets, pub/sub, message storage, presence | Node or Spring Boot, Redis pub/sub, a database |
| Job queue / email sender | Message queues, retries, idempotency, dead-letter queues | RabbitMQ or Kafka, a worker process |
| News feed (small scale) | Fan-out on write vs read, caching, pagination | App server, Redis lists or sorted sets, PostgreSQL |
| Load-balanced app | Reverse proxy, health checks, stateless services | 3 app containers behind Nginx |
| Search service | Inverted index, relevance, indexing pipeline | Elasticsearch or OpenSearch with a small dataset |
| RAG chatbot | Embeddings, vector search, retrieval, LLM calls | See the [AI/ML/LLM roadmap](https://github.com/DivaQueen-dev/free-ai-ml-llm-roadmap) |

Load test what you build with [k6](https://k6.io) (free and open source). Watch where it breaks first: the CPU, the database, the network, or your code. That is how bottleneck intuition is built.

---

## Low-level design (LLD)

Many interviews, especially in India, include an object-oriented design round: design a parking lot, a library system, an elevator, a vending machine, a chess game. These test OOP, design patterns, and clean code rather than distributed systems.

| Resource | What it is |
| -------- | ---------- |
| [Refactoring Guru: Design Patterns](https://refactoring.guru/design-patterns) | Clear explanations of all the classic design patterns with examples. |
| [Awesome Low Level Design](https://github.com/ashishps1/awesome-low-level-design) | A curated GitHub repo of LLD problems with solutions in several languages. |
| [MIT OCW](https://ocw.mit.edu) | Software construction and object-oriented courses. |

A simple approach to LLD questions:

1. Clarify requirements and the scope.
2. Identify the main entities (nouns) and their relationships.
3. Define responsibilities and interfaces (verbs).
4. Apply the SOLID principles. Use a design pattern only where it clearly fits (for example, Strategy for pricing rules, Observer for notifications, State for a vending machine).
5. Write the key classes and walk through a use case.

---

## Study plans

### 2 weeks: crash course (for an interview coming up soon)

```
Days 1-2:   Read INTERVIEW_GUIDE.md. Skim FUNDAMENTALS.md sections 1-8.
Days 3-5:   Finish FUNDAMENTALS.md. Make a one-page cheat sheet in your own words.
Days 6-8:   Do 3 case studies from CASE_STUDIES.md: URL shortener, chat, news feed.
            For each: solve on paper for 40 minutes first, then compare.
Days 9-11:  Do 3 more: rate limiter, notification system, file storage.
Days 12-13: Two timed mock interviews with a friend or Discord partner.
Day 14:     Review your mistakes and revise the trade-off tables.
```

### 4 weeks: solid prep

```
Week 1: Fundamentals sections 1-8 (scaling, networking, load balancing, caching, CDN,
        databases, replication, sharding). Watch ByteByteGo and Gaurav Sen videos alongside.
Week 2: Fundamentals sections 9-17 (CAP, messaging, API design, reliability,
        distributed concepts, patterns). Build the URL shortener project.
Week 3: Interview guide + 6 case studies. Read one engineering blog post per day.
Week 4: 4 more case studies, 3 timed mocks, behavioural prep, final revision.
```

### 8 weeks: thorough (including hands-on work)

```
Weeks 1-2: Fundamentals, read carefully. Take notes in your own words.
Weeks 3-4: Build 2 projects (URL shortener + chat app). Load test them.
Weeks 5-6: 10 case studies. Read the Dynamo and Raft papers. Start MIT 6.824 lectures.
Week 7:    Engineering blog deep dives on 5 companies. 4 mock interviews.
Week 8:    Final revision, weak-topic review, 2 more mocks.
```

---

## How to practise a design problem

For every problem in [CASE_STUDIES.md](CASE_STUDIES.md), follow this loop:

1. **Solve it alone first.** Set a 40-minute timer. Use paper or Excalidraw. Don't peek.
2. **Say it out loud.** Explain your design to a friend, a rubber duck, or a recording.
3. **Compare.** Read the worked solution and note what you missed.
4. **Write a one-page summary** in your own words: requirements, estimates, diagram, top 3 trade-offs.
5. **Revisit** after a week. Try again from scratch with a different twist (10x more traffic, a new requirement).

Keep a design journal. Over time, you will notice the same building blocks recurring. That repetition is the real learning.

---

## Progress tracker

**Fundamentals**
- [ ] Latency, throughput, availability, consistency
- [ ] Vertical vs horizontal scaling, stateless services
- [ ] Back-of-envelope estimation
- [ ] DNS, HTTP, TCP, WebSockets
- [ ] Load balancing and reverse proxies
- [ ] Caching strategies and problems
- [ ] CDNs
- [ ] SQL vs NoSQL and database types
- [ ] Indexes
- [ ] Replication
- [ ] Sharding and consistent hashing
- [ ] CAP and consistency models
- [ ] Message queues and event streams
- [ ] Delivery semantics and idempotency
- [ ] API design, pagination, rate limiting
- [ ] Reliability patterns (retries, circuit breakers)
- [ ] Observability (metrics, logs, traces)
- [ ] Security basics
- [ ] Distributed concepts (consensus, quorum, clocks)
- [ ] Microservice patterns (saga, outbox, CQRS)

**Case studies**
- [ ] URL shortener
- [ ] Rate limiter
- [ ] News feed
- [ ] Chat application
- [ ] Notification system
- [ ] Web crawler
- [ ] Autocomplete
- [ ] File storage and sync
- [ ] Video streaming
- [ ] Ride sharing
- [ ] Ticket booking
- [ ] Payment system
- [ ] RAG chatbot

**Milestones**
- [ ] Built and load-tested one project
- [ ] Read 10 engineering blog posts
- [ ] Completed 5 timed mock interviews
- [ ] Wrote a one-page summary for 10 case studies

---

## Common mistakes

- **Jumping straight to the architecture.** Always clarify requirements and estimate scale first.
- **Name-dropping technologies without reasons.** Saying "I'll use Kafka" is weak. Saying "I'll use Kafka because we need durable, replayable events and consumers at different speeds" is strong.
- **Designing for Google scale when the requirements are small.** A single database might be perfectly fine. Say so, and scale only when the numbers demand it.
- **Ignoring failure.** What happens when a server, a database, or a network link dies? Good designs answer this.
- **Never stating trade-offs.** Every choice costs something. Say what you give up.
- **Skipping the data model and API.** They anchor the rest of the design.
- **Silent thinking.** Interviewers can only grade what you say. Narrate your reasoning.
- **Memorising solutions.** Interviewers change requirements. Understand the building blocks instead.

---

## FAQ

**Do freshers need system design?**
Usually only basics (how a web app scales, caching, SQL vs NoSQL), plus LLD. Full HLD rounds are more common from around 2 to 3 years of experience, but learning the basics early is a big advantage.

**Do I need to read Designing Data-Intensive Applications?**
It is an excellent book, but it is not free and not required. The resources here cover the same ideas at interview depth. If your college library has it, the chapters on replication, partitioning, and consistency are worth reading.

**Which technology should I pick in an interview?**
Pick what you can justify. Interviewers care about your reasoning, not whether you chose PostgreSQL or MySQL. Know one relational database, one key-value store (Redis), one message system (Kafka or RabbitMQ), and one object store (S3) well.

**How deep should I go?**
Go deep enough to explain how something works and when it fails. For example: not just "use consistent hashing", but why it reduces data movement when nodes join or leave.

**How is system design different from learning microservices?**
Microservices are one architectural style. System design is the broader skill of choosing the right architecture, including when a monolith is the better answer.

**Can I get good without working at a big company?**
Yes. Build projects, read engineering blogs, and practise on case studies. The concepts are the same at any scale.

---

## Contributing

Found a better resource, a broken link, or an error? Open an issue or a pull request.

We accept: free resources you have personally verified, with a clear description, in the right section.
We don't accept: paid resources, affiliate links, or low-quality content.

---

## Related repos

| Repo | What's inside |
| ---- | ------------- |
| [free-cs-roadmap](https://github.com/DivaQueen-dev/free-cs-roadmap) | The main hub: all domains, resume tips, getting hired |
| [free-dsa-roadmap](https://github.com/DivaQueen-dev/free-dsa-roadmap) | DSA patterns, notes, problem lists |
| [free-ai-ml-llm-roadmap](https://github.com/DivaQueen-dev/free-ai-ml-llm-roadmap) | AI/ML, deep learning, RAG and LLMs |

---

Built for students who deserve a fair shot but can't afford a paywall. If this helped you, share it with one person who needs it and star the repo.

[Join Discord](https://discord.gg/ETCSm74A59)
