# 🚀 Java Backend Interview Questions (Real Interviews)

> This document contains **only the actual questions** asked in my interviews at **Jio** and **CELESTIAL SYSTEMS PRIVATE LIMITED**.
>
> ❌ No generic interview questions.
> ✅ Only real interview questions.
> ✅ Duplicate questions removed.
> ✅ Topic-wise organized for quick revision.

---

# 📝 Introduction & Project

- Tell me about yourself.
- Explain your current project.
- Walk me through your projects and your specific responsibilities.
- What are your responsibilities in your current project?
- What work have you done in your project?
- Tell me about a critical production bug you handled and how you resolved it.

---

# ☕ Core Java

## Serialization

- What is Serialization?

## Marker Interface

- What is a Marker Interface?
- Why do we use a Marker Interface?

## Functional Interface

- What is a Functional Interface?
- Where is a Functional Interface used?

## Interface vs Abstract Class

- What is the difference between an Interface and an Abstract Class?
- After the introduction of default methods in Java 8, what differences still remain between an Interface and an Abstract Class?
- When should we use an Interface and why?
- When should we use an Abstract Class and why?

## Java Concepts

- What is the `transient` keyword?
- Explain the Diamond Problem in Java.
- What are Wrapper Classes?
- Why do we use Wrapper Classes?

---

# ☕ Java 8

- What are the important features introduced in Java 8?
- Give examples of Lambda Expressions and the Stream API.
- Explain Stream operations like `filter()`, `map()`, and common collectors such as `toList()` and `groupingBy()`.

---

# 📚 Collections

- What is the difference between `remove(int index)` and `remove(Object o)`?
- What happens if you iterate over a collection while removing elements from it? (`ConcurrentModificationException`, `HashMap`, `Hashtable`, `ConcurrentHashMap`)
- What happens if you try to add an element to an immutable list created using `List.of()` or a fixed-size list created using `Arrays.asList()`?

---

# 🧵 Multithreading & Concurrency

- How is rate limiting implemented in your current project?
- What is a Thread Pool?
- How would you handle a failing microservice without breaking the entire application flow? (Circuit Breaker, Retry, Timeout, Fallback)
- How would you create 10 threads using `ExecutorService` and submit tasks to them?
- What are the different ways to create a thread in Java?
- Where have you used concurrency in your project?
- How do you start a thread and get the current thread's name?
- Explain the Thread Lifecycle.
- If there are 10 tasks but only 2–3 threads available, how are tasks scheduled internally? (Queue/FIFO, Thread Reuse)
- What problems can occur if concurrency isn't handled properly?

---

# 🧠 JVM & Memory Management

- How is memory managed in Java?
- How does Garbage Collection work?

---

# ⚠️ Exception Handling

- What are the different types of exceptions in Java?
- How do you implement a custom exception?
- How do you handle exceptions using `try-catch`, `throw`, `throws`, and `finally`?

---

# 🗄️ SQL & Database

- What is the difference between a Primary Key and a Unique Key?
- What is Indexing in a database?
- How many types of indexing are there?
- Data fetching from a table is taking too much time. How would you optimize it?
- A table contains duplicate email addresses. How would you find the duplicate emails?
- What is the difference between `IN` and `EXISTS`?

---

# 🚀 Redis

- Have you used Redis?
- Where and why did you use Redis?

---

# 📩 Kafka

- Have you used Kafka in your project?
- Explain the Kafka use case in your project.

---

# 📄 Jasper Reports

- What are Fields in Jasper Reports?
- What are Parameters in Jasper Reports?
- What are Variables in Jasper Reports?
- A Jasper Report is taking too much time to render. How would you debug and optimize it?

---

# 📊 Data Structures

- If you have **10 million boolean values**, which would you choose and why?
  - `Boolean[]`
  - `boolean[]`
  - `BitSet`

---

# 📌 Interview Coverage

## Companies

- Jio
- CELESTIAL SYSTEMS PRIVATE LIMITED

## Topics Covered

- Introduction & Project
- Core Java
- Java 8
- Collections
- Multithreading & Concurrency
- JVM & Memory Management
- Exception Handling
- SQL & Database
- Redis
- Kafka
- Jasper Reports
- Data Structures

---

> 💡 **Note:** This document contains only the questions that were actually asked during my interviews. It is intended for quick revision before future interviews.
