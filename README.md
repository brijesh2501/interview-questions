# 📚 Fullstack Interview Questions (Node.js, React.js, SQL, JavaScript, Java, .NET, ADO.NET)

This repository contains a **curated list of interview questions** collected from real interviews in **2025** for Fullstack developers (React.js + Node.js + SQL + .NET + JavaScript + Java).

---

## 🔹 Node.js
- Callstack, Event Loop, Thread pool , Task / Callback Queue , Microtask Queue , Web API ?
- How to handle 1 million concurrent requests using Node.js?
- What are streams / buffers in Node.js?
- How to create custom middleware in Node.js?
- Have you created custom middleware in Node.js and how?
- How do you handle CPU intensive tasks in Node.js?
- How do you handle concurrent requests in Node.js?
- How do you manage a high CPU on a server?
- How do you create indexing in MongoDB?
- How do you design a scalable schema using MongoDB?
- CAP Theorem
- Kafka – why use it instead of SQL?
- How to build Docker image (dependencies)?
- Sharding and partitioning
- Horizontal vs vertical scaling
- What is child process in nodejs

---

## 🔹 React.js
- Controlled vs Uncontrolled components
- Static site vs server-side rendering
- How do you manage state in React?
- How to avoid prop drilling in React?
- Context API vs Redux (re-renders)
- React.memo vs useMemo
- useEffect vs useLayoutEffect
- useReducer vs useCallback vs useMemo
- useRefs in React vs DOM manipulation in JavaScript
- React portals
- mapStateToProps
- Redux connect() arguments
- React virtualization (react-window, react-virtualized)
- How to unmount a component in functional React?
- How many virtual DOMs does React use?
- Filter elements from array in React (search example)
- Jest unit test for button render and API response
- How do you secure React applications?
- How do you make code more maintainable and readable in React?
- How do you debug React apps (e.g. login failure)?
- Difference Between Axios Vs Fetch API ?
- Create search feature in reactJs for below given array
[
    "Banana",
    "Apple",
    "Orange",
    "Mango",
    "Pineapple",
    "Watermelon"
  ]
- Create todo application in reactJs
- How do you handle concurrency in reactJs like using useTransion
- React fibre Algorithim
- Create a functionality in reactjs using react function component ON / OFF button , when click on ON button its text changes to OFF and Vice a versa
- What is higher order functions ? why and when use HOC ?
- React Reconcillation algo ?
- Throttling VS Debouncing ?
- Redux Thunk Vs Redux Saga middleware ? 
- React Hydration ?



---

## 🔹 JavaScript
- ES6 + features (Spread operator, Rest , arrow functions , destructuring , promises , import , class
)
- Closure
- Hoisting
- Rest vs Spread operator
- call(), bind(), apply()
- forEach vs map()
- map vs filter vs reducer function
- Currying (with and without nested functions)
- Currying using closures
- Memoization
- Normal function vs Arrow function
- Longest continuous increasing subsequence
- Remove adjacent duplicates from string
- Rearrange array evens/odds
- Find non-repeating char in string
- Count characters in string
- Question based on javascript
```javascript
console.log([]==[]); // false
let {length} = 'lyakat';//6
console.log(length);
let arr = [];
console.log(arr.push(6));
const  a = "brijesh";
console.log(a++);
let a = 5;
let b = a++;
console.log(a+b);
console.log(3+"2"+5);
```
- Event bubbling Or Event Delegation ? 
- Write a javascript Program , Input : [20, 30 , 40] and output [70, 60, 50]
- Find  non repeating char in string Input “Sdbfsbd”   Output :  f
- Find count of characters in string Input : “aaddbbcf” : output : {a : 2, b: 2 , f: 1, d:2, c:1} and sort keys in object and out  {a : 2, b: 2 , c: 1, d:2, f:1}
```javascript
Const a = [‘Fname’: ‘A’]
a =  [‘Fname’: ‘B’] // this will throw error
a[[‘Fname’] = ‘B’; // this will work
```
```javascript
console.log([1]+[2])//12
console.log([1,3]+[2,4])//1,32,4
```
- Deep copy vs shallow copy?
---

## 🔹 SQL
- ACID properties
- CTE (Common Table Expressions)
- Normalization vs Denormalization
- 1NF, 2NF, 3NF
- Database table partitioning
- Views, Indexes, Stored Procedures
- Joins (INNER, OUTER, LEFT, RIGHT, CROSS)
- Clustered vs Non-clustered index
- Delete vs Drop table
- Debugging slow queries (EXPLAIN, indexes)
- InnoDB vs MyISAM
- Constraints in SQL
- CHAR vs VARCHAR
- Nth highest salary query
- SQL vs NoSQL
- Can identity column be DOUBLE?
- Magic tables
- RANK vs DENSE_RANK

---

## 🔹 Java
- Boxing and Unboxing
- Hibernate
- Java memory (Stack vs Heap)
- Memory leak identification
- Multithreading (e.g., concurrency, synchronization, thread pools)
- Data structures (e.g., List, Map, Set implementations and their complexities)
### Core Java
- What are the differences between JDK, JRE, and JVM?
- How does Java achieve platform independence?
- Explain OOP principles (Encapsulation, Abstraction, Inheritance, Polymorphism) with examples.
- Difference between abstract class vs interface?
- How does Java handle memory management (Heap, Stack, Garbage Collection)?
- What is the difference between String, StringBuilder, and StringBuffer?
- What are checked vs unchecked exceptions?
- How does Java’s class loading mechanism work?
- Explain the concept of immutable classes in Java. How do you create one?
- What are functional interfaces and lambdas introduced in Java 8?

### Multithreading & Concurrency
- Difference between process vs thread?
- What are the states of a Thread lifecycle?
- Explain synchronized vs ReentrantLock.
- What are volatile and atomic variables?
- Difference between ConcurrentHashMap vs HashMap.
- How does ExecutorService work?
- What is the difference between parallel stream vs sequential stream in Java 8?
- Deadlock – how to detect and prevent it?

### Java Collections Framework
- Difference between HashMap, LinkedHashMap, and TreeMap.
- How does HashMap work internally (hashing, collision, resizing)?
- Difference between ArrayList vs LinkedList.
- What is the difference between fail-fast and fail-safe iterators?
- When to use Set vs List vs Map?
- How does ConcurrentHashMap handle concurrency?

### Java 8+ Features
- Explain Streams API and its advantages.
- Difference between map() vs flatMap() in Streams.
- What are Optional and its best practices?
- Explain default and static methods in interfaces.
- What is the difference between Functional Interface vs Abstract Class?
- How does method reference (::) work?

### JVM & Performance
- What are the components of the JVM architecture?
- Difference between heap vs stack memory.
- What are class loaders in Java?
- Explain Just-In-Time (JIT) compiler.
- Different types of Garbage Collectors (Serial, Parallel, G1, ZGC).
- How do you analyze memory leaks in a Java application?

### Spring Boot & Microservices (Java Ecosystem)
- Difference between Spring vs Spring Boot.
- How does Dependency Injection (DI) work in Spring?
- What is the role of @Component, @Service, @Repository, @Controller?
- Explain Spring Boot Auto-Configuration.
- How do you secure REST APIs in Spring Boot (Spring Security / JWT)?
- How does Spring handle transactions?
- How do you implement circuit breaker, rate limiting, or service discovery in microservices?
- How do you design a scalable microservice architecture in Java?

### Scenario-Based / Problem-Solving
- You have a Java app facing high CPU usage – how would you debug it?
- Your Java service is facing memory leaks – what tools and steps will you use?
- How do you handle large data processing efficiently in Java?
- You need to implement a real-time notification system – which Java concurrency/async features will you use?
- How do you design a thread-safe singleton in Java?
- Given a large JSON payload, how would you efficiently parse it in Java?

---

## 🔹 Python

### Core Python
- Difference between list, tuple, set, dictionary?
- Explain Python’s GIL (Global Interpreter Lock).
- Shallow copy vs deep copy?
- Explain Python decorators with an example.
- Difference between @classmethod, @staticmethod, and instance method?
- What is a generator? How does yield work?
- Explain Python’s memory management.
- Difference between is and ==?
- What are Python data classes?
- How do you handle concurrency in Python? (threading vs multiprocessing vs asyncio)

### Coding style Qs:
- Reverse a string in Python in 3 ways.
- Flatten a nested list.
- Implement LRU cache in Python.

### AI / ML
- What is bias-variance tradeoff?
- Difference between supervised, unsupervised, reinforcement learning?
- What is overfitting? How to prevent it?
- Difference between bagging and boosting?
- Explain precision, recall, F1-score.
- What is PCA? Why is it used?
- Explain gradient descent.
- What is regularization (L1, L2)?
- What is transfer learning?
- Difference between CNN, RNN, Transformer?

### Coding style Qs:
- Implement linear regression using gradient descent (without sklearn).
- Train/test split and accuracy calculation in Python.
- Use scikit-learn to train a logistic regression on sample data.

### Agents (GenAI / LangChain / AI Ops)
- What are AI Agents?
- Difference between an LLM and an Agent?
- What is LangChain?
- How does a ReAct Agent work?
- How do Agents use tools (APIs, databases, search)?
- What is vector embedding? Why is it important for Agents?
- Explain RAG (Retrieval Augmented Generation).
- What is chain-of-thought reasoning?
- How do autonomous Agents (like AutoGPT, BabyAGI) work?
- What are limitations of Agents (hallucination, cost, latency)?

### Coding style Qs:
- Create a simple LangChain agent to call a weather API.
- Use OpenAI + vector DB to answer from PDFs.
- Build a task-planning agent (multi-step reasoning).

### Django
- What is Django ORM? How does it compare to raw SQL?
- Difference between @login_required vs middleware authentication?
- What is Django Rest Framework (DRF)?
- How do signals work in Django?
- What are Django middleware and their use cases?
- How do you handle migrations in Django?
- Explain difference between select_related and prefetch_related.
- How does Django handle CSRF?
- What is Django’s class-based view vs function-based view?
- How do you scale a Django app?

### Coding style Qs:
- Write a Django model for Order with ForeignKey to Customer.
- Write a DRF view to return JSON list of products.
- Implement a custom Django middleware.

### FastAPI
- Difference between Django REST Framework and FastAPI?
- How does FastAPI handle async vs sync?
- Explain dependency injection in FastAPI.
- How does FastAPI handle validation (Pydantic models)?
- What is the role of BackgroundTasks?
- How do you implement authentication/authorization in FastAPI?
- How does FastAPI handle WebSockets?
- How do you integrate Celery with FastAPI for background jobs?
- Explain caching strategies in FastAPI (Redis, in-memory).
- How do you scale FastAPI with Gunicorn + Uvicorn workers?

### Coding style Qs:
- Create a FastAPI endpoint for CRUD operations on Book.
- Implement JWT auth in FastAPI.
- Implement rate-limiting middleware in FastAPI.

---

## 🔹 .NET (C#, .NET Core, .NET Framework)
- Collections and types of collections
- LINQ
- Generic vs Non-generic classes
- Class vs Structure
- Value types vs Reference types
- == vs .Equals()
- Abstract class vs Interface
- const vs readonly vs static
- async / await in C#
- Filters vs Middleware
- Middleware vs custom middleware
- What are the challenges faced during .NET development?
- Latest version of .NET used?
- .NET Framework vs .NET Core
- Design patterns in .NET
- Factory design pattern return type
- IActionResult vs ActionResult
- API authentication
- Is there a way to avoid storing token in local storage and sending it again and again?
- IEnumerable vs IEnumerator
- Difference between .NET, Java, and Python apps
- What is Kestrel in .NET Core?
- What is CLR, GAC, AppDomain?
- WebForms vs MVC vs Web API

---

## 🔹 ADO.NET
- Connected vs Disconnected architecture
- SqlDataReader vs SqlDataAdapter
- Preventing SQL Injection in ADO.NET
- Transactions in ADO.NET

---

## 🔹 Solution Architecture / System Design  / Solution Architect
- When we use kafka - lots of cross questions on why we use kafka and not use SQL , more use cases of kafka
- How to build docker image - is the dependency automatically added or we need to add manually.
- Scenario based questions : How to create a Movie booking app with block and unblock seat.
- When to use mongodb over sql.
- Horizontal scaling and vertical scaling.
- Micro service vs Monolithik architecture ?
- Micro Frontend Architecture ?
- Major challenges faced during your last project ?
- CAP Theoram ?
- ACID Properties ?
- SOLID Priciple Understanding ?
- Data Structure , how and why use different types of data Strucure ?
- SQS , SNS , alternatives of Kafka ?


## 📌 Usage
Use this repository as a **quick reference** when preparing for **Fullstack, Backend, or .NET interviews**.

✅ Covers **Node.js, React.js, SQL, JavaScript, Java, .NET, and ADO.NET**.  
✅ Includes both **theory & coding questions**.  
✅ Based on **real interviews from 2025**.  

---
