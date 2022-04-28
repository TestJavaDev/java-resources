---
layout: default
title: Multithreading in Java
parent: Multithreading
has_children: true
nav_order: 2
permalink: /multithreading/in_java
---
<div align="center" markdown="1">
Multithreading in Java / Java resources / Tutorial

{: .fs-8 .fw-400 }
</div>

## Multithreading in Java

## Atomic Assignments

## Overview
Multithreading revolves around the ability to execute actions atomically, that is without interference from other threads. We use various language provided constructs to ensure that critical sections of code are executed atomically. However, this also begs the questions, what operations are performed atomically by the language. For instance we already know that incrementing an integer counter as follows is never thread-safe:

counter++;

The above expression breaks down into several lower-level instructions that may or may not be performed atomically and therefore we can’t guarantee that the execution of this expression is thread-safe. However, what about simple operations such as an assignment? Consider the following:

void someMethod(int passedInt) {
   counter = passedInt; // counter is an instance variable
}

If several threads were to invoke someMethod and each passing a different value for the integer can we assume the assignment will be thread-safe? To make the example concrete, say we have two threads one invoking someMethod(5) and the other invoking ``someMethod(7). There are three outcomes for the counter`

counter is assigned 5 counter is assigned 7 counter has an arbitrary value because some bits are written by the first thread and some by the second thread.

In our example the variable counter is of primitive type int which is 32 bits in Java. The astute reader would question what guarantees an assignment operation as atomic?

## Java specification

The question if assignment is atomic or not is a valid one and the confusion is addressed by the Java specification itself, which states:
* Assignments and reads for primitive data types except for double and long are always atomic. If two threads are invoking someMethod() and passing in 5 and 7 for the integer counter variable then the variable will hold either 5 or 7 and not any other value. There will be no partial writes of bits from either thread.
* The reads and writes to double and long primitive types aren’t atomic. The JVM specification allows implementations to break-up the write of the 64 bit double or long primitive type into two writes, one for each 32 bit half. This can result in a situation where two threads are simultaneously writing a double or long value and a third thread observes the first 32 bits from the write by the first thread and the next 32 bits from the write by the second thread. As a result the third thread reads a value that has neither been written by either of the two threads or is a garbage value. In order to make reads and writes to double or long primitive types atomic, we must mark them as volatile. The specification guarantees writes and reads to volatile double and long primitive types as atomic. Note that some JVM implementations may make the writes and reads to double and long types as atomic but this isn’t universally guaranteed across all the JVM implementations. We’ll cover volatile in a later lesson, for now, just remember that primitive double and long types must be marked as volatile for atomic assignments.
* All reference assignments are atomic. By reference we mean a variable holding a memory location address, where an object has been allocated by the JVM. For instance, consider the snippet Thread currentThread = Thread.currentThread(); The variable currentThread holds the address for the current thread’s object. If several threads execute the above snippet, the variable currentThread will hold one valid memory location address and not a garbage value. It can’t happen that the variable currentThread holds some bytes from the assignment operation of one thread and other bytes from the assignment operation of an another thread. Whatever reference the variable holds will reflect an assignment from one of the threads. Reference reads and writes are always atomic whether the reference (memory address) itself consists of 32 or 64 bits.

Bear in mind that atomic assignments promised by the Java platform don’t imply thread-safety! Our example method someMethod() is not thread-safe. Consider more complex situations such as reading and then assigning a variable in a method (e.g. initializing a singleton), such scenarios need to be made thread-safe using locks or synchronized.

## Thready Safety & Synchronized

With the abstract concepts discussed, we'll now turn to the concurrency constructs offered by Java and use them in later sections to solve practical coding problems.

## Thread Safe
A class and its public APIs are labelled as thread safe if multiple threads can consume the exposed APIs without causing race conditions or state corruption for the class. Note that composition of two or more thread-safe classes doesn't guarantee the resulting type to be thread-safe.

## Synchronized
Java’s most fundamental construct for thread synchronization is the synchronized keyword. It can be used to restrict access to critical sections one thread at a time.

Each object in Java has an entity associated with it called the "monitor lock" or just monitor. Think of it as an exclusive lock. Once a thread gets hold of the monitor of an object, it has exclusive access to all the methods marked as synchronized. No other thread will be allowed to invoke a method on the object that is marked as synchronized and will block, till the first thread releases the monitor which is equivalent of the first thread exiting the synchronized method.

Note carefully:
1. For static methods, the monitor will be the class object, which is distinct from the monitor of each instance of the same class.
2. If an uncaught exception occurs in a synchronized method, the monitor is still released.
3. Furthermore, synchronized blocks can be re-entered.

You may think of "synchronized" as the mutex portion of a monitor.

![jmm](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/jmm/jmm19.png)

As an example look at the employee class above. All the three methods are synchronized on the "this" object. If we created an object and three different threads attempted to execute each method of the object, only one will get access, and the other two will block. If we synchronized on a different object other than the this object, which is only possible for the getName method given the way we have written the code, then the 'critical sections' of the program become protected by two different locks. In that scenario, since setName and resetName would have been synchronized on the this object only one of the two methods could be executed concurrently. However getName would be synchronized independently of the other two methods and can be executed alongside one of them. The change would look like as follows:

![jmm](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/jmm/jmm20.png)

All the sections of code that you guard with synchronized blocks on the same object can have at most one thread executing inside of them at any given point in time. These sections of code may belong to different methods, classes or be spread across the code base.

Note with the use of the synchronized keyword, Java forces you to implicitly acquire and release the monitor-lock for the object within the same method! One can't explicitly acquire and release the monitor in different methods. This has an important ramification, the same thread will acquire and release the monitor! In contrast, if we used semaphore, we could acquire/release them in different methods or by different threads.

A classic newbie mistake is to synchronize on an object and then somewhere in the code reassign the object. As an example, look at the code below. We synchronize on a Boolean object in the first thread but sleep before we call wait() on the object. While the first thread is asleep, the second thread goes on to change the flag's value. When the first thread wakes up and attempts to invoke wait(), it is met with a IllegalMonitorState exception! The object the first thread synchronized on before going to sleep has been changed, and now it is attempting to call wait() on an entirely different object without having synchronized on it.

{% highlight java %}
class Demonstration {
    public static void main( String args[] ) throws InterruptedException {
        IncorrectSynchronization.runExample();
    }
}

class IncorrectSynchronization {

    Boolean flag = new Boolean(true);

    public void example() throws InterruptedException {

        Thread t1 = new Thread(new Runnable() {

            public void run() {
                synchronized (flag) {
                    try {
                        while (flag) {
                            System.out.println("First thread about to sleep");
                            Thread.sleep(5000);
                            System.out.println("Woke up and about to invoke wait()");
                            flag.wait();
                        }
                    } catch (InterruptedException ie) {

                    }
                }
            }
        });

        Thread t2 = new Thread(new Runnable() {

            public void run() {
                flag = false;
                System.out.println("Boolean assignment done.");
            }
        });

        t1.start();
        Thread.sleep(1000);
        t2.start();
        t1.join();
        t2.join();
    }

    public static void runExample() throws InterruptedException {
        IncorrectSynchronization incorrectSynchronization = new IncorrectSynchronization();
        incorrectSynchronization.example();
    }
}
{% endhighlight %}

Marking all the methods of a class synchronized in order to make it thread-safe may reduce throughput. As a naive example, consider a class with two completely independent properties accessed by getter methods. Both the getters synchronize on the same object, and while one is being invoked, the other would be blocked because of synchronization on the same object. The solution is to lock at a finer granularity, possibly use two different locks for each property so that both can be accessed in parallel.

## Wait & Notify

## wait()
The wait method is exposed on each java object. Each Java object can act as a condition variable. When a thread executes the wait method, it releases the monitor for the object and is placed in the wait queue. Note that the thread must be inside a synchronized block of code that synchronizes on the same object as the one on which wait() is being called, or in other words, the thread must hold the monitor of the object on which it'll call wait. If not so, an illegalMonitor exception is raised!

## notify()
Like the wait method, notify() can only be called by the thread which owns the monitor for the object on which notify() is being called else an illegal monitor exception is thrown. The notify method, will awaken one of the threads in the associated wait queue, i.e., waiting on the thread's monitor.

However, this thread will not be scheduled for execution immediately and will compete with other active threads that are trying to synchronize on the same object. The thread which executed notify will also need to give up the object's monitor, before any one of the competing threads can acquire the monitor and proceed forward.

##notifyAll()
This method is the same as the notify() one except that it wakes up all the threads that are waiting on the object's monitor.

## Interrupting Threads

## Interrupted Exception
You'll often come across this exception being thrown from functions. When a thread wait()-s or sleep()-s then one way for it to give up waiting/sleeping is to be interrupted. If a thread is interrupted while waiting/sleeping, it'll wake up and immediately throw Interrupted exception.

The thread class exposes the interrupt() method which can be used to interrupt a thread that is blocked in a sleep() or wait() call. Note that invoking the interrupt method only sets a flag that is polled periodically by sleep or wait to know the current thread has been interrupted and an interrupted exception should be thrown.

Below is an example, where a thread is initially made to sleep for an hour but then interrupted by the main thread.

{% highlight java %}
class Demonstration {

    public static void main(String args[]) throws InterruptedException {
        InterruptExample.example();
    }
}

class InterruptExample {

    static public void example() throws InterruptedException {

        final Thread sleepyThread = new Thread(new Runnable() {

            public void run() {
                try {
                    System.out.println("I am too sleepy... Let me sleep for an hour.");
                    Thread.sleep(1000 * 60 * 60);
                } catch (InterruptedException ie) {
                    System.out.println("The interrupt flag is cleard : " + Thread.interrupted() + " " + Thread.currentThread().isInterrupted());                  
                    Thread.currentThread().interrupt();
                    System.out.println("Oh someone woke me up ! ");
                    System.out.println("The interrupt flag is set now : " + Thread.currentThread().isInterrupted() + " " + Thread.interrupted());                                    
                  
                }
            }
        });

        sleepyThread.start();

        System.out.println("About to wake up the sleepy thread ...");
        sleepyThread.interrupt();
        System.out.println("Woke up sleepy thread ...");

        sleepyThread.join();
    }
}

{% endhighlight %}

Take a minute to go through the output of the above program. Observe the following:
* Once the interrupted exception is thrown, the interrupt status/flag is cleared as the output of line-19 shows.
* On line-20 we again interrupt the thread and no exception is thrown. This is to emphasize that merely calling the interrupt method isn't responsible for throwing the interrupted exception. Rather the implementation should periodically check for the interrupt status and take appropriate action.
* On line 22 we print the interrupt status for the thread, which is set to true because of line 20.
* Note that there are two methods to check for the interrupt status of a thread. One is the static method Thread.interrupted() and the other is Thread.currentThread().isInterrupted(). The important difference between the two is that the static method would return the interrupt status and also clear it at the same time. On line 22 we deliberately call the object method first followed by the static method. If we reverse the ordering of the two method calls on line 22, the output for the line would be true and false, instead of true and true.

## Volatile

## Explanation
The volatile concept is specific to Java. Its easier to understand volatile, if you understand the problem it solves.

If you have a variable say a counter that is being worked on by a thread, it is possible the thread keeps a copy of the counter variable in the CPU cache and manipulates it rather than writing to the main memory. The JVM will decide when to update the main memory with the value of the counter, even though other threads may read the value of the counter from the main memory and may end up reading a stale value.

If a variable is declared volatile then whenever a thread writes or reads to the volatile variable, the read and write always happen in the main memory. As a further guarantee, all the variables that are visible to the writing thread also get written-out to the main memory alongside the volatile variable. Similarly, all the variables visible to the reading thread alongside the volatile variable will have the latest values visible to the reading thread.

## Example
Consider the program below:

![jmm](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/jmm/jmm21.png)

In the above program, we would expect that threadA would exit the while loop once threadB sets the variable flag to true but threadA may unfortunately find itself spinning forever if it has cached the variable flag's value. In this scenario, marking flag as volatile will fix the problem. Note that volatile presents a consistent view of the memory to all the threads. However, remember that volatile doesn’t imply or mean thread-safety. Consider the program below where we declare the variable count volatile and several threads increment the variable a 1000 times each. If you run the program several times you’ll see count summing up to values other than the expected 10,000.

{% highlight java %}
class Demonstration {

    // volatile doesn't imply thread-safety!
    static volatile int count = 0;
  
    public static void main(String[] args) throws InterruptedException {

        int numThreads = 10;
        Thread[] threads = new Thread[numThreads];

        for (int i = 0; i < numThreads; i++) {
            threads[i] = new Thread(new Runnable() {
                @Override
                public void run() {
                    for (int i = 0; i < 1000; i++)
                        count++;
                }
            });
        }

        for (int i = 0; i < numThreads; i++) {
            threads[i].start();
        }

        for (int i = 0; i < numThreads; i++) {
            threads[i].join();
        }

        System.out.println("count = " + count);
    }
}
{% endhighlight %}

## When is volatile thread-safe
Volatile comes into play because of multiples levels of memory in hardware architecture required for performance enhancements. If there's a single thread that writes to the volatile variable and other threads only read the volatile variable then just using volatile is enough, however, if there's a possibility of multiple threads writing to the volatile variable then "synchronized" would be required to ensure atomic writes to the variable.

## Reentrant Locks & Condition Variables

## Reentrant Lock
Java's answer to the traditional mutex is the reentrant lock, which comes with additional bells and whistles. It is similar to the implicit monitor lock accessed when using synchronized methods or blocks. With the reentrant lock, you are free to lock and unlock it in different methods but not with different threads. If you attempt to unlock a reentrant lock object by a thread which didn't lock it initially, you'll get an IllegalMonitorStateException. This behavior is similar to when a thread attempts to unlock a pthread mutex.

## Condition Variable
We saw how each java object exposes the three methods, wait(),notify() and notifyAll() which can be used to suspend threads till some condition becomes true. You can think of Condition as factoring out these three methods of the object monitor into separate objects so that there can be multiple wait-sets per object. As a reentrant lock replaces synchronized blocks or methods, a condition replaces the object monitor methods. In the same vein, one can't invoke the condition variable's methods without acquiring the associated lock, just like one can't wait on an object's monitor without synchronizing on the object first. In fact, a reentrant lock exposes an API to create new condition variables, like so:

Lock lock = new ReentrantLock();
Condition myCondition  = lock.newCondition();

Notice, how we can now have multiple condition variables associated with the same lock. In the synchronized paradigm, we could only have one wait-set associated with each object.

## java.util.concurrent
Java's util.concurrent package provides several classes that can be used for solving everyday concurrency problems and should always be preferred than reinventing the wheel. Its offerings include thread-safe data structures such as ConcurrentHashMap.

## Missed Signals
A missed signal happens when a signal is sent by a thread before the other thread starts waiting on a condition. This is exemplified by the following code snippet. Missed signals are caused by using the wrong concurrency constructs. In the example below, a condition variable is used to coordinate between the signaller and the waiter thread. The condition is signaled at a time when no thread is waiting on it causing a missed signal.

In later sections, you'll learn that the way we are using the condition variable's await method is incorrect. The idiomatic way of using await is in a while loop with an associated boolean condition. For now, observe the possibility of losing signals between threads.

{% highlight java %}
class Demonstration {

    public static void main(String args[]) throws InterruptedException {
        MissedSignalExample.example();
    }
}

class MissedSignalExample {

    public static void example() throws InterruptedException {

        final ReentrantLock lock = new ReentrantLock();
        final Condition condition = lock.newCondition();

        Thread signaller = new Thread(new Runnable() {

            public void run() {
                lock.lock();
                condition.signal();
                System.out.println("Sent signal");
                lock.unlock();
            }
        });

        Thread waiter = new Thread(new Runnable() {

            public void run() {

                lock.lock();

                try {
                    condition.await();
                    System.out.println("Received signal");
                } catch (InterruptedException ie) {
                    // handle interruption
                }

                lock.unlock();

            }
        });

        signaller.start();
        signaller.join();

        waiter.start();
        waiter.join();

        System.out.println("Program Exiting.");
    }
}
{% endhighlight %}
The above code when ran, will never print the statement Program Exiting and execution would time out. Apart from refactoring the code to match the idiomatic usage of condition variables in a while loop, the other possible fix is to use a semaphore for signalling between the two threads as shown below
{% highlight java %}
class Demonstration {

    public static void main(String args[]) throws InterruptedException {
        FixedMissedSignalExample.example();
    }
}

class FixedMissedSignalExample {

    public static void example() throws InterruptedException {

        final Semaphore semaphore = new Semaphore(1);

        Thread signaller = new Thread(new Runnable() {

            public void run() {
                semaphore.release();
                System.out.println("Sent signal");
            }
        });

        Thread waiter = new Thread(new Runnable() {

            public void run() {
                try {
                    semaphore.acquire();
                    System.out.println("Received signal");
                } catch (InterruptedException ie) {
                    // handle interruption
                }
            }
        });

        signaller.start();
        signaller.join();
        Thread.sleep(5000);
        waiter.start();
        waiter.join();

        System.out.println("Program Exiting.");
    }
}
{% endhighlight %}

## Semaphore in Java

## Explanation
Java’s semaphore can be release()-ed or acquire()-d for signalling amongst threads. However the important call out when using semaphores is to make sure that the permits acquired should equal permits returned. Take a look at the following example, where a runtime exception causes a deadlock.

{% highlight java %}
class Demonstration {

    public static void main(String args[]) throws InterruptedException {
        IncorrectSemaphoreExample.example();
    }
}

class IncorrectSemaphoreExample {

    public static void example() throws InterruptedException {

        final Semaphore semaphore = new Semaphore(1);

        Thread badThread = new Thread(new Runnable() {

            public void run() {

                while (true) {

                    try {
                        semaphore.acquire();
                    } catch (InterruptedException ie) {
                        // handle thread interruption
                    }

                    // Thread was meant to run forever but runs into an
                    // exception that causes the thread to crash.
                    throw new RuntimeException("exception happens at runtime.");

                    // The following line to signal the semaphore is never reached
                    // semaphore.release();
                }
            }
        });

        badThread.start();

        // Wait for the bad thread to go belly-up
        Thread.sleep(1000);

        final Thread goodThread = new Thread(new Runnable() {

            public void run() {
                System.out.println("Good thread patiently waiting to be signalled.");
                try {
                    semaphore.acquire();
                } catch (InterruptedException ie) {
                    // handle thread interruption
                }
            }
        });

        goodThread.start();
        badThread.join();
        goodThread.join();
        System.out.println("Exiting Program");
    }
}
{% endhighlight %}
The above code when run would time out and show that one of the threads threw an exception. The code is never able to release the semaphore causing the other thread to block forever. Whenever using locks or semaphores, remember to unlock or release the semaphore in a finally block. The corrected version appears below.
{% highlight java %}
class Demonstration {

    public static void main(String args[]) throws InterruptedException {
        CorrectSemaphoreExample.example();
    }
}

class CorrectSemaphoreExample {

    public static void example() throws InterruptedException {

        final Semaphore semaphore = new Semaphore(1);

        Thread badThread = new Thread(new Runnable() {

            public void run() {

                while (true) {

                    try {
                        semaphore.acquire();
                        try {
                            throw new RuntimeException("");
                        } catch (Exception e) {
                            // handle any program logic exception and exit the function
                            return;
                        } finally {
                            System.out.println("Bad thread releasing semahore.");
                            semaphore.release();
                        }

                    } catch (InterruptedException ie) {
                        // handle thread interruption
                    }
                }
            }
        });

        badThread.start();

        // Wait for the bad thread to go belly-up
        Thread.sleep(1000);

        final Thread goodThread = new Thread(new Runnable() {

            public void run() {
                System.out.println("Good thread patiently waiting to be signalled.");
                try {
                    semaphore.acquire();
                } catch (InterruptedException ie) {
                    // handle thread interruption
                }
            }
        });

        goodThread.start();
        badThread.join();
        goodThread.join();
        System.out.println("Exiting Program");
    }
}
{% endhighlight %}

## Spurious Wakeups

## Waking-up for no reason

Spurious mean fake or false. A spurious wakeup means a thread is woken up even though no signal has been received. Spurious wakeups are a reality and are one of the reasons why the pattern for waiting on a condition variable happens in a while loop as discussed in earlier chapters. There are technical reasons beyond our current scope as to why spurious wakeups happen, but for the curious on POSIX based operating systems when a process is signaled, all its waiting threads are woken up. Below comment is a directly lifted from Java's documentation for the wait(long timeout) method.

![jmm](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/jmm/jmm22.png)

## Atomic Classes

## Introduction

As part of your senior engineer interview, you may be quizzed on the atomic classes and their utility. Though this is an advanced topic, understanding of it broadens your depth about, and command over concurrent systems and their workings.

So far we have seen locks that allow shared data to be manipulated safely among multiple threads. However, locking doesn’t come for free and takes a toll on performance especially when the shared data/state is being contented for access by multiple threads.

## Cons of Locking

Locking comes with its downsides some of which include:

## Thread scheduling vs useful work
JVM is very efficient when it comes to acquiring and releasing a lock that is requested by a single thread. However, when multiple threads attempt to acquire the same lock, only one wins and the rest must be suspended. The suspension and resumption of threads is costly and introduces significant overhead and this can be an issue for scenarios where several threads contend for the same lock but execute very little functionality. In such cases, the time spent in scheduling overhead overwhelms the useful work done. This is true of synchronized collections where the majority of methods perform very few operations.

## Priority inversion
A higher priority thread can be blocked by a lower priority thread that holds the lock and itself is blocked because of a page fault, scheduling delay etc. This situation effectively downgrades the priority of the higher-priority thread to that of the lower-priority thread since the former can’t make progress until the latter releases the lock. In general, all threads that require a particular lock can’t make progress until the thread holding the lock releases it.

## Liveness issues
Locking also introduces the possibility of liveness issues such as deadlocks, livelock or simply programming bugs that have threads caught in infinite loops blocking other threads from making progress.

## Locking, a heavyweight mechanism
In general locking is a heavyweight mechanism, especially for fine-grained tasks such as manipulating a counter. Locking is akin to assuming the worst or preparing for the worst possible scenario, i.e. the thread assumes it would necessarily run into contention with another thread and acquires a lock to manipulate shared state. Another approach could be to update shared state hoping it would complete without contention/interference from other participants. In case contention is detected, the update operation can be failed, and if desired, reattempted later. We’ll see how this approach is supported by hardware later.

## Atomic vs volatile
Short of locking, we have volatile variables that promise the same visibility guarantees as a lock, however, volatile variables can’t be used for:
* Executing compound actions, .e.g. Decrementing a counter involves fetching the counter value, decrementing it and then writing the updated value for a total of three steps.
* When the value of a variable depends on another or the new value of a variable depends on its older value.

The above limitations are addressed by atomic classes, which offer similar memory visibility guarantees as volatile variables and also allow operations such as read-modify-write to be executed atomically. As an aside, consider the following snippet:

volatile AtomicInteger atomicInteger = new AtomicInteger();

Note that the marking the AtomicInteger variable above volatile isn’t superfluous and implies that when the variable atomicInteger is updated to a new reference, the updated value atomicInteger holds will be observed by all threads that read the variable . In the absence of volatile the atomicInteger variable’s value (which points to a memory location) may get cached by a processor and the new object the variable points to after the update, may not be visible to the processor that cached the old value.

Atomic variables can also be thought of as “better volatiles”. Atomic variables make ideal counters, sequence generators, and variables that accumulate running statistics. They offer the same memory semantics as volatile variables with additional support for atomic updates and may be better choices than volatile variables in most circumstances.

## Atomic Processor Instructions
Modern processors have instructions that can atomically execute compound operations offering a compromise between locking and volatile variables. Hardware support for concurrency is ubiquitous in present-day processors and the most well-known of these instructions is the Compare and Swap instruction or CAS for short. The CAS instruction is the secret sauce behind atomically executing compound operations.

## Compare and Swap

In general, the CAS instruction has three operands:
1. A memory location, say M,representing the variable we desire to manipulate.
2. An expected value for the variable, say A. This is the latest value seen for the variable.
3. The new value, say B, which we want the variable to update to.

CAS instruction works by performing the following actions atomically:
1. Check the latest value of the memory location M.
2. If the memory location has a value other than A, then it implies that another thread changed the variable since the last time we examined it and therefore the requested update operation should be aborted.
3. If the variable’s value is indeed A, then it implies that no other thread has had a chance to change the variable to a different value than A, since we last examined the variable’s value and therefore we can proceed to update the variable/memory location to the new value B.

CAS takes the optimistic approach when performing an update on a shared variable. Expressed in prose, the instruction says I have seen and expect the variable’s value to be A, if that is still true, update the variable to the new value B, otherwise fail my request and let me know. When multiple threads invoke CAS to manipulate a shared variable, only a single thread succeeds and the rest fail. However, the crucial difference between CAS and locking is that with CAS the threads that fail executing the CAS command have a choice to retry or go do some other useful work, unlike locking where all the threads unsuccessful in acquiring the lock will block. This may sound trivial but can improve throughput and performance many fold.

The idiomatic usage of CAS usually takes the form of reading the value A of a shared variable, deriving a new value B from the value A, and finally invoking CAS to update the variable from A to B if it hasn’t been changed to another value in the meantime.

## ABA Problem
The astute reader would recognize that CAS succeeds even if the value of a shared variable is changed from A to B and then back to A. Consider the following sequence:
1. A thread T1 reads the value of a shared variable as A and desires to change it to B. After reading the variable’s value, thread
2. T1 undergoes a context switch. Another thread, T2 comes along, changes the value of the shared variable from A to B and then back to A from B.
3. Thread T1 is scheduled again for execution and invokes CAS with A as the expected value and B as the new value. CAS succeeds since the current value of the variable is A, even though it changed to B and then back to A in the time thread T1 was context switched.

For some algorithms the ABA problem may not be an issue but for others changing the value from A to B and then back to A may require re-executing some step(s) of an algorithm. This problem usually occurs when a program manages its own memory rather than leaving it to the Garbage Collector. For example, you may want to recycle the nodes in your linked list for performance reasons. Thus noting that the head of the list still references the same node, may not necessarily imply that the list wasn’t changed. One solution to this problem is to attach a version number with the value, i.e. instead of storing the value as A, we store it as a pair (A, V1). Another thread can change the value to (B, V1) but when it changes it back to A the associated version is different i.e. (A, V2). In this way, a collision can be detected. There are two classes in Java that can be used to address the ABA problem:
* AtomicStampedReference (please see this class in our reference section for detailed explanation of ABA problem)
* AtomicMarkableReference

## More on Atomics

## Taxonomy of atomic classes

There are a total of sixteen atomic classes divided into four groups:
* Scalars
* Field updaters
* Arrays
* Compound variables

Most well-known and commonly used are the scalar ones such as AtomicInteger, AtomicLong, AtomicReference, which support the CAS (compare-and-set). Other primitive types such as double and float can be simulated by casting short or byte values to and from int and using methods floatToIntBits() and doubleToLongBits() for floating point numbers. Atomic scalar classes extend from Number and don’t redefine hashCode() or equals().

## Atomics are not primitvies
The following widget highlights these differences between Integer and AtomicInteger. Note, that the Integer class has the same hashcode for the same integer value but that’s not the case for AtomicInteger. Thus Atomic* scalar classes are unsuitable as keys for collections that rely on hashcode.

{% highlight java %}
class Demonstration {
    public static void main( String args[] ) {
        AtomicInteger atomicFive = new AtomicInteger(5);
        AtomicInteger atomicAlsoFive = new AtomicInteger(5);

        System.out.println("atomicFive.equals(atomicAlsoFive) : " + atomicFive.equals(atomicAlsoFive));
        System.out.println("atomicFive.hashCode() == atomicAlsoFive.hashCode() : " + (atomicFive.hashCode() == atomicAlsoFive.hashCode()));


        Integer integer1 = new Integer(23235);
        Integer integer2 = new Integer(23235);

        System.out.println("integer1.equals(integer2) : " + integer1.equals(integer2));
        System.out.println("integer1.hashCode() == integer2.hashCode() : " + (integer1.hashCode() == integer2.hashCode()));
    }
}
{% endhighlight %}
Atomics provides the users with an option to back off when faced with contention. For instance the AtomicInteger class has a compareAndSet()method that returns false if the operation doesn’t succeed. The invoking thread now has the opportunity to either retry the operation immediately or use a custom retry strategy. In essence, responding to contention or contention management is pushed to the invoking thread and the JVM doesn’t make a decision for the caller, as it does in case of locking by suspending the thread.

## Performance of atomics vs locks
In the case of a single thread, i.e. zero contention environment, an operation that relies on CAS (e.g. updating an AtomicInteger) will be faster than an operation that involves locking first. On single CPU machines, CAS operations almost always succeed other than in the very rare case of a thread being interrupted in the middle of a read-modify-write operation. Even with moderate contention, CAS operations are faster as they avoid thread suspension and resumption, which locking solutions must deal with.

In benchmark tests, it has been observed that atomics perform better than locks under low to moderate contention, which is representative of real-life programs. However, in a highly contended environment, the majority of threads will waste CPU cycles retrying CAS operations but using locks in the same situation would have the threads suspended and then resumed later. Granted, thread suspension/resumption incurs overhead but at some point the CAS-retry expense dwarfs the overhead of suspending and resuming threads. In reality such high contention is unlikely and atomics are always preferable over lock-based solutions.

We can conduct a crude test to measure the performance of an AtomicInteger counter versus an ordinary counter. The test involves creating a thread pool of ten threads and then having each thread increment the same counter a million times so that the counter value reaches ten million at the end of the test. We time the two scenarios in the widget below:
{% highlight java %}
class Demonstration {

    static AtomicInteger counter = new AtomicInteger(0);
    static int simpleCounter = 0;

    public static void main( String args[] ) throws Exception {
        test(true);
        test(false);
    }

    synchronized static void incrementSimpleCounter() {
        simpleCounter++;
    }

    static void test(boolean isAtomic) throws Exception {
        ExecutorService executorService = Executors.newFixedThreadPool(10);
        long start = System.currentTimeMillis();

        try {
            for (int i = 0; i < 10; i++) {
                executorService.submit(new Runnable() {
                    @Override
                    public void run() {
                        for (int i = 0; i < 1000000; i++) {

                            if (isAtomic) {
                                counter.incrementAndGet();
                            } else {
                                incrementSimpleCounter();
                            }
                        }
                    }
                });
            }
        } finally {
            executorService.shutdown();
            executorService.awaitTermination(1, TimeUnit.HOURS);
        }

        long timeTaken = System.currentTimeMillis() - start;
        System.out.println("Time taken by " + (isAtomic ? "atomic integer counter " : "integer counter ") + timeTaken + " milliseconds.");
    }    
}
{% endhighlight %}

## Keeping state thread local
Finally, the best choice for scalability and performance is to share as little state as possible among threads. Keeping variables and state, thread local results in maximum performance and elimination of contention. Even though atomics achieve better scalability than using locks, choosing not to share any state among threads will result in the best scalability.

## Non-blocking Synchronization

## Introduction
Much of the performance improvements seen in classes such as Semaphore and ConcurrentLinkedQueue versus their synchronized equivalents come from the use of atomic variables and non-blocking synchronization. Non-blocking algorithms use machine-level atomic instructions such as compare-and-swap instead of locks to provide data integrity when multiple threads access shared resources. Non-blocking algorithms are harder to design and implement but out perform lock-based alternatives in terms of liveness and scalability. As the name suggests, non-blocking algorithms don’t block when multiple threads contend for the same data, and as a consequence greatly reduce scheduling overhead. These algorithms don’t suffer from deadlocks, liveness issues and individual thread failures. More formally:
* An algorithm is called non-blocking if the failure or suspension of a thread doesn’t cause the failure or suspension of another thread.
* An algorithm is called lock free if at every step of the algorithm some thread participant of the algorithm can make progress.

## Nonblocking counter
Designing a thread-safe counter would require using locks so that threads don’t step over each other. An increment operation on a long variable consists of three steps. Fetching the current value, incrementing it and then writing it back. All three have to be executed atomically to achieve thread-safety. A lock-based implementation of the lock appears below:

{% highlight java %}
class LockBasedCounter {
    private long value;

    public synchronized long getValue() {
        return value;
    }

    // When multiple threads attempt to invoke the method at the same time,
    // only one is allowed to do so while the rest are suspended
    public synchronized void increment() {
        value++;
    }
}
{% endhighlight %}
Locking comes with its baggage and we can design a counter that doesn’t cause threads to be suspended in the face of contention. To build such a counter, we’ll need the hardware to support the CAS instruction. For our purposes we’ll write a class SimulatedCAS that imitates the CAS instruction. The listing for this class along with comments appears in the widget below:
{% highlight java %}
    public class SimulatedCAS {

        // Let's assume for simplicity our value is a long
        private long value = 0;

        // constructor to initialize the value
        public SimulatedCAS(long initValue) {
            value = initValue;
        }

        synchronized long getValue() {
            return value;
        }

        // The synchronized keyword causes all the steps in this method to execute
        // atomically, which is akin to simulating the compare and swap processor
        // instruction. The behavior of the function is as follows:
        //
        // 1. Return the expectedValue if the CAS instruction completes successfully, i.e.
        //    the newValue is written.
        // 2. Return the current value if the CAS instruction doesn't complete successfully
        //
        // The method is setup such that when expectedValue equals the return value
        // the caller can assume success.
        synchronized long compareAndSwap(long expectedValue, long newValue) {

            if (value == expectedValue) {
                value = newValue;
                return expectedValue;
            }

            // return whatever is the current value
            return value;
        }

        // This method uses the compareAndSwap() method to indicate if the CAS
        // instruction completed successfully or not.
        synchronized boolean compareAndSet(long expectedValue, long newValue) {
            return compareAndSwap(expectedValue, newValue) == expectedValue;
        }
    }
{% endhighlight %}
The compare and swap (CAS) functionality is also implemented by some processors as a pair of instructions loadlinked and store-conditional. Using the SimulatedCAS class we can now construct a non-blocking counter that doesn’t block threads when multiple of them attempt to manipulate shared state. The listing for the class NonblockingCounter has comments describing the operation of the counter:

## CAS-based counter performance
The performance of CAS instruction varies across processors and architectures and though it may seem that a CAS-based counter may perform poorly in comparision to a lock-based counter, the reality is otherwise. In practice CAS-based locks outperform lock-based counters when there is no contention (as the thread doesn’t go through the process of acquiring a lock) and often when there is low to moderate contention. Acquiring a lock usually involves at least one CAS operation and peripheral lock-related housekeeping tasks, which implies more work is done by a lock-based counter in the best case of zero contention compared to a CAS-based counter.

## Conclusion
There are well-known non-blocking algorithms for commonly used data structures such as hashtables, priority queues, stacks, linked-lists etc. However, designing non-blocking algorithms is much more complex than lock-based alternatives. Generally, non-blocking algorithms skirt many of the vices associated with lock-based approaches such as deadlocks or priority inversion, however, threads participating in a non-blocking algorithm can still experience starvation or livelocks as they may perform repeated retries without success.

## Miscellaneous Topics

## Lock Fairness
We'll briefly touch on the topic of fairness in locks since its out of scope for this course. When locks get acquired by threads, there's no guarantee of the order in which threads are granted access to a lock. A thread requesting lock access more frequently may be able to acquire the lock unfairly greater number of times than other locks. Java locks can be turned into fair locks by passing in the fair constructor parameter. However, fair locks exhibit lower throughput and are slower compared to their unfair counterparts.

## Thread Pools
Imagine an application that creates threads to undertake short-lived tasks. The application would incur a performance penalty for first creating hundreds of threads and then tearing down the allocated resources for each thread at the ends of its life. The general way programming frameworks solve this problem is by creating a pool of threads, which are handed out to execute each concurrent task and once completed, the thread is returned to the pool

Java offers thread pools via its Executor Framework. The framework includes classes such as the ThreadPoolExecutor for creating thread pools.
