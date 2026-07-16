# Kafka Interview Answers

> This document contains answers only for the Kafka questions that were actually asked in my interviews.

**Companies**

- Jio

---

# Q1. Have you used Kafka in your project? Explain the use case.

## Answer

Yes.

I have worked with Kafka for asynchronous communication between microservices.

Instead of one service directly calling another service synchronously, the producer publishes an event to Kafka, and the consumer processes it independently.

This improves scalability, fault tolerance, and system performance.

---

## Real-world Flow

```
User Registration

        │
        ▼

User Service

        │
 Publish Event
        │
        ▼

+----------------+
|     Kafka      |
+----------------+
        │
        ├─────────────► Email Service
        │
        ├─────────────► Notification Service
        │
        └─────────────► Analytics Service
```

---

## Example

Suppose a user registers.

Instead of

```
User Service

↓

Email Service

↓

Notification Service

↓

Analytics Service
```

(which is synchronous)

We publish an event.

```
User Registered Event

↓

Kafka Topic

↓

Consumers process independently
```

This makes the system loosely coupled.

---

## Advantages

- Asynchronous Processing
- Loose Coupling
- High Throughput
- Fault Tolerance
- Scalability
- Better Performance

---

## Interview Tip

Never say

> "Kafka is used for messaging."

Instead explain **where** you used it.

Example:

> "After user registration, an event is published to Kafka. Email and Notification services consume the event independently."

---

## Quick Revision

```
Producer

↓

Kafka Topic

↓

Consumer
```

---

## Possible Follow-up Questions

- Why Kafka?
- Kafka vs RabbitMQ?
- What is a Topic?

---

# Q2. What is Apache Kafka?

## Answer

Apache Kafka is a distributed event streaming platform used to exchange messages between applications.

It allows producers to publish messages and consumers to read them independently.

Kafka is designed for high throughput, scalability, and fault tolerance.

---

## Architecture

```
Producer

↓

Topic

↓

Broker

↓

Consumer
```

---

## Example

```
Order Service

↓

Kafka

↓

Inventory Service

↓

Email Service

↓

Payment Service
```

---

## Interview Tip

Remember

Kafka is **distributed**, **fault tolerant**, and **event-driven**.

---

## Quick Revision

```
Producer

↓

Broker

↓

Consumer
```

---

# Q3. What are Producer, Consumer, Topic and Broker?

## Producer

A Producer sends messages to Kafka.

Example

```
Order Service
```

publishes

```
Order Created
```

event.

---

## Consumer

A Consumer reads messages from Kafka.

Example

```
Email Service

↓

Reads

↓

Order Created
```

---

## Topic

A Topic is a logical channel where messages are stored.

Example

```
order-created
```

---

## Broker

A Broker is a Kafka server that stores topics and messages.

A Kafka cluster can have multiple brokers.

---

## Architecture

```
Producer

↓

Broker

↓

Topic

↓

Consumer
```

---

## Interview Tip

Remember

```
Producer

↓

Writes
```

```
Consumer

↓

Reads
```

```
Topic

↓

Stores Messages
```

```
Broker

↓

Kafka Server
```

---

## Quick Revision

| Component | Responsibility |
|-----------|----------------|
| Producer | Sends Messages |
| Topic | Stores Messages |
| Broker | Kafka Server |
| Consumer | Reads Messages |

---

# Q4. Why Kafka instead of REST API?

## Answer

REST APIs are synchronous.

The client waits until the server responds.

Kafka is asynchronous.

The producer publishes an event and continues without waiting.

---

## REST API

```
Order Service

↓

Payment Service

↓

Wait

↓

Response
```

---

## Kafka

```
Order Service

↓

Publish Event

↓

Continue Processing

↓

Consumer Processes Later
```

---

## Difference

| REST | Kafka |
|------|-------|
| Synchronous | Asynchronous |
| Tight Coupling | Loose Coupling |
| Request/Response | Event Driven |
| Client Waits | Producer Doesn't Wait |

---

## Real-world Example

After an order is placed,

there is no need to wait for:

- Email
- SMS
- Invoice

These can be processed asynchronously using Kafka.

---

## Quick Revision

```
REST

↓

Wait
```

```
Kafka

↓

Fire Event

↓

Continue
```

---

# Q5. What happens if a Consumer is down?

## Answer

Kafka stores messages inside the topic.

If a consumer is temporarily unavailable,

the messages remain in Kafka.

When the consumer comes back online,

it resumes processing from the last committed offset.

---

## Flow

```
Producer

↓

Kafka

↓

Consumer Down

↓

Message Stored

↓

Consumer Up

↓

Message Consumed
```

---

## Benefits

- No Data Loss
- Reliable Messaging
- Fault Tolerant
- Consumer Recovery

---

## Interview Tip

Kafka retains messages based on the configured **retention policy**, not based on whether a consumer has read them.

---

## Quick Revision

```
Consumer Down

↓

Kafka Stores Message

↓

Consumer Reads Later
```

---

## Possible Follow-up Questions

- What is Offset?
- What is Consumer Group?
- What is Retention?

---

# Q6. What is an Offset?

## Answer

Every message in a Kafka partition has a unique sequential number called an **Offset**.

Kafka uses offsets to keep track of which messages have already been consumed.

---

## Example

```
Partition-0

Offset 0

Offset 1

Offset 2

Offset 3

Offset 4
```

If a consumer has processed up to Offset 2,

it will continue from Offset 3 after restarting.

---

## Interview Tip

Offset is **not** the message ID.

It is the position of the message inside a partition.

---

## Quick Revision

```
Partition

↓

Offset

↓

Consumer Progress
```

---

# Q7. What is a Consumer Group?

## Answer

A Consumer Group is a set of consumers working together to consume messages from a topic.

Each partition is consumed by only one consumer within the same consumer group.

This enables parallel processing and scalability.

---

## Example

```
Topic

↓

4 Partitions

↓

Consumer Group

↓

Consumer-1 → P0, P1

Consumer-2 → P2, P3
```

---

## Benefits

- Parallel Processing
- Load Balancing
- Scalability
- High Throughput

---

## Interview Tip

If there are more consumers than partitions,

some consumers remain idle.

---

## Quick Revision

```
Topic

↓

Partitions

↓

Consumer Group

↓

Parallel Processing
```

---

# ✅ Kafka Questions Covered

### Actual Interview Question

- Have you used Kafka in your project? Explain the use case.

### Important Follow-up Questions

- What is Kafka?
- Producer
- Consumer
- Topic
- Broker
- Kafka vs REST API
- Consumer Down Scenario
- Offset
- Consumer Group

---
