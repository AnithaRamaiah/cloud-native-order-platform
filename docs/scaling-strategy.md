# Scaling Strategy

## Phase 1 – Vertical Scaling
- Increase CPU and memory
- Optimize database indexing
- Tune JVM and connection pools

Limitation:
Hardware ceiling reached eventually.

---

## Phase 2 – Horizontal Scaling

### Application Layer
- Increase pod replicas
- Kubernetes HPA based on CPU and custom metrics

### Messaging Layer
- Increase partition count
- Enable producer batching
- Use compression
- Tune message size

### Database Layer
- Introduce sharding
- Shard based on customer_id
- Write distribution across nodes

---

## Stream Optimization

Focus Areas:
- Producer batching
- Partition count
- Message compression

Goal:
Reduce IO overhead and increase parallelism.
