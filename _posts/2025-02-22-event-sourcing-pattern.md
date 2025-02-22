---
layout: post
title: "Event Sourcing Design Pattern"
date: 2025-02-22
tags: design development
---

## Context
* A service command needs to create/update/delete (CRUD) aggregates in the database _and_ send messages/events to a message broker.
* Not viable to use a traditional distributed transaction (two phase commit)
* Messages must be sent to the message broker in the order they were sent by the service.
* Undesirable to couple the service to both the database and the message broker.

## Problem
* Atomically update the database and send messages to a message broker
* CRUD Performance: As the system scales, the performance will degrade due to contention for resources and locking issues.
* CRUD Scalability: Data operations block on updates - bottlenecks and higher latency when the system is under load.
* CRUD Auditability: Systems only store the latest state of the data.

## Solution
* The state of a business entity is persisted as a sequence of state-changing events.
* Saving an event is a single operation, it is inherently atomic.
* The application reconstructs an entity’s current state by replaying the events.
* The event store behaves like a message broker.
* To reconstruct the current state, the application finds the most recent snapshot and the events that have occurred since that snapshot.

## Concepts
* Events: Permanent records of system state changes.
* Event Sourcing: State is defined by a sequence of events.
* Event Publishing: Event is published whenever state changes
* Event Store: Applications persist events in an event store (database of events).
* Event Bus: Messaging infrastructure that enables system components to communicate about events.
* Snapshot: Periodically saved entity’s current state.

## Benefits
* Events are immutable and can be stored using an append-only operation.
* Provides a 100% reliable audit log of the changes made to a business entity
* Events are simple objects.
* Mostly avoids the object‑relational impedance mismatch problem avoided by persisting events rather than domain objects.
* Decoupling of the tasks from the events provides flexibility and extensibility.
* Event sourcing can help prevent concurrent updates from causing conflicts.
* Makes it possible to implement temporal queries that determine the state of an entity at any point in time.
* Makes easier to migrate from a monolithic application to a microservice architecture.

## Drawbacks
* Different and unfamiliar style of programming and so there is a learning curve.
* The event store is difficult to query since it requires typical queries to reconstruct the state of the business entities.
* The applications must handle eventually consistent data.

## Challenges
* The only way to update an entity or undo a change is to add a compensating event to the event store.
* The consistency of events in the event store is vital.
* There's no standard approach for reading the events to obtain information. 
* The current state of an entity can be determined only by replaying all of the events that relate to it against the original state of that entity.
* Deal with inconsistencies that result from eventual consistency and the lack of transactions.
* Be mindful of scenarios where the processing of one event involves the creation of one or more new events since this can cause an infinite loop.

## Design considerations
* Versioning events - events structures should support changes
* Event ordering - consider adding timestamp to event or annotate each event resulting from a request with an incremental identifier.
* Querying events - add event identifier
* Consider creating snapshots at specific intervals such as a specified number of events to reduce cost of state recreation.
* Handle conflicts by back order or setting consumer policy.
* Consumers of the events must be idempotent - must not reapply the update described in an event if the event is handled more than once. 

## References
* [Pattern: Event sourcing](https://microservices.io/patterns/data/event-sourcing.html)
* [Event Sourcing pattern](https://learn.microsoft.com/en-us/azure/architecture/patterns/event-sourcing)
* [Event Sourcing](https://martinfowler.com/eaaDev/EventSourcing.html)
* [Microservices Patterns: Event Sourcing](https://medium.com/cloud-native-daily/microservices-patterns-event-sourcing-7c6e765681c1)
* [Event Sourcing Pattern](https://www.geeksforgeeks.org/event-sourcing-pattern/)
* [What is Event Sourcing?](https://www.confluent.io/learn/event-sourcing/)
* [Event Sourcing Explained: Benefits, Challenges, and Use Cases](https://medium.com/@alxkm/event-sourcing-explained-benefits-challenges-and-use-cases-d889dc96fc18)