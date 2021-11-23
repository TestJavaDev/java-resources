---
layout: default
title: Achieving Atomicity
parent: Distributed Systems
grand_parent: System design
nav_order: 2
permalink: /systemdesign/dissystem/atomicy
---
<div align="center" markdown="1">
Achieving Atomicity / Java resources / Tutorial

{: .fs-8 .fw-400 }
</div>

## Achieving Atomicity

## Hard to Guarantee Atomicity

As explained before, the second challenging aspect of transactions, and especially distributed transactions, is atomicity.

One of the benefits of grouping operations inside a transaction is the guarantee that either all of them will be performed, or none of them will be. As a result, the application developer does not need to think about scenarios of partial failures, where the transaction fails after some of the operations were already performed.

Similar to the isolation guarantees, the atomicity guarantee makes it easier to develop applications. It delegates some of the complexity around handling these situations to the persistence layer, e.g., to the datastore used by the application that provides atomicity guarantees.

Let’s see why atomicity is hard to achieve in general, and how it is even more difficult in distributed systems.

## Guaranteeing atomicity is a hard problem
Guaranteeing atomicity is hard in general, and not only in distributed systems.

The reason is that components can fail unexpectedly regardless of whether they are software or hardware components.

According to Pillai et al., “Even the simple act of writing some bytes to a file requires extra work to ensure it will be performed in an atomic way and the file will not end up in a corrupted state if the disk fails while executing part of the operation”.

## A way to achieve atomicity
One common way of achieving atomicity, in this case, is through journalling or write-ahead logging. In this technique, metadata about the operation are first written to a separate file, along with markers that denote whether an operation has been completed or not.

Based on this data, the system can identify which operations were in progress when a failure happened, and drive them to completion either by undoing their effects and aborting them, or by completing the remaining part and committing them. This approach is used extensively in file systems and databases.

## Atomicity in a distributed system
The issue of atomicity in a distributed system becomes even more complicated because components (nodes in this context) are separated by the network that is slow and unreliable, as explained already.

Furthermore, we do not only need to make sure that an operation is performed atomically in a node. In most cases, we need to ensure that an operation is performed atomically across multiple nodes. This means that the operation needs to take effect either at all the nodes or at none of them. This problem is also known as atomic commit.

In the following three lessons, 2PC, 3PC, and the quorum-based commit protocol, we will look at how we can achieve atomicity in distributed settings. Algorithms are discussed in chronological order so that we can understand what the pitfalls of each algorithm are, and how subsequent algorithms addressed them.

## 2-Phase Commit (2PC)

In a distributed system with an unreliable network, just sending a message to the involved nodes would not be enough for executing a distributed transaction. The node initiating the transaction would not know whether the other nodes committed successfully, or aborted because of some failure, to make a final decision about the result of the transaction.

When we think about it, the simplest idea is to add another round of messages, and check what the result was on each node. This is essentially the 2-phase commit protocol (2PC).

## Phases
The 2-phase commit protocol consists of two phases, hence the name.

The protocol contains two different roles. Their names reflect their actual responsibilities in the protocol.

The coordinator is responsible for coordinating the different phases of the protocol

The participants correspond to all the nodes that participate in the transaction

Note that one of the participants could also play the role of the coordinator.

## Voting phase
In this phase, the coordinator sends the transaction to all the participants. The participants execute the transaction up to the point where they are supposed to commit.

In some cases, the operations of each transaction are executed separately and before the voting phase, which starts after all the operations of a transaction has been executed. Agreement protocols like this usually involve some locking protocol as well, so that other concurrent transactions cannot make participants that have already voted change their mind on whether they can commit or not. For example, the 2-phase commit protocol can be combined with the 2-phase locking protocol.

Then, participants respond to the coordinator with a vote that shows if the transaction’s operations are executed successfully (“Yes” vote) or there is some error that means the transaction cannot be committed (“No” vote).

## Commit phase
In this phase, the coordinator gathers all the votes from the participants. If all the votes are “Yes”, then the coordinator messages the participants again with an instruction to commit the transaction.

Otherwise, if at least one vote is “No”, the coordinator instructs the participants to abort the transaction. Finally, the participants reply with an acknowledgment and close this phase.

The fact that a unanimous positive vote is needed for a commit means that the transaction will either commit to all the participants, or will be aborted to all of them (atomicity property).

The coordinator and the participants make use of a write-ahead-log, where they persist their decisions during the various steps so that they can recover in case of a failure.

The coordinator also uses a timeout when waiting for the responses from the first phase. If the timeout expires, the coordinator interprets this timeout as a No vote and considers the node as failed.

On the other hand, the participants do not apply any timeouts while waiting for the coordinator’s messages, since that could lead to participants reaching different conclusions due to timing issues.

The following illustration shows what this flow looks like.

![advanced](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/big/car61.png)
![advanced](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/big/car62.png)
![advanced](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/big/car63.png)
![advanced](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/big/car64.png)
![advanced](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/big/car65.png)
![advanced](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/big/car66.png)
![advanced](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/big/car67.png)
![advanced](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/big/car68.png)
![advanced](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/big/car69.png)
![advanced](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/big/car70.png)
![advanced](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/big/car71.png)
![advanced](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/big/car72.png)

## Handling failures
Since the happy path is straightforward, let’s examine how the protocol handles various kinds of failures.

## Failure of a participant in the voting phase
If a participant fails in the voting phase before replying to the coordinator, the coordinator will timeout waiting and assume a No vote on behalf of this participant.

This means that the protocol will end up aborting the transaction.

## Failure of a participant in the commit phase
In this scenario, a participant votes in the voting phase but then fails before it receives the message from the coordinator and completes the transaction (either by committing or abort).

In this case, the protocol will conclude without this node. If this node recovers, later on, it will identify that pending transaction and communicate with the coordinator to find out what the result was, and conclude it in the same way.

So, if the result of the transaction is successful, any crashed participant will eventually find out upon recovery and commit it. The protocol does not allow aborting it unilaterally. Thus, atomicity is maintained.

Some readers may have noticed that there is a chance that the participants may fail at the point they try to commit the transaction and break their promise, e.g., because they are out of disk space. Indeed, this is true. Thus, participants have to make the minimum work possible as part of the commit phase to avoid this. For example, the participants can write all the necessary data on the disk during the first phase so that they can signal a transaction is committed by doing minimal work during the second phase (e.g., flipping a bit).

## Network failures
Network failures have similar results to those described previously, since timeouts make them equivalent to node failures.

Even though a 2-phase commit can handle all the aforementioned failures gracefully, there’s a single point of failure: the coordinator.

## Blocking nature of 2-phase commit protocol
Because of the blocking nature of the protocol, failures of the coordinator at specific stages of the protocol can bring the whole system to a halt. More specifically, if a coordinator fails after sending a prepared message to the participants, the participants will block. The participants will wait for the coordinator to recover and find out the outcome of the transaction, so that they commit or abort it as needed.

This means that failures of the coordinator can decrease the availability of the system significantly. Moreover, if the data from the coordinator’s disk cannot be recovered (e.g., due to disk corruption), the result of pending transactions cannot be discovered, and manual intervention might be needed to unblock the protocol.

## Usage of the 2-phase commit protocol
Despite the blocking nature of the protocol, the 2-phase commit is widely used. A specification, called the eXtended Architecture (XA), has also been released.

In this specification, each of the participant nodes is referred to as resources, and they must implement the interface of a resource manager.

The specification also defines the concept of a transaction manager that acts as the coordinator that starts, coordinates, and ends transactions.

## Conclusion
The 2PC protocol satisfies the safety property that ensures all participants always arrive at the same decision (atomicity). However, it does not satisfy the liveness property that implies it will always make progress.

## 3-Phase Commit (3PC)

## The problem with 2-phase commit protocol
As we described previously, the main bottleneck of the 2-phase commit protocol was failures of the coordinator leading the system to a blocked state.

Ideally, we would like the participants to be able to take the lead in some way and continue the execution of the protocol in this case, but this is not so easy.

The underlying reason is the fact that in the commit phase, the participants are not aware of the state of the other participants—only the coordinator is So, taking the lead without waiting for the coordinator can result in breaking the atomicity property.

For instance, imagine the following scenario: in the commit phase of the protocol, the coordinator manages to send a commit (or abort) message to one of the participants but then fails, and this participant also fails. If one of the other participants takes the lead, it will only be able to query the live participants. So, it will be unable to make the right decision without waiting for the failed participant (or the coordinator) to recover.

## Tackling the 2PC problem with 3-phase commit protocol
The 2-phase commit problem could be tackled by splitting the first round (voting phase) into 2 sub-rounds, where the coordinator first communicates the votes result to the nodes, waits for an acknowledgment, and then proceeds with the commit or abort message.

In this case, the participants would know the result from the votes and complete the protocol independently in case of a coordinator failure. This is essentially the 3-phase commit protocol (3PC).

Wikipedia contains a detailed description of the various stages of the protocol and a nice visual demonstration. Feel free to refer to this resource for additional study on the protocol.

## Benefit of 3PC
The main benefit of this protocol is that the coordinator stops being a single point of failure.

In case of a coordinator failure, the participants are able to take over and complete the protocol.

A participant taking over can commit the transaction if it receives a prepare-to-commit, knowing that all the participants have voted “Yes”. If it does not receive a prepare-to-commit, it can abort the transaction, knowing that no participant has committed, without all the participants receiving a prepare-to-commit message first.

As a result, the 3PC protocol increases availability and prevents the coordinator from being a single point of failure.

However, this comes at the cost of correctness, since the protocol is vulnerable to failures such as network partitions.

## Network partition failure in 3PC
An example of such a failure case is shown in the following illustration.

![advanced](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/big/car73.png)
![advanced](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/big/car74.png)
![advanced](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/big/car75.png)
![advanced](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/big/car76.png)
![advanced](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/big/car77.png)
![advanced](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/big/car78.png)
![advanced](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/big/car79.png)
![advanced](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/big/car80.png)

In this example, a network partition occurs at a point where the coordinator manages to send a prepare-to-commit message only to some participants. Meanwhile, the coordinator fails right after this point, so the participants time out and have to complete the protocol on their own.

In this case, one side of the partition has participants that receive a prepare-to-commit and continue with committing the transaction. However, the participants at the other side of the partition do not receive a prepare-to-commit message and, thus, unilaterally abort the transaction.

This can seem like a failure case that is very unlikely to happen. However, the consequences are disastrous if it happens, since the system is at an inconsistent state after the network partition is fixed. The atomicity property of the transaction has been violated.

## Conclusion
The 3PC protocol satisfies the liveness property that ensures it will always make progress, at the cost of violating the safety property of atomicity.

## Quorum-Based Commit Protocol

## The problem with 3-phase commit protocol
As we observed in the previous lesson, the main issue with the 3PC protocol occurs at the end of the second phase, where a potential network partition can bring the system to an inconsistent state.

This can happen when participants attempt to unblock the protocol by taking the lead without having a picture of the overall system, resulting in a split-brain situation.

## Coping with the problem
Ideally, we would like to cope with this network partition without compromising the safety of the protocol. This can be done using a concept we have already learned in this course: a quorum.

This approach is followed by the quorum-based commit protocol.

This protocol is significantly more complex when compared to the other two protocols we described previously, so we should study the original paper carefully to examine all the possible edge cases. However, we will attempt to give a high-level overview of the protocol in this section.

As we mentioned before, this protocol leverages the concept of a quorum to ensure that different sides of a partition do not arrive at conflicting results.

The protocol establishes the concept of a commit quorum (V_C) and an abort quorum (V_A)

A node can proceed with committing only if a commit quorum has been formed, while a node can proceed with aborting only if an abort quorum has been formed.

The values of the abort and commit quorums have to be selected so that the following property holds:

V_A + V_C > VV

VV is the total number of participants of the transaction.

Based on the fact that a node can be in only one of the two quorums, it’s impossible for both quorums to be formed at two different sides of the partition and lead to conflicting results.

## Sub-protocols in quorum-based commit protocol
The quorum-based commit protocol comprises three different sub-protocols used in different cases:
* The commit protocol, which is used when a new transaction starts
* The termination protocol, which is used when there is a network partition
* The merge protocol, which is used when the system recovers from a network partition

## Commit protocol
This protocol is very similar to the 3PC protocol. The only difference is that the coordinator waits for V_C number of acknowledgments at the end of the third phase to proceed with committing the transaction.

If there is a network partition at this stage, the coordinator can be rendered unable to complete the transaction. In this case, the participants on each side of a partition will investigate whether they can complete the transaction, using the following protocol.

## Termination protocol
Initially, a (surrogate) coordinator will be selected from amongst the participants with a leader election.

Note that it’s irrelevant which leader election algorithm is used. Even if multiple leaders are elected, the correctness of the protocol is not violated.

The elected coordinator queries the nodes of the partition for their status.

If there is at least one participant that has committed (or aborted), the coordinator commits (or aborts) the transaction, maintaining the atomicity property.

If there is at least one participant at the prepare-to-commit state, and at least V_C participants waiting for the result of the votes, the coordinator sends prepare-to-commit to the participants and continues to the next step.

Alternatively, if there’s no participant at the prepare-to-commit state and at least V_A participants waiting for the results vote, the coordinator sends a prepare-to-abort message.

Note that this message does not exist in the commit protocol, but only in the termination protocol.

The last phase of the termination protocol waits for acknowledgments and attempts to complete the transaction in a similar fashion to the commit protocol.

## Merge protocol
The merge protocol is simple. It includes a leader election amongst the leaders of the two partitions that are merged, and then the execution of the termination protocol we described.

## Example
Let’s examine what would happen in the network partition example from the previous lesson. We have shown the same illustration below.

![advanced](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/big/car81.png)
![advanced](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/big/car82.png)
![advanced](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/big/car83.png)
![advanced](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/big/car84.png)
![advanced](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/big/car85.png)
![advanced](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/big/car86.png)
![advanced](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/big/car87.png)
![advanced](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/big/car88.png)

![advanced](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/big/car89.png)

![advanced](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/big/car90.png)
![advanced](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/big/car91.png)
![advanced](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/big/car92.png)
![advanced](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/big/car93.png)
![advanced](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/big/car94.png)
![advanced](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/big/car95.png)
![advanced](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/big/car96.png)
![advanced](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/big/car97.png)
![advanced](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/big/car98.png)
![advanced](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/big/car99.png)
![advanced](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/big/car100.png)
![advanced](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/big/car101.png)

## Conclusion
The quorum-based commit protocol satisfies the safety property that ensures that all participants will always arrive at the same decision (atomicity). It does not satisfy the liveness property that ensures that it will always make progress, since there are always degenerate, extreme failure cases (e.g., multiple, continuous, and small partitions). However, the quorum-based commit protocol is much more resilient that 2PC and other protocols, and can make progress in the most common types of failures.


## Concluding Distributed Transactions

As we have described often, transactions need to provide some guarantees if applications are to benefit from them.

Distributed transactions need to provide similar guarantees.

## Guarantees distributed systems should provide
Some basic guarantees commonly used are contained in the ACID acronym that we analyzed earlier.

## Consistency and durability guarantees
Consistency and durability do not require very different treatment in a distributed setting when compared to a centralized, single-node system. For durability, it’s enough for the data to be stored in non-volatile storage before it is acknowledged by the client.

To achieve durability in a distributed system, we should store data in more than one replicas before acknowledging, so that the system can survive the failures of a single node.

To achieve consistency, the system can introduce some additional read and write operations in the transaction’s context to guarantee the preservation of application consistency. These operations may be automatically generated, such as referential integrity constraints from foreign keys or cascades, or they may be defined by the application, e.g., via triggers.

## Atomicity and isolation guarantees
The guarantees of atomicity and isolation are more challenging to preserve, and we previously analyzed some of the algorithms we can use for this purpose.

The course examined some algorithms that can help preserve isolation across transactions, and some algorithms that can help preserve atomicity in a distributed system.

## Combining algorithms to guarantee all properties
The algorithms must combine to guarantee all properties: atomicity, consistency, isolation, and durability.

Some combinations of these algorithms might be easier to implement in practice because of their common characteristics. For example, two-phase locking has very similar characteristics to two-phase commit, so it’s easier to understand how they can be combined.

Spanner is an example of a system that uses a combination of these two techniques to achieve atomicity and isolation, as explained later in the course.

## Complexity in algorithms
Looking at the previous algorithms presented, it is easy to realize that some of them introduce either brittleness (e.g., two-phase commit) or a lot of additional complexity to a system (e.g., quorum-based commit).

## Algorithms that work for both systems
The algorithms presented for isolation can be used in both centralized and distributed systems. However, their use in a distributed system has several additional implications.

For example, two-phase locking requires the use of distributed locks, which is something that is not trivial to implement in a distributed system, as we will explain later in the course.

Optimistic techniques, such as snapshot isolation, require a lot of data transfer between different nodes in a distributed system, which has adverse effects on performance.

As a consequence, using transactions in a distributed system comes at a higher cost compared to a centralized system. So, systems that do not have a strong need for distributed systems can be designed to operate safely without them.

That is also one of the reasons why many distributed databases either do not provide full support for ACID transactions or force the user to opt in to use them explicitly.

## Long-Lived Transactions and Sagas

As explained previously, achieving complete isolation between transactions is relatively expensive.

The system either has to maintain locks for each transaction and potentially block other concurrent transactions from making progress, or abort some transactions to maintain safety, which leads to some wasted effort.

Furthermore, the longer the duration of a transaction is the bigger the impact of these mechanisms is expected to be on the overall throughput.

There is also a positive feedback cycle: using these mechanisms can cause transactions to take longer, which can increase the impact of these mechanisms.

## Long-lived transactions
There is a specific class of transactions, called long-lived transactions (LLT).

These are transactions that by their nature have a longer duration in the order of hours or even days, instead of milliseconds. This can happen because this transaction processes a large amount of data, requires human input to proceed, or needs to communicate with third party systems that are slow.

## Examples of LLTs
Batch jobs that calculate reports over big datasets
Claims at an insurance company, containing various stages that require human input
An online order of a product that spans several days from order to delivery
As a result, running these transactions using the common concurrent mechanisms degrades performance significantly, since they need to hold resources for long periods of time, while not operating on them.

Sometimes, long-lived transactions do not really require full isolation between each other, but they still need to be atomic, so that consistency is maintained under partial failures. Thus, researchers came up with a new concept: the saga.

## Saga
The saga is a sequence of transactions T_1, T_2T, …, T_N that can be interleaved with other transactions.

However, it’s guaranteed that either all of the transactions will succeed, or none of them will, maintaining the atomicity guarantee.

Each transaction T_i is associated with a so-called compensating transaction C_i, that is executed in case a rollback is needed.

## Benefits of the saga
The concept of saga transactions can be really useful in distributed systems. As demonstrated in the previous sections, distributed transactions are generally hard and can only be achieved by making compromises on performance and availability.

There are cases where we can use a saga transaction instead of a distributed transaction. This will satisfy all of our business requirements while keeping our systems loosely coupled and achieving good availability and performance.

## Example scenario
Let’s imagine we are building an e-commerce application, where every order of a customer requires several discrete steps: credit card authorization, checking warehouse inventory, item shipping, invoice creation and delivery, etc.

One approach could be to perform a distributed transaction across all these systems for every order. However, in this case, the failure of a single component (i.e., the payment system) could potentially bring the whole system to a halt.

An alternative, leveraging the saga pattern, would be to model the order operation as a saga operation, consisting of all these sub-transactions, where each of them is associated with a compensating transaction.

For example, debiting a customer’s bank account could have a compensating transaction that would give a refund. Then, we can build the order operation as a sequential execution of these transactions, as shown in the following transactions. In case any of these transactions fail, we can rollback the transactions that have been executed and run their corresponding compensating transactions.

![advanced](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/big/car102.png)

There might still be cases where some form of isolation is needed.

In the example above, orders from different customers about the same product might share some data, which can lead to interference between each other.

## Cases where isolation is required
Think about the scenario of two concurrent orders A and B, where A has reserved the last item from the warehouse. As a result of this, order B fails at the first step and is rejected because of zero inventory. Later on, order A also fails at the second step because the customer’s card does not have enough money. Then, the associated compensating transaction runs, returning the reserved item to the warehouse.

This would mean that an order was rejected while it could have been processed normally. Of course, this violation of isolation does not have severe consequences. However, in some cases the consequences might be more serious, e.g. customers being charged without receiving a product.

To prevent these scenarios, some form of isolation can be introduced at the application layer.

## Providing isolation at the application layer
Previous research on this topic proposed some concrete techniques that are countermeasures to isolation anomalies.

Some of these techniques are as follows:

## Semantic lock
The use of a semantic lock essentially signals that some data items are currently in process and should be treated differently or not accessed at all. The final transaction of a saga takes care of releasing this lock and resetting the data to its normal state.

## Commutative updates
The use of commutative updates that have the same effect regardless of their order of execution. This can help mitigate cases that are otherwise susceptible to lost update phenomena.

## Re-ordering the structure of the saga
Re-order the saga structure so that a transaction called a pivot transaction delineates a boundary between transactions that can fail and those that can’t.

In this way, transactions that can’t fail, but could lead to serious problems if rolled back due to failures of other transactions, can be moved after the pivot transaction.

An example of this is a transaction that increases the balance of an account. This transaction could have serious consequences if another concurrent saga reads this increase in the balance, but then the previous transaction is rolled back. Moving this transaction after the pivot transaction means that it will never be rolled back, since only all the transactions after the pivot transaction can succeed.

We can apply these techniques selectively in cases where they are needed. However, they introduce significant complexity and move some of the burdens back to the application developers; the developers have to think again about all the possible failures and design accordingly. We need to consider trade-offs when choosing between using saga transactions or leveraging the transaction capabilities of the underlying datastore.

Before Getting Started

Introduction
Introduction to Distributed Systems

Getting Started
Fallacies of Distributed Computing
Difficulties Designing Distributed Systems
Measures of Correctness in Distributed Systems
System Models
Types of Failures
The Tale of Exactly-Once Semantics
Failure in the World of Distributed Systems
Stateless and Stateful Systems
Quiz
Basic Concepts and Theorems

Partitioning
Algorithms for Horizontal Partitioning
Replication
Single-Master Replication Algorithm
Multi-Master Replication Algorithm
Quorums in Distributed Systems
Safety Guarantees in Distributed Systems
ACID Transactions
The CAP Theorem
Consistency Models
CAP Theorem's Consistency Model
Isolation Levels and Anomalies
Prevention of Anomalies in Isolation Levels
Consistency and Isolation
Hierarchy of Models
Why All the Formalities?
Quiz
Distributed Transactions

Introduction to Distributed Transactions
Quiz
Achieving Isolation

Achieving Serializability
Pessimistic Concurrency Control (PCC)
Optimistic Concurrency Control (OCC)
Achieving Snapshot Isolation
Achieving Full Serializable Snapshot Isolation
Quiz
Achieving Atomicity

Hard to Guarantee Atomicity
2-Phase Commit (2PC)
3-Phase Commit (3PC)
Quorum-Based Commit Protocol
Quiz
Concluding Distributed Transactions

How It All Fits Together
Long-Lived Transactions and Sagas
Consensus

Defining the Consensus Problem
FLP Impossibility
The Paxos Algorithm
Intricacies of Paxos
Paxos in Real Life
Replicated State Machine via Consensus
Distributed Transactions via Consensus
An introduction to Raft
Communication among Raft Nodes
Raft's Implementation
Standing on the Shoulders of Giants
Quiz
Time

What is Different in a Distributed System?
A Practical Perspective
A Theoretical Perspective
Logical Clocks
Quiz
Order

Total and Partial Ordering
The Concept of Causality
Lamport Clocks
Vector Clocks
Version Vectors
Dotted Version Vectors
Distributed Snapshot Problem
Solving the Distributed Snapshot Problem
Physical and Logical Time: Closing Thoughts
Quiz
Networking

Introduction
The Physical Layer
The Link Layer - Services
The Link-Layer Protocols
The Network Layer
The Transport Layer
The Application Layer
Taking a Step Back
Quiz
Security

Introduction
Authentication
Confidentiality
Integrity
A Cryptography Primer
Symmetric/Asymmetric Encryption and Digital Signatures
Quiz
Security Protocols

Transport Layer Security (TLS)
Public-Key Infrastructure (PKI)
Web of Trust (PGP)
OAuth Protocol
Quiz
From Theory to Practice

Quiz
Practices & Patterns

Introduction
Communication Patterns

Creating and Parsing Data
Transfer of Data
Datastores for Asynchronous Communication
Communication Models
Coordination Patterns

Coordination Patterns
Data Synchronization

Data Synchronisation
Event Sourcing
Change Data Capture (CDC)
Shared-nothing Architectures

Sharing Problems and their Solution
Benefits and Drawbacks
Distributed Locking

Leases in Distributed Systems
Preventing Safety Risks in Leases
Compatibility Patterns

Backwards Compatibility
Maintaining Backwards Compatibility
Dealing with Failure

Failure Handling Techniques
Applying Failure Handling Techniques
Retries
Containing Impact of Failure
Backpressure
Reacting to Backpressure


