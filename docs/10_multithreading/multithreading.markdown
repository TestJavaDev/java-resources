---
layout: default
title: Multithreading
nav_order: 10
permalink: /multithreading
has_children: true
---
<div align="center" markdown="1">
Multithreading / Java resources / Grokking the interview

{: .fs-6 .fw-300 }
</div>
  
### Multithreading basics
{: .label }
*  Program vs Process vs Thread  [first site](https://neharustagiblog.wordpress.com/2014/09/26/program-vs-process-vs-thread-vs-task/) [second site](https://learnc.info/c/processes_and_threads.html) [third site](https://coderoad.ru/200469/%D0%92-%D1%87%D0%B5%D0%BC-%D1%80%D0%B0%D0%B7%D0%BD%D0%B8%D1%86%D0%B0-%D0%BC%D0%B5%D0%B6%D0%B4%D1%83-%D0%BF%D1%80%D0%BE%D1%86%D0%B5%D1%81%D1%81%D0%BE%D0%BC-%D0%B8-%D0%BF%D0%BE%D1%82%D0%BE%D0%BA%D0%BE%D0%BC) [fourth site](https://habr.com/ru/post/40275/)
*  Concurrency vs Parallelism  [first site](http://tutorials.jenkov.com/java-concurrency/concurrency-vs-parallelism.html) [second site](https://learnc.info/c/processes_and_threads.html)
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
*  Thready Safety & Synchronized
*  Wait & Notify
*  Interrupting Threads
*  Volatile
*  Reentrant Locks & Condition Variables
*  Missed Signals
*  Semaphore in Java
*  Spurious Wakeups
*  Miscellaneous Topics

### Java Memory Model
{: .label }
*  Java Memory Model
*  Reordering Effects
*  The happens-before Relationship

### Interview Practice Problems
{: .label }
*  Blocking Queue, Bounded Buffer, Consumer Producer
*  Rate Limiting Using Token Bucket Filter
*  Thread Safe Deferred Callback
*  Implementing Semaphore
*  ReadWrite Lock
*  Unisex Bathroom Problem
*  Implementing a Barrier
*  Uber Ride Problem
*  Dining Philosophers
*  Barber Shop
*  Superman Problem
*  Multithreaded Merge Sort
*  Asynchronous to Synchronous Problem
*  Epilogue
*  Ordered Printing
*  Printing Foo Bar n Times
*  Printing Number Series (Zero, Even, Odd)
*  Build a Molecule
*  Fizz Buzz Problem

### Java Thread Basics
{: .label }
*  Setting-up Threads
*  Basic Thread Handling
*  Executor Framework
*  Executor Implementations
*  Thread Pools
*  Types of Thread Pools
*  An Example: Timer vs ScheduledThreadPool
*  Callable Interface
*  Future Interface
*  CompletionService Interface
*  ThreadLocal
*  CountDownLatch
*  CyclicBarrier
*  Concurrent Collections

- [Фундаментальный поворот к параллелизму в программировании](https://habrahabr.ru/post/145432/)
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
- <a href="http://www.intuit.ru/studies/courses/16/16/lecture/27127">Потоки выполнения. Синхронизация.</a>
- <a href="http://www.intuit.ru/studies/courses/16/16/lecture/27127?page=4">Методы wait(), notify(), notifyAll() класса Object</a>

### Многопоточное программирование в Java

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

- [Pair (tuple) in Java](http://stackoverflow.com/questions/521171/a-java-collection-of-value-pairs-tuples) 
- [Java 8 Lambda with exception](http://stackoverflow.com/questions/18198176/java-8-lambda-function-that-throws-exception)
- [What's Wrong in Java 8](https://dzone.com/articles/whats-wrong-java-8-part-iv)
- [Durian](https://github.com/diffplug/durian) ( [Дуриан](https://ru.wikipedia.org/wiki/Дуриан) )












