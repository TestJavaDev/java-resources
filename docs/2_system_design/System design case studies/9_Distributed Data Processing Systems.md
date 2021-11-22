---
layout: default
title: Distributed Data Processing Systems
parent: Design case studies
grand_parent: System design
nav_order: 9
permalink: /systemdesign/case/distrb
---
<div align="center" markdown="1">
Distributed Data Processing Systems / Java resources / Tutorial

{: .fs-8 .fw-400 }
</div>

## Distributed Data Processing Systems

This chapter will examine distributed systems used to process large amounts of data that would be impossible or very inefficient to process using only a single machine.

Categories of distributed data processing systems#
Distributed data processing systems can be classified into the following two main categories:

Batch processing systems#
Batch processing systems group individual data items into groups called batches, which are processed one at a time. In many cases, these groups can be quite large (e.g., all items for a day), so the main goal for these systems is usually to provide high throughput, but sometimes at the cost of higher latency.

Stream processing systems#
Stream processing systems receive and process data continuously as a stream of data items. As a result, the main goal for these systems is to provide very low latency sometimes at the cost of decreased throughput.

The following illustration helps us differentiate between a batch and a stream processing system:

![advanced](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/big/car5.png)

There is also a form of processing that is essentially a hybrid between these two categories, called micro-batch processing. This approach processes data in batches, but these are kept very small to achieve a balance between throughput and latency.

In this chapter, we will study the following three distributed data processing systems in detail:

Mapreduce
Apache Spark
Apache Flink

## Introduction to MapReduce

MapReduce is a framework for batch data processing originally developed internally in Google by Dean et al… It was later incorporated in the wider Apache Hadoop framework.

Inspiration#
The framework draws inspiration from the field of functional programming and is based on the following main idea:

Idea#
Many real-word computations can be expressed with the use of two main primitive functions, map and reduce.

Map#
The map function processes a set of key-value pairs and produces another set of intermediate key-value pairs as output…

Reduce#
The reduce function receives all the values for each key and returns a single value, essentially merging all the values according to some logic

An important property of map and reduce functions#
The map and reduce functions can easily be parallelized and run across multiple machines for different parts of the dataset. As a result,

The application code is responsible for defining these two methods.
The framework is responsible for partitioning the data, scheduling the program’s execution across multiple nodes, handling node failures, and managing the required inter-machine communication.
Working of MapReduce#
Let’s see a typical example to understand better how this programming model practically works.

Suppose we have a huge collection of documents (e.g., webpages), and we need to count the number of occurrences for each word. To achieve that via MapReduce, we would use the following functions:

![advanced](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/big/car6.png)

## MapReduce's Master-Worker Architecture

The master node is responsible for scheduling tasks for worker nodes and managing their execution, as shown in the following illustration:

![advanced](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/big/car7.png)

Apart from the definition of the map and reduce functions, the user can also specify the number M of map tasks, the number R of reduce tasks. MapReduce can also specify the number of input or output files, and a partitioning function that defines how key-value pairs from the map tasks are partitioned before being processed by the reduce tasks. By default, a hash partitioner is used that selects a reduce task using the formula hash(key) mod R.

Steps for the execution of MapReduce#
The execution of MapReduce proceeds in the following way:

The framework divides the input files into M pieces, called input splits, typically between 16 and 64 MB per split.

It then starts an instance of a master node and multiple worker node instances on an existing cluster of machines.

The master selects idle worker nodes and assigns map tasks to them.

A worker node assigned a map task reads the contents of the associated input split parses key-value pairs and passes them to the user-defined map function. The entries emitted by the map function are buffered in memory and periodically written to the local disk, partitioned into R regions using the partitioning function. When a worker node completes a map task, it sends the location of the local file to the master node.

The master node assigns reduce tasks to worker nodes providing the location to the associated files. These worker nodes then perform remote procedure calls (RPCs) to read the data from the local disks of the map workers. The data is first sorted so that all occurrences of the same key are grouped together and then passed into the reduce function.

If the size is prohibitively large to fit in memory, external sorting is used.

When all map and reduce tasks are completed, the master node returns the control to the user program. After successful completion, the output of the MapReduce job is available in the R output files that can either be merged or passed as input to a separate MapReduce job.
The master node communicates with every worker periodically in the background in a form of a heartbeat. If no response is received for a specific time, the master node considers the worker node as failed and re-schedules all its tasks for re-execution.

More specifically, completed reduce tasks do not need to be rerun since the output files are stored in an external file system. However, map tasks are rerun regardless of whether they were completed since their output is stored on the local disk and is therefore inaccessible to the reduce tasks that need it.

Note: The network partitions between the master node and worker nodes might lead to multiple executions of a single map or reduce tasks.

Duplicate map tasks executions are deduplicated at the master node, which ignores completion messages for already completed map tasks. The reduce tasks write their output to a temporary file, atomically renamed when the reduce task completes.

Note: This atomic rename operation provided by the underlying file system guarantees that the output files will contain just the data produced by a single execution of each reduce task. However, if the mapor reduce functions defined by the application code have additional side effects (e.g., writing to external datastores), the framework does not provide any guarantees. The application writer must make sure these side effects are atomic and idempotent since the framework might trigger them more than once as part of a task re-execution.

Storage#
Input and output files are usually stored in a distributed file system, such as HDFS or GFS. MapReduce can take advantage of this to perform several optimizations, such as scheduling map tasks to worker nodes that contain a replica of the corresponding input to minimize network traffic or aligning the size of input splits to the block size of the file system.

Guarantees provided by MapReduce#
The MapReduce framework guarantees that the intermediate key-value pairs are processed in increasing key order within a given partition. This ordering guarantee makes it easy to produce a sorted output file per partition, which is helpful for use cases that need to support efficient random access lookups by key or need sorted data in general.

Furthermore, some use-cases would benefit from some form of pre-aggregation at the map level to reduce the amount of data transferred between map and reduce tasks. This was evident in the example presented above. A single map would emit multiple entries for each occurrence of a word instead of a single entry with the number of occurrences. For this reason, the framework allows the application code also to provide a combine function. This method has the same type as the reduce function and is run as part of the map task in order to pre-aggregate the data locally.

## Introduction to Apache Spark

Apache Spark is a data processing system that was initially developed at the University of California by Zaharia et al., and then donated to the Apache Software Foundation.

Note: Apache Spark was developed in response to some of the limitations of MapReduce…

Limitation of MapReduce#
The MapReduce model allowed developing and running embarrassingly parallel computations on a big cluster of machines. Still, every job had to read the input from the disk and write the output to the disk. As a result, there was a lower bound in the latency of job execution, which was determined by disk speeds. So the MapReduce was not a good fit for:

Iterative computations, where a single job was executed multiple times or data were passed through multiple jobs.
Interactive data analysis, where a user wants to run multiple ad hoc queries on the same dataset.
Note: Spark addresses the above two use-cases.

Foundation of Spark#
Spark is based on the concept of Resilient Distributed Datasets (RDD).

Resilient Distributed Datasets (RDD)#
RDD is a distributed memory abstraction used to perform in-memory computations on large clusters of machines in a fault-tolerant way. More concretely, an RDD is a read-only, partitioned collection of records.

RDDs can be created through operations on data in stable storage or other RDDs.

Types of operations performed on RDDs#
The operations performed on an RDD can be one of the following two types:

Transformations#
Transformations are lazy operations that define a new RDD. Some examples of transformations are map, filter, join, and union.

Actions#
Actions trigger a computation to return a value to the program or write data to external storage. Some examples of actions are count, collect, reduce, and save.

Creating an RDD#
A typical Spark application will create an RDD by reading some data from a distributed file system. It will then process the data by calculating new RDDs through transformations and storing the results in an output file.

For example, an application used to read some log files from HDFS and count the number of lines that contain the word “sale completed” would look like the following:


![advanced](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/big/car8.png)

The above program can either be submitted as an individual application in the background or each one of the commands can be executed interactively in the Spark interpreter.

Note: A Spark program is executed from a coordinator process, called the driver.

Architecture of Spark#
The Spark cluster contains a cluster manager node, and a set of worker nodes as shown in the following illustration:

![advanced](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/big/car9.png)

The responsibilities between Spark components are split in the following ways:

Cluster manager#
The cluster manager manages the resources of the cluster (i.e. the worker nodes) and allocates resources to clients that need to run applications.

Worker nodes#
The worker nodes are the nodes of the cluster that wait to receive applications/jobs to execute.

Master process#
Spark also contains a master process that requests resources in the cluster and makes them available to the driver.

Note: Spark supports both a standalone and some clustering modes using third-party cluster management systems, such as YARN, Mesos, and Kubernetes. In the standalone mode, the master process also performs the functions of the cluster manager. In some of the other clustering modes, such as Mesos and YARN, they are separate processes.

Driver#
The driver is responsible for:

Requesting the required resources from the master.
Starting a Spark agent process on each node that runs for the entire lifecycle of the application, called the executor.
Analyzing the user’s application code into a directed acyclic graph (DAG) of stages
Partitioning the associated RDDs
Assigning the corresponding tasks to the executors available to compute them.
The driver is also responsible for managing the overall execution of the application, e.g., receiving heartbeats from executors and restarting failed tasks.

Note: In the previous example, the second line completed_sales = lines.filter(_.contains("sale completed")) is executed without any data being read or processed yet since the filter is a transformation. The data is being read from HDFS, filtered, and then counted when the third line is processed, containing the count operation, which is an action. To achieve that, the driver maintains the relationship between the various RDDs through a lineage graph. When an action is performed, it triggers the calculation of an RDD and all its ancestors.

RDD operations#
RDDs provide the following basic operations:

partitions(): Returns a list of partition objects. For example, an RDD representing an HDFS file has a partition for each block of the file by default. The user can specify a custom number of partitions for an RDD if needed.

partitioner(): Returns metadata determining whether the RDD is hash/range partitioned. This is relevant to transformations that join multiple key-value RDDs based on their keys, such as join or groupByKey. In these cases, hash partitioning is used by default on the keys, but the application can specify a custom range partitioning if needed. An example is provided in Zaharia’s paper, which showed that execution of the PageRank algorithm on Spark can be optimized by providing a custom partitioner that groups all the URLs of a single domain in the same partition.

preferredLocations(p): Lists nodes where partition p are accessed faster due to data locality. This might return nodes that contain the blocks of an HDFS file corresponding to that partition or a node that already contains in memory a partition that needs to be processed.

dependencies(): Returns a list of dependencies on parent RDDs. These dependencies can be classified into two major types: narrow and wide dependencies:

A narrow dependency is where a partition of the parent RDD is used by at most one partition of the child RDD, such as map, filter, or union.
A wide dependency is where multiple child partitions may depend on a single parent partition, such as a join or groupByKey.
Note: join of two RDDs can lead to two narrow dependencies if both RDDs are partitioned with the same partitioner, as shown in the following illustration:

iterator(p, parentIters): Computes the elements of a partition p given iterators for its parent partitions.

![advanced](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/big/car10.png)

## Stages of Digital Acrylic Graph (DAG) in Apache Spark

DAG scheduler of stages#
A DAG of Stages is shown in the following illustration:

![advanced](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/big/car11.png)

Each stage contains as many pipelined transformations with narrow dependencies (one-to-one) as possible.
The boundaries of each stage correspond to operations with wide dependencies (one-to-many) that require a data shuffle between partitions or any previously computed partitions that have been persisted. And it can short-circuit the computation of ancestor RDDs.
The driver launches tasks to compute missing partitions from each stage until it has computed the target RDD.

Note: Spark is based on the concept of Resilient Distributed Datasets (RDD), which is a distributed memory abstraction used to perform in-memory computations on large clusters of machines in a fault-tolerant way.

The tasks are assigned to executors based on data locality. If a task needs to process a partition in memory on a node, it’s submitted to that node. If a task processes a partition for which the containing RDD provides preferred locations (e.g., an HDFS file), it’s submitted to these nodes.

For wide dependencies that require data shuffling, nodes holding parent partitions materialize intermediate records locally that are later pulled by nodes from the next stage, similar to MapReduce.

Note: This graph is the basic building block for efficient fault tolerance.

Tolerating fault#
When an executor fails for some reason, any tasks running on it are re-scheduled on another executor. Along with this, tasks are scheduled for any parent RDDs required to calculate the RDD of this task. Consequently, wide dependencies are much more inefficient than narrow dependencies when recovering from failures, as shown in the following illustration:

![advanced](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/big/car12.png)

Slow recovery#
Long lineage graphs can make a recovery very slow since many RDDs will need to be recomputed in a potential failure near the end of the graph.

Fast recovery process#
Spark provides a checkpointing capability to make fast recovery.

Checkpointing capability#
Checkpointing capability is used to store RDDs from specified tasks to stable storage (e.g., a distributed file system). In this way, checkpointed RDDs can be read from stable storage during recovery, thus only having to rerun smaller portions of the graph. Users can call a persist() method to indicate which RDDs need to be stored on the disk.

Note: The checkpoint capability is very useful for interactive applications, where a specific RDD is calculated and used in multiple ways to explore a dataset without having to calculate the whole lineage each time.

## Perks of Apache Spark

Keeps application running#
Spark provides graceful degradation in cases where memory is not enough so that the application does not fail but keeps running with decreased performance.

For instance, Spark can recalculate any partitions on demand when they don’t fit in memory or spill them to disk.

Increasing performance#
Wide dependencies cause more data to be exchanged between nodes compared to narrow dependencies, so performance is increased significantly by reducing wide dependencies, or the amount of data that needs to be shuffled. One way to do this is by pre-aggregating data, also known as map-side reduction.

Note: As explained previously, the map-side reduction is a capability provided in the MapReduce framework through combiners.

Example#
The following code performs a word count in two different ways:

The first one will send multiple records of value 1 for each word across the network
The second one will send one record for each word containing the number of occurrences.

![advanced](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/big/car13.png)

Resilient to failures of the master process#
We can configure Spark in a way that is resilient to failures of the master process. This is achieved via Zookeeper.

Zookeeper#
In Zookeeper, all the masters perform leader election, and one of them is elected as the leader, with the rest remaining in standby mode.

When a new worker node is added to the cluster, it registers with the master node. If failover occurs, the new master will contact all previously registered worker nodes to inform them of the change in leadership. So, only the scheduling of new applications is affected during a failover; already running applications are unaffected.

When submitting a job to the Spark cluster, the user can specify through a --supervise option that the driver needs to be automatically restarted by the master if it fails with a non-zero exit code.

Ensuring data persistence#
Spark supports multiple, different systems for data persistence.

Commit protocol#
Spark has a commit protocol that aims to provide exactly-once guarantees on the job’s output under specific conditions. It means that no matter how many times worker nodes fail and tasks are rerun, there will be no duplicate or corrupt data in the final output file if a job completes. This might not be the case for every supported storage system, and it’s achieved differently depending on the available capabilities.

For instance, when using HDFS, each task writes the output data to a unique, temporary file (e.g., targetDirectory/_temp/part-XXXX_attempt-YYYY). When the write is complete, the file is moved to the final location (e.g., targetDirectory/part-XXXX) using an atomic rename operation provided by HDFS. As a result, even if a task is executed multiple times due to failures, the final file will contain its output exactly once.

Furthermore, no matter which execution was completed successfully, the output data will be the same as long as the transformations used were deterministic and idempotent. It is true for any transformations that act solely on the data provided by the previous RDDs using deterministic operations.

Note: However, this is not the case if these transformations use data from other systems that might change between executions or if they use non-deterministic actions (e.g., mathematical calculations based on random number generation). Furthermore, if transformations perform side-effects on external systems that are not idempotent, no guarantee is provided since Spark might execute each side-effect more than once.

## Apache Flink

Apache Flink is an open-source stream-processing framework developed by Carbone et al. at Apache Software Foundation to provide a high throughput, low latency data processing engine.

Note: This is the main differentiator between Flink and Spark. Flink processes incoming data as they arrive, which provides sub-second latency that can go down to single-digit millisecond latency. Spark also provides a streaming engine called Spark Streaming. However, that is running some form of micro-batch processing, where an input data stream is split into batches, which are then processed to generate the final results with the associated latency trade-off.

Basic constructs in Flink#
The basic constructs in Flink are streams and transformations.

Stream#
A stream is an unbounded flow of data records.

Note: Flink can also execute batch processing applications, where data is treated as a bounded stream. As a result, the mechanisms described in this section are used in this case also with slight variations.

Transformation#
A transformation is an operation that takes one or more streams as input and produces one or more output streams as a result.

Flink provides many different APIs that are used to define these transformations. For example:

The ProcessFunction API is a low-level interface that allows the user to define imperatively what each transformation should do by providing the code that will process each record.
The DataStream API is a high-level interface that allows the user to define declaratively the various transformations by re-using basic operations, such as map, flatMap, filter, union etc.
Additional Flink constructs#
Since streams can be unbounded, the application has to produce some intermediate, periodic results. For this purpose, Flink provides some additional constructs, such as windows, timers, and local storage for stateful operators.

Flink provides a set of high-level operators that specify the windows over which data from the stream will be aggregated. These windows can be time-driven (e.g., time intervals) or data-driven (e.g., number of elements). The timer API allows applications to register callbacks to be executed at specific points in time in the future.

Flow of data in data processing Flink application#
A data processing application in Flink is represented as a directed acyclic graph (DAG), where nodes represent computing tasks and edges represent data subscriptions between tasks.

Note: Flink also supports cyclic dataflow graphs, which can be used for use-cases such as iterative algorithms.

Flink is responsible for translating the logical graph corresponding to the application code to the actual physical graph executed. It includes logical data flow optimizations, such as the fusion of multiple operations to a single task (e.g., a combination of two consecutive filters). It also includes partitioning each task into multiple instances that can be executed in parallel in different compute nodes. This process is shown in the following illustration:

![advanced](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/big/car14.png)

The architecture of Flink#
The high-level architecture of Flink consists of three main components , as shown in the following illustration:

![advanced](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/big/car15.png)
![advanced](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/big/car16.png)
![advanced](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/big/car17.png)
![advanced](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/big/car18.png)
![advanced](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/big/car19.png)
![advanced](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/big/car20.png)
![advanced](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/big/car21.png)
![advanced](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/big/car22.png)

The Flink client receives the program code, transforms it into a dataflow graph, and submits it to the Job Manager, which coordinates the distributed execution of the dataflow.

The Job Manager schedules tasks on Task Managers, tracking their progress, and coordinating checkpoints and recovery from possible tasks failures.

Each Task Manager executes one or more tasks that perform user-specified operators that can produce other streams and report their status to the Job Manager along with heartbeats used for failure detection. When processing unbounded streams, these tasks are supposed to be long-lived. If they fail, the Job Manager is responsible for restarting them.

Avoid making the Job Manager a single point of failure#
To avoid making the Job Manager a single point of failure multiple instances can run in parallel. One of them will be elected leader via Zookeeper and will be responsible for coordinating the execution of applications. The rest will be waiting to take over in case of a leader failure. As a result, the leader Job Manager stores some critical metadata about every application in Zookeeper so that it’s accessible to newly elected leaders.

## Time and Watermarks in Flink

Processing time#
Processing time refers to the system time of the machine that is executing an operation.

Event time#
Event time is the time that each event occurred on its producing device.

We can use processing time or event time with some trade-offs, which are following.

Processing time trade-offs#
When a streaming program runs on processing time, all time-based operations (e.g., time windows) will use the system clock of the machines that runs the respective operation. It is the simplest notion of time and requires no coordination between the nodes of the system. It also provides good performance and reliably low latency on the produced results.

However, all this comes at the cost of consistency and non-determinism. The system clocks of different machines will differ, and the various nodes of the system will process data at different rates. As a consequence, different nodes might assign the same event to different windows depending on timing.

Event time trade-offs#
When a streaming program runs on event time, all time-based operations will use the event time embedded within the stream records to track time, instead of system clocks. It brings consistency and determinism to the execution of the program since nodes will now have a common mechanism to track the progress of time and assign events to windows.

However, it requires some coordination between the various nodes, as we will see below. It also introduces some additional latency since nodes might have to wait for out of order or late events.

Tracking progress in event time#
The main mechanism to track progress in event time in Flink is watermarks.

Watermarks#
Watermarks are control records that flow as part of a data stream and carry a timestamp t.

A Watermark(t) record indicates that event time has reached time t in that stream, which means there should be no more elements with a timestamp t' ≤ t. Once a watermark reaches an operator, the operator can advance its internal event time clock to the value of the watermark.

Generating watermarks#
Watermarks are generated either directly in the data stream source or by a watermark generator at the beginning of a Flink pipeline.

The operators later in the pipeline are supposed to use the watermarks for their processing (e.g., to trigger calculation of windows) and then emit them downstream to the next operators.

Example#
There are many different strategies for generating watermarks. For example the BoundedOutOfOrdernessGenerator, which assumes that the latest elements for a certain timestamp t will arrive at most n milliseconds after the earliest elements for timestamp t. Of course, there could be elements that do not satisfy this condition and arrive after the associated watermark has been emitted and the corresponding windows have been calculated. These are called late elements.

Flink provides different ways to deal with late elements, such as discarding them or re-triggering the calculation of the associated window.

The following illustration shows the flow of watermarks and the progress of event time in a flink pipeline.

![advanced](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/big/car23.png)

## Failure Recovery in Flink

As mentioned previously, stream processing applications in Flink are supposed to be long-lived. So there must be an efficient way to recover from failures without repeating a lot of work. For this purpose, Flink periodically checkpoints the operators’ state and the position of the consumed stream to generate this state. In case of a failure, an application can be restarted from the latest checkpoint and continue processing from there.

All this is achieved via an algorithm similar to the Chandy-Lamport algorithm for distributed snapshots, called Asynchronous Barrier Snapshotting (ABS).

Asynchronous Barrier Snapshotting (ABS)#
The ABS algorithm operates slightly differently for acyclic and cyclic graphs, so we will examine the first case here, which is a bit simpler.

Working#
The algorithm works in the following way:

The Job Manager periodically injects some control records in the stream, referred to as stage barriers. These records are supposed to divide the stream into stages. At the end of a stage, the set of operator states reflects the whole execution history up to the associated barrier. Thus it can be used for a snapshot.

When a source task receives a barrier, it takes a snapshot of its current state and then broadcasts the barrier to all its outputs.

When a non-source task receives a barrier from one of its inputs, it blocks that input until it has received a barrier from all the inputs. It then takes a snapshot of its current state and broadcasts the barrier to its outputs. Finally, it unblocks its inputs. This blocking guarantees that the checkpoint contains the state after processing all the elements before the barrier and no elements after the barrier.

Note: The snapshot taken while the inputs are blocked are logical , where the actual, physical snapshot is happening asynchronously in the background. One way to achieve this is through copy-on-write techniques. This is done to reduce the duration of this blocking phase to start processing data again as quickly as possible.

Once the background copy process is completed, each task acknowledges the checkpoint back to the Job Manager.The checkpoint is considered complete after the job manager receives the acknowledgement from all the tasks and can be used for recovery if a failure happens later. At this point, the Job Manager notifies all the tasks that the checkpoint is complete so that they can perform any cleanup or bookkeeping logic required.
Subtle points in the checkpoint algorithm#
There are two subtle points in the checkpoint algorithm and the recovery process.

During recovery, tasks will be reset to the last checkpoint and start processing again from the first element after the checkpoint was taken. It means that any state that might have been produced by elements after the last checkpoint will be essentially discarded so that each element is processed exactly-once. However, this raises the following questions:

How is the state produced after the last checkpoint is discarded in practice if it persisted in the operator’s state?

What happens to sink tasks that interact with external systems and records that might have been emitted after the last checkpoint in case of a failure?

What happens with sources that do not support the replay of records?

The answers to all these questions partially rely on a core characteristic of the checkpoint algorithm.

Phases of ABS#
The ABS algorithm has a two-phase commit protocol.

In the first phase, the job manager instructes all the tasks to create a checkpoint.
In the second phase, the job manager informs them that all the tasks successfully created a checkpoint.
Storing operator’s state#
The state of an operator can be stored in different ways, such as in the operator’s memory, in an embedded key-value store, or in an external datastore.

If that datastore supports multi-version concurrency control (MVCC), then all the updates to the state are stored under a version that corresponds to the next checkpoint. During recovery, updates that were performed after the last checkpoint are automatically ignored since reads will return the version corresponding to the last checkpoint.

If the datastore does not support MVCC, all the state changes are maintained temporarily in local storage as a write-ahead-log (WAL), which will be committed to the datastore during the second phase of the checkpoint protocol.

Integration of Flink with other systems#
Flink can also integrate with various other systems such as Kafka, RabbitMQ, etc., to retrieve input data from (sources) or send output data to (sinks). Each one of them provides different capabilities…

Integration with Kafka#
Kafka provides an offset-based interface, which makes it very easy to replay data records in case of recovery from a failure. A sink task keeps track of the offset of each checkpoint and starts reading from that offset during recovery. However, message queues do not provide this interface, so Flink uses alternative methods to provide the same guarantees.

Note: In the case of RabbitMQ, messages are acknowledged and removed from the queue only after the associated checkpoint is complete, during the second phase of the protocol

Similarly, a sink needs to coordinate with the checkpoint protocol to provide exactly-once guarantee. Kafka is a system that can support this through the use of its transactional client.

When the sink creates a checkpoint, the flush() operation is called part of the checkpoint. After the checkpoint completion notification is received from the Job Manager in all operators, the sink calls Kafka’s commitTransaction method.

Note: Flink provides an abstract class called TwoPhaseCommitSinkFunction that provides the basic methods that need to be implemented by a sink that wants to provide these guarantees (i.e. beginTransaction, preCommit, commit, abort).

Guarantees provided by Flink#
Flink provides exactly-once processing semantics even across failures depending on the types of sources and sinks used.
The user can also optionally downgrade to at-least-once processing semantics, which can provide increased performance.
The exactly- once guarantees apply to stream records and local state produced using the Flink APIs. If an operator performs additional side effects on systems external to Flink, then no guarantees are provided for them.
Flink does not provide ordering guarantees after any form of repartitioning or broadcasting. And the responsibility of dealing with out-of-order records is left to the operator implementation.






