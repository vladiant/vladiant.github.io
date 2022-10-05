---
layout: post
title: "Software Flow Management"
date: 2022-10-05
tags: design ci cd
---

## Management styles
| Feature | Pathological | Bureaucratic | Generative |
|---------|--------------|--------------|------------|
| Main | Power-Oriented | Rule-Oriented | Performance-Oriented |
| Cooperation | Low | Modest | High |
| Messengers | "shot" (blamed) | Neglected | Trained |
| Responsibilities | Shirked | Narrow | Risks are shared |
| Bridging (communication acrosss teams/silos) | Discouraged | Tolerated | Encouraged |
| Failure | Leads to scapegoating | Leads to justice | Leads to inquiry |
| Novelty | Crushed | Leads to problems | Implemented |

## How defects are prevented

### Pre-commit
* Design
* Design review
* Implementation
* Unit testing
* Code review
* Static analysis
* Repeat unit testing
* Submit

### Commit
* Post-commit CI
* Dynamic analysis
* Integration testing
* Release qualification

### Deploy
* Canary release
* Full deploy!
* Signals based monitoring and alerting
* End-to-end monitoring

## Reference
* [Tradeoffs in the Software Workflow - Titus Winters - ACCU 2022](https://www.youtube.com/watch?v=l6Q7XaTleyI)
