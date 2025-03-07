---
layout: post
title: "Two Phase Commit Protocol"
date: 2025-03-07
tags: design development
---

## Context
* Distributed transaction updates data across multiple systems or databases.
* Data needs to be atomically stored on multiple cluster nodes
* Nodes cannot make the data accessible to clients until the decision of other cluster nodes is known. 
* Each node needs to know if other nodes successfully stored the data or if they failed.
* Assume that each site logs actions at that site, but there is no global log.

## Problem
* Keep data accurate across all systems (consistency)
* Make sure all parts of a transaction succeed or fail together (atomicity)

## Solution
* To ensure atomicity property Transaction must either commit at all the sites, or it must abort at all sites. 
* The protocol has two phases: Prepare and Commit/Abort
* Phase 1 - Coordinator sends a Prepare message to all the sites where the Transaction is executed. Each site must eventually send a response
* Phase 2 - Response abort or commit received by the Coordinator from all the sites that are collaboratively executing the transaction.

## Concepts
* Transaction - Prepare, Commit, Abort
* Coordinator - First asks sites to prepare their part. Then asks to commit when all agreed, asks to abort when all disagreed. Waits for all to respond.
* Sites - Responds to prepare by lock resources, prepare data changes and check if they can finish.

## Benefits
* Guarantees data consistency
* Guarantees data atomicity
* Handles failures

## Drawbacks
* Coordinator site failure may result in blocking
* Impossible to determine what decision has been made if the Coordinator fails and the active sites keep no additional log-record
* Can negatively impact system performance

## Challenges
* Blocking Problem - the locked data items remain inaccessible for other transactions until the Coordinator is restored or fixed
* Keeping data in sync across systems
* Dealing with network problems
* Handling partial failures
* Coordinating all systems involved

## Design considerations
* Consider coordinator failure after prepare message - set a timeout, then check other sites.
* Consider site failure - should others continue?
* Set timeouts for responses
* Keep good logs
* Have a manual fix plan
* Use query messages for the status of coordinator and sites
* Handle system / network failures

## References
* [Two Phase Commit Protocol : Distributed Transaction Management](https://www.geeksforgeeks.org/two-phase-commit-protocol-distributed-transaction-management/)
* [Two-Phase Commit](https://martinfowler.com/articles/patterns-of-distributed-systems/two-phase-commit.html)
* [Two-Phase Commit Protocol Explained](https://endgrate.com/blog/two-phase-commit-protocol-explained)
