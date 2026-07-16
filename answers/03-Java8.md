# Java 8 Interview Answers

> This document contains answers only for the Java 8 questions that were actually asked in my interviews.

**Companies**

- Jio

---

# Q1. What are the important features introduced in Java 8?

## Answer

Java 8 is one of the most significant releases of Java. It introduced several features that made Java more functional, concise, and suitable for modern application development.

### Important Features

- Lambda Expressions
- Functional Interfaces
- Stream API
- Method References
- Default Methods
- Static Methods in Interfaces
- Optional Class
- Date & Time API (`java.time`)
- CompletableFuture
- Nashorn JavaScript Engine

---

## Explanation

### 1. Lambda Expression

Allows writing anonymous functions in a concise way.

Example

```java
(a, b) -> a + b
```

---

### 2. Functional Interface

An interface having exactly one abstract method.

Example

```java
@FunctionalInterface
interface Calculator {

    int add(int a, int b);

}
```

---

### 3. Stream API

Used to process collections efficiently.

Supports

- Filtering
- Mapping
- Sorting
- Collecting
- Grouping

---

### 4. Method Reference

Shorter version of Lambda.

Example

```java
list.forEach(System.out::println);
```

---

### 5. Default Methods

Allows interfaces to have implemented methods.

Example

```java
interface Vehicle {

    default void start() {
        System.out.println("Started");
    }

}
```

---

### 6. Optional Class

Helps avoid NullPointerException.

Example

```java
Optional<String> name = Optional.of("Rahul");
```

---

### 7. New Date & Time API

Package

```java
java.time
```

Classes

- LocalDate
- LocalTime
- LocalDateTime
- ZonedDateTime

---

### 8. CompletableFuture

Used for asynchronous programming.

---

## Real-world Usage

In Spring Boot projects, Java 8 features are widely used.

Examples

- Stream API
- Lambda Expressions
- Optional
- Functional Interfaces
- Method References

---

## Interview Tip

If the interviewer asks,

**"Which Java 8 features have you used?"**

Mention only the features you've actually worked with:

- Lambda
- Streams
- Optional
- Default Methods
- Functional Interfaces

---

## Quick Revision

Java 8 introduced

- Lambda
- Stream API
- Functional Interface
- Optional
- Method Reference
- Default Method
- Date-Time API
- CompletableFuture

---

## Common Mistakes

❌ Saying Java 8 introduced Collections.

❌ Saying Streams modify the original collection.

---

## Possible Follow-up Questions

- What is a Functional Interface?
- What is Lambda?
- Difference between Collection and Stream?

---

# Q2. Give examples of Lambda Expressions and the Stream API.

## Answer

### Lambda Expression

A Lambda Expression is an anonymous function.

Instead of creating an anonymous class, Java 8 allows writing shorter code.

---

## Syntax

```java
(parameters) -> expression
```

---

## Example 1

Without Lambda

```java
Runnable r = new Runnable() {

    @Override
    public void run() {
        System.out.println("Hello");
    }

};
```

Using Lambda

```java
Runnable r = () -> System.out.println("Hello");
```

---

## Example 2

```java
Calculator add = (a, b) -> a + b;
```

---

## Stream API

A Stream is used to process data from collections.

It does not modify the original collection.

---

## Example

```java
List<String> names = List.of(
        "Rahul",
        "Amit",
        "Neha",
        "Rohit"
);

names.stream()
     .forEach(System.out::println);
```

---

## Lambda + Stream Example

```java
List<Integer> numbers = List.of(
        2,
        4,
        5,
        8,
        10
);

numbers.stream()
       .filter(n -> n % 2 == 0)
       .forEach(System.out::println);
```

Output

```
2
4
8
10
```

---

## Real-world Example

Suppose you have a list of employees.

Instead of using loops,

you can use

- filter()
- map()
- sorted()
- collect()

to write cleaner code.

---

## Interview Tip

Remember

Collection stores data.

Stream processes data.

---

## Quick Revision

Lambda

```
(parameters) -> expression
```

Stream

```
Collection → Stream → Process → Result
```

---

## Common Mistakes

❌ Streams modify the collection.

❌ Lambda can exist without Functional Interface.

---

## Possible Follow-up Questions

- What is Stream?
- What is Lazy Evaluation?
- What is Terminal Operation?

---

# Q3. Explain Stream operations like filter(), map(), and common collectors such as toList() and groupingBy().

## Answer

A Stream processes data using a pipeline.

Example

```
Collection
      ↓
stream()
      ↓
filter()
      ↓
map()
      ↓
collect()
```

---

# filter()

Used to filter elements based on a condition.

Example

```java
List<Integer> numbers = List.of(
        1,
        2,
        3,
        4,
        5
);

List<Integer> even = numbers.stream()
                            .filter(n -> n % 2 == 0)
                            .toList();
```

Output

```
2
4
```

---

# map()

Used to transform data.

Example

```java
List<String> names = List.of(
        "rahul",
        "amit"
);

List<String> upper = names.stream()
                          .map(String::toUpperCase)
                          .toList();
```

Output

```
RAHUL
AMIT
```

---

# toList()

Collects Stream elements into a List.

Example

```java
List<Integer> list = numbers.stream()
                            .filter(n -> n > 5)
                            .toList();
```

---

# groupingBy()

Groups objects based on a property.

Example

```java
Map<Integer, List<String>> map =
        names.stream()
             .collect(Collectors.groupingBy(String::length));
```

Example Output

```
4 → [Amit]

5 → [Rahul, Neeraj]
```

---

## Real-world Example

Suppose an Employee list contains

- Name
- Department
- Salary

You can

- filter employees having salary > 50000
- convert names to uppercase
- group employees by department

using Stream API.

---

## Interview Tip

Remember

Intermediate Operations

- filter()
- map()
- sorted()
- distinct()

Terminal Operations

- collect()
- forEach()
- count()
- reduce()
- anyMatch()

---

## Quick Revision

filter()

```
Filters data
```

map()

```
Transforms data
```

collect()

```
Collects result
```

groupingBy()

```
Groups data
```

---

## Common Mistakes

❌ map() filters data.

❌ filter() changes objects.

❌ Streams can be reused after a terminal operation.

---

## Possible Follow-up Questions

- Difference between map() and flatMap()?
- Difference between Stream and Parallel Stream?
- What are Intermediate and Terminal Operations?
- What is Lazy Evaluation?

---

# ✅ Java 8 Questions Covered

- What are the important features introduced in Java 8?
- Give examples of Lambda Expressions and the Stream API.
- Explain Stream operations like `filter()`, `map()`, `toList()`, and `groupingBy()`.

---
