# Architectural Trade-offs
 
# Architectural Trade-offs

## Consistency vs Availability

The system prioritizes availability and scalability.
Eventual consistency is accepted for distributed workflows.

---

## Simplicity vs Scalability

A monolith would simplify development but limit scalability.
Microservices increase operational overhead but allow independent scaling.

---

## Vertical Scaling vs Horizontal Scaling

Vertical scaling is used initially for simplicity.
Beyond hardware limits, sharding and partitioning enable horizontal scale.

---

## Synchronous vs Asynchronous Communication

Synchronous:
- Simpler reasoning
- Immediate consistency

Asynchronous:
- Better scalability
- Failure isolation

Hybrid approach used based on business need.

---

## Build vs Buy

For production:
- Managed Kafka
- Managed databases
- Managed Kubernetes

In learning/demo:
- Self-managed components used for deeper understanding.
