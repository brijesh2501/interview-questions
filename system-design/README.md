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

| Policy   | Description                 | Use Case         |
| -------- | --------------------------- | ---------------- |
| **LRU**  | Evict Least Recently Used   | General purpose  |
| **LFU**  | Evict Least Frequently Used | Trending content |
| **TTL**  | Expire after fixed time     | Session data     |
| **FIFO** | Evict oldest entry          | Event logs       |

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

| Feature         | Redis                                     | Memcached                |
| --------------- | ----------------------------------------- | ------------------------ |
| Data Structures | Strings, Lists, Sets, Hashes, Sorted Sets | Strings only             |
| Persistence     | Yes (RDB/AOF)                             | No                       |
| Cluster Support | Yes                                       | Yes                      |
| Pub/Sub         | Yes                                       | No                       |
| Replication     | Yes                                       | No                       |
| Use Case        | Rich data, sessions, leaderboards         | Simple key-value caching |

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

|            | Vertical           | Horizontal         |
| ---------- | ------------------ | ------------------ |
| Cost       | Expensive hardware | Commodity servers  |
| Limit      | Hardware ceiling   | Nearly unlimited   |
| Downtime   | Yes (resize)       | No                 |
| Complexity | Low                | High (distributed) |

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

| Strategy  | How                     | Pros              | Cons                     |
| --------- | ----------------------- | ----------------- | ------------------------ |
| Range     | user_id 0–999 → Shard 1 | Simple            | Hotspots                 |
| Hash      | hash(user_id) % N       | Even distribution | Cross-shard queries hard |
| Directory | Lookup table            | Flexible          | Extra hop                |

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
>
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

| Feature         | REST        | GraphQL          | gRPC              |
| --------------- | ----------- | ---------------- | ----------------- |
| Protocol        | HTTP/1.1    | HTTP/1.1         | HTTP/2            |
| Format          | JSON        | JSON             | Protobuf (binary) |
| Over-fetching   | Yes         | No               | No                |
| Type Safety     | Manual      | Schema           | Proto contract    |
| Browser Support | Native      | Native           | Needs proxy       |
| Best For        | Public APIs | Flexible queries | Microservice RPC  |

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

| Code | Meaning               | Use                        |
| ---- | --------------------- | -------------------------- |
| 200  | OK                    | GET success                |
| 201  | Created               | POST success               |
| 204  | No Content            | DELETE success             |
| 400  | Bad Request           | Validation error           |
| 401  | Unauthorized          | No/invalid token           |
| 403  | Forbidden             | Valid token, no permission |
| 404  | Not Found             | Resource missing           |
| 409  | Conflict              | Duplicate resource         |
| 429  | Too Many Requests     | Rate limited               |
| 500  | Internal Server Error | Bug                        |

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

| Concept   | Meaning                              |
| --------- | ------------------------------------ |
| Topic     | Category/feed name                   |
| Partition | Parallelism unit within a topic      |
| Offset    | Position of a message in a partition |

---

# 6. Interview Questions & Answers on REST & RESTful API Design Principles

## 1️⃣ Basic Questions

### Q1. What is REST, and how does it differ from SOAP?

**Answer:** REST (Representational State Transfer) is an architectural style that defines a set of constraints for designing web services. It primarily uses standard HTTP methods and focuses on resources rather than operations.

**Differences between REST and SOAP:**

| Aspect        | REST                           | SOAP                                       |
| ------------- | ------------------------------ | ------------------------------------------ |
| Protocol Type | Architectural style            | Strict protocol                            |
| Data Format   | JSON, XML, HTML, etc.          | XML only                                   |
| Performance   | Lightweight and faster         | Higher overhead due to XML and WS-Security |
| Flexibility   | Supports multiple data formats | XML-based only                             |
| Statefulness  | Stateless                      | Can be stateful                            |
| Use Case      | Public APIs, microservices     | Enterprise services                        |

---

### Q2. What are the six constraints of REST architecture?

**Answer:** The six constraints that define REST are:

1. **Client-Server Architecture** – The client and server are independent of each other, allowing for better scalability and separation of concerns.

2. **Statelessness** – Each request from the client contains all the necessary information; the server does not store session data between requests.

3. **Cacheability** – Responses can be cached to improve performance and reduce server load.

4. **Layered System** – An API can be designed in layers (e.g., authentication, load balancing, security) without affecting clients.

5. **Uniform Interface** – Standardized communication methods using HTTP verbs (GET, POST, PUT, DELETE, PATCH).

6. **Code on Demand (Optional)** – The server can send executable code (e.g., JavaScript) to the client.

---

### Q3. What is the difference between a REST API and a RESTful API?

**Answer:**

- **REST API** – Any API that follows some REST principles but may not strictly adhere to all six constraints.
- **RESTful API** – An API that fully follows all REST constraints and principles rigorously.

---

### Q4. What is a resource in REST, and how is it represented?

**Answer:**

- A **resource** is any object or entity that can be accessed via the API (e.g., users, orders, products, comments).
- Resources are represented using **URIs (Uniform Resource Identifiers)**.

**Examples:**

```
GET /users/123            – Retrieve specific user
GET /products/456         – Retrieve specific product
POST /orders              – Create new order
DELETE /comments/789      – Delete specific comment
```

---

### Q5. What are endpoints in a REST API?

**Answer:** An endpoint is a specific URL where a client interacts with a resource.

**Examples:**

```
GET /users/{id}          – Retrieve user details
POST /orders             – Create an order
PUT /users/{id}          – Update entire user
PATCH /users/{id}        – Partially update user
DELETE /users/{id}       – Delete user
```

---

## 2️⃣ HTTP Methods & Status Codes

### Q6. Explain the difference between GET, POST, PUT, PATCH, and DELETE.

**Answer:**

| Method     | Purpose                   | Idempotent | Safe | Use Case               |
| ---------- | ------------------------- | ---------- | ---- | ---------------------- |
| **GET**    | Retrieve resource data    | Yes        | Yes  | Fetch user profile     |
| **POST**   | Create a new resource     | No         | No   | Create new order       |
| **PUT**    | Replace entire resource   | Yes        | No   | Update user all fields |
| **PATCH**  | Partially update resource | No\*       | No   | Change user email only |
| **DELETE** | Remove a resource         | Yes        | No   | Delete user account    |

\*PATCH can be idempotent if designed carefully

---

### Q7. When would you use PUT vs. PATCH?

**Answer:**

- **Use PUT** when replacing an **entire resource** (all fields must be sent).

  ```
  PUT /users/1
  {
    "name": "John",
    "email": "john@example.com",
    "age": 30,
    "country": "USA"
  }
  ```

- **Use PATCH** when making **partial updates** (only changed fields).
  ```
  PATCH /users/1
  {
    "email": "newemail@example.com"
  }
  ```

**Key Difference:** PUT replaces the entire resource; PATCH updates specific fields.

---

### Q8. What are the commonly used HTTP status codes in REST APIs?

**Answer:**

| Code    | Status                | Use Case                              |
| ------- | --------------------- | ------------------------------------- |
| **200** | OK                    | Successful GET/PUT request            |
| **201** | Created               | Resource successfully created (POST)  |
| **204** | No Content            | Successful DELETE, no response body   |
| **400** | Bad Request           | Client-side error (malformed request) |
| **401** | Unauthorized          | Authentication required/failed        |
| **403** | Forbidden             | Client lacks permission for resource  |
| **404** | Not Found             | Resource does not exist               |
| **409** | Conflict              | Duplicate resource or state conflict  |
| **429** | Too Many Requests     | Rate limit exceeded                   |
| **500** | Internal Server Error | Unexpected server-side issue          |
| **503** | Service Unavailable   | Server overloaded or maintenance      |

---

## 3️⃣ RESTful API Design & Best Practices

### Q9. What are the best practices for designing RESTful APIs?

**Answer:**

1. **Use plural nouns for resource names**

   ```
   ✅ GET /users          (not /user)
   ✅ GET /products       (not /product)
   ✅ POST /orders        (not /order)
   ```

2. **Implement proper HTTP status codes** – Don't return 200 for all responses.

3. **Support versioning** to avoid breaking existing clients

   ```
   /v1/users     (deprecated)
   /v2/users     (current)
   /v3/users     (future)
   ```

4. **Use pagination for large datasets**

   ```
   GET /products?page=2&limit=20&sort=price
   ```

5. **Implement rate limiting** to prevent abuse

   ```
   X-RateLimit-Limit: 1000
   X-RateLimit-Remaining: 999
   X-RateLimit-Reset: 1234567890
   ```

6. **Use OAuth 2.0 or JWT** for authentication

   ```
   Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...
   ```

7. **Support filtering and sorting**

   ```
   GET /products?category=electronics&minPrice=100&sort=-price
   ```

8. **Use hypermedia links (HATEOAS)** for discoverability

   ```json
   {
     "id": 1,
     "name": "John",
     "links": {
       "self": "/users/1",
       "all_users": "/users",
       "orders": "/users/1/orders"
     }
   }
   ```

9. **Provide meaningful error messages**

   ```json
   {
     "error": "Validation Error",
     "message": "Email field is required",
     "code": "MISSING_FIELD",
     "details": [
       {
         "field": "email",
         "message": "Email is required"
       }
     ]
   }
   ```

10. **Document API thoroughly** (use Swagger/OpenAPI)

---

### Q10. How do you design a RESTful API for a blogging platform?

**Answer:**

**Endpoints structure:**

```
# Posts
GET    /api/v1/posts              – Get all posts (with pagination)
POST   /api/v1/posts              – Create new post
GET    /api/v1/posts/{id}         – Get specific post
PUT    /api/v1/posts/{id}         – Update entire post
PATCH  /api/v1/posts/{id}         – Partially update post
DELETE /api/v1/posts/{id}         – Delete post

# Comments (nested resource)
GET    /api/v1/posts/{postId}/comments           – Get post comments
POST   /api/v1/posts/{postId}/comments           – Add comment to post
GET    /api/v1/posts/{postId}/comments/{id}      – Get specific comment
PATCH  /api/v1/posts/{postId}/comments/{id}      – Update comment
DELETE /api/v1/posts/{postId}/comments/{id}      – Delete comment

# Authors (users)
GET    /api/v1/users              – Get all users
POST   /api/v1/users              – Register user
GET    /api/v1/users/{id}         – Get user profile
PUT    /api/v1/users/{id}         – Update user profile
GET    /api/v1/users/{id}/posts   – Get user's posts

# Query parameters
GET /api/v1/posts?page=2&limit=10&sort=-createdAt&category=tech
GET /api/v1/posts/{id}/comments?sort=createdAt
```

**Response Examples:**

```json
{
  "status": "success",
  "data": {
    "id": 1,
    "title": "REST API Best Practices",
    "content": "...",
    "author": {
      "id": 5,
      "name": "John Doe",
      "email": "john@example.com"
    },
    "createdAt": "2024-01-15T10:30:00Z",
    "updatedAt": "2024-01-15T14:22:00Z",
    "commentCount": 12,
    "links": {
      "self": "/api/v1/posts/1",
      "comments": "/api/v1/posts/1/comments",
      "author": "/api/v1/users/5"
    }
  },
  "pagination": {
    "page": 1,
    "limit": 10,
    "total": 156,
    "totalPages": 16
  }
}
```

---

### Q11. What is HATEOAS in REST?

**Answer:** HATEOAS (Hypermedia As The Engine Of Application State) is a principle where API responses include links to relevant actions, making the API self-discoverable.

**Without HATEOAS (Client must know URLs):**

```json
{
  "id": 1,
  "name": "John",
  "email": "john@example.com"
}
```

**With HATEOAS (Self-descriptive):**

```json
{
  "id": 1,
  "name": "John",
  "email": "john@example.com",
  "links": {
    "self": { "href": "/users/1", "method": "GET" },
    "update": { "href": "/users/1", "method": "PUT" },
    "delete": { "href": "/users/1", "method": "DELETE" },
    "all_users": { "href": "/users", "method": "GET" },
    "orders": { "href": "/users/1/orders", "method": "GET" }
  }
}
```

**Benefit:** Client can discover available actions without prior knowledge of API structure.

---

### Q12. How do you handle authentication and authorization in REST APIs?

**Answer:**

1. **OAuth 2.0 for user authentication**

   ```
   Client → Authorization Server → Request Token → Use Token for API calls
   ```

2. **JWT (JSON Web Token) for session management**

   ```
   POST /api/v1/auth/login
   {
     "email": "user@example.com",
     "password": "secure123"
   }

   Response:
   {
     "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...",
     "expiresIn": 3600
   }

   Usage:
   GET /api/v1/users
   Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...
   ```

3. **API Keys for third-party access**

   ```
   GET /api/v1/data?api_key=abc123xyz789
   ```

4. **Role-Based Access Control (RBAC)**

   ```
   Admin Role   → Can create, update, delete all resources
   Editor Role  → Can create and edit own posts
   Viewer Role  → Can only view posts
   ```

5. **Implement refresh tokens**

   ```
   Access Token: Expires in 15 minutes (short-lived)
   Refresh Token: Expires in 7 days (long-lived)

   POST /api/v1/auth/refresh
   {
     "refreshToken": "refresh_token_value"
   }
   ```

---

## 4️⃣ Advanced & Real-World Questions

### Q13. How does caching work in REST APIs?

**Answer:** Use HTTP headers to implement caching strategies:

```
Response Headers:
Cache-Control: max-age=3600             (Cache for 1 hour)
Cache-Control: public, max-age=86400    (Public, cache 24 hours)
Cache-Control: private, max-age=3600    (Private cache only)
Cache-Control: no-cache, no-store       (Never cache)
ETag: "33a64df551425fcc55e4d42a148795d9f25f89d4"  (Version for validation)
Last-Modified: Wed, 21 Oct 2024 07:28:00 GMT
```

**Caching Strategies:**

1. **Cache-Aside** – Application fetches from cache, misses fetch from DB
2. **Write-Through** – Write to cache and DB simultaneously
3. **Write-Behind** – Write to cache, async write to DB

**Real Example:**

```python
@app.get("/api/v1/products/{id}")
async def get_product(id: int):
    return {
        "data": product,
        "headers": {
            "Cache-Control": "public, max-age=3600",
            "ETag": f'"{hash(product)}"'
        }
    }
```

---

### Q14. How do you implement pagination in REST APIs?

**Answer:**

```
GET /api/v1/users?page=2&limit=10&sort=-createdAt
```

**Response:**

```json
{
  "data": [
    { "id": 11, "name": "User 11" },
    { "id": 12, "name": "User 12" },
    ...
    { "id": 20, "name": "User 20" }
  ],
  "pagination": {
    "page": 2,
    "limit": 10,
    "total": 1500,
    "totalPages": 150,
    "hasNextPage": true,
    "hasPrevPage": true,
    "nextPage": "/api/v1/users?page=3&limit=10",
    "prevPage": "/api/v1/users?page=1&limit=10"
  }
}
```

**Implementation Tips:**

- Validate page and limit parameters
- Set maximum limit (e.g., max 100 per page)
- Use database query optimization (LIMIT, OFFSET)
- Include next/prev links for navigation

---

### Q15. How does versioning work in REST APIs?

**Answer:** Three common versioning strategies:

1. **URI-based versioning** (Most common)

   ```
   GET /api/v1/users
   GET /api/v2/users
   GET /api/v3/users
   ```

2. **Header-based versioning**

   ```
   GET /api/users
   Accept-Version: v2
   ```

3. **Query parameter versioning**
   ```
   GET /api/users?version=2
   GET /api/users?apiVersion=2.0
   ```

**Best Practice:** Use URI versioning as it's explicit and clear.

**Deprecation Strategy:**

```
v1 → Deprecated (sunset date: 2025-01-01)
v2 → Current (active)
v3 → Beta (testing)
```

---

### Q16. Explain the differences between REST, GraphQL, and gRPC.

**Answer:**

| Feature             | REST                 | GraphQL             | gRPC                      |
| ------------------- | -------------------- | ------------------- | ------------------------- |
| **Protocol**        | HTTP/1.1             | HTTP/1.1            | HTTP/2                    |
| **Data Format**     | JSON, XML            | JSON                | Protocol Buffers (Binary) |
| **Query Model**     | Fixed endpoints      | Custom queries      | RPC methods               |
| **Over-fetching**   | Common issue         | Eliminated          | N/A                       |
| **Under-fetching**  | Common issue         | Eliminated          | N/A                       |
| **Type System**     | Manual documentation | Strong schema       | Proto contracts           |
| **Performance**     | Medium               | Better (exact data) | Very fast                 |
| **Browser Support** | Native               | Needs proxy         | Needs proxy               |
| **Learning Curve**  | Easy                 | Medium              | Hard                      |
| **Use Case**        | Public APIs          | Complex data        | Microservices             |

**Example Comparison:**

REST Endpoint:

```
GET /users/1
Response includes all user fields (over-fetch)
```

GraphQL Query:

```graphql
{
  user(id: 1) {
    name
    email
  }
}
Response includes only requested fields (exact fetch)
```

gRPC Call:

```protobuf
service UserService {
  rpc GetUser(UserId) returns (User);
}
```

---

### Q17. How would you improve the performance of a REST API?

**Answer:**

1. **Enable caching**

   ```
   Cache-Control: public, max-age=3600
   Redis for frequently accessed data
   ```

2. **Use gzip compression**

   ```
   Accept-Encoding: gzip
   Reduces payload size by 70-80%
   ```

3. **Implement asynchronous processing**

   ```
   POST /api/v1/reports
   Response: 202 Accepted (Job queued)
   GET /api/v1/reports/{id}/status (Check status)
   ```

4. **Use database indexing**

   ```sql
   CREATE INDEX idx_users_email ON users(email);
   ```

5. **Pagination for large datasets**

   ```
   GET /products?page=1&limit=20
   ```

6. **Connection pooling**

   ```python
   pool = ConnectionPool(max_connections=10)
   ```

7. **CDN for static content**

   ```
   CSS, JS, images served from edge servers
   ```

8. **Rate limiting** (prevent abuse)

   ```
   100 requests per minute per user
   ```

9. **Database query optimization**

   ```sql
   SELECT user.name, COUNT(orders.id)
   FROM users
   LEFT JOIN orders ON users.id = orders.user_id
   GROUP BY users.id
   (Use JOINs, not N+1 queries)
   ```

10. **API Gateway** (aggregation, logging, authentication)
    ```
    Client → API Gateway → Microservices
    ```

---

### Q18. Can a REST API be stateful?

**Answer:** Theoretically **no**, REST APIs should be stateless. However, in practice:

- **Pure REST:** Stateless (each request is independent)

  ```
  Every request contains all necessary information
  Server doesn't store user session state
  ```

- **In Practice:** Some services use session-based authentication

  ```
  POST /login → Server creates session
  GET /data → Include sessionId in request
  This is NOT fully RESTful but pragmatic
  ```

- **Modern Approach:** Use stateless tokens (JWT)
  ```
  POST /login → Returns JWT token
  GET /data Authorization: Bearer {token}
  Server validates token without storing session
  ```

---

### Q19. How does REST handle security vulnerabilities?

**Answer:**

1. **Prevent SQL Injection**

   ```python
   # ❌ Vulnerable
   query = f"SELECT * FROM users WHERE id = {user_id}"

   # ✅ Safe - Parameterized queries
   query = "SELECT * FROM users WHERE id = ?"
   db.execute(query, [user_id])
   ```

2. **Prevent CSRF (Cross-Site Request Forgery)**

   ```
   Include CSRF token in requests
   POST /api/users
   X-CSRF-Token: abcd1234xyz
   ```

3. **Use HTTPS/TLS** for secure communication

   ```
   https://api.example.com/users
   All data encrypted in transit
   ```

4. **Implement OAuth 2.0** for secure authentication

   ```
   Authorization: Bearer {access_token}
   ```

5. **Use JWT with proper expiration**

   ```
   Token expires in 15 minutes (short-lived)
   Refresh token used to get new access token
   ```

6. **Validate and sanitize input**

   ```python
   from pydantic import BaseModel, EmailStr

   class User(BaseModel):
       email: EmailStr  # Validates email format
       name: str = Field(min_length=1, max_length=100)
   ```

7. **Implement rate limiting**

   ```
   Prevent brute force attacks
   Max 5 failed login attempts → lock account
   ```

8. **Add Content Security Policy (CSP) headers**

   ```
   Content-Security-Policy: default-src 'self'
   ```

9. **Use API Keys securely**

   ```
   Don't expose in client-side code
   Rotate keys regularly
   ```

10. **Enable CORS properly**
    ```
    Access-Control-Allow-Origin: https://trusted-domain.com
    NOT * (overly permissive)
    ```

---

## 5️⃣ Summary & Key Takeaways

### ✅ REST Fundamentals

- REST follows **six constraints**: stateless, cacheable, client-server, uniform interface, layered system, code-on-demand (optional)
- Uses **standard HTTP methods** (GET, POST, PUT, PATCH, DELETE)
- **Resource-oriented** architecture (not operation-oriented)

### ✅ API Design

- Use **proper HTTP status codes** (200, 201, 400, 401, 404, 500)
- Implement **versioning** (/v1, /v2)
- Support **pagination** and **filtering**
- Use **plural nouns** for resources (/users, not /user)

### ✅ Performance & Scalability

- Enable **caching** with appropriate TTL
- Use **compression** (gzip)
- Implement **rate limiting** and **pagination**
- Optimize **database queries**

### ✅ Security & Authentication

- Use **OAuth 2.0** or **JWT** for authentication
- Always use **HTTPS/TLS**
- Prevent **SQL injection**, **CSRF**, **XSS**
- Validate and **sanitize input**

### ✅ Best Practices

- Document API thoroughly (Swagger/OpenAPI)
- Include **HATEOAS links** for discoverability
- Provide **meaningful error messages**
- Use **API Gateway** for centralized management
- Implement **monitoring** and **logging**

---

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

| Feature    | Kafka                      | RabbitMQ         |
| ---------- | -------------------------- | ---------------- |
| Model      | Log / Stream               | Queue            |
| Throughput | Millions/sec               | Thousands/sec    |
| Retention  | Days/weeks                 | Until consumed   |
| Replay     | Yes (by offset)            | No               |
| Ordering   | Per partition              | Per queue        |
| Use Case   | Event streaming, audit log | Task queues, RPC |

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

|                 | Monolith         | Microservices           |
| --------------- | ---------------- | ----------------------- |
| Deployment      | All-or-nothing   | Independent             |
| Scaling         | Scale everything | Scale specific services |
| Technology      | Single stack     | Polyglot                |
| Fault isolation | None             | Yes                     |
| Complexity      | Simple           | High (distributed)      |
| Team size       | Small team       | Multiple teams          |

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

|               | SQL (PostgreSQL, MySQL)       | NoSQL (MongoDB, Cassandra, DynamoDB) |
| ------------- | ----------------------------- | ------------------------------------ |
| Schema        | Fixed (migrations)            | Flexible / schemaless                |
| Relationships | JOINs                         | Denormalized / embedded              |
| ACID          | Full                          | Eventual (most)                      |
| Scale         | Vertical + limited horizontal | Horizontal by design                 |
| Query         | Powerful (SQL)                | Limited (key-access)                 |
| Use Case      | Financial, ERP, OLTP          | Catalogs, IoT, Time-series           |

**Choose SQL when:** strong consistency, complex queries, relationships matter.  
**Choose NoSQL when:** massive scale, flexible schema, simple access patterns.
