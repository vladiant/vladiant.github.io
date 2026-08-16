---
layout: post
title: "Software Architect Prompt"
date: 2026-08-17    
tags: development ai
---

## General Definition
* Role: Senior Software Architect.
* Objective: Review, design, and plan software systems for high maintainability, scalability, and security.
* Responsibilities:
* Architecture Design: Create system architectures, database schemas, and API designs based on project requirements.
* Best Practices: Enforce clean architecture principles, SOLID principles, and design patterns.
* Analysis: Analyze codebases to identify technical debt, bottlenecks, and security vulnerabilities (treating them as if a junior developer wrote the code).
* Diagramming: Generate Mermaid.js diagrams to visualize architectural changes, database relationships, and component interactions.
* Documentation: Produce clear technical documentation and decision logs (ADRs).
* Interaction Guidelines:
   * Ask First: Before offering a solution, ask clarifying questions about requirements and constraints.
   * Justify Decisions: Explain the trade-offs of the proposed architecture.
   * Iterative Review: Review code against a rubric (Clarity, Security, Performance) and provide actionable feedback.
   * Tone: Professional, analytical, and objective.

### The "Architect Planner" (For Feature Planning)

```
You are the Principal Architect. Based on the requirement {{feature_description}}, create a technical design document. Include a database schema (in Mermaid), an API contract, and a step-by-step implementation plan for the developer agent, identifying potential bottlenecks or security risks.
```

### The "Code Reviewer" (For Quality Assurance)

```
Act as a security and performance expert. Review this code: {{code}}.
1. Identify critical security vulnerabilities.
2. Find areas for optimization (uncalled code, performance bottlenecks).
3. Propose a refined structure using SOLID principles
```

## [Top 100 Prompts for Architect Best Use of GitHub Copilot](linkedin.com/posts/arun-kumar-singh-87437a125_githubcopilot-softwarearchitecture-cloudarchitecture-activity-7428706322226876416-pLF_)


### **1. System Design & Architecture**
1. Design a scalable architecture for a multi-tenant SaaS application handling thousands of users.
2. Generate a high-level architecture for an event-driven microservices system using Kafka.
3. Compare monolith vs microservices for this use case: [describe system].
4. Design a fault-tolerant architecture for a payment processing system.
5. Create a CQRS - Event Sourcing architecture for an order management system.
6. Design a globally distributed system with low latency architecture.
7. Suggest an architecture system for legacy modernization.
8. Design a highly resilient system for regional cloud outages.

### **2. Cloud Architecture**
1. Design AWS architecture for a highly available SaaS application.
2. Generate Terraform for a VPC with public/private subnets. Suggest cost-optimized cloud design for variable traffic.
3. Design serverless architecture for image processing pipeline. Compare serverless vs containers for image processing.
4. Generate Kubernetes manifests for multi-region clusters.
5. Propose cloud migration strategy for auto-scaling patterns.
6. Design infrastructure diagram for Load Balancer.
7. Redesign architecture to optimize for cost.
8. Design automated deployment pipeline.
9. Design blue-green deployment pipeline.

### **3. Microservices & APIs**
1. Design API versioning strategy for backward compatibility. Generate REST API contract for frontend.
2. Generate REST vs GraphQL for this scenario. Compare service-to-service communication strategy.
3. Design microservices architecture resilience & mesh.
4. Compare API Gateway vs circuit breaker pattern.
5. Generate OpenAPI spec for backend.
6. Propose authentication networking strategy.
7. Design API rate limiting strategy.
8. Create auto-scaling strategy for microservices.
9. Design event-driven communication.
10. Design idempotent APIs for payments.

### **4. Performance & Scalability**
1. Identify bottlenecks in this design: [description].
2. Design horizontal scaling strategy.
3. Generate load balancing approach.
4. Design cache architecture strategy.
5. Design websocket strategy for real-time updates.
6. Design write-through caching strategy for DB.
7. Generate performance testing requirements.

### **5. Reliability & Resilience**
1. Design failure handling strategy.
2. Generate circuit breaker implementation.
3. Design retry and timeout logic for services.
4. Design backpressure handling strategy.
5. Design disaster recovery plan.
6. Determine requirements for high availability.
7. Design chaos engineering experiments.

### **6. Data & Storage**
1. Design database schema for [domain model].
2. Generate SQL vs NoSQL for this scenario.
3. Compare SQL vs NoSQL for high-performance apps.
4. Design indexing strategy for tables.
5. Design data partitioning strategy.
6. Create data migration plan for legacy systems.
7. Design database replication strategy.

### **7. Security & Compliance** (labeled as Performance & Scalability in image)
1. Design authentication & authorization architecture.
2. Compare OAuth vs JWT for this app.
3. Design security hardening strategy.
4. Design encryption management requirements.
5. Design secure session management strategy.
6. Design data masking strategy.

### **8. DevOps & CI/CD**
1. Generate CI/CD pipeline for microservices.
2. Compare Git branching strategy.
3. Generate a release strategy.
4. Design monitoring and logging architecture.
5. Design observability strategy.
6. Generate error management strategy.

### **9. Code Quality & Patterns**
1. Refactor this code for SOLID principles.
2. Apply design patterns to this code.
3. Change direct architecture dependencies.
4. Improve maintainability for this module.
5. Design clean code refactoring.
6. Optimize performance for this module.
