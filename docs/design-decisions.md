# Design Decisions & Rationale
 
## Why Event-Driven Architecture?
- Reduces tight coupling between services
- Improves system resilience
- Enables horizontal scalability
 
Trade-off: Eventual consistency and increased debugging complexity.

 
## Why Database Per Service?
- Prevents shared data coupling
- Allows independent schema evolution
- Enables better ownership boundaries
 
Trade-off: Complex cross-service queries, addressed via events and APIs.
 
 
## Why API Gateway?
- Centralized security
- Simplified client interactions
- Better traffic control and monitoring
 
Trade-off: Gateway becomes a critical component; mitigated through redundancy.
 
 
## Why Spring Boot?
- Mature ecosystem
- Strong community support
- Production-proven in enterprise systems
