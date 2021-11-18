---
layout: default
title: The Basics
parent: Multithreading
has_children: true
nav_order: 1
permalink: /multithreading/basics
---
<div align="center" markdown="1">
Multithreading / Java resources / Tutorial

{: .fs-8 .fw-400 }
</div>

## Benefits of Threads
Higher throughput, though in some pathetic scenarios it is possible to have the overhead of context switching among threads steal away any throughput gains and result in worse performance than a single-threaded scenario. However such cases are unlikely and an exception, rather than the norm.

Responsive applications that give the illusion of multi-tasking.

Efficient utilization of resources. Note that thread creation is light-weight in comparison to spawning a brand new process. Web servers that use threads instead of creating new processes when fielding web requests, consume far fewer resources.

All other benefits of multi-threading are extensions of or indirect benefits of the above.

## Performance Gains via Multi-Threading
As a concrete example, consider the example code below. The task is to compute the sum of all the integers from 0 to Integer.MAX_VALUE. In the first scenario, we have a single thread doing the summation while in the second scenario we split the range into two parts and have one thread sum for each range. In the end, we add the two half sums to get the combined sum. We measure the time taken for each scenario and print it.
{% highlight java %}
class Demonstration {
    public static void main( String args[] ) throws InterruptedException {
        SumUpExample.runTest();
    }
}

class SumUpExample {

    long startRange;
    long endRange;
    long counter = 0;
    static long MAX_NUM = Integer.MAX_VALUE;

    public SumUpExample(long startRange, long endRange) {
        this.startRange = startRange;
        this.endRange = endRange;
    }

    public void add() {

        for (long i = startRange; i <= endRange; i++) {
            counter += i;
        }
    }

    static public void twoThreads() throws InterruptedException {

        long start = System.currentTimeMillis();
        SumUpExample s1 = new SumUpExample(1, MAX_NUM / 2);
        SumUpExample s2 = new SumUpExample(1 + (MAX_NUM / 2), MAX_NUM);

        Thread t1 = new Thread(() -> {
            s1.add();
        });

        Thread t2 = new Thread(() -> {
            s2.add();
        });

        t1.start();
        t2.start();
        
        t1.join();
        t2.join();

        long finalCount = s1.counter + s2.counter;
        long end = System.currentTimeMillis();
        System.out.println("Two threads final count = " + finalCount + " took " + (end - start));
    }

    static public void oneThread() {

        long start = System.currentTimeMillis();
        SumUpExample s = new SumUpExample(1, MAX_NUM );
        s.add();
        long end = System.currentTimeMillis();
        System.out.println("Single thread final count = " + s.counter + " took " + (end - start));
    }


    public static void runTest() throws InterruptedException {

        oneThread();
        twoThreads();

    }
}
{% endhighlight %}

In my run, I see the two threads scenario run within 652 milliseconds whereas the single thread scenario runs in 886 milliseconds. You may observe different numbers but the time taken by two threads would always be less than the time taken by a single thread. The performance gains can be many folds depending on the availability of multiple CPUs and the nature of the problem being solved. However, there will always be problems that don't yield well to a multi-threaded approach and may very well be solved efficiently using a single thread.

## Problems with Threads

However, as it is said, there's no free lunch in life. The premium for using threads manifests in the following forms:
1. Usually very hard to find bugs, some that may only rear head in production environments
2. Higher cost of code maintenance since the code inherently becomes harder to reason about
3. Increased utilization of system resources. Creation of each thread consumes additional memory, CPU cycles for book-keeping and waste of time in context switches.
4. Programs may experience slowdown as coordination amongst threads comes at a price. Acquiring and releasing locks adds to program execution time. Threads fighting over acquiring locks cause lock contention.

With this backdrop lets delve into more details of concurrent programming about which you are likely to be quizzed in an interview.

## Program vs Process vs Thread

## Program
A program is a set of instructions and associated data that resides on the disk and is loaded by the operating system to perform some task. An executable file or a python script file are examples of programs. In order to run a program, the operating system's kernel is first asked to create a new process, which is an environment in which a program executes.

## Process
A process is a program in execution. A process is an execution environment that consists of instructions, user-data, and system-data segments, as well as lots of other resources such as CPU, memory, address-space, disk and network I/O acquired at runtime. A program can have several copies of it running at the same time but a process necessarily belongs to only one program.

## Thread
Thread is the smallest unit of execution in a process. A thread simply executes instructions serially. A process can have multiple threads running as part of it. Usually, there would be some state associated with the process that is shared among all the threads and in turn each thread would have some state private to itself. The globally shared state amongst the threads of a process is visible and accessible to all the threads, and special attention needs to be paid when any thread tries to read or write to this global shared state. There are several constructs offered by various programming languages to guard and discipline the access to this global state, which we will go into further detail in upcoming lessons.

## Caveats
Note a program or a process are often used interchangeably but most of the times the intent is to refer to a process.

There's also the concept of "multiprocessing" systems, where multiple processes get scheduled on more than one CPU. Usually, this requires hardware support where a single system comes with multiple cores or the execution takes place in a cluster of machines. Processes don't share any resources amongst themselves whereas threads of a process can share the resources allocated to that particular process, including memory address space. However, languages do provide facilities to enable inter-process communication.
 
![jmm](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/jmm/jmm1.png)

## Counter Program
Below is an example highlighting how multi-threading necessitates caution when accessing shared data amongst threads. Incorrect synchronization between threads can lead to wildly varying program outputs depending on in which order threads get executed.

Consider the below snippet of code

![jmm](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/jmm/jmm2.png)

The increment on line 4 is likely to be decompiled into the following steps on a computer:
* Read the value of the variable counter from the register where it is stored
* Add one to the value just read
* Store the newly computed value back to the register

The innocuous looking statement on line 4 is really a three step process!

Now imagine if we have two threads trying to execute the same function incrementCounter then one of the ways the execution of the two threads can take place is as follows:

Lets call one thread as T1 and the other as T2. Say the counter value is equal to 7.
1. T1 is currently scheduled on the CPU and enters the function. It performs step A i.e. reads the value of the variable from the register, which is 7.
2. The operating system decides to context switch T1 and bring in T2.
3. T2 gets scheduled and luckily gets to complete all the three steps A, B and C before getting switched out for T1. It reads the value 7, adds one to it and stores 8 back.
4. T1 comes back and since its state was saved by the operating system, it still has the stale value of 7 that it read before being context switched. It doesn't know that behind its back the value of the variable has been updated. It unfortunately thinks the value is still 7, adds one to it and overwrites the existing 8 with its own computed 8. If the threads executed serially the final value would have been 9.

The problems should be apparent to the astute reader. Without properly guarding access to mutable variables or data-structures, threads can cause hard to find to bugs.

Since the execution of the threads can't be predicted and is entirely up to the operating system, we can't make any assumptions about the order in which threads get scheduled and executed.

## Thread unsafe class
Take a minute to go through the following program. It increments a counter and decrements it an equal number of times. The final value of the counter should be zero, however, if you run the program enough times, you'll sometimes get the correct zero value, and at others, you'll get a non-zero value. We sleep the threads to give them a chance to run in a non-deterministic order.

{% highlight java %}
class DemoThreadUnsafe {

    // We'll use this to randomly sleep our threads
    static Random random = new Random(System.currentTimeMillis());

    public static void main(String args[]) throws InterruptedException {

        // create object of unsafe counter
        ThreadUnsafeCounter badCounter = new ThreadUnsafeCounter();

        // setup thread1 to increment the badCounter 200 times
        Thread thread1 = new Thread(new Runnable() {

            @Override
            public void run() {
                for (int i = 0; i < 100; i++) {
                    badCounter.increment();
                    DemoThreadUnsafe.sleepRandomlyForLessThan10Secs();
                }
            }
        });

        // setup thread2 to decrement the badCounter 200 times
        Thread thread2 = new Thread(new Runnable() {

            @Override
            public void run() {
                for (int i = 0; i < 100; i++) {
                    badCounter.decrement();
                    DemoThreadUnsafe.sleepRandomlyForLessThan10Secs();
                }
            }
        });

        // run both threads
        thread1.start();
        thread2.start();

        // wait for t1 and t2 to complete.
        thread1.join();
        thread2.join();

        // print final value of counter
        badCounter.printFinalCounterValue();
    }

    public static void sleepRandomlyForLessThan10Secs() {
        try {
            Thread.sleep(random.nextInt(10));
        } catch (InterruptedException ie) {
        }
    }
}

class ThreadUnsafeCounter {

    int count = 0;

    public void increment() {
        count++;
    }

    public void decrement() {
        count--;
    }

    void printFinalCounterValue() {
        System.out.println("counter is: " + count);
    }
}
{% endhighlight %}

## Concurrency vs Parallelism

## Introduction
Concurrency and Parallelism are often confused to refer to the ability of a system to run multiple distinct programs at the same time. Though the two terms are somewhat related yet they mean very different things. To clarify the concept, we'll borrow a juggler from a circus to use as an analogy. Consider the juggler to be a machine and the balls he juggles as processes.

## Serial Execution
When programs are serially executed, they are scheduled one at a time on the CPU. Once a task gets completed, the next one gets a chance to run. Each task is run from the beginning to the end without interruption. The analogy for serial execution is a circus juggler who can only juggle one ball at a time. Definitely not very entertaining!

## Concurrency
A concurrent program is one that can be decomposed into constituent parts and each part can be executed out of order or in partial order without affecting the final outcome. A system capable of running several distinct programs or more than one independent unit of the same program in overlapping time intervals is called a concurrent system. The execution of two programs or units of the same program may not happen simultaneously.

A concurrent system can have two programs in progress at the same time where progress doesn't imply execution. One program can be suspended while the other executes. Both programs are able to make progress as their execution is interleaved. In concurrent systems, the goal is to maximize throughput and minimize latency. For example, a browser running on a single core machine has to be responsive to user clicks but also be able to render HTML on screen as quickly as possible. Concurrent systems achieve lower latency and higher throughput when programs running on the system require frequent network or disk I/O.

The classic example of a concurrent system is that of an operating system running on a single core machine. Such an operating system is concurrent but not parallel. It can only process one task at any given point in time but all the tasks being managed by the operating system appear to make progress because the operating system is designed for concurrency. Each task gets a slice of the CPU time to execute and move forward.

Going back to our circus analogy, a concurrent juggler is one who can juggle several balls at the same time. However, at any one point in time, he can only have a single ball in his hand while the rest are in flight. Each ball gets a time slice during which it lands in the juggler's hand and then is thrown back up. A concurrent system is in a similar sense juggling several processes at the same time.

## Parallelism
A parallel system is one which necessarily has the ability to execute multiple programs at the same time. Usually, this capability is aided by hardware in the form of multicore processors on individual machines or as computing clusters where several machines are hooked up to solve independent pieces of a problem simultaneously. Remember an individual problem has to be concurrent in nature, that is portions of it can be worked on independently without affecting the final outcome before it can be executed in parallel.

In parallel systems the emphasis is on increasing throughput and optimizing usage of hardware resources. The goal is to extract out as much computation speedup as possible. Example problems include matrix multiplication, 3D rendering, data analysis, and particle simulation.

Revisiting our juggler analogy, a parallel system would map to at least two or more jugglers juggling one or more balls. In the case of an operating system, if it runs on a machine with say four CPUs then the operating system can execute four tasks at the same time, making execution parallel. Either a single (large) problem can be executed in parallel or distinct programs can be executed in parallel on a system supporting parallel execution.

## Concurrency vs Parallelism
From the above discussion it should be apparent that a concurrent system need not be parallel, whereas a parallel system is indeed concurrent. Additionally, a system can be both concurrent and parallel e.g. a multitasking operating system running on a multicore machine.

Concurrency is about dealing with lots of things at once. Parallelism is about doing lots of things at once. Last but not the least, you'll find literature describing concurrency as a property of a program or a system whereas parallelism as a runtime behaviour of executing multiple tasks.

We end the lesson with an analogy, frequently quoted in online literature, of customers waiting in two queues to buy coffee. Single-processor concurrency is akin to alternatively serving customers from the two queues but with a single coffee machine, while parallelism is similar to serving each customer queue with a dedicated coffee machine.

![jmm](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/jmm/jmm3.png)

## Cooperative Multitasking vs Preemptive Multitasking

## Introduction

A system can achieve concurrency by employing one of the following multitasking models:
* Preemptive Multitasking
* Cooperative Multitasking

## Preemptive Multitasking
In preemptive multitasking, the operating system preempts a program to allow another waiting task to run on the CPU. Programs or threads can't decide how long for or when they can use the CPU. The operating system’s scheduler decides which thread or program gets to use the CPU next and for how much time. Furthermore, scheduling of programs or threads on the CPU isn’t predictable. A thread or program once taken off of the CPU by the scheduler can't determine when it will get on the CPU next. As a consequence, if a malicious program initiates an infinite loop, it only hurts itself without affecting other programs or threads. Lastly, the programmer isn't burdened to decide when to give up control back to the CPU in code.

## Cooperative Multitasking
Cooperative Multitasking involves well-behaved programs to voluntarily give up control back to the scheduler so that another program can run. A program or thread may give up control after a period of time has expired or if it becomes idle or logically blocked. The operating system’s scheduler has no say in how long a program or thread runs for. A malicious program can bring the entire system to a halt by busy waiting or running an infinite loop and not giving up control. The process scheduler for an operating system implementing cooperative multitasking is called a cooperative scheduler. As the name implies, the participating programs or threads are required to cooperate to make the scheduling scheme work.

## Cooperative vs Preemptive
Early versions of both Windows and Mac OS used cooperative multitasking. Later on preemptive multitasking was introduced in Windows NT 3.1 and in Mac OS X. However, preemptive multitasking has always been a core feature of Unix based systems.

## Synchronous vs Asynchronous

## Synchronous
Synchronous execution refers to line-by-line execution of code. If a function is invoked, the program execution waits until the function call is completed. Synchronous execution blocks at each method call before proceeding to the next line of code. A program executes in the same sequence as the code in the source code file. Synchronous execution is synonymous to serial execution.

## Asynchronous
Asynchronous (or async) execution refers to execution that doesn't block when invoking subroutines. Or if you prefer the more fancy Wikipedia definition: Asynchronous programming is a means of parallel programming in which a unit of work runs separately from the main application thread and notifies the calling thread of its completion, failure or progress. An asynchronous program doesn’t wait for a task to complete and can move on to the next task.

In contrast to synchronous execution, asynchronous execution doesn't necessarily execute code line by line, that is instructions may not run in the sequence they appear in the code. Async execution can invoke a method and move onto the next line of code without waiting for the invoked function to complete or receive its result. Usually, such methods return an entity sometimes called a future or promise that is a representation of an in-progress computation. The program can query for the status of the computation via the returned future or promise and retrieve the result once completed. Another pattern is to pass a callback function to the asynchronous function call which is invoked with the results when the asynchronous function is done processing. Asynchronous programming is an excellent choice for applications that do extensive network or disk I/O and spend most of their time waiting. As an example, Javascript enables concurrency using AJAX library's asynchronous method calls. In non-threaded environments, asynchronous programming provides an alternative to threads in order to achieve concurrency and fall under the cooperative multitasking model.

Asynchronous programming support in Java has become a lot more robust starting with Java 8, however, the topic is out of scope for this course so we only mention it in passing.

## I/O Bound vs CPU Bound

## I/O Bound vs CPU Bound

We write programs to solve problems. Programs utilize various resources of the computer systems on which they run. For instance a program running on your machine will broadly require:
* CPU Time
* Memory
* Networking Resources
* Disk Storage

Depending on what a program does, it can require heavier use of one or more resources. For instance, a program that loads gigabytes of data from storage into main memory would hog the main memory of the machine it runs on. Another can be writing several gigabytes to permanent storage, requiring abnormally high disk i/o.

## CPU Bound
Programs which are compute-intensive i.e. program execution requires very high utilization of the CPU (close to 100%) are called CPU bound programs. Such programs primarily depend on improving CPU speed to decrease program completion time. This could include programs such as data crunching, image processing, matrix multiplication etc.

If a CPU bound program is provided a more powerful CPU it can potentially complete faster. Eventually, there is a limit on how powerful a single CPU can be. At this point, the recourse is to harness the computing power of multiple CPUs and structure your program code in a way that can take advantage of the multiple CPU units available. Say we are trying to sum up the first 1 million natural numbers. A single-threaded program would sum in a single loop from 1 to 1000000. To cut down on execution time, we can create two threads and divide the range into two halves. The first thread sums the numbers from 1 to 500000 and the second sums the numbers from 500001 to 1000000. If there are two processors available on the machine, then each thread can independently run on a single CPU in parallel. In the end, we sum the results from the two threads to get the final result. Theoretically, the multithreaded program should finish in half the time that it takes for the single-threaded program. However, there will be a slight overhead of creating the two threads and merging the results from the two threads.

Multithreaded programs can improve performance in cases where the problem lends itself to being divided into smaller pieces that different threads can work on independently. This may not always be true though.

## I/O Bound
I/O bound programs are the opposite of CPU bound programs. Such programs spend most of their time waiting for input or output operations to complete while the CPU sits idle. I/O operations can consist of operations that write or read from main memory or network interfaces. Because the CPU and main memory are physically separate a data bus exists between the two to transfer bits to and fro. Similarly, data needs to be moved between network interfaces and CPU/memory. Even though the physical distances are tiny, the time taken to move the data across is big enough for several thousand CPU cycles to go waste. This is why I/O bound programs would show relatively lower CPU utilization than CPU bound programs.

## Caveats
Both types of programs can benefit from concurrent architectures. If a program is CPU bound we can increase the number of processors and structure our program to spawn multiple threads that individually run on a dedicated or shared CPU. For I/O bound programs, it makes sense to have a thread give up CPU control if it is waiting for an I/O operation to complete so that another thread can get scheduled on the CPU and utilize CPU cycles. Different programming languages come with varying support for multithreading. For instance, Javascript is single-threaded, Java provides full-blown multithreading and Python is sort of multithreaded as it can only have a single thread in running state because of its global interpreter lock (GIL) limitation. However, all three languages support asynchronous programming models which is another way for programs to be concurrent (but not parallel).

For completeness we should mention that there are also memory-bound programs that depend on the amount of memory available to speed up execution.

## Throughput vs Latency

## Throughput
Throughput is defined as the rate of doing work or how much work gets done per unit of time. If you are an Instagram user, you could define throughput as the number of images your phone or browser downloads per unit of time.

## Latency
Latency is defined as the time required to complete a task or produce a result. Latency is also referred to as response time. The time it takes for a web browser to download Instagram images from the internet is the latency for downloading the images.

## Throughput vs Latency
The two terms are more frequently used when describing networking links and have more precise meanings in that domain. In the context of concurrency, throughput can be thought of as time taken to execute a program or computation. For instance, imagine a program that is given hundreds of files containing integers and asked to sum up all the numbers. Since addition is commutative each file can be worked on in parallel. In a single-threaded environment, each file will be sequentially processed but in a concurrent system, several threads can work in parallel on distinct files. Of course, there will be some overhead to manage the state including already processed files. However, such a program will complete the task much faster than a single thread. The performance difference will become more and more apparent as the number of input files increases. The throughput in this example can be defined as the number of files processed by the program in a minute. And latency can be defined as the total time taken to completely process all the files. As you observe in a multithreaded implementation throughput will go up and latency will go down. More work gets done in less amount of time. In general, the two have an inverse relationship.

## Critical Sections & Race Conditions

A program is a set of instructions being executed, and multiple threads of a program can be executing different sections of the program code. However, caution should be exercised when threads of the same program attempt to execute the same portion of code as explained in the following paragraphs.

## Critical Section
Critical section is any piece of code that has the possibility of being executed concurrently by more than one thread of the application and exposes any shared data or resources used by the application for access.

## Race Condition
Race conditions happen when threads run through critical sections without thread synchronization. The threads "race" through the critical section to write or read shared resources and depending on the order in which threads finish the "race", the program output changes. In a race condition, threads access shared resources or program variables that might be worked on by other threads at the same time causing the application data to be inconsistent.

As an example consider a thread that tests for a state/condition, called a predicate, and then based on the condition takes subsequent action. This sequence is called test-then-act. The pitfall here is that the state can be mutated by the second thread just after the test by the first thread and before the first thread takes action based on the test. A different thread changes the predicate in between the test and act. In this case, action by the first thread is not justified since the predicate doesn't hold when the action is executed.

Consider the snippet below. We have two threads working on the same variable randInt. The modifier thread perpetually updates the value of randInt in a loop while the printer thread prints the value of randInt only if randInt is divisible by 5. If you let this program run, you'll notice some values get printed even though they aren't divisible by 5 demonstrating a thread unsafe version of test-then-act.

## Example Thread Race
The below program spawns two threads. One thread prints the value of a shared variable whenever the shared variable is divisible by 5. A race condition happens when the printer thread executes a test-then-act if clause, which checks if the shared variable is divisible by 5 but before the thread can print the variable out, its value is changed by the modifier thread. Some of the printed values aren't divisible by 5 which verifies the existence of a race condition in the code.


{% highlight java %}
class Demonstration {

    public static void main(String args[]) throws InterruptedException {
          RaceCondition.runTest();
    }
}

class RaceCondition {

    int randInt;
    Random random = new Random(System.currentTimeMillis());

    void printer() {

        int i = 1000000;
        while (i != 0) {
            if (randInt % 5 == 0) {
                if (randInt % 5 != 0)
                  System.out.println(randInt);
            }
            i--;
        }
    }

    void modifier() {

        int i = 1000000;
        while (i != 0) {
            randInt = random.nextInt(1000);
            i--;
        }
    }

    public static void runTest() throws InterruptedException {


        final RaceCondition rc = new RaceCondition();
        Thread thread1 = new Thread(new Runnable() {

            @Override
            public void run() {
                rc.printer();
            }
        });
        Thread thread2 = new Thread(new Runnable() {

            @Override
            public void run() {
                rc.modifier();
            }
        });

        
        thread1.start();
        thread2.start();

        thread1.join();
        thread2.join();
    }
}
{% endhighlight %}

Even though the if condition on line 19 makes a check for a value which is divisible by 5 and only then prints randInt. It is just after the if check and before the print statement i.e. in-between lines 19 and 21, that the value of randInt is modified by the modifier thread! This is what constitutes a race condition.

For the impatient, the fix is presented below where we guard the read and write of the randInt variable using the RaceCondition object as the monitor. Don't fret if the solution doesn't make sense for now, it would, once we cover various topics in the lessons ahead.


{% highlight java %}
class Demonstration {

    public static void main(String args[]) throws InterruptedException {
          RaceCondition.runTest();
    }
}

class RaceCondition {

    int randInt;
    Random random = new Random(System.currentTimeMillis());

    void printer() {

        int i = 1000000;
        while (i != 0) {
            synchronized(this) {
              if (randInt % 5 == 0) {
                  if (randInt % 5 != 0)
                    System.out.println(randInt);
              }
            }
            i--;
        }
    }

    void modifier() {

        int i = 1000000;
        while (i != 0) {
            synchronized(this) {
              randInt = random.nextInt(1000);
              i--;
            }
        }
    }

    public static void runTest() throws InterruptedException {


        final RaceCondition rc = new RaceCondition();
        Thread thread1 = new Thread(new Runnable() {

            @Override
            public void run() {
                rc.printer();
            }
        });
        Thread thread2 = new Thread(new Runnable() {

            @Override
            public void run() {
                rc.modifier();
            }
        });

        
        thread1.start();
        thread2.start();

        thread1.join();
        thread2.join();
    }
}
{% endhighlight %}

Below is a pictorial representation of what a race condition, in general, looks like.

![jmm](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/jmm/jmm4.png)

## Deadlocks, Liveness & Reentrant Locks

Logical follies committed in multithreaded code, while trying to avoid race conditions and guarding critical sections, can lead to a host of subtle and hard to find bugs and side-effects. Some of these incorrect usage patterns have their names and are discussed below.

## DeadLock
Deadlocks occur when two or more threads aren't able to make any progress because the resource required by the first thread is held by the second and the resource required by the second thread is held by the first.

## Liveness
Ability of a program or an application to execute in a timely manner is called liveness. If a program experiences a deadlock then it's not exhibiting liveness.

## Live-Lock
A live-lock occurs when two threads continuously react in response to the actions by the other thread without making any real progress. The best analogy is to think of two persons trying to cross each other in a hallway. John moves to the left to let Arun pass, and Arun moves to his right to let John pass. Both block each other now. John sees he's blocking Arun again and moves to his right and Arun moves to his left seeing he's blocking John. They never cross each other and keep blocking each other. This scenario is an example of a livelock. A process seems to be running and not deadlocked but in reality, isn't making any progress.

## Starvation
Other than a deadlock, an application thread can also experience starvation, when it never gets CPU time or access to shared resources. Other greedy threads continuously hog shared system resources not letting the starving thread make any progress.

## Deadlock Example

![jmm](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/jmm/jmm5.png)

The above code can potentially result in a deadlock. Note that deadlock may not always happen, but for certain execution sequences, deadlock can occur. Consider the below execution sequence that ends up in a deadlock:

![jmm](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/jmm/jmm6.png)

Thread T2 can't make progress as it requires MUTEX_A which is being held by T1. Now when T1 wakes up, it can't make progress as it requires MUTEX_B and that is being held up by T2. This is a classic text-book example of a deadlock.

You can come back to the examples presented below as they require an understanding of the synchronized keyword that we cover in later sections. Or you can just run the examples and observe the output for now to get a high-level overview of the concepts we discussed in this lesson.

If you run the code snippet below, you'll see that the statements for acquiring locks: lock1 and lock2 print out but there's no progress after that and the execution times out. In this scenario, the deadlock occurs because the locks are being acquired in a nested fashion.

{% highlight java %}
class Demonstration {

    public static void main(String args[]) {
        Deadlock deadlock = new Deadlock();
        try {
            deadlock.runTest();
        } catch (InterruptedException ie) {
        }
    }
}

class Deadlock {

    private int counter = 0;
    private Object lock1 = new Object();
    private Object lock2 = new Object();

    Runnable incrementer = new Runnable() {

        @Override
        public void run() {
            try {
                for (int i = 0; i < 100; i++) {
                    incrementCounter();
                    System.out.println("Incrementing " + i);
                }
            } catch (InterruptedException ie) {
            }
        }
    };

    Runnable decrementer = new Runnable() {

        @Override
        public void run() {
            try {
                for (int i = 0; i < 100; i++) {
                    decrementCounter();
                    System.out.println("Decrementing " + i);
                }
            } catch (InterruptedException ie) {
            }

        }
    };

    public void runTest() throws InterruptedException {

        Thread thread1 = new Thread(incrementer);
        Thread thread2 = new Thread(decrementer);

        thread1.start();
        // sleep to make sure thread 1 gets a chance to acquire lock1
        Thread.sleep(100);
        thread2.start();

        thread1.join();
        thread2.join();

        System.out.println("Done : " + counter);
    }

    void incrementCounter() throws InterruptedException {
        synchronized (lock1) {
            System.out.println("Acquired lock1");
            Thread.sleep(100);

            synchronized (lock2) {
                counter++;
            }
        }
    }

    void decrementCounter() throws InterruptedException {
        synchronized (lock2) {
            System.out.println("Acquired lock2");
            
            Thread.sleep(100);
            synchronized (lock1) {
                counter--;
            }
        }
    }
}
{% endhighlight %}

## Reentrant Lock
Re-entrant locks allow for re-locking or re-entering of a synchronization lock. This can be best explained with an example. Consider the NonReentrant class below.

Take a minute to read the code and assure yourself that any object of this class if locked twice in succession would result in a deadlock. The same thread gets blocked on itself, and the program is unable to make any further progress. If you click run, the execution would time-out.

If a synchronization primitive doesn't allow reacquisition of itself by a thread that has already acquired it, then such a thread would block as soon as it attempts to reacquire the primitive a second time.

{% highlight java %}
class Demonstration {

    public static void main(String args[]) throws Exception {
        NonReentrantLock nreLock = new NonReentrantLock();

        // First locking would be successful
        nreLock.lock();
        System.out.println("Acquired first lock");
      
        // Second locking results in a self deadlock 
        System.out.println("Trying to acquire second lock");      
        nreLock.lock();
        System.out.println("Acquired second lock");
    }
}

class NonReentrantLock {

    boolean isLocked;

    public NonReentrantLock() {
        isLocked = false;
    }

    public synchronized void lock() throws InterruptedException {

        while (isLocked) {
            wait();
        }
        isLocked = true;
    }

    public synchronized void unlock() {
        isLocked = false;
        notify();
    }
}
{% endhighlight %}

## Mutex vs Semaphore

Having laid the foundation of concurrent programming concepts and their associated issues, we'll now discuss the all-important mechanisms of locking and signaling in multi-threaded applications and the differences amongst these constructs.

## Mutex
Mutex as the name hints implies mutual exclusion. A mutex is used to guard shared data such as a linked-list, an array or any primitive type. A mutex allows only a single thread to access a resource or critical section.

Once a thread acquires a mutex, all other threads attempting to acquire the same mutex are blocked until the first thread releases the mutex. Once released, most implementations arbitrarily chose one of the waiting threads to acquire the mutex and make progress.

## Semaphore
Semaphore, on the other hand, is used for limiting access to a collection of resources. Think of semaphore as having a limited number of permits to give out. If a semaphore has given out all the permits it has, then any new thread that comes along requesting for a permit will be blocked, till an earlier thread with a permit returns it to the semaphore. A typical example would be a pool of database connections that can be handed out to requesting threads. Say there are ten available connections but 50 requesting threads. In such a scenario, a semaphore can only give out ten permits or connections at any given point in time.

A semaphore with a single permit is called a binary semaphore and is often thought of as an equivalent of a mutex, which isn't completely correct as we'll shortly explain. Semaphores can also be used for signaling among threads. This is an important distinction as it allows threads to cooperatively work towards completing a task. A mutex, on the other hand, is strictly limited to serializing access to shared state among competing threads.

## Mutex Example
The following illustration shows how two threads acquire and release a mutex one after the other to gain access to shared data. Mutex guarantees the shared state isn't corrupted when competing threads work on it.

![jmm](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/jmm/jmm7.png)

## When a Semaphore Masquerades as a Mutex?
A semaphore can potentially act as a mutex if the permits it can give out is set to 1. However, the most important difference between the two is that in case of a mutex the same thread must call acquire and subsequent release on the mutex whereas in case of a binary sempahore, different threads can call acquire and release on the semaphore. The pthreads library documentation states this in the pthread_mutex_unlock() method's description.

If a thread attempts to unlock a mutex that it has not locked or a mutex which is unlocked, undefined behavior results.
This leads us to the concept of ownership. A mutex is owned by the thread acquiring it till the point the owning-thread releases it, whereas for a semaphore there's no notion of ownership.

## Semaphore for Signaling
Another distinction between a semaphore and a mutex is that semaphores can be used for signaling amongst threads, for example in case of the classical producer/consumer problem the producer thread can signal the consumer thread by incrementing the semaphore count to indicate to the consumer thread to consume the freshly produced item. A mutex in contrast only guards access to shared data among competing threads by forcing threads to serialize their access to critical sections and shared data-structures.

Below is a pictorial representation of how a mutex works.

![jmm](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/jmm/jmm8.png)

Below is a depiction of how a semaphore works. The semaphore initially has two permits and allows at most two threads to enter the critical section or access protected resources

![jmm](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/jmm/jmm9.png)

## Summary

* Mutex implies mutual exclusion and is used to serialize access to critical sections whereas semaphore can potentially be used as a mutex but it can also be used for cooperation and signaling amongst threads. Semaphore also solves the issue of missed signals.
* Mutex is owned by a thread, whereas a semaphore has no concept of ownership.
* Mutex if locked, must necessarily be unlocked by the same thread. A semaphore can be acted upon by different threads. This is true even if the semaphore has a permit of one
* Think of semaphore analogous to a car rental service such as Hertz. Each outlet has a certain number of cars, it can rent out to customers. It can rent several cars to several customers at the same time but if all the cars are rented out then any new customers need to be put on a waitlist till one of the rented cars is returned. In contrast, think of a mutex like a lone runway on a remote airport. Only a single jet can land or take-off from the runway at a given point in time. No other jet can use the runway simultaneously with the first aircraft.

## Mutex vs Monitor

Continuing our discussion from the previous section on locking and signaling mechanisms, we'll now pore over an advanced concept the monitor. It is exposed as a concurrency construct by some programming language frameworks including Java.

## When Mutual Exclusion isn’t Enough
Concisely, a monitor is a mutex and then some. Monitors are generally language level constructs whereas mutex and semaphore are lower-level or OS provided constructs.

To understand monitors, let's first see the problem they solve. Usually, in multi-threaded applications, a thread needs to wait for some program predicate to be true before it can proceed forward. Think about a producer/consumer application. If the producer hasn't produced anything the consumer can't consume anything, so the consumer must wait on a predicate that lets the consumer know that something has indeed been produced. What could be a crude way of accomplishing this? The consumer could repeatedly check in a loop for the predicate to be set to true. The pattern would resemble the pseudocode below:

![jmm](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/jmm/jmm10.png)

Within the while loop we'll first release the mutex giving other threads a chance to acquire it and set the loop predicate to true. And before we check the loop predicate again, we make sure we have acquired the mutex again. This works but is an example of "spin waiting" which wastes a lot of CPU cycles. Next, let's see how condition variables solve the spin-waiting issue.

## Condition Variables
Mutex provides mutual exclusion, however, at times mutual exclusion is not enough. We want to test for a predicate with a mutually exclusive lock so that no other thread can change the predicate when we test for it but if we find the predicate to be false, we'd want to wait on a condition variable till the predicate's value is changed. This thus is the solution to spin waiting.

Conceptually, each condition variable exposes two methods wait() and signal(). The wait() method when called on the condition variable will cause the associated mutex to be atomically released, and the calling thread would be placed in a wait queue. There could already be other threads in the wait queue that previously invoked wait() on the condition variable. Since the mutex is now released, it gives other threads a chance to change the predicate that will eventually let the thread that was just placed in the wait queue to make progress. As an example, say we have a consumer thread that checks for the size of the buffer, finds it empty and invokes wait() on a condition variable. The predicate in this example would be the size of the buffer.

Now imagine a producer places an item in the buffer. The predicate, the size of the buffer, just changed and the producer wants to let the consumer threads know that there is an item to be consumed. This producer thread would then invoke signal() on the condition variable. The signal() method when called on a condition variable causes one of the threads that has been placed in the wait queue to get ready for execution. Note we didn't say the woken up thread starts executing, it just gets ready - and that could mean being placed in the ready queue. It is only after the producer thread which calls the signal() method has released the associated mutex that the thread in the ready queue starts executing. The thread in the ready queue must wait to acquire the mutex associated with the condition variable before it can start executing.

Lets see how this all translates into code.

![jmm](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/jmm/jmm11.png)

Let's dry run the above code. Say thread A executes efficientWaitingFunction() first and finds the loop predicate is false and enters the loop. Next thread A executes the statement condVar.wait() and is be placed in a wait queue. At the same time thread A gives up the mutex. Now thread B comes along and executes changePredicate() method. Since the mutex was given up by thread A, thread B is be able to acquire it and set the predicate to true. Next it signals the condition variable condVar.signal(). This step places thread A into the ready queue but thread A doesn't start executing until thread B has released the mutex.

Note that the order of signaling the condition variable and releasing the mutex can be interchanged, but generally, the preference is to signal first and then release the mutex. However, the ordering might have ramifications on thread scheduling depending on the threading implementation.

## Why the while Loop
The wary reader would have noticed us using a while loop to test for the predicate. After all, the pseudocode could have been written as follows

![jmm](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/jmm/jmm12.png)

If the snippet is re-written in the above manner using an if clause instead of a while then,, we need a guarantee that once the variable condVar is signaled, the predicate can't be changed by any other thread and that the signaled thread becomes the owner of the monitor. This may not be true. For one, a different thread could get scheduled and change the predicate back to false before the signaled thread gets a chance to execute, therefore the signaled thread must check the predicate again, once it acquires the monitor. Secondly, use of the loop is necessitated by design choices of monitors that we'll explore in the next section. Last but not the least, on POSIX systems, spurious or fake wakeups are possible (also discussed in later chapters) even though the condition variable has not been signaled and the predicate hasn't changed. The idiomatic and correct usage of a monitor dictates that the predicate always be tested for in a while loop.

## Monitor Explained
After the above discussion, we can now realize that a monitor is made up of a mutex and one or more condition variables. A single monitor can have multiple condition variables but not vice versa. Theoretically, another way to think about a monitor is to consider it as an entity having two queues or sets where threads can be placed. One is the entry set and the other is the wait set. When a thread A enters a monitor it is placed into the entry set. If no other thread owns the monitor, which is equivalent of saying no thread is actively executing within the monitor section, then thread A will acquire the monitor and is said to own it too. Thread A will continue to execute within the monitor section till it exits the monitor or calls wait() on an associated condition variable and be placed into the wait set. While thread A owns the monitor no other thread will be able to execute any of the critical sections protected by the monitor. New threads requesting ownership of the monitor get placed into the entry set.

Continuing with our hypothetical example, say another thread B comes along and gets placed in the entry set, while thread A sits in the wait set. Since no other thread owns the monitor, thread B successfully acquires the monitor and continues execution. If thread B exits the monitor section without calling notify() on the condition variable, then thread A will remain waiting in the wait set. Thread B can also invoke wait() and be placed in the wait set along with thread A. This then would require a third thread to come along and call notify() on the condition variable on which both threads A and B are waiting. Note that only a single thread will be able to own the monitor at any given point in time and will have exclusive access to data structures or critical sections protected by the monitor.

Practically, in Java each object is a monitor and implicitly has a lock and is a condition variable too. You can think of a monitor as a mutex with a wait set. Monitors allow threads to exercise mutual exclusion as well as cooperation by allowing them to wait and signal on conditions.
![jmm](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/jmm/jmm13.png)
![jmm](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/jmm/jmm14.png)
![jmm](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/jmm/jmm15.png)

## Java's Monitor & Hoare vs Mesa Monitors

We discussed the abstract concept of a monitor in the previous section and now let's see the working of a concrete implementation of it in Java.

## Java’s Monitor
In Java every object is a condition variable and has an associated lock that is hidden from the developer. Each java object exposes wait() and notify() methods.

Before we execute wait() on a java object we need to lock its hidden mutex. That is done implicitly through the synchronized keyword. If you attempt to call wait() or notify() outside of a synchronized block, an IllegalMonitorStateException would occur. It's Java reminding the developer that the mutex wasn't acquired before wait on the condition variable was invoked. wait() and notify() can only be called on an object once the calling thread becomes the owner of the monitor. The ownership of the monitor can be achieved in the following ways:
* the method the thread is executing has synchronized in its signature
* the thread is executing a block that is synchronized on the object on which wait or notify will be called
* in case of a class, the thread is executing a static method which is synchronized.

## Bad Synchronization Example 1
In the below snippet, wait() is being called outside of a synchronized block, i.e. without implicitly locking the associated mutex. Running the code results in IllegalMonitorStateException
{% highlight java %}
class BadSynchronization {

    public static void main(String args[]) throws InterruptedException {
        Object dummyObject = new Object();

        // Attempting to call wait() on the object
        // outside of a synchronized block.
        dummyObject.wait();
    }
}
{% endhighlight %}

## Bad Synchronization Example 2
Here's another example where we try to call notify() on an object in a synchronized block which is synchronized on a different object. Running the code will again result in an IllegalMonitorStateException
{% highlight java %}
class BadSynchronization {

    public static void main(String args[]) {
        Object dummyObject = new Object();
        Object lock = new Object();

        synchronized (lock) {
            lock.notify();

            // Attempting to call notify() on the object
            // in synchronized block of another object
            dummyObject.notify();
        }
    }
}
{% endhighlight %}
## Hoare vs Mesa Monitors
So far we have determined that the idiomatic usage of a monitor requires using a while loop as follows. Let's see how the design of monitors affects this recommendation.


while( condition == false ) {
    condVar.wait();
}
Once the asleep thread is signaled and wakes up, you may ask why does it need to check for the condition being false again, the signaling thread must have just set the condition to true?

In Mesa monitors - Mesa being a language developed by Xerox researchers in the 1970s - it is possible that the time gap between thread B calls notify() and releases its mutex and the instant at which the asleep thread A, wakes up and reacquires the mutex, the predicate is changed back to false by another thread different than the signaler and the awoken threads! The woken up thread competes with other threads to acquire the mutex once the signaling thread B empties the monitor. On signaling, thread B doesn't give up the monitor just yet; rather it continues to own the monitor until it exits the monitor section.

In contrast, Hoare monitors - Hoare being one of the original inventor of monitors - the signaling thread B yields the monitor to the woken up thread A and thread A enters the monitor, while thread B sits out. This guarantees that the predicate will not have changed and instead of checking for the predicate in a while loop an if-clause would suffice. The woken-up/released thread A immediately starts execution when the signaling thread B signals that the predicate has changed. No other thread gets a chance to change the predicate since no other thread gets to enter the monitor.

Java, in particular, subscribes to Mesa monitor semantics and the developer is always expected to check for condition/predicate in a while loop. Mesa monitors are more efficient than Hoare monitors.

## Semaphore vs Monitor

Monitor, mutex, and semaphores can be confusing concepts initially. A monitor is made up of a mutex and a condition variable. One can think of a mutex as a subset of a monitor. Differences between a monitor and semaphore are discussed below.

## Difference between Semaphore and Monitor
A monitor and a semaphore are interchangeable and theoretically, one can be constructed out of the other or one can be reduced to the other. However, monitors take care of atomically acquiring the necessary locks whereas, with semaphores, the onus of appropriately acquiring and releasing locks is on the developer, which can be error-prone.

Semaphores are lightweight when compared to monitors, which are bloated. However, the tendency to misuse semaphores is far greater than monitors. When using a semaphore and mutex pair as an alternative to a monitor, it is easy to lock the wrong mutex or just forget to lock altogether. Even though both constructs can be used to solve the same problem, monitors provide a pre-packaged solution with less dependency on a developer's skill to get the locking right.

Java monitors enforce correct locking by throwing the IllegalMonitorState exception object when methods on a condition variable are invoked without first acquiring the associated lock. The exception is in a way saying that either the object's lock/mutex was not acquired at all or that an incorrect lock was acquired.

A semaphore can allow several threads access to a given resource or critical section, however, only a single thread at any point in time can own the monitor and access associated resource.

Semaphores can be used to address the issue of missed signals, however with monitors additional state, called the predicate, needs to be maintained apart from the condition variable and the mutex which make up the monitor, to solve the issue of missed signals.

## Amdahl's Law

## Definition
No text on concurrency is complete without mentioning the Amdahl's Law. The law specifies the cap on the maximum speedup that can be achieved when parallelizing the execution of a program.

If you have a poultry farm where a hundred hens lay eggs each day, then no matter how many people you hire to process the laid eggs, you still need to wait an entire day for the 100 eggs to be laid. Increasing the number of workers on the farm can't shorten the time it takes for a hen to lay an egg. Similarly, software programs consist of parts which can't be sped up even if the number of processors is increased. These parts of the program must execute serially and aren't amenable to parallelism.

Amdahl's law describes the theoretical speedup a program can achieve at best by using additional computing resources. We'll skip the mathematical derivation and go straight to the simplified equation expressing Amdahl's law:

![jmm](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/jmm/jmm16.png)

he speed-up steadily increases as we increase the number of processors or threads. However, as you can see the theoretical maximum speed-up for our program with 10% serial execution will be 10. We can't speed-up our program execution more than 10 times compared to when we run the same program on a single CPU or thread. To achieve greater speed-ups than 10 we must optimize or parallelize the serially executed portion of the code.

Another important aspect to realize is that when we speed-up our program execution by roughly 5 times, we do so by employing 10 processors. The utilization of these 10 processors, in turn, decreases by roughly 50% because now the 10 processors remain idle for the rest of the time that a single processor would have been busy. Utilization is defined as the speedup divided by the number of processors.

As an example say the program runs in 10 minutes using a single core. We assumed the parallelizable portion of the program is 90%, which implies 1 minute of the program time must execute serially. The speedup we can achieve with 10 processors is roughly 5 times which comes out to be 2 minutes of total program execution time. Out of those 2 minutes, 1 minute is of mandatory serial execution and the rest can all be parallelized. This implies that 9 of the processors will complete 90% of the non-serial work in 1 minute while 1 processor remains idle and then one out of the 10 processors, will execute the serial portion for another minute. The rest of the 9 processors are idle for that 1 minute during which the serial execution takes place. In effect, the combined utilization of the ten processors drops by 50%.

As N approaches infinity, the Amdahl's law takes the following form:
S(n)=\frac{1}{(1-P)+\frac{P}{n} }

One should take the calculations using Amdahl's law with a grain of salt. If the formula spits out a speed-up of 5x it doesn't imply that in reality one would observe a similar speed-up. There are other factors such as the memory architecture, cache misses, network and disk I/O etc that can affect the execution time of a program and the actual speed-up might be less than the calculated one.

The Amdahl's law works on a problem of fixed size. However as computing resources are improved, algorithms run on larger and even larger datasets. As the dataset size grows, the parallelizable portion of the program grows faster than the serial portion and a more realistic assessment of performance is given by Gustafson's law, which we won't discuss here as it is beyond the scope of this text.

## Moore’s Law#

In this lesson, we'll cover a high-level overview of Moore's law to present a final motivation to the reader for writing multi-threaded applications and realize that concurrency is inevitable in the future of software.

Gordon Moore, co-founder of Intel, observed the number of transistors that can be packed into a given unit of space doubles about every two years and in turn the processing power of computers doubles and the cost halves. Moore's law is more of an observation than a law grounded in formal scientific research. It states that the number of transistors per square inch on a chip will double every two years. This exponential growth has been going on since the 70’s and is only now starting to slow down. The following graph shows the growth of the transistor count.

![jmm](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/jmm/jmm17.png)

Initially, the clock speeds of processors also doubled along with the transistor count. This is because as transistors get smaller, their frequency increases and propagation delays decrease because now the transistors are packed closer together. However, the promise of exponential growth by Moore’s law came to an end more than a decade ago with respect to clock speeds. The increase in clock speeds of processors has slowed down much faster than the increase in number of transistors that can be placed on a microchip. If we plot clock speeds we find that the linear exponential growth stopped after 2003 and the trend line flattened out. The clock speed (proportional to difference between supply voltage and threshold voltage) cannot increase because the supply voltage is already down to an extent where it cannot be decreased to get dramatic gains in clock speed. In 10 years from 2000 to 2009, clock speed just increased from 1.3 GHz to 2.8 GHz merely doubling in a decade rather than increasing 32 times as expected by Moore's law. The following plot shows the clock speeds flattening out towards 2010.

![jmm](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/jmm/jmm18.png)

Since processors aren't getting faster as quickly as they use to, we need alternative measures to achieve performance gains. One of the ways to do that is to use multicore processors. Introduced in the early 2000s, multicore processors have more than one CPU on the same machine. To exploit this processing power, programs must be written as multi-threaded applications. A single-threaded application running on an octa-core processor will only use 1/8th of the total throughput of that machine, which is unacceptable in most scenarios.

Another analogy is to think of a bullock cart being pulled by an ox. We can breed the ox to be stronger and more powerful to pull more load but eventually there's a limit to how strong the ox can get. To pull more load, an easier solution is to attach several oxen to the bullock cart. The computing industry is also going in the direction of this analogy.
