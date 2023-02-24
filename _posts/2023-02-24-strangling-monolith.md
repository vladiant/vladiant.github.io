---
layout: post
title: "Strangling The Monolith"
date: 2023-02-24
tags: design
---

## Improvement process

### 1. Identify the most valuable coponents and their boundaries
* Create, merge, split, and release capabilities
* Success pattern: Wardley Mapping https://learnwardleymapping.com/portfolio/wardley-mapping-canvas/
* Success pattern: Team Topologies and DDD https://github.com/ddd-crew/core-domain-charts

### 2. Align the organisation around the future boundary cutmarks
* Success Pattern: Inverse-Conway Maneuver https://ctocraft.com/blog/how-can-the-inverse-conway-manoeuvre-help-drive-organisational-change/
* Success Pattern: Explicit ownership transfer

### 3. Measure and analyse the current system's migration complexity.
* Identify the low hanging fruits
* Success Pattern: Code analysis - Static, Behavioral, Risk

### 4. Pick the mext most valuable component and start the migration.
* Success Pattern: Collaborative Discovery
* Success Pattern: Tracing Use Case Entrypoints
* Success Pattern: Rich Models
* Success Pattern: Strangler Facade

### 5. Finish that migration and go back to 4.

## Success Patterns summary
* Start with creating a new target picture based on strategic and economic factors. For us Wardley Maps, Strategic DDD and Team Topologies worked.
* Realign the organisation around the new system architecture. Inverse-Conway Maneuvers worked for us, but it is not for everyone since it isa huge social perturbation.
* Measure an analyze the code, the behaviours and risks before diving into implementation. You'll often find surprises!
* Design your new APIs using collaborative modelling and modern approaches. In the end, that's what modernization is all about.
* Leverage observability platforms and other tooltip to help find the entry points to the use cases you want to tackle - by analyzing the traces from the DB to the code entry-points.
* Tackle each of entry-points with the newly designed Strangler Facade. We used the Transactional Outbox pattern and asynchronous event integrations successfully.
* Continue while it is valuable for the organisation, but constantly inspect and adapt.

## References
* [Strangling The Monolith: Applied Patterns & Practices From The Trenches - Thomas Ploch](https://www.youtube.com/watch?v=cGcrReJ6FbY)
* [Strangling The Monolith: Slides](https://slides.com/tploch/strangling-the-monolith-applied-patterns-practices-from-the-trenches)