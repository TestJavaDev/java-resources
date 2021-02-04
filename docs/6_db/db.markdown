---
layout: default
title: DB, JDBC, ORM
nav_order: 6
permalink: /db_jdbc_orm
has_children: true
---
<div align="center" markdown="1">
DB, JDBC, ORM / Java resources / Grokking the interview

{: .fs-6 .fw-300 }
</div>

### JDBC
{: .label }

* Intro
  * RDBMS vs DB  [first site](https://stackoverflow.com/questions/18419137/what-is-the-difference-between-dbms-and-rdbms)
  * JDBC Driver types, transport types  [first site](https://proselyte.net/tutorials/jdbc/introduction/) [second site](https://www.tutorialspoint.com/jdbc/jdbc-driver-types.htm) [third site](https://www.progress.com/faqs/datadirect-jdbc-faqs/what-are-the-types-of-jdbc-drivers)
* Connect to database
  * Driver, DriverManager, DataSource  [first site](https://stackoverflow.com/questions/15198319/why-do-we-use-a-datasource-instead-of-a-drivermanager) [second site](http://java-online.ru/jdbc-drivermanager.xhtml) [third site](https://overcoder.net/q/80648/%D0%BF%D0%BE%D1%87%D0%B5%D0%BC%D1%83-%D0%BC%D1%8B-%D0%B8%D1%81%D0%BF%D0%BE%D0%BB%D1%8C%D0%B7%D1%83%D0%B5%D0%BC-datasource-%D0%B2%D0%BC%D0%B5%D1%81%D1%82%D0%BE-drivermanager)
  * Connection, JDBC URL   [first site](https://proselyte.net/tutorials/jdbc/connection/) [second site](https://www.tutorialspoint.com/jdbc/jdbc-db-connections.htm)
* Query database
  * DDL and DML [first site](https://info-comp.ru/what-is-ddl-dml-dcl-tcl)
  * Statement  [first site](https://proselyte.net/tutorials/jdbc/statements/) [second site](https://www.tutorialspoint.com/jdbc/jdbc-statements.htm)
  * Statement.executeUpdate: INSERT, UPDATE, DELETE  [first site](https://www.codota.com/code/java/methods/java.sql.Statement/executeUpdate)
  * Statement.executeQuery: SELECT, ResultSet  [first site](https://www.codota.com/code/java/methods/java.sql.Statement/executeQuery)
  * Statement.execute  [first site](http://tutorials.jenkov.com/jdbc/statement.html) [second site](https://www.codota.com/code/java/methods/java.sql.Statement/execute)
  * SQLException: errorCode and errorState  [first site](https://docs.microsoft.com/en-us/sql/connect/jdbc/handling-errors?view=sql-server-ver15) [second site](https://www.codota.com/code/java/classes/java.sql.SQLException) [third site](https://www.codota.com/code/java/methods/java.sql.Statement/getWarnings)
* ResultSet
  * ResultSet: (positioning, transition, type, concurrency, holdability)  [first site](https://proselyte.net/tutorials/jdbc/result-set/) [second site](https://stackoverflow.com/questions/55531375/why-is-reading-a-jdbc-resultset-by-position-faster-than-by-name-and-how-much-fas)
* Optimizations(important)
  * PreparedStatement = + precompilation — SQL injection  [first site](https://stackoverflow.com/questions/23845383/what-does-it-mean-when-i-say-prepared-statement-is-pre-compiled) [second site](https://stackoverflow.com/questions/1582161/how-does-a-preparedstatement-avoid-or-prevent-sql-injection)
  * Batch update = vectorization  [first site](https://www.codejava.net/java-se/jdbc/jdbc-batch-update-examples)  [second site](https://stackoverflow.com/questions/14264953/how-is-jdbc-batch-update-helpful)  [third site](http://tutorials.jenkov.com/jdbc/batchupdate.html)
  * Connection pooling  [first site](https://stackoverflow.com/questions/2835090/how-to-establish-a-connection-pool-in-jdbc)
* Transactions for JDBC
  * Transaction manager
  * Transaction boundaries
  * Savepoints //Connection.commit()/.rollback()/.setAutoCommit(), savepoint
  * SQLTransientException

### ORM
{: .label }

* Introduction
  * O/R Mismatch
  * JPA vs. Hibernate
  * Logging SQL Statements 
  * Schema Management 
* Connection Management
  * Connection Management and Hibernate Connection Providers
  * Hibernate Connection Lifecycle
  * Connection Monitoring
  * Hibernate Statistics
* Types and Identifiers
  * JPA and Hibernate Types
  * Custom Hibernate Types
  * The hibernate-types project
  * JPA and Hibernate Identifiers
  * Hibernate Identifier Optimizers (e.g. hilo, pooled, pooled-lo)
* Relationships
  * JPA and Hibernate Relationships
  * Equals and Hashcode
  * ManyToOne
  * OneToMany
  * OneToOne
  * ManyToMany
  
* Inheritance
  * ORM implementations  [Hibernate](https://ru.wikipedia.org/wiki/Hibernate_(библиотека)) [OpenJPA](https://en.wikipedia.org/wiki/Apache_OpenJPA) [EсlipseLink](http://en.wikipedia.org/wiki/EclipseLink) [TopLink](http://en.wikipedia.org/wiki/TopLink)
  * Hibernate VS JDBC  [first site](https://habiletechnologies.com/blog/reasons-to-choose-hibernate-over-jdbc)
  * JPA Inheritance Basics  [first site]() [second site]() [third site]() [fourth site]() [fifth site]()
  * Single Table Inheritance   [first site]() [second site]() [third site]() [fourth site]() [fifth site]()
  * Discriminator Column  [first site]() [second site]() [third site]() [fourth site]() [fifth site]()
  * Joined Inheritance  [first site]() [second site]() [third site]() [fourth site]() [fifth site]()
  * TablePerClass Inheritance  [first site]() [second site]() [third site]() [fourth site]() [fifth site]()
  * Hibernate Cache  [first site](http://habrahabr.ru/post/135176/) [second site](http://habrahabr.ru/post/136375/) [third site](http://www.tutorialspoint.com/hibernate/hibernate_caching.htm) [fourth site](http://stackoverflow.com/questions/3663979/how-to-use-jpa2s-cacheable-instead-of-hibernates-cache) [fifth site](http://vladmihalcea.com/2015/06/08/how-does-hibernate-query-cache-work/) [sixth](https://www.javacodegeeks.com/2014/06/pitfalls-of-the-hibernate-second-level-query-caches.html)
* Persistence Context  [first site]() [second site]() [third site]() [fourth site]() [fifth site]()
  * Persistence Context and Flushing Basics  [first site]() [second site]() [third site]() [fourth site]() [fifth site]()
  * Action Queue  [first site]() [second site]() [third site]() [fourth site]() [fifth site]()
  * The AUTO FlushModeType  [first site]() [second site]() [third site]() [fourth site]() [fifth site]()
  * Dirty Checking Mechanism  [first site]() [second site]() [third site]() [fourth site]() [fifth site]()
  * Bytecode Enhancement Dirty Checking  [first site]() [second site]() [third site]() [fourth site]() [fifth site]()
* Batching and Statement Caching  [first site]() [second site]() [third site]() [fourth site]() [fifth site]()
  * Statement Lifecycle and Execution Plans  [first site]() [second site]() [third site]() [fourth site]() [fifth site]()
  * Statement Caching
  * Statement Batching and Cascade Operations
  * Batching Update Operations
  * SQL Injection
* Fetching
  * Direct and Natural id fetching
  * DTO projections vs Entity queries
  * LAZY vs. EAGER
  * Query-time fetching
  * Pagination queries
  
* Transactions and Concurrency Control
  * ACID  [first site]() [second site]() [third site]() [fourth site]() [fifth site]()
  * Phenomena  [first site]() [second site]() [third site]() [fourth site]() [fifth site]()
    * Dirty Write,  [first site]() [second site]() [third site]() [fourth site]() [fifth site]()
    * Dirty Read,  [first site]() [second site]() [third site]() [fourth site]() [fifth site]()
    * Non-Repeatable Read,  [first site]() [second site]() [third site]() [fourth site]() [fifth site]()
    * Phantom Read,  [first site]() [second site]() [third site]() [fourth site]() [fifth site]()
    * Read Skew,  [first site]() [second site]() [third site]() [fourth site]() [fifth site]()
    * Write Skew,  [first site]() [second site]() [third site]() [fourth site]() [fifth site]()
    * Lost Update  [first site]() [second site]() [third site]() [fourth site]() [fifth site]()
  * 2PL (Two-Phase Locking)  [first site]() [second site]() [third site]() [fourth site]() [fifth site]()
  * MVCC (Multi-Version Concurrency Control)  [first site]() [second site]() [third site]() [fourth site]() [fifth site]()
  * Isolation levels and database concurrency control  [first site]() [second site]() [third site]() [fourth site]() [fifth site]()
  * Logical vs. physical clock optimistic locking:  [first site]() [second site]() [third site]() [fourth site]() [fifth site]()
    * OPTIMISTIC,  [first site]() [second site]() [third site]() [fourth site]() [fifth site]()
    * OPTIMISTIC FORCE INCREMENT,  [first site]() [second site]() [third site]() [fourth site]() [fifth site]()
    * PESSIMISTIC FORCE INCREMENT,  [first site]() [second site]() [third site]() [fourth site]() [fifth site]()
    * PESSIMISTIC READ,  [first site]() [second site]() [third site]() [fourth site]() [fifth site]()
    * PESSIMISTIC WRITE  [first site]() [second site]() [third site]() [fourth site]() [fifth site]()
  * Versionless optimistic locking  [first site]() [second site]() [third site]() [fourth site]() [fifth site]()
  * JPA physical and optimistic lock types  [first site]() [second site]() [third site]() [fourth site]() [fifth site]()
  * Skip locked and queuing access  [first site]() [second site]() [third site]() [fourth site]() [fifth site]()
  * Preventing lost updates in long conversations  [first site]() [second site]() [third site]() [fourth site]() [fifth site]()
  
* Database, Application and Hibernate Caching
  * Database caching
  * Application-level caching
  * Second-level caching
  * Cache synchronization strategies
  * Cache concurrency strategies
    * READ ONLY,
    * NONSTRICT READ WRITE,
    * READ WRITE,
    * TRANSACTIONAL
  * Collection Cache
  * Query Cache
  
* Local Tx-Manager: by-hands  [first site]() [second site]() [third site]() [fourth site]() [fifth site]()
  * Base realization: ThreadLocal Tx-context  [first site]() [second site]() [third site]() [fourth site]() [fifth site]()
  * @Transactional annotation  [first site]() [second site]() [third site]() [fourth site]() [fifth site]()
  * AOP realization of @Transactional  [first site]() [second site]() [third site]() [fourth site]() [fifth site]()
  * Application server = Tx-context + Auth-context + Thread management  [first site]() [second site]() [third site]() [fourth site]() [fifth site]()
* Distributed Transactions
  * 2PC-protocol  [first site]() [second site]() [third site]() [fourth site]() [fifth site]()
  * javax.jdbc.xa.* — XA-standart realization of 2PC-client  [first site]() [second site]() [third site]() [fourth site]() [fifth site]()
  * Distribured-Tx Manager Architecture  [first site]() [second site]() [third site]() [fourth site]() [fifth site]()
*  Query Meta-Information  [first site]() [second site]() [third site]() [fourth site]() [fifth site]()
  * Database meta-info  [first site]() [second site]() [third site]() [fourth site]() [fifth site]()
  * Table meta-info  [first site]() [second site]() [third site]() [fourth site]() [fifth site]()
  * Row meta-info  [first site]() [second site]() [third site]() [fourth site]() [fifth site]()


- <a href="https://dou.ua/lenta/articles/hibernate-fetch-types/">Стратегии загрузки коллекций в Hibernate</a>
-  <a href="http://habrahabr.ru/post/265061/">JPA и Hibernate в вопросах и ответах</a>
- [Hibernate — о чем молчат туториалы](https://habr.com/ru/post/416851/)
- [Наследование в Hibernate: выбор стратегии](https://habrahabr.ru/post/337488/)
- [Field vs property access](http://stackoverflow.com/a/6084701/548473)

- <a href="http://validator.hibernate.org">hibernate-validator</a>
- <a href="http://stackoverflow.com/questions/8994864/how-would-i-specify-a-hibernate-pattern-annotation-using-a-regular-expression">Validate by RegExp</a>
- <a href="http://stackoverflow.com/questions/13027214">Do not use `CascadeType` for @ManyToOne</a>
- <a href="http://stackoverflow.com/questions/836569">CascadeType meaning</a>
- <a href="https://en.wikibooks.org/wiki/Java_Persistence/ElementCollection">No cascade option on an ElementCollection, the target objects are always persisted, merged, removed with their parent.</a>
- <a href="http://stackoverflow.com/questions/21149660">Create ON DELETE CASCADE: `@OnDelete`</a>
- <a href="http://stackoverflow.com/questions/3087040">Hibernate second level cache and ON DELETE CASCADE in database schema</a>
- [`orphanRemoval=true` vs `CascadeType.REMOVE`](http://stackoverflow.com/a/19645397/548473)
- [JPA `cascade/orphanRemoval` doesn't work with `NamedQuery`](http://stackoverflow.com/questions/7825484/jpa-delete-where-does-not-delete-children-and-throws-an-exception)


-  Ресурсы:
- <a href="http://stackoverflow.com/questions/1069992/jpa-entitymanager-why-use-persist-over-merge">Merge vs Persist</a>
- <a href="https://developer.jboss.org/wiki/OpenSessionInView">Паттерн "открытие транзакции в фильтре"</a> и <a href="http://stackoverflow.com/questions/1103363/why-is-hibernate-open-session-in-view-considered-a-bad-practice">почему это bad-practice</a>



### DB
{: .label }

* Реляционные базы данных (MySQL)
  * Устанавливаем, администрируем
  * Физическая организация данных
  * реляционная алгебра, реляционное исчисление
  * SQL types, CREATE/ALTER/DELETE table
* Логическое проектирование
  * ER-моделирование
  * Нормальные формы, денормализация
  * Целостность данных
  * Транзакции
* Физическое проектирование
  * Индексы
  * Блокировки
* Документно-ориентированные (MongoDB)
  * архитектура и особенности MongoDB
  * работаем с MongoDB на Java
* Key-value хранилища (Riak)
  * архитектура и особенности Riak
  * работаем с Riak на Java
  
- <a href="https://docs.google.com/document/d/1ul1jH7sccyQVqpjItdFo_OQI9YxJV3V5hxqI7xa-YPM">DB Migration rules</a>
- [Опыт 1440 миграций баз данных](https://habr.com/company/wrike/blog/414441/)
-  [BoneCP to be deprecated ](https://stackoverflow.com/a/1662916/548473)
-  Выбор реализации пула коннектов: <a href="https://commons.apache.org/proper/commons-dbcp/">Commons Database Connection Pooling</a>, <a href="https://github.com/brettwooldridge/HikariCP">HikariCP</a>
-  <a href="https://habrahabr.ru/post/269023/">Самый быстрый пул соединений на java (читаем комменты)</a>
-  <a href="http://blog.ippon.fr/2013/03/13/improving-the-performance-of-the-spring-petclinic-sample-application-part-3-of-5">Tomcat pool</a>
- [Оптимизация запросов. Основы EXPLAIN в PostgreSQL](https://habrahabr.ru/post/203320/)
- [Оптимизация запросов. Часть 2](https://habrahabr.ru/post/203386/)
- [Оптимизация запросов. Часть 3](https://habrahabr.ru/post/203484/)
- [Документация Postgres: индексы](https://postgrespro.ru/docs/postgresql/9.6/indexes.html)
- [Стратегии работы с транзакциями, pаспространенные ошибки](https://www.ibm.com/developerworks/ru/library/j-ts1/index.html)
- <a href="https://ru.wikipedia.org/wiki/Транзакция_(информатика)">wiki Транзакция</a>
- <a href="https://jira.spring.io/browse/DATAJPA-601">readOnly и Propagation.SUPPORTS</a>
- <a href="http://www.ibm.com/developerworks/ru/library/j-ts1/">Стратегии работы с транзакциями: Распространенные ошибки</a>
- <a href="http://habrahabr.ru/post/208400/">Принципы работы СУБД. MVCC</a>
- <a href="https://ru.wikipedia.org/wiki/MVCC">MVCC</a>
- <a href="http://ru.wikipedia.org/wiki/Транзакция_(информатика)">Транзакция. ACID. Уровни изоляции транзакций.</a>
- <a href="https://www.ibm.com/developerworks/ru/library/j-ts2/">Стратегии работы с транзакциями</a>
- [DB-Engines Ranking](http://db-engines.com/en/ranking)
- [Реляционная СУБД](https://ru.wikipedia.org/wiki/Реляционная_СУБД) (wiki)
- [Введение в базы данных](http://www.codenet.ru/progr/vbasic/vb_db/1.php)
- [Реляционные базы vs NoSQL](http://habrahabr.ru/post/103021). SQL. Денормализация. PK, FK, Cascade
- [PostgreSQL: надёжность](https://ru.wikipedia.org/wiki/PostgreSQL#Качество_исходного_кода)
- [Работа с базами данных из IDEA](https://habrahabr.ru/company/JetBrains/blog/204064)
- [IDEA Database tools](https://www.jetbrains.com/datagrip/features)
- [Как работает реляционная БД](https://habrahabr.ru/company/mailru/blog/266811)
- [SQL ключи во всех подробностях](https://habrahabr.ru/company/oleg-bunin/blog/348172)
- [Книги по postgreSQL](https://postgrespro.ru/education/books)
- [Интерактивная обучалка по postgreSQL](https://www.pgexercises.com/)
- <a href="http://ru.wikipedia.org/wiki/Транзакция_(информатика)">Транзакция. ACID.</a> <a href="https://ru.wikipedia.org/wiki/Уровень_изолированности_транзакций">Уровни изоляции транзакций.</a>
- <a href="http://www.osp.ru/pcworld/2009/07/9708191/">Уровни изоляции транзакций в SQL</a>
- <a href="https://habr.com/ru/post/120003/">БД Oracle для программиста</a>

### Database Performance Tuning
{: .label }

### Blog
{: .label }

- [Vlad Mihalcea High-Performance Java Persistence Book ](https://vladmihalcea.com/books/high-performance-java-persistence/)
- [The best Tutorials on High-Performance Hibernate](https://vladmihalcea.com/tutorials/hibernate/)

### Video
{: .label }

- <a href="https://www.youtube.com/watch?v=dFASbaIG-UU">Видео: Вячеслав Круглов — Как начинающему Java-разработчику подружиться со своей базой данных?</a>
- <a href="http://www.youtube.com/watch?v=YzOTZTt-PR0">Видео: Николай Алименков — Босиком по граблям Hibernate</a>
- <a href="https://www.youtube.com/watch?v=-EpP0Vo63FM">Hibernate, how the magic is really done?</a>   - [code](https://github.com/xpinjection/hibernate-basics)
- <a href="https://www.youtube.com/watch?v=b52Qz6qlic0">Видео: Николай Алименков — Сделаем Hibernate снова быстрым</a>   - [code](https://github.com/xpinjection/hibernate-performance)
- <a href="https://www.youtube.com/watch?list=PLYj3Bx1JM6Y7BKivc3eZwRUhWwBmbIFXg&v=V-ljsrVy6pE">Hibernate performance tuning (Mikalai Alimenkou /Igor Dmitriev)</a>
- <a href="http://www.youtube.com/watch?v=1KphwODu1gg">Видео: работа в ZK с OpenJPA (в чем Hibernate хуже)</a>








