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
- Closure
- Hoisting
- Rest vs Spread operator
- call(), bind(), apply()
- forEach vs map()
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
- Java memory (Stack vs Heap)
- Memory leak identification
- Multithreading (e.g., concurrency, synchronization, thread pools)
- Data structures (e.g., List, Map, Set implementations and their complexities)

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
