# Capacity Planning & Throughput Estimation

This document provides quantitative reasoning behind scaling decisions.

---

## Assumptions

- 5000 concurrent users
- Average 2 write operations per second per active user
- Peak load multiplier: 2x normal traffic
- Average event size: 2 KB

---

## Peak Write Throughput Calculation

Concurrent active users = 5000  
Avg writes/sec per user = 2  

Base write throughput:
5000 × 2 = 10,000 writes/sec

Applying peak multiplier (2x):

Peak throughput = 20,000 writes/sec

---

## Network Throughput Requirement

Event size = 2 KB  

20,000 × 2 KB = 40,000 KB/sec  
= ~40 MB/sec ingress traffic to Kafka

---

## Kafka Partition Sizing

Assumption:
One partition can reliably handle ~10 MB/sec sustained throughput.

Required partitions:
40 MB/sec ÷ 10 MB/sec ≈ 4 partitions minimum

To allow headroom and parallelism:
Configured partitions per topic: 8–12

This supports:
- Parallel consumers
- Future traffic growth
- Reduced consumer lag

---

## Database Capacity Planning

Peak writes = 20,000 writes/sec

Assuming:
- Each shard handles 5,000 writes/sec safely

Required shards:
20,000 ÷ 5,000 = 4 shards minimum

Sharding Key:
customer_id (ensures write distribution)

---

## Storage Growth Estimation

Assuming:
- 20,000 events/sec during peak
- 5,000 events/sec average sustained
- 2 KB per event

Average daily data:

5,000 × 2 KB × 60 × 60 × 24  
≈ 864 GB/day (event stream before retention policy)

Retention Strategy:
- Hot storage: 7 days
- Cold storage archival beyond 7 days

---

## Autoscaling Strategy

Application Pods:
- Scale based on CPU and Kafka consumer lag

Kafka Consumers:
- HPA triggered when consumer lag > threshold

Database:
- Shard-based horizontal scale
- Connection pool tuning to avoid saturation

---

## Headroom Policy

System operates at:
Maximum 70% sustained capacity

Reason:
- Handle traffic spikes
- Reduce tail latency
- Prevent cascading failures

---

## Conclusion

Capacity planning ensures:
- Predictable scaling
- No single-node bottleneck
- Controlled infrastructure growth
- Data-driven partition and shard decisions
