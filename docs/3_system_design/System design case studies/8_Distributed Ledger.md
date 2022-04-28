---
layout: default
title: Distributed Ledger
parent: Design case studies
grand_parent: System design
nav_order: 8
permalink: /systemdesign/case/ledger
---
<div align="center" markdown="1">
Distributed Ledger / Java resources / Tutorial

{: .fs-8 .fw-400 }
</div>

## Distributed Ledger

## Introduction to Corda

edger with shared facts amongst each other.

Note: By its nature, Corda is a distributed system similar to the systems analyzed previously.

A distinctive characteristic of this system is this lack of trust between the nodes that are part of the system, which also gives it a decentralization aspect. This distrust is managed through various cryptographic primitives.

Note: This chapter will give a rather brief overview of Corda’s architecture. You can refer to the available whitepapers by Brown et al. and Hearn et al. for a more detailed analysis.

Corda network#
Each node in Corda is a JVM runtime environment with a unique identity on the network. A Corda network comprises many such nodes that want to transact with each other to maintain and evolve a set of shared facts. Corda network is permissioned, which means nodes need to acquire an X.509 certificate from the network operator to be part of the network.

The component that issues X.509 certificates is referred to as the doorman. In this context, the doorman operates as a certificate authority for the nodes that are part of the network.

Public and private keys#
Each node maintains a public and a private key.

The private key is used to attest to facts by signing the associated data.
The public key is used by other nodes to verify these signatures.
This X.509 certificate creates an association between the public key of the node and a human-readable X.500 name (e.g., O=MegaCorp, L=London, C=GB).

Map service#
The network also contains a network map service, which provides some form of service discovery to the nodes part of the network. The nodes can query this service to discover other nodes that are part of the network in order to transact with them.

Interestingly, the nodes do not fully trust the network operator for the distribution of this information. So each entry of this map that contains the identifying data of a node (i.e., IP address, port, X.500 name, public key, X.509 certificate, etc.) is also signed by the corresponding node. In order to avoid censorship by the network operator, the nodes can even exchange the files that contain this information with each other out-of-band and install them locally.

## Corda's Data Model

States#
States represent the shared facts between Corda nodes. States are immutable objects which can contain arbitrary data depending on the use case.

Since states are immutable, they cannot be modified directly to reflect a change in the state of the world. Instead, the current state is marked as historic and is replaced by a new state, which creates a chain of states that gives us a full view of the evolution of a shared fact over time. A Corda transaction does this evolution.

Corda transaction#
Corda transaction specifies the states marked as historic (also known as the input states of the transaction) and the new states that supersede them (also known as the output states of the transaction).

Of course, there are particular rules to specify the kind of states each state can be replaced by. Smart contracts specify these rules, and each state also contains a reference to the contract that governs its evolution.

Smart contract#
The smart contract is a pure function that takes a transaction as an input and determines whether this transaction is considered valid based on the contract’s rules.

Transactions can also contain commands, which indicate the transaction’s intent regarding how the data of the states are used. Each command is also associated with a list of public keys that need to sign the transaction to be valid.

Corda’s data model for electronic money#
The following illustration shows a simple example of the Corda’s data model for electronic money:

![advanced](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/big/car1.png)
![advanced](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/big/car2.png)
![advanced](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/big/car3.png)

In the above illustration, each state represents an amount of money issued by a specific bank and owned by a specific party at some point in time. We can see that Alice combines two cash states to perform payment and transfer 10 GBP to Bob. After that, Bob decides to redeem this money to get some cash from the bank.

As shown in the above illustration, there are two different commands for each case. We can also guess some of the rules of the associated contract for this Cash state.

For a Spend command, the contract will verify that the sum of all input states equals the sum of all output states so that no money is lost or created out of thin air. It will most likely check that the Spend command contains all the owners of the input states as signers, which need to attest to this transfer of money.

Double-spend problem#
In the above example, we can notice that nothing would prevent someone from spending a specific cash state to two different parties who would not be able to detect that. This is known as double-spend.

Preventing double-spend#
Double-spend is prevented in Corda via the concept of notaries.

A notary is a Corda service responsible for attesting that a specific state is not spent more than once.

Transaction finalization#
In practice, every state is associated with a specific notary and every transaction that wants to spend this state needs to acquire a signature from this notary that proves that the state was not spent already by another transaction. This process is known as transaction finalization in Corda.

Fault tolerance and availability with a Notary cluster#
The notarisation services are not necessarily provided by a single node; it can also be a notary cluster of multiple nodes in order to provide better fault tolerance and availability. In that case, these nodes will form a consensus group.

Corda allows the consensus algorithm used by the notary service to be pluggable depending on the requirements in terms of privacy, scalability, performance, etc. For instance:

A notary cluster might choose to use a crash fault tolerant (CFT) consensus algorithm (e.g., Raft) that provides high performance but also requires high trust between the nodes of the cluster.

Alternatively, a notary cluster might choose to use a byzantine fault tolerant (BFT) algorithm that provides lower performance but also requires less trust between the nodes of the cluster.

Implications of permissions on Corda nodes and notaries#
Permissioning has different implications on regular Corda nodes and notaries.

In the first case, it forms the foundation for authentication of communication between nodes.
In the second case, it makes it easier to detect when a notary service deviates from a protocol (e.g., violating finality), identify the associated real-world entity, and take the necessary actions.
This means that finalized transactions are not reversible in Corda unless someone violates the protocol.

Note: Corda is in contrast to some other distributed ledger systems where nodes are anonymous and can thus collude in order to revert historic transactions, such as Bitcoin.

As mentioned previously, in some cases, even a limited amount of protocol violation can be tolerated, i.e., when using a byzantine consensus protocol.

## Corda's Architecture

Problem with applications deployed in a single network#
The size of the ledger of all Corda applications deployed in a single network can become large. The various nodes of the network communicate in a peer-to-peer fashion only with the nodes they need to transact. Still the notary service seems to be something that needs to be used by all the nodes and could potentially become a scalability and performance bottleneck.

Solution by Corda#
To deal with the above-discussed problem, Corda supports both vertical and horizontal partitioning.

Each network can contain multiple notary clusters so that different applications can use different clusters (vertical partitioning). Even the same application can distribute its states between multiple notary clusters for better performance and scalability (vertical partitioning).

Note: The only requirement for all input states of a transaction is to belong to the same notary. This is so that the operation of checking whether a state is spent and marking it as spent can be done atomically in a simple and efficient way without the use of distributed transaction protocols.

Notary-change transaction#
It is a particular transaction type provided by Corda, which allows one to change the notary associated with a state by essentially spending the state and creating a new one associated with the new notary.

In some use cases, the notary-change transaction partitions the datasets to require a minimum number of such transactions, because most transactions are expected to access states from the same partition.

For example, the partitioning of states according to geographic regions if we know in advance that most of the transactions will be accessing data from the same region. This architecture also makes it possible to use states from different applications very easily without the use of distributed transaction protocols.

Note: This above described process is known as atomic swap and, a real use case in the financial world is delivery-versus-payment (DvP).

Corda applications#
Corda applications are called CorDapps and contain several components, of which the most important ones are the states, their contracts, and the flows.

The flows define the workflows between nodes used to update the ledger or simply exchange some messages.

Defining nodes interaction#
Corda provides a framework that allows the application to define the interaction between nodes as a set of blocking calls that send and receive messages. The framework is responsible for transforming this into an asynchronous, event-driven execution.

Providing message serialization#
Corda also provides a custom serialization framework that determines how application messages are serialized when sent across the wire and how they are deserialized when received.

Messaging between nodes#
Messaging between nodes is performed with the use of message queues, using the Apache ActiveMQ Artemis message broker. Specifically, each node maintains an inbound queue for messages received by other nodes and outbound queues for messages sent to other nodes. A bridge process is responsible for forwarding messages from the node’s outbound queues to the corresponding inbound queues of the other nodes.

Even though all of these moving parts can crash and restart in the middle of some operation, the platform guarantees that every node will process each message exactly-once.

Achieving exactly-once guarantee#
The guarantee of every node to process each message exactly once is achieved by resending messages until they are acknowledged and having nodes keeping track of messages processed already and discarding duplicates.

Performing operations in an atomic way#
Nodes also need to acknowledge a message, store its identifier and perform any related side-effects in an atomic way. It is achieved by doing all of this in a single database transaction. All the states from the ledger that are relevant to a node are stored in its database. This part of the database is called the vault.

A node provides some more APIs that are used for various purposes, such as:

Starting flows
Querying the node’s vault
These APIs are accessed remotely via a client, which provides a remote procedure call (RPC) interface implemented on top of the existing messaging infrastructure and using the serialization protocol described before.

The following illustration contains a high-level overview of Corda’s architecture:

![advanced](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/big/car4.png)

## Backwards Compatibility provided by Corda

Corda is a very interesting case study from the perspective of backwards compatibility.

In a distributed system, the various nodes of the system might be running different versions of the software. In many cases, the software is deployed incrementally to them and not in a single step. There is an additional challenge in a decentralized system because different organizations now control the various nodes of the systems so that these discrepancies might last longer.

Corda provides a lot of different mechanisms to preserve backwards compatibility in different areas, so let’s explore some of them.

API & ABI backwards compatibility#
Corda provides API & ABI backwards compatibility for all the public APIs available to CorDapps. It means that any CorDapp should run in future versions of the platform without any change or re-compilation.

Similar to other applications, CorDapps are expected to evolve, which might involve:

Changing the structure of data exchanged between nodes
Changing the structure of data stored in the ledger (e.g., states)
Changing the structure of data exchanged between nodes#
The serialization framework provides some support for the evolution of this case.

Example: Adding nullable properties#
Nullable properties can be added to a class, and the framework will take care of the associated conversions. A node running an older version of the CorDapp will ignore this new property if data is sent from a node running a newer version of the CorDapp. A node running a newer version of the CorDapp will populate the property with null when receiving data from a node running the older version of the CorDapp.

Example: Removing nullable properties and adding non-nullable properties#
Removing nullable properties and adding a non-nullable property is also possible by providing a default value. However, the serialization framework does not allow this form of data loss for data that persisted in the ledger, such as states and commands.

Since states can evolve and the ledger might contain states from many earlier versions of a CorDapp, newer versions of a contract need to contain appropriate logic that can process states from earlier versions of the CorDapp.

The contract logic for handling states from version v_iv
​i
​​  of the CorDapp can be removed by a subsequent release of the CorDapp only after all unspent states in the ledger are from version v_jv
​j
​​  of the CorDapp, where j > ij>i.

New backwards incompatible feature#
In some cases, the platform might introduce a new feature that is not backward compatible. The older versions of the platform cannot understand it . This feature can be problematic for two reasons:

Two nodes running different versions of the platform might reach different conclusions with regards to the validity of a transaction.

When validating a transaction, nodes are also supposed to validate previous transactions involved in the chain of the provenance of the states consumed in the current transaction.

This means that a node running an older version of the platform might fail to validate a transaction that was valid in the past simply because the transaction uses a feature introduced in a newer version of the platform.

Corda solving multiple versioning problem#
Corda solves the multiple versioning problem with the use of the network minimum platform version.

Minimum platform version#
Every network comes with a set of parameters that every node participating in the network needs to agree on and use to interoperate with each other correctly. This set contains a parameter called minimumPlatformVersion, which determines the minimum platform version that the nodes must be running. Any node which is below this will not be able to start.

Any platform feature that is not backwards compatible and requires a minimum version of the platform can check this parameter and be enabled only when the network is over a specific platform version. In this way, the nodes of a network can start using a feature only after they can be certain all other nodes will also be able to use it.

This process establishes a balance between nodes in a network that are keen on using a new feature and nodes that are risk-averse and are not willing to upgrade to a new version of the platform.

Note: However, this process applies only to features that have network-wide implications, e.g., ones that determine how data are stored on the ledger.

Features that do not affect the whole network#
There are features that do not affect the whole network. For example changes to how two nodes interact during the execution of a flow or even how a single node executes some part of a CorDapp locally.

Multiple versioning levers provided by Corda#
Corda provides multiple versioning levers for more fine-grained control. CorDapps provide two version numbers for this purpose: minimumPlatformVersion and targetPlatformVersion.

minimumPlatformVersion indicates the minimum platform version the node must have for the CorDapp to function properly, which is essentially determined based on the necessary features to the CorDapp and the platform version they were introduced in.

targetPlatformVersion indicates the highest version the CorDapp has been tested against and helps the platform disable backwards compatibility codePaths that might make the CorDapp less efficient or secure.

Note: These two versions only have implications on the node running the CorDapp, instead of the whole network.

Another example is the fact that flows in a CorDapp can be versioned to evolve while maintaining backwards compatibility. In this way, a flow can behave differently depending on the deployed version of the CorDapp on the counterparty node. This makes it possible to upgrade a CorDapp incrementally across various nodes, instead of all of them having to do it in lockstep.
