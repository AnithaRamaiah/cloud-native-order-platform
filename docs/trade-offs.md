# Architectural Trade-offs
 
## Consistency vs Availability
The system favors **eventual consistency** for improved availability and scalability.
 
 
## Simplicity vs Flexibility
A hybrid communication model is used to avoid over-engineering while maintaining flexibility.
 
 
## Operational Complexity
Microservices introduce operational overhead, which is mitigated using:
- Containerization
- Kubernetes
- Centralized observability
 
 
## Build vs Buy
In real-world scenarios, managed cloud services would replace many self-managed components.
