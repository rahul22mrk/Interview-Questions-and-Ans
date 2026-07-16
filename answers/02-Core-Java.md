# Core Java Interview Answers

> This document contains answers only for the Core Java questions that were actually asked in my interviews.

**Companies**
- CELESTIAL SYSTEMS PRIVATE LIMITED

---

# Q1. What is Serialization?

## Answer

Serialization is the process of converting a Java object into a byte stream so that it can be stored in a file, sent over a network, or transferred between applications.

To serialize an object, the class must implement the `Serializable` interface.

---

## Why is Serialization Used?

- Store objects in files.
- Transfer objects over the network.
- Session replication.
- Distributed systems.
- Caching.
- Messaging systems like Kafka.

---

## Syntax

```java
import java.io.Serializable;

class Employee implements Serializable {

    private int id;
    private String name;

}
```

---

## Deserialization

Deserialization is the reverse process of Serialization.

It converts the byte stream back into a Java object.

---

## Real-world Example

Suppose an object needs to be sent from one microservice to another.

The object is first serialized into bytes, transferred through the network, and then deserialized at the receiving end.

---

## Interview Tip

If the interviewer asks **"Why do we need Serialization?"**, don't just say *"to convert an object into bytes."*

Always mention real-world use cases like:

- Network communication
- File storage
- Session replication
- Distributed systems

---

## Possible Follow-up Questions

- What is Deserialization?
- What is Serializable?
- What is serialVersionUID?
- What happens if a class doesn't implement Serializable?

---

# Q2. What is a Marker Interface?

## Answer

A Marker Interface is an interface that does not contain any methods or constants.

It is used to provide metadata to the JVM or framework so that special processing can be performed.

---

## Syntax

```java
public interface Serializable {

}
```

No methods.

No variables.

Just a marker.

---

## Examples

- Serializable
- Cloneable
- Remote

---

## Why is it Used?

It tells the JVM or framework that the class has a special capability.

Example:

```java
class Employee implements Serializable {

}
```

Now the JVM knows that this object can be serialized.

---

## Real-world Example

Whenever an object is stored in a file or transferred over the network, the class implements `Serializable`.

---

## Interview Tip

Nowadays annotations like `@Override`, `@Entity`, and `@Component` are preferred in many frameworks, but Marker Interfaces are still used in Java.

---

## Possible Follow-up Questions

- Name some Marker Interfaces.
- Marker Interface vs Annotation.
- Why is Serializable called a Marker Interface?

---

# Q3. What is a Functional Interface?

## Answer

A Functional Interface is an interface that contains exactly one abstract method.

It is mainly used with Lambda Expressions introduced in Java 8.

---

## Syntax

```java
@FunctionalInterface
interface Calculator {

    int add(int a, int b);

}
```

---

## Why is it Used?

Functional Interfaces allow us to write Lambda Expressions, making the code shorter and more readable.

---

## Example

Without Lambda

```java
Calculator calculator = new Calculator() {

    @Override
    public int add(int a, int b) {
        return a + b;
    }

};
```

Using Lambda

```java
Calculator calculator = (a, b) -> a + b;
```

---

## Common Functional Interfaces

- Predicate
- Function
- Consumer
- Supplier
- Runnable
- Callable
- Comparator

---

## Where is it Used?

- Lambda Expressions
- Stream API
- Method References

---

## Interview Tip

A Functional Interface can contain:

- One abstract method ✅
- Multiple default methods ✅
- Multiple static methods ✅

Only **one abstract method** is mandatory.

---

## Possible Follow-up Questions

- What is @FunctionalInterface?
- Can a Functional Interface have default methods?
- Can it have static methods?

---

# Q4. Difference Between Interface and Abstract Class

| Interface | Abstract Class |
|-----------|----------------|
| Supports multiple inheritance | Supports single inheritance |
| No constructor | Constructor allowed |
| No instance variables | Instance variables allowed |
| Variables are public static final | Can have normal instance variables |
| Used to define a contract | Used to provide common implementation |

---

## Example

### Interface

```java
interface Payment {

    void pay();

}
```

Implementations

```java
class PhonePe implements Payment {

    @Override
    public void pay() {

    }

}
```

---

### Abstract Class

```java
abstract class Vehicle {

    String brand;

    Vehicle(String brand) {
        this.brand = brand;
    }

    abstract void start();

}
```

---

## Interview Tip

Remember this line:

> Interface defines **what to do**, whereas an Abstract Class defines **how to do it**.


# Core Java Interview Answers (Continued)

---

# Q5. After Java 8 introduced Default Methods, what differences still remain between an Interface and an Abstract Class?

## Answer

Java 8 introduced **default** and **static** methods in interfaces, allowing them to have method implementations. However, interfaces and abstract classes still have several important differences.

| Interface | Abstract Class |
|-----------|----------------|
| Supports multiple inheritance | Supports single inheritance |
| Cannot have constructors | Can have constructors |
| Cannot maintain object state | Can maintain object state using instance variables |
| Variables are `public static final` by default | Can have instance, static, final variables |
| Used to define a contract | Used to provide common implementation |
| Object cannot be created | Object cannot be created |

---

## Example

### Interface

```java
interface Vehicle {

    default void start() {
        System.out.println("Vehicle Started");
    }

}
```

### Abstract Class

```java
abstract class Vehicle {

    String company;

    Vehicle(String company) {
        this.company = company;
    }

    abstract void start();

}
```

---

## Interview Tip

If the interviewer asks,

> "Default methods aa gaye, phir Abstract Class ki kya need hai?"

Answer:

Because an Abstract Class can still have:

- Constructors
- Instance variables
- Protected and private methods
- Shared business logic
- State management

Interfaces are still used only to define behavior (contract).

---

## Possible Follow-up Questions

- Can an Interface have private methods?
- Can an Interface have constructors?
- Can an Abstract Class implement an Interface?

---

# Q6. When should we use an Interface and why?

## Answer

Use an Interface when multiple classes need to follow the same contract but can have different implementations.

It represents **capability** or **behavior**.

---

## Example

```java
interface Payment {

    void pay();

}
```

Implementations

```java
class PhonePe implements Payment {

    @Override
    public void pay() {
        System.out.println("Payment using PhonePe");
    }

}

class GooglePay implements Payment {

    @Override
    public void pay() {
        System.out.println("Payment using Google Pay");
    }

}
```

---

## Real-world Example

Spring Boot uses interfaces extensively.

Example

```java
UserRepository extends JpaRepository
```

Your implementation changes, but the contract remains the same.

---

## Interview Tip

Remember:

> Interface = Contract

---

## Possible Follow-up Questions

- Why not use an Abstract Class?
- Can one class implement multiple interfaces?

---

# Q7. When should we use an Abstract Class and why?

## Answer

Use an Abstract Class when multiple classes share common code, common properties, or common business logic.

It provides partial implementation.

---

## Example

```java
abstract class Vehicle {

    String company;

    Vehicle(String company) {
        this.company = company;
    }

    void stop() {
        System.out.println("Vehicle Stopped");
    }

    abstract void start();

}
```

---

## Real-world Example

Suppose every vehicle has:

- Company Name
- Fuel Type
- Registration Number

These common properties can be placed inside an Abstract Class.

---

## Interview Tip

Remember:

> Abstract Class = Common Implementation

---

## Possible Follow-up Questions

- Can an Abstract Class have constructors?
- Can an Abstract Class contain concrete methods?
- Can an Abstract Class contain final methods?

---

# Q8. What is the `transient` keyword?

## Answer

The `transient` keyword is used to prevent a field from being serialized.

When an object is serialized, all non-transient fields are converted into bytes.

Transient fields are ignored.

---

## Example

```java
import java.io.Serializable;

class User implements Serializable {

    String username;

    transient String password;

}
```

After deserialization,

```
username = Rahul
password = null
```

---

## Why is it Used?

Sensitive information should not be serialized.

Examples:

- Password
- OTP
- Access Token
- Temporary Cache
- Session Data

---

## Real-world Example

When a User object is stored in Redis or transferred over the network, the password should not be serialized.

---

## Interview Tip

Only instance variables can be transient.

Static variables are never serialized.

---

## Possible Follow-up Questions

- Can a static variable be transient?
- What happens during deserialization?

---

# Q9. Explain the Diamond Problem in Java.

## Answer

The Diamond Problem occurs when a class inherits the same default method from multiple interfaces.

The compiler cannot determine which implementation should be used.

---

## Example

```java
interface A {

    default void show() {
        System.out.println("A");
    }

}

interface B extends A {

}

interface C extends A {

}

class D implements B, C {

    @Override
    public void show() {
        System.out.println("Resolved");
    }

}
```

---

## How Java Solves It

Java forces the implementing class to override the conflicting method.

This removes ambiguity.

---

## Interview Tip

The Diamond Problem occurs only because of **default methods** in interfaces.

---

## Possible Follow-up Questions

- Why doesn't Java support multiple inheritance with classes?
- Does C++ have the Diamond Problem?

---

# Q10. What are Wrapper Classes and why are they used?

## Answer

Wrapper Classes convert primitive data types into objects.

---

## Primitive → Wrapper

| Primitive | Wrapper Class |
|------------|---------------|
| byte | Byte |
| short | Short |
| int | Integer |
| long | Long |
| float | Float |
| double | Double |
| char | Character |
| boolean | Boolean |

---

## Why are Wrapper Classes Needed?

Primitive types cannot be used where objects are required.

Wrapper Classes are mainly used in:

- Collections
- Generics
- Frameworks
- Hibernate
- Spring
- Reflection

---

## Example

```java
List<Integer> numbers = new ArrayList<>();

numbers.add(10);
numbers.add(20);
```

This works because Java automatically converts:

```java
int → Integer
```

This is called **Autoboxing**.

Similarly,

```java
Integer → int
```

is called **Unboxing**.

---

## Real-world Example

Whenever we store values inside a `List`, `Set`, or `Map`, Wrapper Classes are used because Java Collections store objects, not primitive data types.

---

## Interview Tip

Remember these two terms:

- Autoboxing → Primitive → Object
- Unboxing → Object → Primitive

---

## Possible Follow-up Questions

- What is Autoboxing?
- What is Unboxing?
- Why can't Collections store primitive data types?

---

# ✅ Core Java Questions Covered

- What is Serialization?
- What is a Marker Interface?
- Why do we use a Marker Interface?
- What is a Functional Interface?
- Where is a Functional Interface used?
- Difference between Interface and Abstract Class.
- After Java 8 default methods, what differences still remain?
- When should we use an Interface and why?
- When should we use an Abstract Class and why?
- What is the `transient` keyword?
- Explain the Diamond Problem.
- What are Wrapper Classes and why are they used?

---
---

## Possible Follow-up Questions

- Why can't an Interface have constructors?
- Can an Interface contain variables?
- Can an Abstract Class have abstract methods?
