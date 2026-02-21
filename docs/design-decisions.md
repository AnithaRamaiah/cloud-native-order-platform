# Design Decisions & Rationale
 
# Design Decisions & Rationale

## Why Event-Driven Architecture?

- Services are loosely coupled
- Failures are isolated
- System can scale horizontally
- Enables asynchronous processing for write-heavy workloads

Trade-off:
- Eventual consistency
- Increased debugging complexity
- Requires strong observability

---

## Why Database Per Service?

- Prevents tight data coupling
- Independent schema evolution
- Clear ownership boundaries
- Enables service-level scaling strategies

Trade-off:
- Complex cross-service queries
- Requires events or API composition

---

## Why Sharding?

The system is write-heavy. Vertical scaling has hardware limits.

Sharding:
- Distributes write load
- Prevents single-node bottlenecks
- Enables horizontal scale beyond hardware constraints

Trade-off:
- Operational complexity
- Requires shard key strategy
- Complex migrations

---

## Why Redis as Secondary Index?

Global queries across services are expensive.

Redis:
- Fast lookup for aggregated views
- Reduces database stress
- Improves latency

Trade-off:
- Cache invalidation complexity
- Eventual consistency window

---

## Why Bulk Stream Processing?

Shift from individual message handling to bulk processing because:

- Reduces IO overhead
- Improves throughput
- Increases partition-level parallelism
- Enables compression efficiency

Trade-off:
- Slight latency increase
- Requires batching strategy tuning
