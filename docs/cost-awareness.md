# Cost Awareness & Infrastructure Trade-offs

This document evaluates architectural decisions from a cost perspective.

---

## Core Cost Drivers

1. Compute (Kubernetes nodes)
2. Kafka cluster
3. Database shards
4. Storage (hot + cold)
5. Data transfer
6. Redis caching layer

---

## Managed vs Self-Managed Services

### Managed Kafka (e.g., MSK)
Pros:
- Operational simplicity
- Automated scaling
- Built-in monitoring

Cons:
- Higher direct cost

### Self-Managed Kafka
Pros:
- Lower infra cost
- Greater tuning flexibility

Cons:
- Higher operational overhead
- Increased reliability risk

Decision:
Production environments favor managed services to reduce operational burden.

---

## Partition Over-Provisioning Trade-off

More partitions:
- Better parallelism
- Improved scalability

But:
- Higher broker memory usage
- Increased metadata overhead

Strategy:
Provision 30% headroom instead of aggressive over-partitioning.

---

## Sharding Cost Considerations

More shards:
- Higher infrastructure cost
- Increased replication storage

But:
- Better write scalability
- Reduced contention

Approach:
Scale shards based on sustained 70% utilization rule.

---

## Caching vs Database Cost

Redis reduces:
- Cross-service queries
- Database read amplification
- Latency spikes

Although Redis adds memory cost,
It reduces database scaling cost long-term.

---

## Storage Tiering Strategy

Hot storage (7 days):
- Fast SSD-backed volumes

Cold storage:
- Object storage (lower cost per GB)
- Used for analytics and archival

This optimizes performance-cost balance.

---

## Observability Cost

Metrics, logs, and traces increase storage cost.

Mitigation:
- Log retention policy
- Sampling for tracing
- Metrics cardinality control

---

## Cost Governance Principles

- Avoid scaling beyond 70% sustained utilization
- Scale based on measurable bottlenecks
- Optimize before adding infrastructure
- Prefer architectural optimization over brute-force scaling

---

## Conclusion

The architecture balances:

- Performance
- Reliability
- Scalability
- Operational cost

Cost is treated as a first-class architectural constraint.
