---
layout: default
title: Java Concurrency Reference
parent: Multithreading
has_children: true
nav_order: 5
permalink: /multithreading/reference
---
<div align="center" markdown="1">
Java Concurrency Reference / Java resources / Tutorial

{: .fs-8 .fw-400 }
</div>

### Multithreading basics
{: .label }
*  Program vs Process vs Thread  [first site](https://neharustagiblog.wordpress.com/2014/09/26/program-vs-process-vs-thread-vs-task/) [second site](https://learnc.info/c/processes_and_threads.html) [third site](https://coderoad.ru/200469/%D0%92-%D1%87%D0%B5%D0%BC-%D1%80%D0%B0%D0%B7%D0%BD%D0%B8%D1%86%D0%B0-%D0%BC%D0%B5%D0%B6%D0%B4%D1%83-%D0%BF%D1%80%D0%BE%D1%86%D0%B5%D1%81%D1%81%D0%BE%D0%BC-%D0%B8-%D0%BF%D0%BE%D1%82%D0%BE%D0%BA%D0%BE%D0%BC) [fourth site](https://habr.com/ru/post/40275/)
*  Concurrency vs Parallelism  [first site](https://habr.com/ru/company/piter/blog/274569/) [second site](http://tutorials.jenkov.com/java-concurrency/concurrency-vs-parallelism.html) [third site](https://learnc.info/c/processes_and_threads.html)
*  Cooperative Multitasking vs Preemptive Multitasking [first site](https://ru.qaz.wiki/wiki/Cooperative_multitasking) [second site](https://ru.qaz.wiki/wiki/Preemption_(computing))
*  Synchronous vs Asynchronous [first site](https://itsobes.ru/JavaSobes/chem-sinkhronnyi-server-otlichaetsia-ot-asinkhronnogo/) [second site](https://coderoad.ru/5385407/%D0%92-%D1%87%D0%B5%D0%BC-%D1%80%D0%B0%D0%B7%D0%BD%D0%B8%D1%86%D0%B0-%D0%BC%D0%B5%D0%B6%D0%B4%D1%83-Jetty-%D0%B8-Netty)
*  I/O Bound vs CPU Bound [first site](https://coderoad.ru/868568/%D0%A7%D1%82%D0%BE-%D0%BE%D0%B7%D0%BD%D0%B0%D1%87%D0%B0%D1%8E%D1%82-%D1%82%D0%B5%D1%80%D0%BC%D0%B8%D0%BD%D1%8B-%D1%81%D0%B2%D1%8F%D0%B7%D0%B0%D0%BD%D0%BD%D1%8B%D0%B5-CPU-bound-%D0%B8-I-O) [second site](https://stackoverflow.com/questions/868568/what-do-the-terms-cpu-bound-and-i-o-bound-mean)
*  Throughput vs Latency  [first site](https://dzone.com/articles/what-latency-throughput-and)
*  Critical Sections & Race Conditions  [first site](https://ru.wikipedia.org/wiki/%D0%9A%D1%80%D0%B8%D1%82%D0%B8%D1%87%D0%B5%D1%81%D0%BA%D0%B0%D1%8F_%D1%81%D0%B5%D0%BA%D1%86%D0%B8%D1%8F) [second site](https://github.com/merry75/educative.io_courses/blob/master/Java%20Multithreading%20for%20Senior%20Engineering%20Interviews%20-%20Learn%20Interactively/8_Critical_Sections___Race_Conditions.pdf)
*  Deadlocks, Liveness & Reentrant Locks  [first site](https://www.baeldung.com/java-deadlock-livelock)
*  Mutex vs Semaphore vs Monitor   [first site](https://javarush.ru/groups/posts/2174-v-chem-raznica-mezhdu-mjhjuteksom-monitorom-i-semaforom) [second site](https://github.com/merry75/educative.io_courses/blob/master/Java%20Multithreading%20for%20Senior%20Engineering%20Interviews%20-%20Learn%20Interactively/10_Mutex_vs_Semaphore.pdf) [third site](https://github.com/merry75/educative.io_courses/blob/master/Java%20Multithreading%20for%20Senior%20Engineering%20Interviews%20-%20Learn%20Interactively/11_Mutex_vs_Monitor.pdf)
*  Amdahl's Law  [first site](https://uk.wikipedia.org/wiki/%D0%97%D0%B0%D0%BA%D0%BE%D0%BD_%D0%90%D0%BC%D0%B4%D0%B0%D0%BB%D0%B0)
*  Moore's Law  [first site](https://uk.wikipedia.org/wiki/%D0%97%D0%B0%D0%BA%D0%BE%D0%BD_%D0%9C%D1%83%D1%80%D0%B0)

### Multithreading in Java
{: .label }
*  Thready Safety & Synchronized  [first site](https://javarush.ru/groups/posts/1055-sinkhronizacija-potokov-blokirovka-obhhekta-i-blokirovka-klassa) [second site](https://github.com/merry75/educative.io_courses/blob/master/Java%20Multithreading%20for%20Senior%20Engineering%20Interviews%20-%20Learn%20Interactively/16_Thready_Safety___Synchronized.pdf)
*  Wait & Notify  [first site](https://javarush.ru/quests/lectures/questmultithreading.level01.lecture06) [second site](https://coderoad.ru/2536692/%D0%9F%D1%80%D0%BE%D1%81%D1%82%D0%BE%D0%B9-%D1%81%D1%86%D0%B5%D0%BD%D0%B0%D1%80%D0%B8%D0%B9-%D1%81-%D0%B8%D1%81%D0%BF%D0%BE%D0%BB%D1%8C%D0%B7%D0%BE%D0%B2%D0%B0%D0%BD%D0%B8%D0%B5%D0%BC-wait-%D0%B8-notify-%D0%B2-java) [third site]() [fourth site]()
*  Interrupting Threads  [first site](https://javarush.ru/quests/lectures/questmultithreading.level05.lecture06) [second site](https://www.ibm.com/developerworks/ru/library/j-jtp05236/index.html) [third site](https://coderoad.ru/20527893/Java-Thread-stop-%D0%BF%D1%80%D0%BE%D1%82%D0%B8%D0%B2-Thread-interrupt) [fourth site](https://habr.com/ru/post/133413/)
*  Volatile  [first site](https://javarush.ru/groups/posts/1998-upravlenie-potokami-metodih-volatile-i-yield) [second site](https://javarush.ru/quests/lectures/questmultithreading.level06.lecture04) [third site](https://www.ibm.com/developerworks/ru/library/j-5things15/index.html)
*  Reentrant Locks & Condition Variables  [first site](https://metanit.com/java/tutorial/8.10.php) [second site](http://java-online.ru/concurrent-locks.xhtml) [third site](https://stackoverflow.com/questions/33229932/reeantrantlock-and-condition-variable)
*  Missed Signals  [first site](https://stackoverflow.com/questions/19509209/what-is-missed-signal-in-java-how-calling-notify-be-missed-by-the-waiting-thr/19509301) [second site](https://github.com/merry75/educative.io_courses/blob/master/Java%20Multithreading%20for%20Senior%20Engineering%20Interviews%20-%20Learn%20Interactively/21_Missed_Signals.pdf)
*  Semaphore in Java  [first site](https://habr.com/ru/post/261273/) [second site](https://pro-java.ru/parallelizm-v-java/klass-semaphore-primery-realizacii-koda-v-java/) [third site](https://www.codeflow.site/ru/article/java__java-semaphore-examples)
*  Spurious Wakeups  [first site](https://coderoad.ru/2540984/%D0%9F%D0%BE%D1%87%D0%B5%D0%BC%D1%83-%D0%BF%D0%BE%D1%82%D0%BE%D0%BA%D0%B8-%D1%81%D0%BF%D0%BE%D0%BD%D1%82%D0%B0%D0%BD%D0%BD%D0%BE-%D0%BF%D1%80%D0%BE%D0%B1%D1%83%D0%B6%D0%B4%D0%B0%D1%8E%D1%82%D1%81%D1%8F-%D0%BE%D1%82-wait) [second site](https://stackoverflow.com/questions/1050592/do-spurious-wakeups-in-java-actually-happen)

### Java Memory Model
{: .label }
*  Java Memory Model  [first site](https://habr.com/ru/post/440590/)
*  Reordering Effects  [first site](https://habr.com/ru/post/133981/) [second site](https://coderoad.ru/52648800/%D0%9A%D0%B0%D0%BA-%D0%BF%D1%80%D0%BE%D0%B4%D0%B5%D0%BC%D0%BE%D0%BD%D1%81%D1%82%D1%80%D0%B8%D1%80%D0%BE%D0%B2%D0%B0%D1%82%D1%8C-%D0%BF%D1%80%D0%BE%D0%B1%D0%BB%D0%B5%D0%BC%D1%8B-%D1%81-%D0%BF%D0%B5%D1%80%D0%B5%D1%83%D0%BF%D0%BE%D1%80%D1%8F%D0%B4%D0%BE%D1%87%D0%B5%D0%BD%D0%B8%D0%B5%D0%BC-%D0%B8%D0%BD%D1%81%D1%82%D1%80%D1%83%D0%BA%D1%86%D0%B8%D0%B9-Java)
*  The happens-before Relationship  [first site](https://ru.stackoverflow.com/questions/547859/java-memory-model-%D0%B8-happens-before) [second site](https://github.com/merry75/educative.io_courses/blob/master/Java%20Multithreading%20for%20Senior%20Engineering%20Interviews%20-%20Learn%20Interactively/27_The_happens_before_Relationship.pdf)

### Interview Practice Problems
{: .label }
*  Blocking Queue, Bounded Buffer, Consumer Producer  [first site](https://uk.wikipedia.org/wiki/%D0%97%D0%B0%D0%B4%D0%B0%D1%87%D0%B0_%D0%BF%D0%BE%D1%81%D1%82%D0%B0%D1%87%D0%B0%D0%BB%D1%8C%D0%BD%D0%B8%D0%BA%D0%B0-%D1%81%D0%BF%D0%BE%D0%B6%D0%B8%D0%B2%D0%B0%D1%87%D0%B0) [second site](https://javarush.ru/groups/posts/1133-primer-synchronousqueue-v-java---reshenie-zadachi-proizvoditeljh-potrebiteljh) [third site](https://github.com/merry75/educative.io_courses/blob/master/Java%20Multithreading%20for%20Senior%20Engineering%20Interviews%20-%20Learn%20Interactively/28_Blocking_Queue___Bounded_Buffer___Consumer_Producer.pdf) [fourth site](https://github.com/merry75/educative.io_courses/blob/master/Java%20Multithreading%20for%20Senior%20Engineering%20Interviews%20-%20Learn%20Interactively/29_____continued.pdf) [fifth site](https://github.com/merry75/educative.io_courses/blob/master/Java%20Multithreading%20for%20Senior%20Engineering%20Interviews%20-%20Learn%20Interactively/30_____continued.pdf)
*  Rate Limiting Using Token Bucket Filter  [first site](https://linkmeup.gitbook.io/sdsm/15.-qos/7.-ogranichenie-skorosti/4-mekhanizmy-leaky-bucket-i-token-bucket/1-algoritm-token-bucket) [second site](https://habr.com/ru/post/448438/) [third site](https://github.com/merry75/educative.io_courses/blob/master/Java%20Multithreading%20for%20Senior%20Engineering%20Interviews%20-%20Learn%20Interactively/31_Rate_Limiting_Using_Token_Bucket_Filter.pdf) [fourth site](https://github.com/merry75/educative.io_courses/blob/master/Java%20Multithreading%20for%20Senior%20Engineering%20Interviews%20-%20Learn%20Interactively/32_____continued.pdf)
*  Thread Safe Deferred Callback  [first site](https://github.com/merry75/educative.io_courses/blob/master/Java%20Multithreading%20for%20Senior%20Engineering%20Interviews%20-%20Learn%20Interactively/33_Thread_Safe_Deferred_Callback.pdf)
*  Implementing Semaphore  [first site](https://stackoverflow.com/questions/33766797/how-to-implement-a-semaphore) [second site](https://github.com/merry75/educative.io_courses/blob/master/Java%20Multithreading%20for%20Senior%20Engineering%20Interviews%20-%20Learn%20Interactively/34_Implementing_Semaphore.pdf)
*  ReadWrite Lock  [first site](https://coderlessons.com/tutorials/java-tekhnologii/izuchite-java-parallelizm/parallelizm-java-interfeis-readwritelock) [second site](https://dou.ua/lenta/articles/clh-lock/) [third site](https://github.com/merry75/educative.io_courses/blob/master/Java%20Multithreading%20for%20Senior%20Engineering%20Interviews%20-%20Learn%20Interactively/35_ReadWrite_Lock.pdf)
*  Unisex Bathroom Problem  [first site](https://stackoverflow.com/questions/11135207/java-unisex-bathroom/11139167) [second site](https://coderoad.ru/11135207/Java-%D1%83%D0%BD%D0%B8%D1%81%D0%B5%D0%BA%D1%81-%D0%B2%D0%B0%D0%BD%D0%BD%D0%B0%D1%8F-%D0%BA%D0%BE%D0%BC%D0%BD%D0%B0%D1%82%D0%B0) [third site](https://github.com/merry75/educative.io_courses/blob/master/Java%20Multithreading%20for%20Senior%20Engineering%20Interviews%20-%20Learn%20Interactively/36_Unisex_Bathroom_Problem.pdf)
*  Implementing a Barrier  [first site](https://pro-java.ru/parallelizm-v-java/klass-cyclicbarrier-primery-realizacii-koda-v-java/) [second site](https://www.codeflow.site/ru/article/java-cyclic-barrier) [third site](https://github.com/merry75/educative.io_courses/blob/master/Java%20Multithreading%20for%20Senior%20Engineering%20Interviews%20-%20Learn%20Interactively/37_Implementing_a_Barrier.pdf)
*  Uber Ride Problem  [first site](https://github.com/merry75/educative.io_courses/blob/master/Java%20Multithreading%20for%20Senior%20Engineering%20Interviews%20-%20Learn%20Interactively/38_Uber_Ride_Problem.pdf)
*  Dining Philosophers  [first site](https://uk.wikipedia.org/wiki/%D0%97%D0%B0%D0%B4%D0%B0%D1%87%D0%B0_%D1%84%D1%96%D0%BB%D0%BE%D1%81%D0%BE%D1%84%D1%96%D0%B2,_%D1%89%D0%BE_%D0%BE%D0%B1%D1%96%D0%B4%D0%B0%D1%8E%D1%82%D1%8C) [second site](https://medium.com/@chekmenev/%D0%B7%D0%B0%D0%B4%D0%B0%D1%87%D0%B0-%D0%BE%D0%B1%D0%B5%D0%B4%D0%B0%D1%8E%D1%89%D0%B8%D1%85-%D1%84%D0%B8%D0%BB%D0%BE%D1%81%D0%BE%D1%84%D0%BE%D0%B2-ac6644ca83b2) [third site](http://is.ifmo.ru/download/phil.pdf) [fourth site](https://github.com/merry75/educative.io_courses/blob/master/Java%20Multithreading%20for%20Senior%20Engineering%20Interviews%20-%20Learn%20Interactively/39_Dining_Philosophers.pdf)
*  Barber Shop  [first site](https://ichi.pro/ru/potoki-java-problema-spasego-parikmahera-26690334138382) [second site](https://ru.wikipedia.org/wiki/%D0%9F%D1%80%D0%BE%D0%B1%D0%BB%D0%B5%D0%BC%D0%B0_%D1%81%D0%BF%D1%8F%D1%89%D0%B5%D0%B3%D0%BE_%D0%BF%D0%B0%D1%80%D0%B8%D0%BA%D0%BC%D0%B0%D1%85%D0%B5%D1%80%D0%B0) [third site](https://github.com/merry75/educative.io_courses/blob/master/Java%20Multithreading%20for%20Senior%20Engineering%20Interviews%20-%20Learn%20Interactively/40_Barber_Shop.pdf)
*  Superman Problem  [first site](https://github.com/merry75/educative.io_courses/blob/master/Java%20Multithreading%20for%20Senior%20Engineering%20Interviews%20-%20Learn%20Interactively/41_Superman_Problem.pdf) [second site](https://github.com/merry75/educative.io_courses/blob/master/Java%20Multithreading%20for%20Senior%20Engineering%20Interviews%20-%20Learn%20Interactively/42_____continued.pdf)
*  Multithreaded Merge Sort  [first site](https://github.com/merry75/educative.io_courses/blob/master/Java%20Multithreading%20for%20Senior%20Engineering%20Interviews%20-%20Learn%20Interactively/43_Multithreaded_Merge_Sort.pdf)
*  Asynchronous to Synchronous Problem  [first site](https://www.geeksforgeeks.org/asynchronous-synchronous-callbacks-java/) [second site](https://github.com/merry75/educative.io_courses/blob/master/Java%20Multithreading%20for%20Senior%20Engineering%20Interviews%20-%20Learn%20Interactively/44_Asynchronous_to_Synchronous_Problem.pdf)
*  Fizz Buzz Problem [first site](https://github.com/merry75/educative.io_courses/blob/master/Java%20Multithreading%20for%20Senior%20Engineering%20Interviews%20-%20Learn%20Interactively/50_Fizz_Buzz_Problem.pdf)

### Java Thread Basics
{: .label }
*  Setting-up Threads  [first site](https://javarush.ru/groups/posts/2047-threadom-java-ne-isportishjh--chastjh-i---potoki) [second site](http://tutorials.jenkov.com/java-concurrency/creating-and-starting-threads.html) [third site](https://dzone.com/articles/java-thread-tutorial-creating-threads-and-multithr) [fourth site](https://javarush.ru/groups/posts/2048-threadom-java-ne-isportishjh--chastjh-ii---sinkhronizacija) [fifth site](https://javarush.ru/groups/posts/2065-threadom-java-ne-isportishjh--chastjh-iv---callable-future-i-druzjhja) [sixth site](https://javarush.ru/groups/posts/2111-threadom-java-ne-isportishjh--chastjh-vi---k-barjheru)
*  Basic Thread Handling  [first site](http://java-online.ru/java-thread.xhtml) [second site](https://dataart.ua/articles/mnogopotochnost-v-java-lekfiya-4-puly-potokov/) [third site](https://stackoverflow.com/questions/6546193/how-to-catch-an-exception-from-a-thread)
*  Executor Framework  [first site](http://java-online.ru/concurrent-executor.xhtml) [second site](https://medium.com/nuances-of-programming/%D1%84%D1%80%D0%B5%D0%B9%D0%BC%D0%B2%D0%BE%D1%80%D0%BA-executor-%D0%B2-java-d5d4c68ccc55) [third site](https://habr.com/ru/post/260953/)
*  Executor Implementations  [first site](https://javarush.ru/quests/lectures/questmultithreading.level08.lecture09) [second site](https://javarush.ru/groups/posts/2078-threadom-java-ne-isportishjh--chastjh-v---executor-threadpool-fork-join-pool) [third site](https://habr.com/ru/sandbox/114046/)
*  Thread Pools  [first site](https://habr.com/ru/post/326146/) [second site](https://www.codeflow.site/ru/article/thread-pool-java-and-guava) [third site](https://coderoad.ru/10360974/%D0%A7%D1%82%D0%BE-%D0%B8%D0%BC%D0%B5%D0%BD%D0%BD%D0%BE-%D0%B4%D0%B5%D0%BB%D0%B0%D0%B5%D1%82-%D0%BF%D1%83%D0%BB-%D0%BF%D0%BE%D1%82%D0%BE%D0%BA%D0%BE%D0%B2-%D0%B2-Java)
*  Types of Thread Pools  [first site](https://www.baeldung.com/thread-pool-java-and-guava) [second site](https://stackoverflow.com/questions/17186206/types-of-thread-pools-in-java)
*  ForkJoinPool [first site](https://habr.com/ru/post/128985/) [second site](https://javarush.ru/groups/posts/2078-threadom-java-ne-isportishjh--chastjh-v---executor-threadpool-fork-join-pool) [third site](https://www.youtube.com/watch?v=t0dGLFtRR9c)
*  Callable Interface  [first site](https://javadevblog.com/java-callable-kratkoe-opisanie-i-primer-ispol-zovaniya.html) [second site](https://coderoad.ru/30976946/%D0%B2-%D1%87%D0%B5%D0%BC-%D0%BF%D1%80%D0%B5%D0%B8%D0%BC%D1%83%D1%89%D0%B5%D1%81%D1%82%D0%B2%D0%BE-%D0%B8%D1%81%D0%BF%D0%BE%D0%BB%D1%8C%D0%B7%D0%BE%D0%B2%D0%B0%D0%BD%D0%B8%D1%8F-FutureTask-%D0%BF%D0%B5%D1%80%D0%B5%D0%B4-Callable)
*  Future Interface  [first site](https://pro-java.ru/java-dlya-opytnyx/interfejsy-callable-i-future-v-java/) [second site](http://java-online.ru/concurrent-callable.xhtml)
*  CompletionService Interface  [first site](https://coderoad.ru/11872520/ExecutorCompletionService-%D0%97%D0%B0%D1%87%D0%B5%D0%BC-%D0%BD%D1%83%D0%B6%D0%B5%D0%BD-%D0%BE%D0%B4%D0%B8%D0%BD-%D0%B5%D1%81%D0%BB%D0%B8-%D1%83-%D0%BD%D0%B0%D1%81-%D0%B5%D1%81%D1%82%D1%8C-invokeAll)
*  ThreadLocal  [first site](https://articles.javatalks.ru/articles/17) [second site]() [third site]() [fourth site]()
*  CountDownLatch  [first site](https://coderoad.ru/17827022/%D0%9A%D0%B0%D0%BA-CountDownLatch-%D0%B8%D1%81%D0%BF%D0%BE%D0%BB%D1%8C%D0%B7%D1%83%D0%B5%D1%82%D1%81%D1%8F-%D0%B2-Java-%D0%BC%D0%BD%D0%BE%D0%B3%D0%BE%D0%BF%D0%BE%D1%82%D0%BE%D1%87%D0%BD%D0%BE%D1%81%D1%82%D0%B8) [second site](https://www.codeflow.site/ru/article/java-countdown-latch) [third site](https://pro-java.ru/parallelizm-v-java/klass-countdownlatch-primery-realizacii-koda-v-java/)
*  CyclicBarrier  [first site](https://javanerd.ru/%D0%BE%D1%81%D0%BD%D0%BE%D0%B2%D1%8B-java/%D0%BC%D0%BD%D0%BE%D0%B3%D0%BE%D0%BF%D0%BE%D1%82%D0%BE%D1%87%D0%BD%D0%BE%D1%81%D1%82%D1%8C-%D0%BA%D0%BB%D0%B0%D1%81%D1%81-cyclicbarrier/) [second site](https://pro-java.ru/parallelizm-v-java/klass-cyclicbarrier-primery-realizacii-koda-v-java/)
*  Concurrent Collections  [first site](https://habr.com/ru/company/luxoft/blog/157273/) [second site](https://habr.com/ru/post/473352/) [third site](http://java-online.ru/concurrent-collections.xhtml)
*  CompletableFuture  [first site](https://www.youtube.com/watch?v=hqR41XVx3kM) [second site](https://annimon.com/article/3462) [third site](https://www.codeflow.site/ru/article/java-completablefuture)

Java Concurrency Reference

Setting-up Threads
Basic Thread Handling
Executor Framework
Executor Implementations
Thread Pools
Types of Thread Pools
An Example: Timer vs ScheduledThreadPool
ThreadPoolExecutor
Callable Interface
Future Interface
CompletionService Interface
ThreadLocal
ThreadLocalRandom
CountDownLatch
CyclicBarrier
Concurrent Collections
ConcurrentHashMap
ConcurrentModificationException
Lock Interface
LockSupport
ReentrantLock
ReadWriteLock
StampedLock
Atomic Boolean
AtomicInteger
AtomicIntegerArray
AtomicLong
AtomicLongArray
LongAdder
LongAccumulator
DoubleAdder
DoubleAccumulator
AtomicReference
AtomicReferenceArray
AtomicStampedReference
Exchanger
Phaser
IllegalMonitorStateException
TimeoutException
CancellationException
ExecutionException
RejectedExecutionException
CompletionException
BrokenBarrierException