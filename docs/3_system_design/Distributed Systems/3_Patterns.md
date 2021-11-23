---
layout: default
title: Patterns
parent: Distributed Systems
grand_parent: System design
nav_order: 3
permalink: /systemdesign/dissystem/patterns
---
<div align="center" markdown="1">
Patterns / Java resources / Tutorial

{: .fs-8 .fw-400 }
</div>

# Communication Patterns

One of the main differentiating characteristics of distributed systems with other systems is that the various nodes need to exchange data across the network boundary. In this chapter, we will examine how we can achieve this and the trade-offs of each approach.

## Serialization and deserialization
Every node needs a way to transform data that resides in memory into a format that can be transmitted over the network, and it also needs a way to translate data received from the network back to the appropriate in-memory representation. These processes are called serialization and deserialization, respectively. The following illustration shows this process:

![advanced](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/big/za1.png)

Note: Serialization are also used to transform data in a format that’s suitable for storage, not only communication.

## Serializing and deserializing data
The various nodes of the system need to agree on a common way to serialize and deserialize data. Otherwise, they will not be able to translate the data they send to each other. There are various options available for this purpose. We will discuss three approaches in this lesson:

## Native support
Some languages provide native support for serialization, such as Java and Python via its pickle module.

## Advantages and disadvantages
The main benefit of this option is convenience since there is very little extra code needed to serialize and deserialize an object. However, this comes at the cost of maintainability, security, and interoperability.

Given the transparent nature of how these serialization methods work, it becomes hard to keep the format stable since it can be affected even by small changes to an object that do not affect the data contained in it (e.g., implementing a new interface).

Furthermore, some of these mechanisms are not very secure since they indirectly allow a remote data sender to initialize any objects they want, thus introducing the risk of remote code execution.

Last but not least, most of these methods are available only in specific languages, which means systems developed in different programming languages will not be able to communicate.

Note: Some third-party libraries operate in a similar way using reflection or bytecode manipulation, such as Kryo. These libraries tend to be subject to the same trade-offs.

## Libraries
Another option is a set of libraries that serialize an in-memory object based on instructions provided by the application. These instructions can be imperative or declarative, i.e., annotating the fields to be serialized instead of explicitly calling operations for every field.

An example of such a library is Jackson, which supports many different formats, such as JSON and XML.

## Advantages and disadvantages
The main benefit of this approach is the ability to interoperate between different languages.

Most of these libraries also have rather simple rules on what gets serialized, so it’s easier to preserve backwards compatibility when evolving some data, i.e., introducing new optional fields.

They also tend to be a bit more secure. As they reduce the exploitation surface by reducing the number of types that can be instantiated during deserialization, i.e. only the ones that have been annotated for serialization and thus implicitly whitelisted.

However, sometimes, they can create additional development efforts since the exact serialization mapping needs to be defined on every application.

## Interface definition languages (IDL)
Interface definition languages (IDL) are specification languages used to define the schema of a data type in a language-independent way.

## Advantages and disadvantages
These definitions can dynamically generate code in different languages that will perform serialization and deserialization when included in the application. It allows applications built in different programming languages to interoperate, depending on the languages supported by the IDL. In addition, each IDL allows for different forms of evolution of the underlying data types.
They also reduce duplicate development effort, but they require adjusting build processes so that they can integrate with the code generation mechanisms. Some examples of IDLs are Protocol Buffers, Avro, and Thrift.
The difference between the library and the interface definition languages (IDL) approach, using Jackson and Protocol Buffers, is shown in the following illustration:

![advanced](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/big/za2.png)

## Transfer of Data

In the previous lesson we studied the options for creating and parsing the data sent through the network. However, the main ways this data is sent and received and the associated trade-offs remain unanswered.

The above question does not refer to the underlying transfer protocols that are used, such as Ethernet, IP, TCP, UDP, etc. Instead, it refers to the two basic, high-level forms of communication, synchronous and asynchronous communication.

## Synchronous and asynchronous communication
If node A is communicating synchronously with node B, node A will wait until it has received a response from node B before proceeding with subsequent tasks.

If node A is communicating asynchronously instead, this means that it does not have to wait until that request is complete; it can proceed and perform other tasks at the same time.

The Following illustration shows the difference between synchronous and asynchronous communication:

![advanced](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/big/za3.png)

## Example
Synchronous communication is typically used in cases where node A needs to retrieve some data to execute the next task, or it needs to be sure a side-effect has been performed successfully on node B’s system before proceeding.

Asynchronous communication is preferred in cases where the operation performed in node B can be executed independently without blocking other operations from making progress.

For example, an e-commerce system might need to know that a payment was performed successfully before dispatching an item, thus using synchronous communication. However, after dispatching the order, the process that sends the appropriate notification e-mail to the customer can be triggered asynchronously.

## Implementing synchronous and asynchronous communication
Synchronous communication is usually implemented on top of the existing protocols, such as using HTTP to transmit data in JSON or some other serialization formats (e.g., protocol buffers)…

In the case of asynchronous communication between two nodes, there is usually a need to store incoming requests until they are processed persistently. This is needed so that requests are not lost even if the recipient node fails for some reason.

Note: This is not necessarily needed in synchronous communication because if the recipient crashes before processing a request, the sender will notice at some point, and it can retry the request. Even when using asynchronous communication, there can be cases where losing requests is not a big problem. For example, the autocomplete functionality of a search engine can be done asynchronously in the background, and losing some requests will lead to fewer suggestions to the user so that it might be acceptable.

These requests can be stored in an intermediate datastore to prevent loss in case of failures. The datastores that are typically used for this purpose belong in two main categories:
* Message queues
* Event logs

## Datastores for Asynchronous Communication

In the previous lesson we learned that to achieve asynchronous communication, we need to store requests in datastores, and these datastores belong to two main categories: message queues and event logs.

## Message Queues
Some commonly used message queues are ActiveMQ, RabbitMQ, and Amazon SQS.

A message queue usually operates with first-in, first-out (FIFO) semantics. This means that messages, in general, are added to the tail of the queue and removed from the head.

Note: Multiple producers can send messages to the queue, and multiple consumers can receive messages and process them concurrently.

Depending on how a message queue is configured, messages can be deleted in one of the following two cases.

As soon as they are delivered to a consumer.
Only after a consumer has explicitly acknowledged, it has successfully processed a message.
The former essentially provides at-most-once guarantees since a consumer might fail after receiving a message but before acknowledging it. The latter can provide at-least-once semantics since at least a single consumer must have processed a message before it is removed from the queue.

## Coping with failed consumers
Most message queues contain a timeout logic on unacknowledged messages to cope with failed consumers ensuring liveness.

Note: For example, Amazon SQS achieves that using a per-message visibility timeout. At the same timeActiveMQ and RabbitMQ rely on a connection to timeout to redeliver all the unacknowledged messages of this connection.

This means that unacknowledged messages are being put back to the queue and redelivered to a new consumer. Consequently, there are cases where a message might be delivered more than once to multiple consumers. The application is responsible for converting the at-least-once delivery semantics to exactly-once processing semantics. As we have learned already, a typical way to achieve this is by associating every operation with a unique identifier that is used to deduplicate operations originating from the same message.

Note: The side-effects from the operation and the storage of the unique identifier must be done atomically to guarantee exactly-once processing. A simple way to do this is to store both in the same datastore using a transaction.

The following illustration shows a practical example of exactly-once processing through deduplication:

![advanced](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/big/za4.png)

## Event log
An event log provides a slightly different abstraction than a message queue. Messages are still inserted by producers at the tail of the log and stored in an ordered fashion. However, the consumers are free to select the point of the log they want to consume messages from, which is not necessarily the head.

Messages are typically associated with an index that consumers can use to declare where they want to consume from.

Another difference with message queues is that the log is typically immutable, so messages are not removed after they are processed. Instead, a garbage collection runs periodically, which removes old messages from the head of the log. The consumers are responsible for keeping track of an offset indicating the part of the log they have already consumed in order to avoid processing the same message twice, thus achieving exactly-once processing semantics. This offset plays the role of the unique identifier for each message similarly as described previously.

Some examples of event logs are Apache Kafka, Amazon Kinesis, and Azure Event Hubs.

## Communication Models

## Communication models
Message queues and event logs can enable two different forms of communication, known as point-to-point and publish-subscribe.

## The point-to-point model
The point-to-point model is used when we need to connect only two applications.

Note: Point-to-point refers to the number of applications, not the actual servers. Every application on each side might consist of multiple servers that produce and consume messages concurrently.

## The publish-subscribe model
The publish-subscribe model is used when more than one application might be interested in the messages sent by a single application.

For example, suppose a customer made an order might be needed by an application sending recommendations for similar products, an application that sends the associated invoices, and an application that calculates loyalty points for the customer.

Using a publish-subscribe model, the application handling the order can send a message about this order to all the applications that need to know about it, sometimes without even knowing which these applications are.

## Implementing point-to-point and publish-subscribe models
These two models of communication are implemented slightly differently depending on whether an event log or a message queue is used. This difference is due to the fact that the consumption of messages behaves differently in each system:

## Using message queue
Point-to-point communication is pretty straightforward when using a message queue. Both applications are connected to a single queue, where messages are produced and consumed.

In the publish-subscribe model, the producer application can create and manage one queue, and every consumer application can create its own queue. There also needs to be a background process that receives messages from the producer’s queue and forwards them to the consumers’ queues.

Note: Some systems might provide facilities that provide this functionality out of the box. For example, this is achieved in ActiveMQ via a bridge and in Amazon SQS via a separate AWS service, called Amazon Simple Notification Service (SNS).

## Using event log
When using an event log, both models of communication can be implemented in the same way. The producer application writes messages to the log, and multiple consumer applications can be consumed from the log concurrently the same messages maintaining independent offsets.

This difference in implementing these models using the message queue and the event log is shown in the following illustration:

![advanced](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/big/za5.png)

# Coordination Patterns

In many cases, a business function is performed by many different systems that cooperate with each other to perform some part of the overall function. For example, displaying a product page might require combining functionality from different systems, such as an advertising system, a recommendation system, a pricing system, etc.

The previous chapter examined the basic ways in which two different systems can communicate. Now we will explore the two basic approaches that can be used to coordinate different systems to perform a common goal: orchestration and choreography.

## Orchestration
In orchestration, a single, central system is responsible for coordinating the execution of the various other systems, thus resembling a star topology, as shown in the following illustration. That central system is referred to as the orchestrator. It needs to know about all the other systems and their capabilities. But these systems can be unaware of each other.

![advanced](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/big/za6.png)

## Choreography
In choreography, systems coordinate with each other without the need for an external coordinator. They are essentially placed in a chain, where each system is aware of the previous and the next system in the topology. A request is successively passed through the chain from each system to the next one. We can see this process in the following illustration:

![advanced](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/big/za7.png)

Note: The communication link between two systems can be of any of the two forms described in the previous section. The systems can either communicate synchronously (i.e., using RPC calls) or asynchronously (i.e., via an intermediary message queue).

Each option is subject to different trade-offs, some of which we will discuss in the next chapters.

## The behavior of coordination patterns
The patterns mentioned above will behave differently depending on whether the function performed has side-effects or not.

## A function with no side-effects
Displaying a product page is most likely a function that does not have side effects. This means that partial failures can be treated simply by retrying any failed requests until they all succeed. Alternatively, if some requests continuously fail, they are abandoned, and the original request is forced to fail.

## A function with side-effects
Processing a customer order is most likely an operation with side effects, which might need to be performed atomically. It’s probably undesirable to charge a customer for an order that cannot be processed or send an order to a customer who cannot pay.

## Ensuring atomicity
Each of the patterns mentioned above needs to ensure atomicity.

One way to achieve this would be via a protocol like a two-phase commit.
An alternative would be to use the concept of saga transactions described previously in the course.
The first approach would fit better in the orchestrator pattern where the orchestrator plays the role of the coordinator of the two-phase commit protocol, while the second approach could be used in both patterns.

# Data Synchronisation

## The need to store data in multiple places
There are cases where we need to store the same data in multiple places and potentially different forms. These are also referred to as materialized views. Below are some examples of such cases:
* Data that resides in a persistent datastore also needs to be cached in a separate in-memory store so that read operations can be processed from the cache with lower latency. Writes operations need to update both the persistent datastore and the in-memory store.
* Data stored in a distributed key-value store must also be stored in a separate datastore that provides efficient full-text search, such as ElasticSearch or Solr. Depending on the form of read operations, the appropriate datastore can be used for optimal performance.
* Data stored in a relational database also needs to be stored in a graph database so that graph queries can be performed in a more efficient way.

Note: Given that the data resides in multiple places, we need a mechanism that keeps them in sync. This chapter will examine some of the approaches available for this purpose and the associated trade-offs.

## Synchronizing data using dual writes
One approach is to perform writes to all the associated datastores from a single application that receives update operations. This approach is sometimes referred to as dual writes. Typically, writes to the associated data stores are performed synchronously to update data in all the locations before responding to the client with a confirmation that the update operation was successful.

![advanced](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/big/za8.png)

## Problems
One drawback of this approach is how the system handles partial failures and their impact on atomicity. If the application updates the first datastore successfully, but the request to update the second datastore fails, then atomicity is violated. Due to this the overall system becomes inconsistent. It’s also unclear what the response to the client should be in this case since data has been updated, but only in some places.

However, even if we assume that there are no partial failures, there is another pitfall in how concurrent writers handle the race conditions and their impact on isolation. Let’s assume two writers submit an update operation for the same item. The application receives them and attempts to update both datastores, but the associated requests are re-ordered, as shown in the following illustration:

![advanced](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/big/za9.png)

In the above illustration, the first datastore contains data from the first request, while the second datastore contains data from the second request. This also leaves the overall system in an inconsistent state.

## Solution
An obvious solution to mitigate these issues is to introduce a distributed transaction protocol that provides the necessary atomicity & isolation, such as a combination of two-phase commit and two-phase locking. To be able to do this, the underlying datastores need to provide support for this. Even in that case, this protocol will have some performance and availability implications, as explained in the previous chapters.

## Event Sourcing

## Synchronizing data using event sourcing
Event sourcing is another approach for data synchronization. It writes any update operations to an append-only event log. The interested applications consume events from this log and store the associated data in their preferred datastore. The current state of the system can be derived simply by consuming all the events from the beginning of the log.

However, applications typically save periodical snapshots (also known as checkpoints) of the state to avoid having to re-consume the whole log in case of failures. In this case, an application that recovers from a failure only needs to replay the events of the log after the latest snapshot.

![advanced](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/big/za10.png)

## Mitigating the problems of dual writes
Event sourcing approach does not violate atomicity, which means there is no need for an atomic commit protocol. The reason is every application is consuming the log independently, and they will eventually process all the events successfully, restarting from the last consumed event in case of a temporary failure.

The isolation problem in the dual writes approach is also mitigated since the applications will be consuming all the events in the same order.

## Caveat in event sourcing approach
There is a small caveat in the event sourcing approach: applications might be consuming the events from the log at different speeds, which means an event will not be reflected instantly on all the applications. This phenomenon can be handled at the application level. For example, if an item is unavailable in the cache, the application can query the other datastores.

A different manifestation of this problem could be a successfully indexed item that was not stored in the authoritative datastore yet, leading to a dangling pointer. This could also be mitigated at the application level by identifying and discarding these items instead of displaying broken links. If no such technique can be applied at the application level, a concurrency control protocol could be used, e.g., a locking protocol with the associated performance and availability costs.

## Problems
Some kinds of applications need to perform update operations that require an up-to-date view of the data. The simplest example is a conditional update operation, it creates a user if no user with the same username exists already.

Note: The Conditional update operation is also known as a compare-and-set (CAS) operation.

It is not easily achievable when using event sourcing because the applications consume the log asynchronously, so they are only eventually consistent.

In the next lesson, we will learn another approach that solves this problem.

## Change Data Capture (CDC)

## Data synchronization using change data capture (CDC)
Change data capture (CDC) is another approach used for data synchronization. It solves the asynchronous consumption of log of event sourcing, as discussed in the previous lesson.

![advanced](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/big/za11.png)

## Mitigating the problem of event sourcing
In the CDC approach, The application selects a datastore as the authoritative source of data, where all update operations are performed. It then creates an event log from this datastore that is consumed by all the remaining operations the same way as in event sourcing. This primary datastore needs to provide the necessary transactional semantics and a way to monitor changes in the underlying data to produce the event log. Relational databases are usually a good fit for this since most of them provide strong transactional guarantees. In addition, they internally use a write- ahead-log (WAL) that imposes an order on the performed operations and can feed an order event log.

Note: An example of such tool is Debezium.

As a result, clients can perform conditional updates on the current state, and the remaining applications can apply these operations independently at their datastores.

# Shared-nothing Architectures

## Problems with sharing
At this point, it must have become evident that sharing leads to coordination, which is one of the main factors that inhibit high availability, performance, and scalability.

For example, we have already explained how distributed databases can scale to larger datasets more cost-efficiently than centralized, single-node databases. At the same time, some form of sharing is sometimes necessary and even beneficial for the same characteristics. For instance, a system can increase its overall availability by reducing sharing through partitioning since the various partitions can have independent failure modes. However, when looking at a single data item, availability can be increased by increasing sharing via replication.

## Solution
A key takeaway from all of the above problems is reducing sharing.

## Reducing sharing
Reducing sharing can be very beneficial when applied properly. Some system architectures follow this principle to the extreme to reduce coordination and contention so that every request can be processed independently by a single node or a single group of nodes in the system. These are usually called shared-nothing architectures.

This chapter will explain how we can use this principle to build such architectures and what are some of its trade-offs.

## Techniques for reducing sharing
A basic and widely used technique for reducing sharing is the decomposing stateful and stateless parts of a system.

## Decomposing stateful and stateless parts of a system
The main benefit from this is that stateless parts of a system tend to be fully symmetric and homogeneous, which means that every instance of a stateless application is indistinguishable from the rest. Separating them makes scaling a lot easier.

Since all the instances of an application are identical, one can balance the load across all of them easily way since all of them should be capable of processing any incoming request.

Note: In practice, the load balancer might need to have some state that reflects the load of the various instances.

The system can be scaled out to handle more load by simply introducing more instances of the applications behind a load balancer. The instances could also send heartbeats to the load balancer so that the load balancer can identify the ones that have potentially failed and stop sending requests to them. The same could also be achieved by the instances exposing an API, where requests can be sent periodically by the load balancer to identify healthy instances.

Of course, to achieve high availability and scale incrementally, the load balancer also needs to be composed of multiple redundant nodes. There are different ways to achieve this, but a typical implementation uses a single domain name (DNS) for the application that resolves multiple IPs belonging to the various servers of the load balancer. The clients, such as web browsers or other applications, can rotate between these IPs. The DNS entry needs to specify a relatively small time-to-live (TTL) so that clients can identify new servers in the load balancer fleet relatively quickly.

## Managing stateful systems
The stateful systems are a bit harder to manage since the various nodes of the system are not identical.

Each node contains different pieces of data, to perform appropriate routing to direct requests to the proper part of the system. As implied before, the presence of this state also creates tension that prevents us from completely eliminating sharing if there is a need for high availability.

A combination of partitioning and replication is used to strike a balance. Data are partitioned to reduce sharing and create some independence and fault isolation, but every partition is replicated across multiple nodes to make every partition fault-tolerant. We have already examined several systems that follow this pattern, such as Cassandra and Kafka.

## Sharing as a spectrum
Sharing is not a binary property of a system but rather a spectrum.

On the one end of the spectrum, there might be systems with as little sharing as possible, i.e., not allowing any transactions across partitions to reduce the coordination needed.

Some systems might fall in the middle of the spectrum, where transactions are supported but performed in a way that introduces coordination only across the involved partitions instead of the whole system.

Lastly, systems that store all the data in a single node fall somewhere on the other end of the spectrum.

## A typical shared-nothing architecture
The following illustration shows an example of a shared-nothing architecture:

![advanced](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/big/za12.png)

## Benefits and Drawbacks

## Benefits
The shared-nothing architecture provides many benefits from a performance and fault-tolerance perspective. It provides scalability and availability guarantees.

## Scalability
All layers of the applications can be incrementally scaled out or in depending on the load.

Note: Scalability is easier and quicker to achieve in the stateless components since it requires less data transfer.

## Availability
The system is resilient to single-node and multi-node failures.

More specifically, these two different forms of failure impact the stateless parts of the system in a similar way. The size of the impact is just different. For example, the remaining nodes might need to handle a bigger load, or more servers might need to be provisioned.

For the stateful parts of the architecture, single and multi-node failures have slightly different behaviors.

Single-node failures are a lot easier to handle since each partition can use a consensus-based technique for replication which can remain fully functional as long as a majority of nodes is healthy.
However, multi-node failures can affect a majority, thus making a partition unavailable
Note: Even in this case, the good thing is only this partition will be unavailable, and the rest of the system’s data will still be available.

## Supporting the problems that are amenable to partitioning
Shared-nothing architecture tends to be a good fit for problems that are amenable to fine-grained partitioning.

Some examples of problems in this space are:
* Managing user sessions
* Managing the products of a catalog

In both cases, data can easily be partitioned in a way where data access operations will need to access a single data item.

Sessions can be assigned a unique identifier, and this attribute can partition them.
Products can be partitioned according to a similar product identifier.
If sessions and products are mostly retrieved and updated by their identifier, they can be done efficiently by querying only the nodes with the associated data.

## Concurrency control
There is also space for some form of limited concurrency control in the scope of a partition.

For cases where single-item access is the norm, a common technique is using the optimistic concurrency control to reduce overhead and contention. It is be achieved by including a version attribute on every data item. Every writer performs a read before a write to find the current version and then includes the current version in the update as a condition to be satisfied for it to be completed.

Of course, this requires the corresponding datastore to provide support for conditional updates. If a concurrent writer has updated the same item in the meanwhile, the first writer will have to abort and restart by performing a new read to determine whether its initial write should still apply and, if so, retry it.

## Drawback of a shared-nothing architecture
Along with the benefits described above, shared-nothing architecture has some drawbacks also…

The main drawback is reduced flexibility. If the application needs access to new data access patterns efficiently, it might be hard to provide it given the system’s data have been partitioned in a specific way.

For example, attempting to query by a secondary attribute that is not the partitioning key might require access to all the nodes of the system. This reduced flexibility might also manifest in a lack of strong transactional semantics.

Applications that need to perform reads of multiple items with strong isolation or write multiple items in a single atomic transaction might not do this under this form of architecture. It might only be possible at the cost of excessive additional overhead.


# Distributed Locking
  
## Recalling concurrency
In the introductory chapters of the course we learned that concurrency is one of the factors that contribute significantly to the complexity of distributed systems.

A mechanism is needed to ensure that all the various components of a distributed system running concurrently do so in a safe way and does not bring the overall system to an inconsistent state.

## Leader election problem
We have already discussed the leader election problem, where the system needs to ensure only one node in the system can perform the leader duties at any point in time.

## Solution
Amongst the available techniques, locking is the simplest solution and one that is used commonly. However, locking techniques are subject to different failure modes when applied in a distributed system.

This chapter will cover common pitfalls in locks and address them to use locking safely in a distributed system.

## Locks
The main property derived from the use of locks is mutual exclusion. Multiple concurrent actors can be sure that only one will perform a critical operation at a time.

All actors follow the same sequence of operations, first they acquire the lock, perform that critical operation, and then release the lock so that other workers can proceed.

This sequence of operation is usually simple to implement when all actors are running inside the same application sharing a single memory address space and the same lifecycle. However, doing the same in a distributed system is much more complicated, mostly due to the potential of partial failures.

## Complication of locking in distributed systems
The main complication of locking in a distributed system is that the various system nodes can fail independently. As a result, a node that is currently holding a lock might fail before it releases the lock. This would bring the system to a halt until that lock is released via some other means (i.e., via an operator), thus reducing availability significantly. A timeout mechanism can be used to cope with this issue.

## Using leases instead of locks
A lease is essentially a lock with an expiry timeout, after which the lock is automatically released by the system responsible for managing the locks. By using leases instead of locks, the system can automatically recover from failures of nodes that have acquired locks by releasing them and allowing other nodes to acquire them to make progress.

## Safety risks in lease
Leases introduce new safety risks.There are now two different nodes in the system that have different views about the state of the system, specifically the nodes that hold a lock. This is because these nodes have different clocks, so the time of expiry can differ between them. And because a failure detector cannot be perfect, as explained earlier in the course.

The fact that part of the system considers a node that can fail does not necessarily mean this node will fail. It could be a network partition that prevents some messages from being exchanged between some nodes, or that node might be busy processing something unrelated. As a result, that node might think it still holds the lock even though it has expired and is automatically released by the system.

The following illustration shows an example, where nodes A and B are trying to acquire a lease in order to perform some operations in a separate system.

# Compatibility Patterns

As explained earlier, a defining characteristic of distributed systems is composed of multiple nodes. It is useful to allow the various nodes of such a system to operate independently for various reasons. A typical requirement for some applications in real life is to deploy new versions of the software with zero downtime.

## Rolling deployments
The simplest way to deploy new versions of the software with zero downtime is to perform rolling deployments instead of deploying in lockstep the software to all the servers at the same time.

Note: In some cases, this is not just a nice-to-have but an inherent characteristic of the system.

## Example
Mobile applications (e.g., Android applications), where user consent is required to perform an upgrade, imply that users are deploying the new version of the software at their own pace. As a result, the various nodes of a distributed system can run different software versions at any time.

This chapter will examine the implications of rolling deployment and some techniques that will help to manage this complication.

## Implications of rolling deployments
When the system performs rolling deployments, it manifests in many different ways. One of the most common ways is when two different applications communicate with each other. At the same time each one of them evolves independently by deploying new versions of its software.

For example, one of the applications might want to expose more data at some point. If this is not done carefully, the other application might not understand the new data making the whole interaction between the applications fail. Two very useful properties related to this are backwards compatibility and forward compatibility.

Backwards compatibility is a property of a system that provides interoperability with an earlier version of itself or other systems.

Forward compatibility is a property of a system that provides interoperability with a later version of itself or other systems.

These two properties essentially reflect a single characteristic viewed from different perspectives, those of the sender and the recipient of data.

## Examples
LLet’s consider an example of two systems, S and R, where the former sends some data to the latter. We can say that a change on system “S” is backwards compatible if older versions of “R” will be able to communicate successfully with a new version of S. We can also say that the system R is designed in a forward compatible way so that it will be able to understand new versions of S. Let’s discuss some examples in detail.

Let’s assume system S needs to change the data type of a specific attribute. Changing the data type of an existing attribute is not a backwards compatible change in general. System R would expect a different type for this attribute, and it would fail to understand the data. However, this change could be decomposed into the following sub-changes that preserve compatibility between the two systems.

The system R can deploy a new version of the software capable of reading that data either from the new attribute with the new data type or the old attribute with the old data type. The system S can then deploy a new version of the software that stops populating the old attribute and starts populating the new attribute.

Note: Whether a change is backwards compatible or not, it can differ depending on the used serialization protocol. This article explains it nicely.

The previous example demonstrated that the seemingly trivial changes to the software are more complicated when they need to perform in a distributed system safely. As a consequence, maintaining backward compatibility imposes a tradeoff between agility and safety.

## Semantic versioning
It’s usually beneficial to version the API of an application since that makes it easier to compare versions of different nodes and applications of the system and determine which versions are compatible with each other or not. Semantic versioning is a very useful convention, where each version number consists of three digits X.Y.Z.

## Protocol negotiation
Protocol negotiation is another technique for maintaining backward compatibility through the use of explicitly versioned software.

Let’s consider an example mentioned previously, where the client of an application is a mobile application. Every version of the application needs to be backward compatible with all the client application versions running on user phones currently. This means that the staged approach described previously cannot be used when making backward incompatible changes since end users cannot be forced to upgrade to a newer version. Instead, the application can identify the version of the client and adjust its behavior accordingly.

For example, consider a feature introduced on version 4.1.2 that is backward incompatible with versions < 4.x.x. If the application receives a request from a 3.0.1 client, it can disable that feature to maintain compatibility. If it receives a request from a 4.0.3 client, it can enable the feature.

![advanced](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/big/za13.png)

Patch version: This version is incremented when a backwards compatible bug fix is made to the software.

Minor version: This version is incremented when new functionality is added in a backward compatible way.

Major version: This version is incremented when a backwards incompatible change is made.

As a result, the clients of the software can easily understand the compatibility characteristics of new software and the associated implications.

When providing software as a binary artifact, the version is usually embedded in the artifact. The consumers of the artifact then need to take the necessary actions if it includes a backwards incompatible change, e.g., adjusting their application’s code.

## Applying semantic versioning to live applications
Semantic versioning is implemented slightly differently in live applications. The major version needs to be embedded in the address of the application’s endpoint, while the major and patch versions can be included in the application’s responses. For an example, see this. This is needed so that clients can automatically upgrade to newer versions of the software if desired, but only if these are backward compatible.

## Application unaware of other applications consuming its data
In some cases, an application might not be aware of the other applications consuming its data. An example of this is the publish-subscribe model.

## The publish-subscribe model
In the publish-subscribe model, the publisher does not necessarily need to know all the subscribers. However, it’s still very important to ensure that the consumers can deserialize and process any produced data successfully as its format changes.

One pattern used here is defining a schema for the data used by both producers and consumers. This schema can be embedded in the message itself. Otherwise, to avoid duplication of the schema data, a reference to the schema can be put inside the message, and the schema can be stored in a separate store. For example, this pattern is commonly used in Kafka via the Schema Registry.

However, it’s important to remember that producers and consumers are evolving independently, even in this case. Hence, consumers are not necessarily using the latest version of the schema used by the producer. So, producers need to preserve compatibility either by ensuring consumers can read data of the new schema using an older schema or by ensuring all consumers have started using the new schema before producing messages with it.

Note that similar considerations need to be made for the compatibility of the new schema with old data. For example, if consumers cannot read old data with the new schema, the producers might have to make sure everyone has consumed all the messages with the previous schema first. Interestingly, the Schema Registry defines different categories of compatibility along these dimensions, which determine what changes are allowed in each category and the upgrade process, e.g., if producers or consumers need to upgrade first. It can also check two different versions of a schema and confirm that they are compatible under one of these categories to prevent errors later on. See this, for example.

## Two-phase deployment
Note that it’s not only changes in data that can break backward compatibility. Slight changes in the behavior or semantics of an API can also have serious consequences in a distributed system. For example, let’s consider a failure detector that uses heartbeats to identify failed nodes. Every node sends a heartbeat every one second, and the failure detector considers a node failed if it hasn’t received a single heartbeat in the last three seconds. This causes a lot of network traffic that affects the performance of the application, so we will increase the interval of a heartbeat from one to five seconds and the threshold of the failure detector from three to fifteen seconds.

Suppose we perform a rolling deployment of this change. In that case all the servers with the old version of the software will start thinking all the servers with the new version have failed. This is due to the fact that their failure detectors will still have the old deadline of three seconds, while the new servers will send a heartbeat every five seconds.

One way to make this change backward compatible would be to perform an initial change that increases the failure detector threshold from three to fifteen seconds. And then, follow this with a subsequent change that increases the heartbeat interval to five seconds only after the first change has been deployed to all the nodes. This technique of splitting a change into two parts to make it backward compatible is commonly used and it’s also known as two-phase deployment.

# Dealing with Failure

Failure is the norm in a distributed system, so building a system that can cope with failures is crucial.This chapter will cover principles on dealing with failures and basic patterns for building systems that are resilient to failures.

In distributed systems, dealing with a failure consists of three main parts: main parts:
* identifying the failure
* recovering from the failure

containing a failure to reduce its impact, in some cases

## Hardware failures
Hardware failures can be the most damaging ones since they can lead to data loss or corruption. Also,the probability of a hardware failure is significantly higher in a distributed system due to the bigger number of hardware components involved.

## Silent hardware failures
Silent hardware failures are the ones with the biggest impact since they can potentially affect the behavior of a system without anyone noticing.

## Example
A node in the network corrupts some part of a message and the recipient receives data that is different from what the sender originally sent without being able to detect that. Similarly, data written to a disk can be corrupted during the write operation or even a long time after that was completed.

## Techniques to handle failures
Following are some techniques that are commonly used to handle the hardware and silent hardware of failures.

## Retransmitting data
One way to detect these failures when sending a message to another node is to introduce redundancy in the message using a checksum derived from the actual payload. If the message is corrupted, the checksum will not be valid. As a result, the recipient can ask the sender to send the message again.

## Storing data to multiple disks
When writing data to disk, the retransmitting data technique might not be useful since the corruption will be detected a long time after a write operation has been performed by the client, which means it might not be feasible to rewrite the data. Instead, the application can make sure that data is written to multiple disks so that corrupted data can be discarded later on and the right data can be read from another disk with a valid checksum.

## Error correcting codes (ECC)
Error correcting codes (ECC) is used in cases where retransmitting or storing the data multiple times is impossible or costly.

These are similar to checksums and are stored alongside the actual payload, but they have the additional property that they can be used to correct corruption errors calculating the original payload again.

The downside of error correcting codes is that they are larger than checksums, thus having a higher overhead in terms of data stored or transmitted across the network.

Note: As a distributed system consists of many different parts, these kinds of failures can happen on any of them. So it raises the question of where and how we can use these failure handling techniques.

## The end-to-end argument principle
The end-to-end argument is a design principle, which suggests that some functions such as the fault tolerance techniques described previously can be implemented completely and correctly only with the knowledge and help of the application standing at the endpoints of the communication system.

A canonical example to illustrate this point is the careful file transfer application, where a file needs to be moved from computer A’s storage to computer B’s storage without damage.

As shown in the following illustration, hardware failures can happen in many places during this process, such as:
* The disks of computers
* The software of the file system
* The hardware processors, their local memory
* The communication system

![advanced](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/big/za14.png)

## Implementing error recovery functionality at the application level
Even if the various subsystems embed error recovery functionality, this can only cover lower levels of the system, and it cannot protect from errors that happen at a higher level of the system.

For example, error detection and recovery implemented at the disk level or in the operating system won’t help if the application has a defect that leads to writing the wrong data in the first place. It means that we can only achieve complete correctness by implementing this function at the application level.

This function can be implemented redundantly at lower levels, but this is mostly done as a performance optimization.

Note: An example of this was already presented in the chapter about networking, where we saw that the link layer provides reliable data transfer for wireless links (e.g., Wi-fi) even though this can also be provided at the transport layer (e.g., TCP).

It’s also important to note that this redundant implementation at lower levels is not always beneficial, but it depends on the use case.The literature by Saltzer et al. and Moors et al. covers this trade-off extensively.

## Providing exactly-once guarantees at the application level
The end-to-end argument principle manifests in many different ways when dealing with a distributed system. The most relevant problem we have encountered repeatedly throughout this course is providing exactly-once guarantees.

Let’s consider an extremely simplified version of the problem, where application A wants to trigger an operation on application B exactly once, and each application consists of a single server.

## Using TCP
The communication subsystem, specifically TCP, can provide reliable data delivery via retries, acknowledgments, and deduplication, which are the techniques already described in this course.

However, TCP is still not sufficient to provide exactly-once guarantees at the application level.

## Problems
The application can encounter the following problems when using TCP to achieve exactly-once guarantees:

The TCP layer on the side of application B might receive a packet and acknowledge it back to the sender side while buffering it locally to be delivered to the application. However, the application crashes before receiving this packet from the TCP layer and processing it. In this case, the application on the sender side will think the packet has been successfully processed while it wasn’t.

The TCP layer on the side of application B might receive a packet and deliver it successfully to the application, which processes it successfully. However, a failure happens at this point, and the applications on both sides are forced to establish a new TCP connection. Application A had not received an application acknowledgment for the last message, so it attempts to resend it on the new connection.

Unfortunately, TCP provides reliable transfer only in the scope of a single connection, so it will not be able to detect if this packet has been received and processed in a previous connection. As a result, a packet will be processed by the application more than once.

## Solution
The main takeaway from the above problems is that any functionality needed for exactly-once semantics (e.g., retries, acknowledgments, and deduplication), needs to be implemented at the application level in order to be correct and safe against all kinds of failures.

## Achieving mutual exclusion
The end-to-end principle manifests in a slightly different shade to achieve mutual exclusion in a distributed system.

The fencing technique discussed previously extends mutual exclusion function to all the involved ends of the application.

Note: The goal of this chapter is not to explore all the problems where the end-to-end argument is applicable. Instead, the goal is to raise awareness and make the reader appreciate its value on system design to consider if and when need be

## Retries

## Using retries in stateless systems
In the case of a stateless system, the application of retries is pretty simple since all the application nodes are identical from the client’s perspective, so it could retry a request on any node.

Note: In some cases, retries are done in a fully transparent way to the client.

For example, suppose the application is fronted by a load balancer that receives all the requests under a single domain. In that case it’s responsible for forwarding the requests to the various nodes of the application. In this way, the client would only have to retry the request to the same endpoint, and the load balancer would take care of balancing the requests across all the available nodes.

## Using retries in stateful systems
In stateful systems, retries get slightly more complicated since nodes are not identical, and retries need to be directed to the right one.

For example, when using a system with leader-follower replication, a failure of the leader node must be followed by failover to a follower node that is now the new leader , and new requests should be going there. There are different mechanisms to achieve this, depending on the technology used. The same applies to consensus-based replication, where a new leader election might need to happen, and write operations must be directed to the current leader.

## Containing Impact of Failure

Most of the techniques described in this chapter are used to identify failure and recover from it. It’s also useful to contain the impact of a failure, so we will now discuss some techniques for this purpose. This can be done via technical means, such as fault isolation.

## Fault isolation
One common way to contain the impact of the failure is to deploy an application redundantly in multiple facilities that are physically isolated and have independent failure modes. So, when an incident affects one of these facilities, the other facilities are not impacted and continue functioning as normal.

Note: Fault isolation introduces a trade-off between availability and latency since physical isolation increases network distance and latency.

## Balancing the trade-off between availability and latency
Most cloud providers provide multiple physically isolated datacenters t and are all located close to each other in a single region to strike a good balance in this trade-off. These are commonly known as availability zones.

## Graceful degradation
Graceful degradation is another technique to contain failure, where an application reduces the quality of its service to avoid failing completely.

For example, suppose a service that provides the capabilities of a search engine by calling downstream services. And one of these services which shows the advertisements for each query is having some issues. The top-level service can just render the results of a search term without any advertisements instead of returning an error message or completely empty response.

Techniques to contain failure are broadly categorized into two main groups:
* Those performed at the client-side
* Those performed at the server-side

## Backpressure

Backpressure is a very useful concept in the field of distributed systems. It is essentially a resistance to the desired flow of data through a system. This resistance can manifest in different ways, such as increased latency of requests or failed requests.

Backpressure can also be implicit or explicit.

## Implicit backpressure
Implicit backpressure arises in a system that is overloaded by a traffic surge and becomes extremely slow.

## Explicit backpressure
A system that rejects some requests during a traffic surge to maintain a good quality service essentially exerts explicit backpressure to its clients.

Note: Most of the techniques used to contain failure reflect how applications exert backpressure and how their clients handle backpressure.

Let’s learn how applications can exert backpressure.

## Techniques used by applications to exert backpressure
It is useful for a system to know its limits and exert backpressure when they are reached instead of relying on implicit backpressure. Otherwise, there can be many unexpected failure modes, which are harder to deal with when they happen.

## Load shedding
The main technique to exert backpressure is load shedding. An application is aware of the maximum load it can handle and rejects any requests that cross this threshold to keep operating at the desired levels.

## Selective client throttling
A more specialized form of load shedding is selective client throttling, where an application assigns different quotas to each of its clients.

This technique can also be used to prioritize traffic from some more important clients.

Let’s consider a service responsible for serving the prices of products, which is used both by systems responsible for displaying product pages and systems responsible for receiving purchases and charging the customer. In case of a failure, that service could throttle the former type of system more than the latter since purchases are considered more important for a business. They also tend to constitute a smaller percentage of the overall traffic.

Note: In the case of asynchronous systems that use message queues, load shedding can be performed by imposing an upper bound on the size of the queue. There is a common misconception that message queues can help absorb any form of backpressure without any consequences. However, this comes at the cost of an increased backlog of messages, leading to increased processing latency or even failure of the messaging system in extreme cases.

## Reacting to Backpressure

## Distributed Tracing

Tracing refers to the particular use of logging to record information about a program’s execution, used for troubleshooting or diagnostic purposes.

## Achieving tracing
We can achieve tracing in its simplest form by associating every request to the program with a unique identifier and recording logs for the most important operations of the program alongside the request identifier.

In this way, when we try to diagnose a specific customer issue, the logs can easily be filtered down to only include a chronologically ordered list of operation logs of the associated request identifier. These logs can provide a summary of the various operations the program executed and the steps it went through.

## Collating traces from multiple programs
A distributed system serves every client request through multiple, different applications. As a result, one needs to collate traces from multiple programs to fully understand how a request was served and where something might have gone wrong.

## Problem
Collating traces from multiple programs is not that simple because every application might be using its own request identifiers, and the applications are most likely processing multiple requests concurrently. This makes it harder to determine which requests correspond to a specific client request.

## Solution
We can solve the above problem through the use of correlation identifiers.

## Correlation identifier
A correlation identifier is a unique identifier that corresponds to a top-level client request. This identifier might be automatically generated, or some external system or manual process might provide it. It is then propagated through the various applications that are involved in serving this request. These applications can then include that correlation identifier in their logs along with their request identifiers. In this way, it is easier to identify all the operations across all applications corresponding to a specific client request by filtering their logs based on this correlation identifier.

Note: By incorporating timing data in this logging, one can use this technique to also retrieve performance data, such as the time spent on every operation.

The following illustration shows distributed tracing via correlation IDs and an example of a trace that shows latency contribution of every application:

## Isolation Levels and Anomalies

The inherent concurrency in distributed systems creates the potential for anomalies and unexpected behaviors. Specifically, transactions that comprise multiple operations and run concurrently can lead to different results depending on how their operations are interleaved.

As a result, there is still a need for some formal models that define what is possible and what is not in a system’s behavior. These are called isolation levels.

We will study the most common ones here, which are the following:
* Serializability
* Repeatable read
* Snapshot isolation
* Read committed
* Read uncommitted

Unlike the consistency models presented in a previous lesson, some of these isolation levels do not define what is possible via some formal specification. Instead, they define what is not possible, i.e., which anomalies of the already known ones are prevented.

Of course, stronger isolation levels prevent more anomalies at the cost of performance. Let’s first have a look at the possible anomalies before examining the various levels.

The origin of the isolation levels above and the associated anomalies was essentially the ANSI SQL-92 standard. However, the definitions in this standard were ambiguous and missed some possible anomalies.

Subsequent research examines more anomalies extensively and attempts a stricter definition of these levels. The basic parts will be covered in this lesson, but please refer to this paper for a deeper analysis.

## Anomalies
The anomalies covered here are the following:
* Dirty writes
* Dirty reads
* (Fuzzy) non-repeatable reads
* Phantom reads
* Lost updates
* Read skew
* Write skew

## Dirty write
A dirty write occurs when a transaction overwrites a value that was previously written by another transaction that is still in-flight and has not been committed yet.

One reason dirty writes are problematic is they can violate integrity constraints. For example, there are two transactions A and B, where transaction A runs the operations [x=1, y=1] and transaction B runs the operations [x=2, y=2]. Then, the serial execution of them would always result in a situation where x and y have the same value. However, this is not necessarily true in a concurrent execution where dirty writes are possible.

## Example

An example could be the following execution [x=1, x=2, y=2, commit B, y=1, commit A] that would result in x=2 and y=1.

Another problem with dirty writes is they make it impossible for the system to automatically rollback to a previous image of the database. As a result, this is an anomaly we need to prevent in most cases.

## Dirty read
A dirty read occurs when a transaction reads a value that has been written by another transaction that has not yet been committed.

This is problematic since the system might make decisions depending on these values, even though the associated transactions might be rolled back subsequently. Even in the case where these transactions eventually commit, though, this can still be a problem.

## Example

An example is the classic scenario of a bank transfer, where the total amount of money should be observed to be the same at all times. For example, imagine transaction A is able to read the balance of two accounts involved in a transfer during another transaction (B) that performs the transfer from account 1 to account 2. During the transfer, it will look as if some money has been lost from account 1.

However, there are a few cases where allowing dirty reads can be useful if done with care. One such case is to generate a big aggregate report on a full table when we can tolerate some inaccuracies on the numbers of the report.

It can also be useful when we troubleshoot an issue and want to inspect the state of the database in the middle of an ongoing transaction.

## Fuzzy or non-repeatable read
A fuzzy or non-repeatable read occurs when a value is retrieved twice during a transaction (without it being updated in the same transaction), and the value is different.

This can lead to problematic situations similar to the example presented above for dirty reads.

Other cases where this can lead to problems are when the first read of the value is used for some conditional logic, and the second is used to update data. In this case, the transaction might act on stale data.

## Phantom read
A phantom read occurs when a transaction does a predicate-based read, and another transaction writes or removes a data item matched by that predicate while the first transaction is still in flight. If that happens, then the first transaction might be acting again on stale data or inconsistent data.

## Example

For example, transaction A runs 2 queries to calculate the maximum and the average age of a specific set of employees. However, between the two queries, transaction B is interleaved and inserts a lot of old employees in this set, thus making transaction A return an average that is larger than the maximum.

Allowing phantom reads can be safe for an application that does not make use of predicate-based reads, i.e., performs only the reads that select records using a primary key.

## Lost update
A lost update occurs when two transactions read the same value and then try to update it to two different values. The end result is that one of the two updates survives, but the process executing the other update is not informed that its update did not take effect Thus it is called a lost update.

## Example

Imagine a warehouse with various controllers that update the database when new items arrive. The transactions are rather simple. They involve reading the number of items currently in the warehouse, adding the number of new items to this number, and then storing the result back in the database.

This anomaly could lead to the following problem:
* Transactions A and B read the current inventory size simultaneously (say, 100 items), add the number of new items to this (say, 5 and 10 respectively), and then store this back to the database. Let’s assume that transaction B was the last one to write. This means that the final inventory is 110 instead of 115. Thus, five new items are not recorded!

See the following illustration for a visualization of this example.

![advanced](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/big/za15.png)

Depending on the application, it might be safe to allow lost updates in some cases. For example, consider an application that allows multiple administrators to update specific parts of an internal website used by employees of a company.

## Read skew
A read skew occurs when there are integrity constraints between two data items that seem to be violated because a transaction can only see partial results of another transaction.

## Example

Let’s imagine an application that contains a table of persons, where each record represents a person and contains a list of all the friends of this person. The main integrity constraint is that friendships are mutual; if person B is included in person A’s list of friends, then A must also be included in B’s list. Every time someone (say, P1) wants to unfriend someone else (say, P2), a transaction is executed that removes P2 from P1’s list and also removes P1 from P2’s list in a single go.

Now, let’s also assume that some other part of the application allows people to view friends of multiple people simultaneously. This is done by a transaction that reads the friends list of these people. If the second transaction reads the friends list of P1 before the first transaction has started, but reads the friends list of P2 after the second transaction has been committed, it will notice an integrity violation. P2 will be in P1’s list of friends, but P1 will not be in P2’s list of friends.

Note that this case is not a dirty read, because any values written by the first transaction are read-only after it has been committed.

See the following illustration for a visualization of this example.

![advanced](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/big/za16.png)

A strict requirement to prevent read skew is quite rare, as we might have guessed already. For example, a common application of this type might allow a user to view the profile of only one person at a time along with their friends, thus not requiring the integrity constraint described above.

## Write skew
A write skew occurs when two transactions read the same data, but then modify disjoint sets of data.

## Example

Imagine an application that maintains the on-call rota of doctors in a hospital. A table contains one record for every doctor with a field indicating whether they are on-call. The application allows a doctor to remove themself from the on-call rota if another doctor is also registered. This is done via a transaction that reads the number of doctors that are on-call from this table. If the number is greater than one, it updates the record corresponding to this doctor to not be on-call.

Now, let’s look at the problems that can arise from the write skew phenomenon. Let’s say two doctors, Alice and Bob, are on-call currently, and they both decide to see if they can remove themselves. Two transactions running concurrently might read the state of the database, see there are two doctors, and remove the associated doctor from being on-call. In the end, the system ends up with no doctors on-call!

See the following illustration for visualization of this example.

![advanced](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/big/za17.png)

## Prevention of Anomalies in Isolation Levels


## Isolation level that prevents all of the anomalies
There is one isolation level that prevents all of these anomalies: the serializable one.

Like the consistency models presented previously, this level provides a more formal specification of what is possible, e.g., which execution histories are possible. More specifically, it guarantees that the result of the execution of concurrent transactions is the same as that produced by some serial execution of the same transactions. This means that we can only analyze serial executions for defects. If all the possible serial executions are safe, then any concurrent execution by a system at the serializable level will also be safe.

However, serializability has performance costs since it intentionally reduces concurrency to guarantee safety.

## Other isolation levels
Isolation levels other than the serializable ones are less strict and provide better performance via increased concurrency at the cost of decreased safety.

These models allow some of the anomalies we described previously. The following illustration contains a table with the most basic isolation levels, along with the anomalies they prevent.

![advanced](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/big/za18.png)

## Consistency and Isolation

The following illustration will help us remember the consistency models and isolation levels.

![advanced](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/big/za19.png)

## Similarities between consistency models and isolation models
It is interesting to observe that isolation levels are not that different from consistency models.

Isolation levels and consistency models are essential constructs that allow us to express:
* Which executions are possible
* Which executions are not possible

In both cases, some of the models are stricter and allow fewer executions, thus providing increased safety at the cost of reduced performance and availability.

For instance, linearizability allows a subset of the executions causal consistency allows, while serializability allows a subset of the executions that snapshot isolation allows.

We can also express this strictness relationship by saying that one model implies another model.

The fact that a system provides linearizability automatically implies that the same system also provides causal consistency.

Note that there are some models that are not directly comparable, which means neither of them is stricter than the other.

## Differences between consistency models & isolation levels
Consistency models and isolation levels have some differences with regards to the characteristics of their allowed and disallowed behaviors.

Consistency models are applied to single-object operations (e.g. read/write to a single register), while isolation levels are applied to multi-object operations (e.g. read and write from/to multiple rows in a table within a transaction).
Looking at the strictest models in these two groups, linearizability and serializability, there is another important difference.

Linearizability provides real-time guarantees, while serializability does not.
Linearizability guarantees that the effects of an operation took place at some point between when the client invoked the operation, and when the result of the operation was returned to the client.

Serializability only guarantees that the effects of multiple transactions will be the same as if they run in serial order. It does not provide any guarantee on whether that serial order would be compatible with real-time order.

## Why real-time guarantees are important
The following illustration shows why real-time guarantees are important from an application perspective.

![advanced](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/big/za20.png)

Think of an automated teller machine that can support two transactions:
* GET_BALANCE()
* WITHDRAW(amount)

The first transaction performs a single operation to read the balance of an account.

The second operation reads the balance of an account, reduces it by the specified amount, and then returns the client the specified amount in cash.

Let’s also assume this system is serializable.

Now, let’s examine the following scenario:

A customer with an initial balance of x reads their balance and then decides to withdraw $20 by executing a WITHDRAW(20) transaction.

After the transaction has been completed and the money is returned, the customer performs a GET_BALANCE() operation to check their new balance. However, the machine still returns x as the current balance instead of x-20.

Note that this execution is serializable and the end result is as if the machine executed the GET_BALANCE() transactions first, and then the WITHDRAW(20) transaction in a completely serial order.

This example shows how serializability is not sufficient in itself in some cases.

## Strict serializability
Strict serializability is a model that is a combination of linearizability and serializability.

This model guarantees that the result of multiple transactions is equivalent to the result of a serial execution of them, and is also compatible with the real-time ordering of these transactions.

As a result, transactions appear to execute serially, and the effects of each of them take place at some point between their invocation and completion.

As we learned before, strict serializability is often a more useful guarantee than plain serializability.

In centralized systems, however, providing strict serializability is simple and just as efficient as only providing serializability guarantees. As a result, systems such as relational databases sometimes advertise serializability guarantees, while they actually provide strict serializability.

This is not necessarily true in a distributed database, where providing strict serializability can be more costly because it requires additional coordination.

It is important to understand the difference between these two guarantees in order to determine which one is needed, depending on the application domain.

## Hierarchy of Models

We can organize all of the models we presented so far— and many others that are not presented in this course for practical reasons—in a hierarchical tree according to their strictness and the guarantees they provide.

## Hierarchy tree
The following illustration depicts such a tree that contains only the models presented in this course.

![advanced](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/big/za21.png)

## Consistency Models

In this lesson, we introduce the forms of consistency that are most relevant to this course.

To accurately define all these forms really, we need to build a formal model. This is usually the consistency model.

## Consistency model
The consistency model defines the set of execution histories that are valid in a system.

In layperson’s terms, a model formally defines the behaviours that are possible in a distributed system.

Consistency models are extremely useful for many reasons:
* They help us formalise the behaviours of systems. Systems can then provide guarantees about their behaviour.
* Software engineers can confidently use a distributed system (i.e. a distributed database) in a way that does not violate any safety properties they care about.

In essence, software engineers can treat a distributed system as a black box that provides a set of properties. Moreover, they can do this without knowing of all the complexity the system internally assumes to provide these properties.

## A strong consistency model
We consider consistency model A stronger than model B when the first allows fewer histories. Alternatively, we say model A makes more assumptions about or poses more restrictions on, the system’s possible behaviors.

Usually, the stronger the consistency model a system satisfies, the easier it is to build an application on top of it. This is because the developer can rely on stricter guarantees.

## List of consistency models
There are many different consistency models used across the modern system design field. In the context of this course, we will focus on the most fundamental ones. These are the following:
* Linearizability
* Sequential Consistency
* Causal Consistency
* Eventual Consistency

## Linearizability
A system that supports the consistency model of linearizability is one where operations appear to be instantaneous to the external client. This means that they happen at a specific point—from the point the client invokes the operation, to the point the client receives the acknowledgment by the system the operation has been completed.

Furthermore, once an operation is complete and the acknowledgment is delivered to the client, it is visible to all other clients. This implies that if a client C2 invokes a read operation after a client C1 receives the completion of its write operation, C2 should see the result of this (or a subsequent) write operation. It may be obvious to some that operations are instantaneous and visible after they’re completed.

In a centralized system, linearizability is obvious. The following illustration shows this.








