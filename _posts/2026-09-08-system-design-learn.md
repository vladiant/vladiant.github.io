---
layout: post
title: "System Design Learning Plan"
date: 2026-09-08    
tags: design ai
---

4-Week System Design Study Plan

## Week 1 - Fundamentals: Scalability, Availability, Components

**Goal:** Build a mental model of what "system design" even covers before touching distributed systems specifics.

- **Day 1 - What is System Design?**
ByteByteGo's YouTube channel is the standard entry point, run by the authors of the *System Design Interview* book series.
<https://www.youtube.com/@ByteByteGo> - start with any "System Design Basics" or "How X Works" video from the channel.

- **Day 2 - Distributed Systems, Beginner Level**
[Distributed Systems Explained Simply | System Design for Software Engineer](https://www.youtube.com/watch?v=8Hoq7FmDsco)

- **Day 3–5 - Scalability, Load Balancing, Caching**
Web Journey with Kashish's playlist is real and covers exactly this
sequence (15 videos, fundamentals → advanced). Watch straight through rather than trusting specific video numbers for specific topics - the numbering wasn't independently verifiable. [System Design Tutorial Series (2025)](https://www.youtube.com/playlist?list=PL9-WUTizcelEMuKaXy7lx17RECaF4xfzQ)

**Weekend practice:** Pick a system (Twitter, YouTube, Instagram) and sketch APIs, data model, components, caching, and scaling approach. No correctness bar - just practice structured thinking.

---

## Week 2 - Distributed Systems, Data & Storage

**Goal:** Sharding, replication, CAP, queues, consistency.

- **Days 1–5 - SQL vs NoSQL, CAP theorem, sharding, replication, queues**
Continue the Web Journey with Kashish playlist above - it covers all five topics across its 15 videos.
[System Design Tutorial Series (2025)](https://www.youtube.com/playlist?list=PL9-WUTizcelEMuKaXy7lx17RECaF4xfzQ)

For a second, deeper pass on each concept, Hello Interview's Core Concepts section is excellent and unambiguous - useful if a playlist video is fuzzy on a topic: [System Design in a Hurry : Core Concepts](https://www.hellointerview.com/learn/system-design/in-a-hurry/core-concepts)

**Weekend deep dive:** Pick Kafka, RabbitMQ, or SQS and sketch how you'd
integrate it into a large system for resilience.

---

## Week 3 - Fault Tolerance, Resilience, Real-World Systems

**Goal:** Redundancy, graceful degradation, and a real large-scale case
study.

- **Days 1–3 - Failure handling, fault tolerance, reliability patterns**
  - GeeksforGeeks, [Failure Models in System Design (article)](https://www.geeksforgeeks.org/system-design/failure-models-in-system-design/)
  - [Reliability, Faults and Failures in Software Engineering (video)](https://www.youtube.com/watch?v=g4EnIOgYuHQ)

- **Day 4 - Real-World Architecture: YouTube**
[HLD, LLD, class structures, DB schema, API design - System Design of Youtube](https://www.geeksforgeeks.org/system-design/system-design-of-youtube-a-complete-architecture/)

- **Day 5 - Microservices Architecture**
[How to Migrate from Monolith to Microservices (Step-by-Step)](https://www.youtube.com/watch?v=nQ-GLrCf020) - covers benefits/trade-offs along the way.


**Weekend journal:** How would you make YouTube more fault tolerant? Think CDN failures, DB failover, cache invalidation, hotspots.

---

## Week 4 - Trade-Offs & Interview Mastery

**Goal:** Architect-level reasoning and interview-format practice.

- **Day 1 - Monolith to Microservices (deeper)**
[𝗠𝗶𝗴𝗿𝗮𝘁𝗶𝗻𝗴 𝗳𝗿𝗼𝗺 𝗠𝗼𝗻𝗼𝗹𝗶𝘁𝗵𝗶𝗰 𝗔𝗿𝗰𝗵𝗶𝘁𝗲𝗰𝘁𝘂𝗿𝗲 𝘁𝗼 𝗠𝗶𝗰𝗿𝗼𝘀𝗲𝗿𝘃𝗶𝗰𝗲𝘀 𝗛𝗮𝗻𝗱𝘀-𝗢𝗻 𝗥𝗲𝗮𝗹-𝗪𝗼𝗿𝗹𝗱 𝗖𝗮𝘀𝗲 𝗦𝘁𝘂𝗱𝘆](https://www.youtube.com/playlist?list=PLjzEd-em7iW-NBbVyI3SskmPixrxfO0My)

- **Day 2 - Interview Roadmap**
Hello Interview's *How to Prepare* page.
[How to Prepare for System Design Interviews](https://www.hellointerview.com/learn/system-design/in-a-hurry/how-to-prepare)

- **Day 3 - Consolidation**
Consolidating before interview practice.
<https://www.youtube.com/@ByteByteGo>

- **Day 4 - Advanced Systems Thinking**
Conference (TigerBeetle's Systems Distributed), talks land on YouTube after each event - search "Systems Distributed" + year on YouTube for the current batch 
<https://systemsdistributed.com>

- **Day 5 - Trade-Off Master Class**
Built by FAANG hiring managers/staff engineers specifically to teach trade-off reasoning under interview constraints.
[System Design in a Hurry - Introduction](https://www.hellointerview.com/learn/system-design/in-a-hurry/introduction)

**Weekend capstone:** Design one from scratch - Twitter Timeline, Uber, Instagram, or YouTube (deeper this time). 
Cover: requirements, capacity estimates, components, DB/schema, scaling, caching, fault tolerance, trade-offs (why X over Y).
