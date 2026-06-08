# What is a Load Balancer?

A Load Balancer is a traffic manager that sits between clients and servers and distributes incoming requests across multiple servers.

## Simple Definition

Instead of all users hitting a single server:

```mermaid
graph LR
    Users((👥 Users)) --> Server1["🖥️ Server 1"]
```

We use:

```mermaid
graph LR
    Users((👥 Users)) --> LB["⚖️ Load Balancer"]
    LB --> Server1["🖥️ Server 1"]
    LB --> Server2["🖥️ Server 2"]
    LB --> Server3["🖥️ Server 3"]
```

The Load Balancer decides which server should process each request.

---

## Real-World Example (Amazon / Flipkart Sale)

Imagine Amazon's Great Indian Festival Sale.

### Without Load Balancer:

```mermaid
graph LR
    Users((100K Users)) --> Server1["🖥️ Server 1<br/>CPU:100%"]
```

Result:

❌ CPU 100%

❌ Memory Exhausted

❌ Website Crash

❌ Revenue Loss

### With Load Balancer:

```mermaid
graph LR
    Users((100K Users)) --> LB["⚖️ Load Balancer"]
    LB --> Web1["🖥️ Web-1<br/>CPU:33%"]
    LB --> Web2["🖥️ Web-2<br/>CPU:33%"]
    LB --> Web3["🖥️ Web-3<br/>CPU:33%"]
```

Result:

✅ Traffic distributed

✅ Faster response

✅ High availability

✅ No single point of failure

This is exactly why e-commerce platforms rely heavily on load balancing during peak events.

---

## Why Load Balancer is Needed?

### 1. High Availability

If one server crashes:

```
Server1 ❌
Server2 ✅
Server3 ✅
```

Traffic automatically shifts to healthy servers.

---

### 2. Traffic Distribution

Instead of:

```
Server1 = 1000 Requests
Server2 = 0
Server3 = 0
```

We get:

```
Server1 = 333
Server2 = 333
Server3 = 334
```

---

### 3. Better Performance

Users get faster response times because workload is shared.

---

### 4. Scalability

Add more servers:

```
3 Servers
   ↓
10 Servers
   ↓
50 Servers
```

No application redesign required.

---

### 5. Fault Tolerance

Failed servers are removed automatically using Health Checks.

---

## Load Balancer Architecture

```mermaid
graph TB
    Internet["🌐 Internet"]
    Internet --> LB["⚖️ Load Balancer"]
    LB --> App1["🖥️ App-1"]
    LB --> App2["🖥️ App-2"]
    LB --> App3["🖥️ App-3"]
    App1 --> DB["💾 Database"]
    App2 --> DB
    App3 --> DB
```

Flow:

1. User sends request
2. Request reaches Load Balancer
3. Load Balancer checks server availability
4. Selects best server
5. Sends response back

---

## Types of Load Balancers

### Layer 4 Load Balancer (Transport Layer)

Works on:

- TCP
- UDP

Looks at:

- IP Address
- Port Number

#### Example

```mermaid
graph LR
    Client["👤 Client"] --> LB["⚖️ LB<br/>Layer 4"]
    LB --> Server["🖥️ Server"]
```

LB only checks:

```
IP: 10.0.0.1
Port: 443
```

Does NOT inspect HTTP content.

#### Advantages

✅ Very Fast

✅ Low Latency

#### Examples

- NLB in AWS
- HAProxy TCP Mode

---

### Layer 7 Load Balancer (Application Layer)

Understands:

- HTTP
- HTTPS
- URL
- Headers
- Cookies

#### Example

```mermaid
graph LR
    LB["⚖️ LB<br/>Layer 7"]
    LB -->|/api/*| API["🔌 API Servers"]
    LB -->|/images/*| IMG["🖼️ Image Servers"]
    LB -->|/admin/*| ADMIN["👮 Admin Servers"]
```

#### Advantages

✅ Smart Routing

✅ SSL Termination

✅ Content-Based Routing

#### Examples

- Nginx
- Envoy
- AWS ALB

---

## Load Balancing Algorithms

### 1. Round Robin

Traffic distributed sequentially.

```
Request 1 -> Server 1
Request 2 -> Server 2
Request 3 -> Server 3
Request 4 -> Server 1
```

**Best when:**

- Servers have equal capacity

---

### 2. Least Connections

Request goes to server with least active connections.

**Example:**

```
Server1 = 100 Connections
Server2 = 20 Connections

Next Request -> Server2
```

**Best for:**

- Long-running requests

---

### 3. IP Hash

Same user always goes to same server.

```
User A -> Server 1
User B -> Server 2
```

**Useful for:**

- Session persistence

---

### 4. Weighted Round Robin

Powerful servers receive more traffic.

**Example:**

```
Server1 Weight = 5
Server2 Weight = 2
Server3 Weight = 1
```

**Traffic Distribution:**

```
Server1 = 62%
Server2 = 25%
Server3 = 13%
```

---

### 5. Least Response Time

Request goes to fastest server.

**Example:**

```
Server1 = 200ms
Server2 = 40ms
Server3 = 80ms

Request -> Server2
```

---

## Health Checks

One of the most important interview topics.

Load Balancer continuously checks:

```
/health
/status
/ping
```

**Response:**

```
200 OK
```

Server remains active.

**If:**

```
500 Error
```

Server removed from rotation.

---

## Load Balancer in Microservices

```mermaid
graph TB
    Internet["🌐 Internet"]
    Internet --> Gateway["🚪 API Gateway"]
    Gateway --> LB["⚖️ Load Balancer"]
    LB --> User["👤 User MS"]
    LB --> Order["📦 Order MS"]
    LB --> Payment["💳 Payment MS"]
```

**Benefits:**

- Better scaling
- Service isolation
- High availability

---

## Load Balancer in Cloud

### AWS

- Amazon Web Services ALB
- NLB
- Classic ELB

### Azure

- Microsoft Azure Load Balancer
- Application Gateway

### GCP

- Google Cloud Load Balancer

---

## Interview Diagram You Can Draw

```mermaid
graph TB
    Users((👥 Users))
    Users --> LB["⚖️ Load Balancer"]
    LB --> Server1["🖥️ Server 1"]
    LB --> Server2["🖥️ Server 2"]
    LB --> Server3["🖥️ Server 3"]
    Server1 --> DB["💾 Database"]
    Server2 --> DB
    Server3 --> DB
```

This diagram alone can help explain:

- High Availability
- Scalability
- Fault Tolerance
- Horizontal Scaling

---

## Top 10 Load Balancer Interview Questions & Answers

### Q1. What is a Load Balancer?

**Answer:** A Load Balancer distributes incoming traffic across multiple servers to improve availability, performance, and scalability.

---

### Q2. Why is Load Balancing Important?

**Answer:** It prevents server overload, improves response time, provides failover, and supports horizontal scaling.

---

### Q3. Difference Between Layer 4 and Layer 7 Load Balancer?

| Aspect             | Layer 4       | Layer 7              |
| ------------------ | ------------- | -------------------- |
| Works on           | TCP/UDP       | HTTP/HTTPS           |
| Speed              | Faster        | Slower               |
| Intelligence       | Less          | More (Content-aware) |
| Content Inspection | No            | Yes                  |
| Routing            | IP/Port based | URL/Header based     |

---

### Q4. What is Round Robin?

**Answer:** Requests are distributed sequentially among available servers in a circular manner.

---

### Q5. What is Least Connections?

**Answer:** Traffic is routed to the server with the fewest active connections at that moment.

---

### Q6. What is Sticky Session?

**Answer:** A user is consistently routed to the same server using cookies or IP hash, ensuring session persistence.

---

### Q7. What Happens When a Server Fails?

**Answer:** Health checks mark it as unhealthy and traffic is automatically redirected to healthy servers.

---

### Q8. What is SSL Termination?

**Answer:** The Load Balancer decrypts HTTPS traffic from clients and forwards HTTP traffic internally to servers, reducing their computational burden.

---

### Q9. How Does Load Balancer Improve Scalability?

**Answer:** New servers can be added to the pool without changing client applications or redeploying code.

---

### Q10. Design Load Balancer for Amazon During Black Friday Sale

**Expected Answer:**

- Use Layer 7 ALB (Application Load Balancer)
- Auto Scaling Group for dynamic scaling
- Multiple Availability Zones for geographic distribution
- Health Checks every 30 seconds
- CDN for static content delivery
- Cache Layer (Redis) to reduce database load
- Database Replication for read scalability
- Connection pooling
- Rate limiting to prevent abuse
- Monitoring and alerts

---

## Key Takeaways

✅ Load Balancer ensures **no single point of failure**

✅ Enables **horizontal scaling** without code changes

✅ Improves **performance** and **availability**

✅ Layer 4 is fast, Layer 7 is intelligent

✅ Always implement **health checks**

✅ Choose algorithm based on use case

✅ Essential for microservices and cloud architecture

---

# 2. Caching

## What is Caching?

Caching stores frequently accessed data in fast storage (memory) to reduce latency and database load.

```mermaid
graph LR
    Client["👤 Client"]
    Cache["⚡ Cache (Redis)"]
    DB["💾 Database"]

    Client -->|Request| Cache
    Cache -->|Cache Hit| Client
    Cache -->|Cache Miss| DB
    DB -->|Store & Return| Cache
    Cache -->|Response| Client
```

## Cache Hit vs Cache Miss

```
Cache Hit:   Client → Cache → Response   (< 1ms)
Cache Miss:  Client → Cache → DB → Cache → Response  (~50ms)
```

**Target:** Hit rate > 90% for good performance.

---

## Caching Strategies

### 1. Cache-Aside (Lazy Loading)

Application manages cache manually — most common pattern.

```
Read:
  1. Check cache
  2. If miss → read DB → write to cache → return
  3. If hit → return cache value

Write:
  1. Write to DB
  2. Invalidate / delete from cache
```

**Real Example — Product Catalog:**

```python
async def get_product(product_id: str):
    # 1. Try cache first
    cached = await redis.get(f"product:{product_id}")
    if cached:
        return json.loads(cached)

    # 2. Cache miss – fetch from DB
    product = await db.products.find_one({"_id": product_id})
    if not product:
        raise NotFoundException()

    # 3. Store in cache with TTL
    await redis.setex(
        f"product:{product_id}",
        300,               # 5 minutes TTL
        json.dumps(product)
    )
    return product

async def update_product(product_id: str, data: dict):
    # 1. Update DB first
    await db.products.update_one({"_id": product_id}, {"$set": data})
    # 2. Invalidate stale cache
    await redis.delete(f"product:{product_id}")
```

---

### 2. Write-Through

Write to cache AND database simultaneously.

```mermaid
graph LR
    App["🔌 Application"]
    Cache["⚡ Cache"]
    DB["💾 DB"]

    App -->|Write| Cache
    Cache -->|Sync Write| DB
```

**Pros:** Cache always fresh  
**Cons:** Higher write latency  
**Use:** Banking balance, order status

---

### 3. Write-Behind (Write-Back)

Write to cache immediately, persist to DB asynchronously.

```mermaid
graph LR
    App["🔌 Application"]
    Cache["⚡ Cache"]
    Queue["📨 Async Queue"]
    DB["💾 DB"]

    App -->|Write| Cache
    Cache -->|Async| Queue
    Queue -->|Batch| DB
```

**Pros:** Very fast writes  
**Cons:** Risk of data loss on crash  
**Use:** Analytics counters, like counts

---

## Cache Eviction Policies

| Policy | Description | Use Case |
|---|---|---|
| **LRU** | Evict Least Recently Used | General purpose |
| **LFU** | Evict Least Frequently Used | Trending content |
| **TTL** | Expire after fixed time | Session data |
| **FIFO** | Evict oldest entry | Event logs |

---

## Real-World Caching Architecture (E-Commerce)

```mermaid
graph TB
    Browser["🌐 Browser"]
    CDN["🌍 CDN\n(Static assets, images)"]
    LB["⚖️ Load Balancer"]
    App["🔌 App Server"]
    Redis["⚡ Redis Cluster\n(Sessions, hot data)"]
    DB["💾 Primary DB"]
    Replica["📖 Read Replica\n(Heavy reads)"]

    Browser --> CDN
    Browser --> LB
    LB --> App
    App --> Redis
    Redis -->|Miss| DB
    App -->|Read queries| Replica
    DB --> Replica
```

**Layers:**
1. **Browser cache** – static files (CSS/JS/images)
2. **CDN** – geographically distributed static content
3. **Redis** – application-level hot data (sessions, product catalog)
4. **DB Read Replica** – offload read queries from primary

---

## Cache Stampede Problem & Fix

**Problem:** Cache expires → thousands of requests hit DB simultaneously.

```
TTL expires at 12:00:00
→ 10,000 concurrent requests all miss cache
→ 10,000 DB queries in 1 second → DB crashes
```

**Solution – Probabilistic Early Expiry:**

```python
import random
import math

async def get_with_stampede_protection(key: str, ttl: int):
    data = await redis.get(key)
    if data:
        meta = json.loads(data)
        # Probabilistically refresh before expiry (prevents stampede)
        remaining = await redis.ttl(key)
        if remaining < ttl * 0.1:  # within last 10% of TTL
            if random.random() < 0.1:  # 10% chance to refresh early
                await refresh_cache(key, ttl)
        return meta["value"]
    return await refresh_cache(key, ttl)
```

---

## Top Cache Interview Questions

### Q1. What is the difference between Redis and Memcached?

| Feature | Redis | Memcached |
|---|---|---|
| Data Structures | Strings, Lists, Sets, Hashes, Sorted Sets | Strings only |
| Persistence | Yes (RDB/AOF) | No |
| Cluster Support | Yes | Yes |
| Pub/Sub | Yes | No |
| Replication | Yes | No |
| Use Case | Rich data, sessions, leaderboards | Simple key-value caching |

### Q2. How would you design a Leaderboard using Redis?

```
# Sorted Set: O(log n) insert, O(log n) rank query
ZADD leaderboard 9500 "Alice"
ZADD leaderboard 8200 "Bob"
ZADD leaderboard 9800 "Carol"

# Top 10 players (highest score first)
ZREVRANGE leaderboard 0 9 WITHSCORES

# Rank of a player
ZREVRANK leaderboard "Alice"   # → 1 (0-indexed)
```

---

# 3. Database Scaling

## Vertical vs Horizontal Scaling

```mermaid
graph LR
    subgraph Vertical["Vertical Scaling (Scale Up)"]
        S1["💻 4 CPU, 16GB"] -->|Upgrade| S2["💻 32 CPU, 256GB"]
    end
    subgraph Horizontal["Horizontal Scaling (Scale Out)"]
        H1["💻 Server 1"]
        H2["💻 Server 2"]
        H3["💻 Server 3"]
        H1 --- H2
        H2 --- H3
    end
```

| | Vertical | Horizontal |
|---|---|---|
| Cost | Expensive hardware | Commodity servers |
| Limit | Hardware ceiling | Nearly unlimited |
| Downtime | Yes (resize) | No |
| Complexity | Low | High (distributed) |

---

## Database Replication

Master-replica setup for read scalability.

```mermaid
graph TD
    App["🔌 Application"]
    Master["📝 Master DB\n(All Writes)"]
    Replica1["📖 Replica 1\n(Reads)"]
    Replica2["📖 Replica 2\n(Reads)"]
    Replica3["📖 Replica 3\n(Reads)"]

    App -->|Writes| Master
    Master -->|Async Replication| Replica1
    Master -->|Async Replication| Replica2
    Master -->|Async Replication| Replica3
    App -->|Reads| Replica1
    App -->|Reads| Replica2
```

**Real Example:** Instagram – 1 master, 10+ replicas. 99% of traffic is reads.

---

## Database Sharding

Splitting data across multiple databases by a shard key.

```mermaid
graph TD
    App["🔌 Application"]
    Router["🔀 Shard Router"]
    Shard1["💾 Shard 1\nUsers A–G"]
    Shard2["💾 Shard 2\nUsers H–N"]
    Shard3["💾 Shard 3\nUsers O–Z"]

    App --> Router
    Router -->|Hash/Range| Shard1
    Router -->|Hash/Range| Shard2
    Router -->|Hash/Range| Shard3
```

**Sharding Strategies:**

| Strategy | How | Pros | Cons |
|---|---|---|---|
| Range | user_id 0–999 → Shard 1 | Simple | Hotspots |
| Hash | hash(user_id) % N | Even distribution | Cross-shard queries hard |
| Directory | Lookup table | Flexible | Extra hop |

**Real Example:** WhatsApp shards message storage by phone number hash across 100+ MySQL shards.

---

## CAP Theorem

A distributed system can guarantee only **2 of 3**:

```mermaid
graph TD
    C["C: Consistency\nAll nodes see same data"]
    A["A: Availability\nEvery request gets response"]
    P["P: Partition Tolerance\nWorks despite network failures"]

    C --- A
    A --- P
    P --- C

    CP["CP Systems\nMongoDB, HBase, ZooKeeper"]
    AP["AP Systems\nCassandra, DynamoDB, CouchDB"]
    CA["CA Systems\nMySQL, PostgreSQL\n(single node)"]

    C -->|+P| CP
    A -->|+P| AP
    C -->|+A| CA
```

**Interview Answer:**
> In practice, network partitions (P) always happen, so you choose between **Consistency (CP)** or **Availability (AP)**.
> - Banking → CP (never show stale balance)
> - Social Media → AP (slightly stale like count is fine)

---

# 4. API Design

## REST vs GraphQL vs gRPC

```mermaid
graph LR
    REST["🌐 REST\nHTTP + JSON\nResource-based"]
    GraphQL["📊 GraphQL\nHTTP + JSON\nQuery-based"]
    gRPC["⚡ gRPC\nHTTP/2 + Protobuf\nContract-based"]
```

| Feature | REST | GraphQL | gRPC |
|---|---|---|---|
| Protocol | HTTP/1.1 | HTTP/1.1 | HTTP/2 |
| Format | JSON | JSON | Protobuf (binary) |
| Over-fetching | Yes | No | No |
| Type Safety | Manual | Schema | Proto contract |
| Browser Support | Native | Native | Needs proxy |
| Best For | Public APIs | Flexible queries | Microservice RPC |

---

## RESTful API Design Best Practices

```
# Resource naming – nouns, not verbs
GET    /orders              – list orders
POST   /orders              – create order
GET    /orders/:id          – get single order
PUT    /orders/:id          – replace order
PATCH  /orders/:id          – partial update
DELETE /orders/:id          – delete order

# Nested resources
GET  /customers/:id/orders         – customer's orders
GET  /customers/:id/orders/:orderId – specific order

# Query params for filtering, sorting, pagination
GET /products?category=electronics&minPrice=100&sort=price&page=2&limit=20

# Versioning – always version your API
GET /api/v1/users   (deprecated)
GET /api/v2/users   (current)
```

**HTTP Status Codes:**

| Code | Meaning | Use |
|---|---|---|
| 200 | OK | GET success |
| 201 | Created | POST success |
| 204 | No Content | DELETE success |
| 400 | Bad Request | Validation error |
| 401 | Unauthorized | No/invalid token |
| 403 | Forbidden | Valid token, no permission |
| 404 | Not Found | Resource missing |
| 409 | Conflict | Duplicate resource |
| 429 | Too Many Requests | Rate limited |
| 500 | Internal Server Error | Bug |

---

## Rate Limiting

Prevent API abuse by limiting request frequency.

```mermaid
graph TD
    Client["👤 Client"]
    RateLimiter["⏱️ Rate Limiter\n100 req/min"]
    API["🔌 API Server"]

    Client -->|Request| RateLimiter
    RateLimiter -->|Under limit| API
    RateLimiter -->|Exceeded| Block["❌ 429 Too Many Requests"]
    API -->|Response| Client
```

**Algorithms:**

```
Token Bucket:     Tokens replenish at fixed rate; burst allowed
Sliding Window:   Track requests per rolling time window
Fixed Window:     Count resets every minute; boundary burst problem
Leaky Bucket:     Queue requests, process at fixed rate (smooth output)
```

**Redis implementation (Sliding Window):**

```python
async def is_rate_limited(user_id: str, limit: int = 100, window_secs: int = 60):
    key  = f"rate:{user_id}"
    now  = time.time()
    pipe = redis.pipeline()
    pipe.zremrangebyscore(key, 0, now - window_secs)  # remove old
    pipe.zadd(key, {str(now): now})                    # add current
    pipe.zcard(key)                                    # count in window
    pipe.expire(key, window_secs)
    _, _, count, _ = await pipe.execute()
    return count > limit
```

---

# 5. Message Queues & Event-Driven Architecture

## Why Message Queues?

```mermaid
graph LR
    subgraph Synchronous["❌ Synchronous (Tight Coupling)"]
        A1["Service A"] -->|Waits| B1["Service B"]
        B1 -->|Waits| C1["Service C"]
    end
    subgraph Async["✅ Async (Loose Coupling)"]
        A2["Service A"] -->|Publish| Q["📨 Queue"]
        Q -->|Consume| B2["Service B"]
        Q -->|Consume| C2["Service C"]
    end
```

**Benefits:** Decoupling, buffering, retry, fan-out, back-pressure.

---

## Kafka Architecture

```mermaid
graph TD
    Producers["📤 Producers\n(Order, Payment, User services)"]
    Kafka["🔔 Kafka Cluster\nTopics with Partitions"]
    CG1["📥 Consumer Group 1\n(Inventory Service)"]
    CG2["📥 Consumer Group 2\n(Email Service)"]
    CG3["📥 Consumer Group 3\n(Analytics)"]

    Producers -->|Publish| Kafka
    Kafka -->|Subscribe| CG1
    Kafka -->|Subscribe| CG2
    Kafka -->|Subscribe| CG3
```

**Key Concepts:**

| Concept | Meaning |
|---|---|
| Topic | Category/feed name |
| Partition | Parallelism unit within a topic |
| Offset | Position of a message in a partition |
| Consumer Group | Set of consumers sharing partition load |
| Retention | How long messages are kept (default 7 days) |

**Real Example – Order Processing:**

```
1. User places order → OrderService publishes "order.placed" to Kafka
2. InventoryService consumes → reserves stock
3. PaymentService consumes → charges card
4. EmailService consumes → sends confirmation
5. AnalyticsService consumes → updates dashboard

All happen in parallel, independently, with retry on failure.
```

---

## Kafka vs RabbitMQ

| Feature | Kafka | RabbitMQ |
|---|---|---|
| Model | Log / Stream | Queue |
| Throughput | Millions/sec | Thousands/sec |
| Retention | Days/weeks | Until consumed |
| Replay | Yes (by offset) | No |
| Ordering | Per partition | Per queue |
| Use Case | Event streaming, audit log | Task queues, RPC |

---

# 6. Microservices Architecture

## Monolith vs Microservices

```mermaid
graph TD
    subgraph Monolith["Monolith"]
        M["Single Deployable\nUser + Order + Payment\n+ Inventory + Email"]
    end
    subgraph Microservices["Microservices"]
        US["👤 User\nService"]
        OS["📦 Order\nService"]
        PS["💳 Payment\nService"]
        IS["📋 Inventory\nService"]
        ES["📧 Email\nService"]
    end
```

| | Monolith | Microservices |
|---|---|---|
| Deployment | All-or-nothing | Independent |
| Scaling | Scale everything | Scale specific services |
| Technology | Single stack | Polyglot |
| Fault isolation | None | Yes |
| Complexity | Simple | High (distributed) |
| Team size | Small team | Multiple teams |

---

## Microservices Communication Patterns

```mermaid
graph TD
    subgraph Sync["Synchronous"]
        C1["Service A"] -->|HTTP/gRPC| C2["Service B"]
    end
    subgraph Async["Asynchronous"]
        A1["Service A"] -->|Event| Q["Kafka/RabbitMQ"]
        Q -->|Event| A2["Service B"]
    end
    subgraph Saga["Saga Pattern (Distributed Transactions)"]
        S1["Order\nService"] -->|Event| S2["Payment\nService"]
        S2 -->|Event| S3["Inventory\nService"]
        S3 -->|Compensate on fail| S2
    end
```

---

## Circuit Breaker Pattern

Prevents cascading failures when a downstream service is down.

```mermaid
stateDiagram-v2
    [*] --> Closed
    Closed --> Open: Failures > threshold
    Open --> HalfOpen: Timeout expires
    HalfOpen --> Closed: Test request succeeds
    HalfOpen --> Open: Test request fails
```

**States:**
- **Closed** – requests pass through normally
- **Open** – requests fail fast (no calls to broken service)
- **Half-Open** – probe with one request; if ok, reset to Closed

```python
class CircuitBreaker:
    def __init__(self, threshold=5, timeout=60):
        self.failures    = 0
        self.threshold   = threshold
        self.state       = "CLOSED"
        self.last_failure = None
        self.timeout     = timeout

    async def call(self, func, *args, **kwargs):
        if self.state == "OPEN":
            if time.time() - self.last_failure > self.timeout:
                self.state = "HALF_OPEN"
            else:
                raise Exception("Circuit OPEN – service unavailable")

        try:
            result      = await func(*args, **kwargs)
            self.failures = 0
            self.state  = "CLOSED"
            return result
        except Exception as e:
            self.failures     += 1
            self.last_failure  = time.time()
            if self.failures >= self.threshold:
                self.state = "OPEN"
            raise
```

---

## Service Discovery

How microservices find each other.

```mermaid
graph TD
    ServiceA["Service A"]
    Registry["📋 Service Registry\n(Consul / Eureka / K8s DNS)"]
    ServiceB1["Service B – Instance 1"]
    ServiceB2["Service B – Instance 2"]
    ServiceB3["Service B – Instance 3"]

    ServiceB1 -->|Register| Registry
    ServiceB2 -->|Register| Registry
    ServiceB3 -->|Register| Registry
    ServiceA -->|Discover| Registry
    Registry -->|Return healthy instance| ServiceA
    ServiceA -->|Call| ServiceB2
```

---

# 7. System Design Case Studies

## Design a URL Shortener (bit.ly)

### Requirements
- Shorten long URLs
- Redirect short → long
- 100M URLs/day created, 10B redirects/day
- Analytics (click count)

### Design

```mermaid
graph TD
    Client["👤 Client"]
    LB["⚖️ Load Balancer"]
    API["🔌 API Servers"]
    Cache["⚡ Redis Cache\n(short→long mapping)"]
    DB["💾 Database\n(short, long, user_id, created_at)"]
    Analytics["📊 Analytics\n(Kafka + Cassandra)"]

    Client -->|POST /shorten| LB
    Client -->|GET /{code}| LB
    LB --> API
    API -->|Read| Cache
    Cache -->|Miss| DB
    API -->|Write analytics| Analytics
```

**Short Code Generation:**

```python
import hashlib
import base64

def generate_short_code(long_url: str, length: int = 7) -> str:
    # MD5 hash → base62 encode → take first 7 chars
    hash_bytes = hashlib.md5(long_url.encode()).digest()
    encoded    = base64.b64encode(hash_bytes).decode("utf-8")
    # Use only URL-safe chars [a-zA-Z0-9]
    safe = encoded.replace("+", "").replace("/", "").replace("=", "")
    return safe[:length]
```

**Key decisions:**
- Short code: 7 chars of base62 = 62^7 = 3.5 trillion combinations
- Cache TTL: popular URLs cached in Redis for 24h
- Redirect HTTP 301 (cacheable) vs 302 (analytics tracked)

---

## Design Twitter/Instagram Feed (News Feed)

### Requirements
- User posts tweet/photo
- Followers see it in their feed
- 300M daily active users

### Fan-Out Strategies

```mermaid
graph TD
    subgraph PushOnWrite["Push on Write (Fan-out on Write)"]
        W1["Alice posts tweet"] -->|Write to all| W2["Bob's feed cache"]
        W1 -->|Write to all| W3["Carol's feed cache"]
        W1 -->|Write to all| W4["10K followers' caches"]
    end
    subgraph PullOnRead["Pull on Read (Fan-out on Read)"]
        R1["Bob opens feed"] -->|Fetch from| R2["Alice's tweets"]
        R1 -->|Fetch from| R3["Carol's tweets"]
        R1 -->|Merge + sort| R4["Bob's feed"]
    end
```

**Hybrid approach (Twitter's actual model):**
- Regular users (<1000 followers) → Push (pre-compute feed)
- Celebrity users (millions followers) → Pull at read time (too expensive to push)

---

## Design a Chat Application (WhatsApp)

### Architecture

```mermaid
graph TD
    AlicePhone["📱 Alice's Phone"]
    BobPhone["📱 Bob's Phone"]
    LB["⚖️ Load Balancer"]
    ChatServer["💬 Chat Server\n(WebSocket)"]
    MQ["📨 Message Queue\n(Kafka)"]
    DB["💾 Message Store\n(Cassandra)"]
    PushNotif["🔔 Push Notification\n(APNs / FCM)"]

    AlicePhone <-->|WebSocket| LB
    BobPhone <-->|WebSocket| LB
    LB <--> ChatServer
    ChatServer -->|Persist| DB
    ChatServer -->|Async| MQ
    MQ --> PushNotif
    PushNotif -->|Offline notify| BobPhone
```

**Key decisions:**
- WebSocket for real-time bidirectional communication
- Cassandra for message storage (time-series, high write throughput)
- Message delivery ACK: sent → delivered → read (double tick system)
- End-to-end encryption: keys exchanged client-side only

---

## Design a Ride-Sharing App (Uber)

### Core Components

```mermaid
graph TD
    RiderApp["📱 Rider App"]
    DriverApp["📱 Driver App"]
    Gateway["🚪 API Gateway"]
    MatchService["🔍 Matching Service"]
    LocationService["📍 Location Service"]
    TripService["🚗 Trip Service"]
    PaymentService["💳 Payment Service"]
    NotifService["🔔 Notification Service"]
    Redis["⚡ Redis\n(Driver locations)"]
    Kafka["📨 Kafka\n(Trip events)"]
    DB["💾 PostgreSQL\n(Trips, Users)"]

    RiderApp --> Gateway
    DriverApp --> Gateway
    Gateway --> MatchService
    Gateway --> LocationService
    Gateway --> TripService
    MatchService --> Redis
    LocationService --> Redis
    TripService --> DB
    TripService --> Kafka
    Kafka --> PaymentService
    Kafka --> NotifService
```

**Driver location updates:**
- Drivers send GPS every 5 seconds
- Stored in Redis Geo (geospatial index): `GEOADD drivers 72.8 18.9 "driver:123"`
- Nearest driver query: `GEORADIUS drivers 72.8 18.9 5 km` (< 1ms)

---

# 8. Consistent Hashing

## The Problem with Simple Hashing

```
3 servers: hash(key) % 3 → server 0/1/2
Add a 4th server: hash(key) % 4 → ALL keys remap → cache miss storm
```

## Consistent Hashing Solution

```mermaid
graph TD
    Ring["🔵 Hash Ring (0 → 2^32)"]
    S1["Server 1\n(position 10)"]
    S2["Server 2\n(position 70)"]
    S3["Server 3\n(position 130)"]
    K1["Key A → 25\n→ Server 2"]
    K2["Key B → 90\n→ Server 3"]

    Ring --> S1
    Ring --> S2
    Ring --> S3
    K1 -.->|clockwise nearest| S2
    K2 -.->|clockwise nearest| S3
```

**Adding/removing a server only remaps ~K/N keys** (K = total keys, N = servers).

**Real Example:** Amazon DynamoDB, Apache Cassandra, Redis Cluster all use consistent hashing with virtual nodes.

---

# 9. CDN (Content Delivery Network)

## How CDN Works

```mermaid
graph LR
    User["👤 User (Mumbai)"]
    CDN_IN["🌍 CDN Edge\n(Mumbai PoP)"]
    CDN_US["🌍 CDN Edge\n(Virginia PoP)"]
    Origin["🖥️ Origin Server\n(US East)"]

    User -->|Request image.jpg| CDN_IN
    CDN_IN -->|Cache Miss| CDN_US
    CDN_US -->|Cache Miss| Origin
    Origin -->|Content| CDN_US
    CDN_US -->|Cache & Forward| CDN_IN
    CDN_IN -->|Serve & Cache| User
```

**CDN Benefits:**
- Reduced latency (user served from nearest PoP)
- Reduced origin server load
- Protection against DDoS (traffic absorbed at edge)
- Auto-scaling at edge

**What to cache on CDN:**
- Static assets: images, CSS, JS bundles
- Videos, fonts
- API responses with `Cache-Control: public, max-age=300`

---

# 10. SOLID Principles in System Design

```
S – Single Responsibility: One service owns one domain
O – Open/Closed: Extend via events/plugins, not modifying existing code
L – Liskov Substitution: Services replaceable without breaking consumers
I – Interface Segregation: Expose only required API surface
D – Dependency Inversion: Depend on abstractions (interfaces), not implementations
```

**Real Example – Payment Service:**

```
❌ Bad: PaymentService handles charging, email, analytics, inventory
✅ Good:
  PaymentService → charges card
  emits "payment.succeeded" event
  EmailService listens → sends receipt
  InventoryService listens → reserves stock
  AnalyticsService listens → updates metrics
```

---

# 11. Data Consistency Patterns

## Eventual Consistency vs Strong Consistency

```
Strong Consistency: Read always returns latest write (slower, requires coordination)
  → Banking, inventory, order placement

Eventual Consistency: Reads may return stale data (faster, highly available)
  → Social media likes, view counts, product ratings
```

## Saga Pattern (Distributed Transactions)

Manage multi-service transactions without 2-phase commit.

```mermaid
graph TD
    Order["1. Create Order\n(Order Service)"]
    Reserve["2. Reserve Stock\n(Inventory Service)"]
    Charge["3. Charge Card\n(Payment Service)"]
    Ship["4. Ship Order\n(Shipping Service)"]
    CompP["❌ Compensate: Refund\n(if shipping fails)"]
    CompI["❌ Compensate: Release stock\n(if payment fails)"]

    Order -->|success| Reserve
    Reserve -->|success| Charge
    Charge -->|success| Ship
    Ship -->|fail| CompP
    CompP -->|rollback| CompI
```

---

# 12. System Design Interview Checklist

When answering any system design question, cover:

```mermaid
graph TD
    Q["System Design Question"]
    R["1. Requirements\n(Functional + Non-Functional)"]
    E["2. Estimation\n(Scale, QPS, Storage)"]
    HLD["3. High-Level Design\n(Components + Data Flow)"]
    DB["4. Database Design\n(Schema + Indexing)"]
    API["5. API Design\n(Endpoints)"]
    Scale["6. Scalability\n(Bottlenecks + Solutions)"]
    Perf["7. Performance\n(Caching + CDN)"]
    Fault["8. Fault Tolerance\n(Replication + Failover)"]
    Sec["9. Security\n(Auth + Encryption)"]
    Mon["10. Monitoring\n(Metrics + Alerts)"]

    Q --> R --> E --> HLD --> DB --> API --> Scale --> Perf --> Fault --> Sec --> Mon
```

**Estimation Template:**
```
QPS (Queries per second) = Daily Active Users × Actions/day ÷ 86400
Storage/day = QPS × avg message size × 86400
Cache size = Hot 20% of data (80/20 rule)
Bandwidth = QPS × avg response size
```

---

## Top System Design Interview Q&A

### Q: How would you design a scalable notification system?

```mermaid
graph TD
    Trigger["⚡ Event Trigger\n(Order, Payment, Chat)"]
    Kafka["📨 Kafka\nnotification-events topic"]
    Worker["⚙️ Notification Worker\n(K8s Pods)"]
    Router["🔀 Channel Router"]
    Email["📧 Email\n(SendGrid)"]
    SMS["📱 SMS\n(Twilio)"]
    Push["🔔 Push\n(FCM/APNs)"]
    Webhook["🔗 Webhook"]

    Trigger --> Kafka
    Kafka --> Worker
    Worker --> Router
    Router --> Email
    Router --> SMS
    Router --> Push
    Router --> Webhook
```

**Key points:**
- Decouple via Kafka (retry on failure)
- User preferences stored in DB (which channels to use)
- Idempotency key prevents duplicate notifications
- Dead letter queue for failed notifications after 3 retries

---

### Q: How would you design a distributed rate limiter?

```
Problem: Rate limiter must work across 10 API servers
Solution: Centralized counter in Redis

Redis command (atomic):
  INCR user:123:count
  EXPIRE user:123:count 60
  If count > 100 → return 429

Alternative: Redis + Sliding Window (ZADD + ZCOUNT)
```

---

### Q: Explain the differences between SQL and NoSQL databases.

| | SQL (PostgreSQL, MySQL) | NoSQL (MongoDB, Cassandra, DynamoDB) |
|---|---|---|
| Schema | Fixed (migrations) | Flexible / schemaless |
| Relationships | JOINs | Denormalized / embedded |
| ACID | Full | Eventual (most) |
| Scale | Vertical + limited horizontal | Horizontal by design |
| Query | Powerful (SQL) | Limited (key-access) |
| Use Case | Financial, ERP, OLTP | Catalogs, IoT, Time-series |

**Choose SQL when:** strong consistency, complex queries, relationships matter.  
**Choose NoSQL when:** massive scale, flexible schema, simple access patterns.
