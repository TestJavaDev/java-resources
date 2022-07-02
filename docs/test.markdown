1. Программа курса «Аппаратное обеспечение, операционные системы и сети»:
....Аппаратное обеспечение
........компоненты: процессор, память, шины, контроллеры
........регистры, биты/байты/слова
........архитектура системы
........роль операционной системы
....Операционная система Linux
........ядро, устройства, драйверы
........файловая система
........процессы, сигналы, потоки
........безопастность, user management
........понятие о программировании на bash
........сети, удаленный доступ, ssh
........кластер, облако, виртуализация

2. Программа курса «Основы программирования на Java (Core Java)»
....Основы Java (терминология, управляющие конструкции, числа, битовые операции, массивы, строки)
....Базовые алгоритмы (итеративные алгоритмы, рекурсия, рекурсивные алгоритмы, динамические структуры данных, память в Java)
....Исключения (try-catch-finally, проверяемые / непроверяемые, стратегии обработки, try-with-resources, важные исключения в JDK)
....Ввод/вывод (кодировки, I/O Streams ,Serialization API, файловая система, NIO, NIO.2)
....Многопоточность (физический уровень, Thread / Runnable, JMM, volatile, synchronized, wait/notify, прерывание потока, java.util.concurrent.*, CompletableFuture, Executor)
....Коллекции (O-нотация, Базовая иерархия (сollection, Set, List, Map), Iterable/Iterator, foreach, ArrayList/LinkedList, equals(), HashMap/HashSet, hashCode(), TreeSet/TreeMap, Comparable/Comparator)
....ООП (понятие о типе (ClassCastException, instanceOf, java.lang.Class), конструирование объектов, сущности (class, interface, abstract class, enum), методы (overloading, overriding, hiding), области видимости (модификаторы доступа, пакеты), внутренние/вложенные, анонимные классы)
....Основные шаблоны проектирования (Builder, Singleton, Factory Method, Adapter, Decorator, Composite, Facade, Proxy, Command, Iterator, Listener, Strategy, Template Method).
....Продвинутые возможности (Reflection API, аннотации, генерики, загрузка классов)
....Java 8 (методы в интерфейсах и ссылки на методы, Лямбды (Project Lambda), Stream API, функциональные алгоритмы)
.


Модуль #1: Между “железом” и “математикой”, примитивы
“железо”
архитектура современных процессоров, кэши
memory barriers, read/write reordering, протоколы когерентности кэшей
“математика”/Java Memory Model
New JMM — описание «на пальцах»
какие гарантии дают Thread.start()/join(), volatile, final, CAS, lazySet, weakCompareAndSet, классы из j.u.c
формальная спецификация New JMM: happens-before edge, commitment protocol
примитивы/конструкции
double checked locking (broken), safe publishing
synchronized+Object.wait()/notify()/notifyAll() — как использовать, какие гарантии, как реализовано в HotSpot
реализуем свои: Dekker's algorithm, Peterson's algorithm, Lamport Bakery algotithm

Модуль #2: java.util.concurrent (Java 5)
многопоточные коллекции
BlockingQueue-s
ConcurrentMap-s: ConcurrentHashMap, ConcurrentSkipListMap
copy-on-write structures: CopyOnWriteArrayList, CopyOnWriteArraySet
“синхронизаторы”
Lock, Condition, ReentrantLock, ReentrantReadWriteLock, Semaphore
CountDownLatch, CyclicBarrier, Exchanger, Phaser
пул потоков + Future
Executors, ExecutorService, ThreadPoolExecutor, ScheduledExecutorService, ScheduledThreadPoolExecutor
Callable, Future, чего не хватает j.u.c.Future
ядро j.u.c: AbstractQueuedSynchronizer + LockSupport
внутреннее устройство j.u.c.AQS
строим свои примитивы на j.u.c.AQS + LockSupport


Модуль #3: Fork/Join Framework (java 7) + Parallel Streams (Java 8)
Fork/Join Framework
решаем задачи в стиле рекурсивного параллелизма
идиомы и типичные задачи
Fork/Join Framework — что «под капотом»
Parallel Streams
Java 8 — работаем с данными через java.util.Stream
java.util.Stream.parallel() — что «под капотом»

Модуль #4: “Неклассические архитектуры”
Non-blocking algorithm
пакет j.u.c.atomic: AtomicXXX, AtomicXXXArray, AtomicXXXFieldUpdater, AtomicStampedReference, AtomicMarkableReference
классификация: blocking, non-blocking, lock-free, wait-free, obstruction free
неблокирующие реализации основных структур данных: stack, queue, deque, hashtable, treemap
архитектуры на основе передачи сообщений (Akka)
библиотека Akka
основные шаблоны, типовые архитектуры
плюсы и минусы архитектур на основе передачи сообщений
Software Transactional Memory (Clojure)
библиотека clojure.lang.*
плюсы и минусы архитектур на транзакционной памяти
Persistent Data Structures
плюсы и минусы персистентных структур данных
персистентные реализации основных структур данных: stack, queue, deque, hashtable, treemap
библиотеки: clojure.lang.*, pcollections

Модуль #1: Между “железом” и “математикой”, примитивы
“железо”
архитектура современных процессоров, кэши
memory barriers, read/write reordering, протоколы когерентности кэшей
“математика”/Java Memory Model
New JMM — описание «на пальцах»
какие гарантии дают Thread.start()/join(), volatile, final, CAS, lazySet, weakCompareAndSet, классы из j.u.c
формальная спецификация New JMM: happens-before edge, commitment protocol
примитивы/конструкции
double checked locking (broken), safe publishing
synchronized+Object.wait()/notify()/notifyAll() — как использовать, какие гарантии, как реализовано в HotSpot
реализуем свои: Dekker's algorithm, Peterson's algorithm, Lamport Bakery algotithm

Модуль #2: java.util.concurrent (Java 5)
многопоточные коллекции
BlockingQueue-s
ConcurrentMap-s: ConcurrentHashMap, ConcurrentSkipListMap
copy-on-write structures: CopyOnWriteArrayList, CopyOnWriteArraySet
“синхронизаторы”
Lock, Condition, ReentrantLock, ReentrantReadWriteLock, Semaphore
CountDownLatch, CyclicBarrier, Exchanger, Phaser
пул потоков + Future
Executors, ExecutorService, ThreadPoolExecutor, ScheduledExecutorService, ScheduledThreadPoolExecutor
Callable, Future, чего не хватает j.u.c.Future
ядро j.u.c: AbstractQueuedSynchronizer + LockSupport
внутреннее устройство j.u.c.AQS
строим свои примитивы на j.u.c.AQS + LockSupport

Модуль #3: Fork/Join Framework (java 7) + Parallel Streams (Java 8)
Fork/Join Framework
решаем задачи в стиле рекурсивного параллелизма
идиомы и типичные задачи
Fork/Join Framework — что «под капотом»
Parallel Streams
Java 8 — работаем с данными через java.util.Stream
java.util.Stream.parallel() — что «под капотом»

Модуль #4: “Неклассические архитектуры”
Non-blocking algorithm
пакет j.u.c.atomic: AtomicXXX, AtomicXXXArray, AtomicXXXFieldUpdater, AtomicStampedReference, AtomicMarkableReference
классификация: blocking, non-blocking, lock-free, wait-free, obstruction free
неблокирующие реализации основных структур данных: stack, queue, deque, hashtable, treemap
архитектуры на основе передачи сообщений (Akka)
библиотека Akka
основные шаблоны, типовые архитектуры
плюсы и минусы архитектур на основе передачи сообщений
Software Transactional Memory (Clojure)
библиотека clojure.lang.*
плюсы и минусы архитектур на транзакционной памяти
Persistent Data Structures
плюсы и минусы персистентных структур данных
персистентные реализации основных структур данных: stack, queue, deque, hashtable, treemap
библиотеки: clojure.lang.*, pcollections




ервая часть

Intro
Install MySQL RDBMS + MySQL Workbench
RDBMS vs DB, create database
JDBC architecture: JDBC API + JDBC Driver
JDBC Driver types, transport types
Connector/J: JDBC Driver to MySQL
JDBC / SQL versions, SQL dialects
Connect to database
Driver, DriverManager, DataSource
Connection
JDBC URL
Connector/J properties
Query database
DDL and DML (TEXT)
Statement
Statement.executeUpdate: INSERT, UPDATE, DELETE
Get auto-generated keys
Statement.executeQuery: SELECT, ResultSet
Statement.execute
SQLException: errorCode and errorState
DAO Pattern
Альтернатива DAO: Transaction Script, Active Record, ORM
ResultSet
ResultSet: positioning and transition
ResultSet: type
ResultSet: concurrency
ResultSet: holdability
Optimizations
PreparedStatement = + precompilation — SQL injection
Batch update = vectorization
Connection pooling
Transactions
ACID properties
Transaction boundaries
Savepoints
Transaction isolation levels
MySQL transactions: MyISAM vs InnoDB
READ UNCOMMITED, Dirty Read “phenomena”
READ COMMITED, NonRepeatable Read “phenomena”
REPEATABLE READ, Phantom Read “phenomena”
SERIALIZABLE


Вторая часть


Local Tx-Manager: by-hands
Base realization: ThreadLocal Tx-context
@Transactional annotation
AOP realization of @Transactional
Application server = Tx-context + Auth-context + Thread management
Distributed Transactions
2PC-protocol
javax.jdbc.xa.* — XA-standart realization of 2PC-client
Distribured-Tx Manager Architecture
Query Meta-Information
Database meta-info
Table meta-info
Row meta-info
