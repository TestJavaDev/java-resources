---
layout: default
title: Multithreading
nav_order: 4
permalink: /multithreading
has_children: true
---
<div align="center" markdown="1">
Multithreading / Java resources / Grokking the interview

{: .fs-6 .fw-300 }
</div>

[What Every Programmer Should Know About Memory](http://diyhpl.us/~bryan/papers2/distributed/distributed-systems/what-every-programmer-should-know-about-memory.2007.pdf)
[Concurrency interview questions](https://github.com/enhorse/java-interview/blob/master/concurrency.md)
[The Deadlock Empire](https://deadlockempire.github.io/)
[Java Concurrent Animated](http://www.jconcurrent.com/)
[Java Multicore Programming](https://habr.com/ru/company/golovachcourses/blog/223083/)
[Java Concurrency(&C) Jeremy Manson blog](http://jeremymanson.blogspot.com/)
  
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

### Многопоточное программирование в Java

- [Фундаментальный поворот к параллелизму в программировании](https://habrahabr.ru/post/145432/)
- [Non-blocking algorithm](https://en.wikipedia.org/wiki/Non-blocking_algorithm)
- <a href="https://habr.com/ru/post/164487/">Многопоточность в Java</a>
- <a href="https://habr.com/ru/post/143237/">А как же всё-таки работает многопоточность? Часть I: синхронизация</a>
- <a href="https://habr.com/ru/post/209128/">А как же всё-таки работает многопоточность? Часть II: memory ordering</a>
- <a href="https://habr.com/ru/post/150801/">Немного о многопоточном программировании. Часть 1. Синхронизация зло или все-таки нет</a>
- <a href="https://ru.wikipedia.org/wiki/Параллелизм_в_Java">Параллелизм в Java</a>
- <a href="http://www.skipy.ru/technics/synchronization.html">Синхронизация потоков</a>
- <a href="https://habrahabr.ru/post/132884/">Как работает ConcurrentHashMap</a>
- <a href="https://habrahabr.ru/post/277669/"> Справочник по синхронизаторам java.util.concurrent.*</a>
- <a href="http://articles.javatalks.ru/articles/17">Использование ThreadLocal переменных</a>
- <a href="https://www.youtube.com/watch?v=8piqauDj2yo">Николай Алименков — Прикладная многопоточность</a>
- <a href="https://www.youtube.com/playlist?list=PL6jg6AGdCNaXo06LjCBmRao-qJdf38oKp">Advanced Java - Concurrency</a>
- <a href="https://www.youtube.com/playlist?list=PLoij6udfBncgVRq487Me6yQa1kqtxobZS">Java Multithreading</a>
- <a href="http://habrahabr.ru/company/luxoft/blog/157273/">Обзор java.util.concurrent.*</a>
- <a href="https://en.wikipedia.org/wiki/Compare-and-swap">Compare-and-swap</a>
- <a href="https://habrahabr.ru/post/277669/"> Справочник по синхронизаторам java.util.concurrent.*</a>
- <a href="https://www.cs.umd.edu/~pugh/java/memoryModel/DoubleCheckedLocking.html">The "Double-Checked Locking is Broken" Declaration</a>
- <a href="https://habr.com/ru/post/248041/">Ещё раз (надеюсь, последний) про double-checked locking</a>
- <a href="http://www.intuit.ru/studies/courses/16/16/lecture/27127?page=4">Методы wait(), notify(), notifyAll() класса Object</a>

- <a href="https://habr.com/ru/post/276255/">Визуализация concurrency в Go с WebGL</a>
- <a href="https://www.overops.com/blog/5-things-you-didnt-know-about-synchronization-in-java-and-scala/">5 Things You Didn’t Know About Synchronization in Java and Scala</a>

- <a href="https://tproger.ru/translations/java8-concurrency-tutorial-1/">1. Параллельное выполнение кода с помощью потоков</a>
- <a href="https://tproger.ru/translations/java8-concurrency-tutorial-2/">2. Синхронизация доступа к изменяемым объектам</a>
- <a href="https://tproger.ru/translations/java8-concurrency-tutorial-3/">3. Атомарные переменные и конкурентные таблицы</a>

- [Fork/Join Framework в Java 7](https://habrahabr.ru/post/128985/)
- [Java Parallel Streams Are Bad for Your Health](https://zeroturnaround.com/rebellabs/java-parallel-streams-are-bad-for-your-health/)
- [Custom thread pool in Java 8 parallel stream](https://stackoverflow.com/a/21172732/548473)

- <a href="http://tutorials.jenkov.com/java-performance/jmh.html">JMH - Java Microbenchmark Harness</a>
- <a href="http://java-performance.info/jmh/">Java Performance Tuning Guide</a>

- <a href="https://habrahabr.ru/post/183150/"> Функторы, аппликативные функторы и монады в картинках</a>
- <a href="https://habrahabr.ru/company/cit/blog/262055/">Монады в Java 8</a>
- <a href="http://stackoverflow.com/a/19932439/548473">Three Monad laws.</a>
- <a href="https://dzone.com/articles/whats-wrong-java-8-part-iv">What's Wrong in Java 8 Monads</a>

- [Руслан Черёмин — Disruptor и прочие фокусы](https://www.youtube.com/watch?v=IsGBA9KEtTM) 
- [Pair (tuple) in Java](http://stackoverflow.com/questions/521171/a-java-collection-of-value-pairs-tuples) 
- [Java 8 Lambda with exception](http://stackoverflow.com/questions/18198176/java-8-lambda-function-that-throws-exception)
- [What's Wrong in Java 8](https://dzone.com/articles/whats-wrong-java-8-part-iv)
- [Durian](https://github.com/diffplug/durian) ( [Дуриан](https://ru.wikipedia.org/wiki/Дуриан) )

### Books
- [Brian Goetz и другие, “Java Concurrency in Practice”](http://www.amazon.com/Java-Concurrency-Practice-Brian-Goetz/dp/0321349601/)
- [Doug Lea, “Concurrent Programming in Java: Design Principles and Pattern”](http://www.amazon.com/Concurrent-Programming-Java-Principles-Pattern/dp/0201310090/)
- [Maurice Herlihy, Nir Shavit, “The Art of Multiprocessor Programming”](http://www.amazon.com/The-Multiprocessor-Programming-Revised-Reprint/dp/0123973376/)

### Articles
- [Martin Thompson, etc, “Disruptor: High performance alternative to bounded queues for exchanging data between concurrent threads”](http://disruptor.googlecode.com/files/Disruptor-1.0.pdf)
- [Ulrich Drepper, “What Every Programmer Should Know About Memory”](http://diyhpl.us/~bryan/papers2/distributed/distributed-systems/what-every-programmer-should-know-about-memory.2007.pdf)
- [Doug Lea, “The JSR-133 Cookbook for Compiler Writers”](http://gee.cs.oswego.edu/dl/jmm/cookbook.html)
- [Brian Goetz, “Double-checked locking: Clever, but broken”](http://www.javaworld.com/article/2074979/java-concurrency/double-checked-locking--clever--but-broken.html)
- [The “Double-Checked Locking is Broken” Declaration](http://www.cs.umd.edu/~pugh/java/memoryModel/DoubleCheckedLocking.html)
- [Jeremy Manson, Brian Goetz, “JSR 133 (Java Memory Model) FAQ”](http://www.cs.umd.edu/~pugh/java/memoryModel/jsr-133-faq.html)
- [Doug Lea, “The JSR-133 Cookbook for Compiler Writers”](http://gee.cs.oswego.edu/dl/jmm/cookbook.html)
- [Doug Lea, “The java.util.concurrent Synchronizer Framework”](http://gee.cs.oswego.edu/dl/papers/aqs.pdf)
- [Doug Lea, “A Java Fork/Join Framework”](http://gee.cs.oswego.edu/dl/papers/fj.pdf)

### Blog
- [Martin Thompson, “Mechanical Sympathy”](http://mechanical-sympathy.blogspot.com/)
- [Руслан Черемин, “Рабочие заметки”](http://cheremin.blogspot.com/)












