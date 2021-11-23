---
layout: default
title: Achieving Isolation
parent: Distributed Systems
grand_parent: System design
nav_order: 1
permalink: /systemdesign/dissystem/achieving
---
<div align="center" markdown="1">
Achieving Isolation / Java resources / Tutorial

{: .fs-8 .fw-400 }
</div>

## Achieving Isolation

## Achieving Serializability

There are different isolation levels that prevent these anomalies. Stronger isolation levels prevent more anomalies at the cost of performance.

We also provided some examples to illustrate the real-life consequences of these anomalies.

As the previous lesson, Consistency and Isolation, explained, the system should be strictly serializable to be completely protected against any of these anomalies.

Strictly serializable is the strongest isolation level. Then comes serializability, which we will see in this lesson.

As the previous chapters explained, a system that provides serializability guarantees that the result of any allowed execution of transactions is the same as that produced by some serial execution of the same transactions(hence its name).

In the context of isolation, the execution of multiple transactions that correspond to an ordering of the associated operations is also called a schedule.

You might ask: what does the same mean in the previous sentence? Let’s explain.

## Types of serializability

There are two major types of serializability that establish two different notions of similarity.

## View serializability
A schedule is a view equivalent to a serial schedule with the same transactions when all the operations from transactions in the two schedules read and write the same data values (“view” the same data).

## Conflict serializability
A schedule is a conflict equivalent to a serial schedule with the same transactions when every pair of conflicting operations between transactions is ordered in the same way in both schedules.

It turns out that calculating whether a schedule is view serializable is a very computationally hard problem. More specifically, it is an NP-complete problem. This means that the time required to solve the problem using any currently known algorithm increases rapidly as the size of the problem grows. So, we will not analyze view serializability further.

However, determining whether a schedule is conflict serializable is a much easier problem to solve, which is one of the reasons conflict serializability is widely used.

Determining whether a schedule is a conflict serializable#
To understand conflict serializability, we first have to define what it means for two operations to be conflicting.

Two operations are conflicting (or conflict) if:
* They belong to different transactions
* They are on the same data item, and at least one of them is a write operation, where a write operation inserts, modifies or deletes an object

As a result, we can have three different forms of conflicts:
* A read-write conflict
* A write-read conflict
* A write-write conflict

## Trivial way
A trivial way to check if a schedule is a conflict serializable is to calculate all possible serial schedules, identify conflicting operations in them, and check if their order is the same as in the schedule under examination.

This is computationally heavy, as it requires us to compute all the possible permutations of transactions.

A more practical way of determining whether a schedule is conflict serializable is through a precedence graph.

## Precedence graph
A precedence graph is a directed graph, where the:
* Nodes represent transactions in a schedule
* Edges represent conflicts between operations

The edges in the graph denote the order in which transactions must execute in the corresponding serial schedule.

As a result, a schedule is a conflict serializable if and only if its precedence graph of committed transactions is acyclic.

Let’s look at an example to get a better idea about this rule.

## Example

![advanced](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/big/car30.png)

![advanced](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/big/car31.png)

![advanced](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/big/car32.png)

![advanced](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/big/car33.png)


## Generating a schedule that is serializable
The notion of a precedence graph is beneficial here.

All we need to do is ensure that no cycle is formed as we execute operations in the schedule. We can achieve this in two basic ways.

Prevent transactions from making progress when there is a risk of introducing a conflict that can create a cycle.
Let transactions execute all their operations and check if committing that transaction could introduce a cycle. In that case, the transaction can be aborted and restarted from scratch.
These two approaches lead to the two main mechanisms for concurrency control.

## Mechanisms for concurrency control
There are two main mechanisms for concurrency control:

## Pessimistic concurrency control
This approach blocks a transaction if it’s expected to cause violation of serializability, and resumes it when it is safe to do so.

This is usually achieved by having transactions acquire locks on the data they process to prevent other transactions from processing the same data concurrently.

The name pessimistic comes from the fact that this approach assumes that the majority of transactions are expected to conflict with each other, so appropriate measures are taken to prevent this from causing issues.

## Optimistic concurrency control
This approach delays the checking of whether a transaction complies with the rules until the end of the transaction. The transaction is aborted if a commit would violate any serializability rules, and is then restarted and re-executed from the beginning.

The name “optimistic” comes from the fact that this approach assumes that the majority of transactions are expected not to have conflicts, so measures are taken only in the rare case that they do.

The main trade-off between pessimistic and optimistic concurrency control is between the extra overhead from locking mechanisms, and the wasted computation from aborted transactions.

## Cases where optimistic methods perform well
In general, optimistic methods are expected to perform well in cases where there are not many conflicts between transactions.

This can be the case for workloads with many read-only transactions and only a few write transactions, or in cases where most of the transactions touch different data.

## Cases where pessimistic methods perform well
Pessimistic methods incur some overhead from the use of locks. Still, they can perform better in workloads that contain a lot of transactions that conflict. This is because they reduce the number of aborts and restarts, thus reducing wasted effort.

## Pessimistic Concurrency Control (PCC)

## 2-Phase locking (2PL)

2-phase locking (2PL) is a pessimistic concurrency control protocol that uses locks to prevent concurrent transactions from interfering. These locks indicate that a record is being used by a transaction, so that other transactions can determine whether it is safe to use it or not.

## Types of locks
There are two basic types of locks used in this protocol:
* Write (exclusive) locks: These locks are acquired when a record is going to be written (inserted/updated/deleted).
* Read (shared) locks: These locks are acquired when a record is read.
* Interaction between write (exclusive) locks and read (shared) locks#
* A read lock does not block a read from another transaction. This is why it is also called shared because multiple read locks can be acquired at the same time.
* A read lock blocks a write from another transaction. The other transaction will have to wait until the read operation is completed and the read lock is released. Then, it will have to acquire a write lock and perform the write operation.
* A write lock blocks both reads and writes from other transactions, which is also the reason it’s also called exclusive. The other transactions will have to wait for the write operation to complete and the write lock to be released; then, they will attempt to acquire the proper lock and proceed.
* If a lock blocks another lock, they are called incompatible. Otherwise, they are called compatible.

As a result, the relationships described above can be visualized in a compatibility matrix, as shown in the following illustration.

![advanced](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/big/car34.png)

The astute reader might notice a similarity between this matrix and the definition of conflicts in conflict serializability. This is not a coincidence. The two-phase locking protocol makes use of these locks to prevent cycles of these conflicts from forming, as described before.

Each type of conflict is represented by an incompatible entry in the above matrix.

## Phases where transactions acquire or release locks
In 2-phase locking protocol, transactions acquire and release locks in two distinct phases:

## Expanding phase
In this phase, a transaction is allowed to only acquire locks, but not release any locks.

## Shrinking phase
In this phase, a transaction is allowed to only release locks, but not acquire any locks.

The following illustration shows these phases.

![advanced](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/big/car35.png)
![advanced](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/big/car36.png)

It’s been implied so far that locks are held per record. However, it’s important to note that if the associated database supports operations based on predicates, there must also be a way to lock ranges of records (predicate locking), e.g., all the customers of ages between 23 and 29. This is to prevent anomalies like phantom reads.

As proven by Franking, this protocol only allows serializable executions to happen.

A schedule generated by two-phase locking will be conflict equivalent to a serial schedule, where transactions are serialized in the order they completed their expanding phase.

There are some slight variations of the protocol that can provide some additional properties, such as:
* Strict two-phase locking (S2PL)
* Strong strict two-phase locking (SS2PL)

## Deadlocks
The locking mechanism introduces the risk for deadlocks, where two transactions might wait on each other for the release of a lock, thus never making progress. This is shown in the following illustration.

![advanced](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/big/car37.png)

## Ways to deal with deadlocks
In general, there are two ways to deal with these deadlocks.

## Prevention
This method prevents the deadlocks from being formed in the first place.

For example, this can be done if transactions know all the locks they need in advance and acquire them in an ordered way. This is typically done by the application since many databases support interactive transactions and are thus unaware of all the data a transaction will access.

## Detection
This method detects deadlocks that occur, and breaks them. For example, this can be achieved by keeping track of which transaction a transaction waits on, using this information to detect cycles that represent deadlocks, and then forcing one of these transactions to abort. This is typically done by the database, without the application having to do anything extra.

## Optimistic Concurrency Control (OCC)

Optimistic concurrency control (OCC) is a concurrency control method that was first proposed in 1981 by Kung et al., where transactions can access data items without acquiring locks on them.

In this method, transactions execute in the following three phases:
* Begin
* Read & modify
* Validate & commit/rollback

## Begin phase
In this phase, transactions are assigned a unique timestamp that marks the beginning of the transaction.

## Read & modify phase
During this phase, transactions execute their read and write operations tentatively. This means that when an item is modified, a copy of the item is written to a temporary, local storage location. A read operation first checks for a copy of the item in this location and returns this one, if it exists. Otherwise, it performs a regular read operation from the database.

## Validate & commit/rollback phase
The transaction enters this phase when all operations have been executed.

During this phase, the transaction checks whether there are other transactions that have modified the data this transaction has accessed, and have started after this transaction’s start time. If there are, then the transaction is aborted and restarted from the beginning, acquiring a new timestamp. Otherwise, the transaction can be committed.

This is shown in the following illustration.

![advanced](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/big/car38.png)
![advanced](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/big/car39.png)
![advanced](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/big/car40.png)

The commit of a transaction is performed by copying all the values from write operations, from the local storage to the common database storage that other transactions access.

It’s important to note that the validation checks and the associated commit operation need to be performed in a single atomic action as part of a critical section.

This requires some form of locking mechanism, so there are various optimizations of this approach that attempt to reduce the duration of this phase to improve performance.

## Ways to implement validation logic
There are two ways to implement validation logic.

## Version checking
One way is via version checking, where every data item is marked with a version number. Every time a transaction accesses an item, it can keep track of the version number it had at that point.

During the validation phase, the transaction can check if the version number is the same. If it is, it would mean that no other transaction has accessed the item in the meanwhile.

## Timestamp ordering
Another way is by using timestamps assigned to transactions, a technique also known as timestamp ordering, since the timestamp indicates the order in which a transaction must occur relative to the other transaction.

In this approach, each transaction keeps track of the items that are accessed by read or write operations, known as the read set and the write set.

During validation, a transaction performs the following inside a critical section:
* It records a fresh timestamp, called the finish timestamp, and iterates over all the transactions that have been assigned a timestamp between the transaction’s start and finish timestamp.
* These are essentially all transactions that have started after the running transaction and have already been committed.
* For each of those transactions, the running transaction checks if their write set intersects with its own read set. If that’s true for any of these transactions, it means that the transaction essentially reads a value “from the future.”
* As a result, the transaction is invalid and must be aborted and restarted from the beginning with a fresh timestamp. Otherwise, the transaction is committed, and is assigned the next timestamp.

## Achieving Snapshot Isolation

## Multi-version concurrency control (MVCC)

Multiversion Concurrency Control (MVCC) is a technique where multiple physical versions are maintained for a single logical data item. As a result, update operations do not overwrite existing records, but they write a new version of these records. Read operations can then select a specific version of a record, possibly an older one.

This is in contrast with the previous techniques, where updates are performed in place and there is a single record for each data item that can be accessed by read operations.

Reed proposed the original protocol in a dissertation in 1978, but many different variations of the original idea have been proposed since then by Silberschatz and Stearns et al.

As the name implies, this technique focuses on the multi-version aspect of storage so that it can be used, theoretically, with both optimistic and pessimistic schemes.

However, most variations use an optimistic concurrency control method to leverage the multiple versions of an item from transactions that run concurrently.

## Achieving snapshot isolation using MVCC
In practice, MVCC is commonly used to implement the snapshot isolation level.

As explained before, snapshot isolation (SI) is an isolation level that guarantees that all reads made in a transaction see a consistent snapshot of the database from the point it started, and the transaction commits successfully if no other transaction has updated the same data since that snapshot. As a result, it is practically easier to achieve snapshot isolation using a MVCC technique.

## Steps

This works in the following way:
* Each transaction is assigned a unique timestamp at the beginning.
* Every entry for a data item contains a version that corresponds to the timestamp of the transaction that created this new version.
* Every transaction records the following pieces of information during its beginning:
* The transaction with the highest timestamp that has committed so far (say, T_sT)
* The number of active transactions that have started but haven’t been committed yet

## Performing a read operation
When performing a read operation for an item, a transaction returns the entry with the latest version that is earlier than Ts and does not belong to one of the transactions that were active at the beginning of this transaction. This prevents dirty reads, as only committed values from other transactions can be returned.

There is an exception to this rule: if the transaction has already updated this item, then this value is returned instead.

Fuzzy reads are also prevented since all the reads return values from the same snapshot and ignore values from transactions that committed after this transaction started.

## Performing a write operation
When performing a write operation for an item, a transaction checks whether there is an entry for the same item that satisfies one of the following criteria: its version is higher than this transaction’s timestamp, or its version is lower than this transaction’s timestamp, but this version belongs to one of the transactions that were active at the beginning of this transaction.

![advanced](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/big/car41.png)

## Not all anomalies can be prevented in MVCC
An example of an anomaly that would not be prevented is a write skew.

## Write-skew example
The following illustration shows why we can’t prevent a write skew from happening.

![advanced](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/big/car42.png)
![advanced](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/big/car43.png)
![advanced](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/big/car44.png)
![advanced](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/big/car45.png)
![advanced](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/big/car46.png)
![advanced](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/big/car47.png)

In the schedule shown in the above illustration, none of the transactions sees the versions written by the other transaction. However, this would not be possible in a serial execution.

## Achieving Full Serializable Snapshot Isolation

Research in the field of concurrency control mechanism for achieving snapshot isolation level has resulted in an improved algorithm, called serializable snapshot isolation (SSI), that can provide full serializability and has been integrated into commercial, widely used databases by Ports et al.

This algorithm is still optimistic and just adds some extensions on top of what we described in the previous lesson.

## Serializable snapshot isolation (SSI)
The solution mechanics are based on a key principle of previous research that showed that all the non-serializable executions under snapshot isolation share a common characteristic.

## Statement
SSI states this: in the precedence graph of any non-serializable execution, there are two rw-dependency edges that form consecutive edges in a cycle. These involve two transactions that have been active concurrently, as shown in the following illustration.

![advanced](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/big/car48.png)

![advanced](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/big/car49.png)

## Approach
The SSI approach detects these cases and breaks the cycle when they are about to happen. It prevents them from being formed by aborting one of the involved transactions. To do this, the SSI performs the following steps:

It keeps track of the incoming and outgoing rw-dependency edges of each transaction.

If there is a transaction that has both incoming and outgoing edges, the algorithm aborts one of the transactions and retries it later.

Note this can lead to aborts that are false positives, since the algorithm does not check whether there is a cycle. This is done intentionally to avoid the computational costs associated with tracking cycles.

So, it is sufficient to maintain two Boolean flags per transaction T.inConflict and T.outConflict, that denote whether there is an incoming and outgoing rw-dependency edge. These flags can be maintained in the following way:

When a transaction TT is performing a read, it is able to detect whether there is a version of the same item that was written after the transaction started, e.g., by another transaction UU. This would imply a rw-dependency edge, so the algorithm can update T.outConflict and U.inConflict to true.
However, this will not detect cases where the write happens after the read. The algorithm uses a different mechanism to detect these cases, too.

Every transaction creates a read lock, called SIREAD lock, when it performs a read. As a result, when a transaction performs a write, it can read the existing SIREAD locks and detect concurrent transactions that have previously read the same item. It thus updates the same Boolean flags accordingly.
Note that these are a softer form of locks, since they do not block other transactions from operating, but exist mainly to signal data dependencies between them. This means the algorithm preserves its optimistic nature.

## Preventing write-skew anomaly using SSI

The following illustration shows how this approach would prevent the write skew anomaly we have seen in the previous lesson.

![advanced](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/big/car50.png)
![advanced](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/big/car51.png)
![advanced](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/big/car52.png)
![advanced](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/big/car53.png)
![advanced](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/big/car54.png)
![advanced](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/big/car55.png)

![advanced](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/big/car56.png)

