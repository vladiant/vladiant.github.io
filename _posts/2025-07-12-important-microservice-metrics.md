---
layout: post
title: "Important Microsertvice Metrics"
date: 2025-07-12
tags: development design coding
---

## 1. Latency
* Average response time
* 95th and 99th percentile response times
* Dependency latency
* Establish acceptable latency ranges for different services

## 2. Throughput
* Number of successful requests processed per unit of time
* Requests per second
* Transactions per second

## 3. Error rates
* Percentage of failed requests
* Exception rates
* Dependency failure rates
* HTTP error codes (4xx and 5xx)

## 4. Resource utilization
* CPU and Memory Utilization
* Disk I/O and network I/O

## 5. Service availability and uptime
* Service uptime percentage
* Downtime incidents
* Health check status

## 6. Request tracing and dependency mapping
* Dependency Metrics
* Trace ID propagation
* Service dependency graphs
* Slow request paths
* Queue length, database query latency, or API call response time
* Inter-Service Communication

## 7. Network Metrics
* Network Traffic
* Network latency
* Bandwidth usage
* Network error rates

## 8. Container and orchestration metrics
* Container CPU and memory limits
* Pod restarts
* Node resource utilization
* Deployment frequency
* Rollback occurrences
* Deployment failure rates

## 9. Business KPIs
* Link operational metrics to business outcomes

## Best Practices
* Define clear Service Level Objectives and Agreements for performance and reliability targets
* Centralised Logging and Metrics
* Using Distributed Tracing
* Set Up Alerts and Notifications
* Automate Monitoring Processes
* Continuous Review and Optimization

## Reference
* [Essential metrics for robust microservices performance monitoring](https://blogs.manageengine.com/application-performance-2/appmanager/2025/04/07/essential-metrics-for-robust-microservices-performance-monitoring.html)
* [Mastering Microservices Monitoring](https://middleware.io/blog/microservices-monitoring/)
* [Key Metrics to Monitor in a Microservices Application](https://article.arunangshudas.com/key-metrics-to-monitor-in-a-microservices-application-9bf09b46d085)
