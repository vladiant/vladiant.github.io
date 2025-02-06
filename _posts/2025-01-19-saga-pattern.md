---
layout: post
title: "Saga Design Pattern"
date: 2025-01-19
tags: design development
---

## Context
* Database per Service
* Some business transactions span multiple service

## Problem
* Implement transactions that span services
* [Two-Phase Commit](https://martinfowler.com/articles/patterns-of-distributed-systems/two-phase-commit.html) is not an option - due to synchronous blocking

## Solution
* A saga is a sequence of local transactions.
* Each local transaction updates the database and publishes a message or event to trigger the next local transaction in the saga. 
* If a local transaction fails because it violates a business rule then the saga executes a series of compensating transactions that undo the changes that were made by the preceding local transactions.

## Concepts
### Compensable transactions
Transactions that other transactions can undo or compensate for with the opposite effect.

### Pivot transaction
Once the pivot transaction succeeds, compensable transactions (which could be undone) are no longer relevant.

### Retryable transactions
Idempotent and ensure that the saga can reach its final state, even if temporary failures occur. It guarantees that the saga achieves a consistent state eventually.

## Choreography-based saga
* Event driven
* Each local transaction publishes domain events that trigger local transactions in other services.
* Saga participants subscribe to each other’s events and respond accordingly.
* Good for simple workflows with few services

## Orchestration-based saga
* Command driven
* State machine
* An orchestrator is responsible to tell saga participants what to do.
* Better suited for complex workflows or when adding new services.
* Better suited for synchronous communication

## Versioning
* The workflow emerges from event chains
* How would a new version affect in-flight workflows?
* Versioning may affect multiple services

## Benefits
* Enables an application to maintain data consistency across multiple services without using distributed transactions
* No blocking due to signle participant
* Gracful handling of failures
* Supports async processing
* Scalable
* Standardized way to handle errors and transactions

### Choreography
* Simplicity
* Loose coupling
* No single point of failure
* Easy to Scale
* No temporal coupling (async)
* No control coupling

### Orchestration
* Simpler dependencies (no cyclic dependencies)
* Less coupling (no need to know published events or business logic implemented by other participants)

## Drawbacks
* The lack of isolation between Sagas.
* Lack of automatic rollback
* Complicated implementation
* Additional latency due to steps coordination

### Choreography
* Difficulty in understanding the flow
* Cyclic dependencies between services
* Difficult integration testing

### Orchestration
* Requires implementation of coordination logic 
* Single point of failure

## Challenges

### Rolling back changes when an error happens within a Saga.
Requires compensating transactions.

### Lost Updates
One saga overwrites an update made by another saga.

### Dirty Reads
One saga reads data that is in the middle of being updated by another saga.

### Fuzzy / Non-repeatable Reads
Two different sets of a saga read the same data and get different results because another saga has made updates.

## Design considerations

### Asynchronous flow
1. The service sends back a response once the saga completes.
2. The service sends back a response after initiating the saga and the client periodically polls to determine the outcome
3. The service sends back a response after initiating the saga, and then sends an event to the client once the saga completes.

### A service must atomically update its database and publish a message/event.

### Compensating transactions 
Should be designed to explicitly undo changes made earlier in a saga rather than relying on the automatic rollback feature of ACID transactions. They may not always succeed.

### Semantic Lock
Use application-level locks where a saga's compensable transaction uses a semaphore to indicate an update is in progress.

### Commutative Updates
Designing the system to have more its update operations to be commutative (updates in an orderly manner). This can basically eliminate lost updates.

### Pessimistic View
Reordering saga participants/services to minimize the effect of dirty reads.

### Reread Values
This countermeasure reread values before updating it to further to re-verify the values are unchanged during the process. This will minimize lost updates.

### Version files
Maintain a log of all operations on a record and ensure they're executed in the correct sequence to prevent conflicts.

### By Value
This strategy will select concurrency mechanisms based on the business risk. This can help to execute low-risk requests using sagas and execute high-risk requests using distributed transactions.

## References
* [Pattern: Saga](https://microservices.io/patterns/data/saga.html)
* [Microservices Patterns: The Saga Pattern](https://medium.com/cloud-native-daily/microservices-patterns-part-04-saga-pattern-a7f85d8d4aa3)
* [SAGA Design Pattern](https://www.geeksforgeeks.org/saga-design-pattern/)
* [Saga Pattern in Microservices](https://www.baeldung.com/cs/saga-pattern-microservices)
* [Saga distributed transactions pattern](https://learn.microsoft.com/en-us/azure/architecture/reference-architectures/saga/saga)
* [Orchestration vs. Choreography: The good, the bad, and the trade-offs - Laila Bougria - NDC Oslo](https://www.youtube.com/watch?v=Jfwriqqkwi4)
* <https://github.com/Azure-Samples/saga-orchestration-serverless>