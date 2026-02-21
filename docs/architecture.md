# 📂 docs/architecture.md
 
```markdown
# Architecture Overview
 
## Architectural Style
The system follows a **microservices architecture** with:
- Independent deployability
- Decentralized data management
- Event-driven communication
 
This approach supports scalability, team autonomy, and faster evolution.
 
## Key Architectural Principles
 
1. **Single Responsibility per Service**
2. **Loose Coupling via Events**
3. **Infrastructure as Code**
4. **Cloud-first Design**
 
## Service Interaction Flow
 
1. Client sends request to API Gateway
2. Gateway authenticates and routes request
3. Order Service validates and creates order
4. OrderPlaced event is published
5. Payment and Inventory services react asynchronously
 
## Why Microservices?
 
Chosen to:
- Scale individual components independently
- Allow parallel team development
- Improve system resilience

## System Invariants

- An order must never be double charged.
- An order must eventually reach a terminal state.
- Payment and order state must not diverge permanently.
- Events must be idempotent.

## Failure Scenarios & Handling

- Payment crash after charge
- Duplicate event delivery
- Refund failure
- Broker lag
- DB shard imbalance

## Observability Strategy

- Trace propagation across async boundaries
- Business metrics vs infra metrics
- Stuck workflow detection
- Saga latency histogram
- Alert philosophy
 
Trade-off: Increased operational complexity, mitigated via automation and observability.
