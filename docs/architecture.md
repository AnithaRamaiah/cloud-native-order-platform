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
 
Trade-off: Increased operational complexity, mitigated via automation and observability.
