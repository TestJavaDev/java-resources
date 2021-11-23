---
layout: default
title: JDBC, ORM
nav_order: 4
parent: References
permalink: /references/orm
has_children: true
---
<div align="center" markdown="1">
JDBC, ORM / Java resources / Grokking the interview

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
* JDBC Optimizations(important)
  * PreparedStatement = + precompilation — SQL injection  [first site](https://stackoverflow.com/questions/23845383/what-does-it-mean-when-i-say-prepared-statement-is-pre-compiled) [second site](https://stackoverflow.com/questions/1582161/how-does-a-preparedstatement-avoid-or-prevent-sql-injection)
  * Batch update = vectorization  [first site](https://www.codejava.net/java-se/jdbc/jdbc-batch-update-examples)  [second site](https://stackoverflow.com/questions/14264953/how-is-jdbc-batch-update-helpful)  [third site](http://tutorials.jenkov.com/jdbc/batchupdate.html)
  * Connection pooling  [first site](https://vladmihalcea.com/the-anatomy-of-connection-pooling/) [second  site](https://stackoverflow.com/questions/2835090/how-to-establish-a-connection-pool-in-jdbc)

### ORM
{: .label }

* Introduction
  * ORM implementations  [Hibernate](https://ru.wikipedia.org/wiki/Hibernate_(библиотека)) [OpenJPA](https://en.wikipedia.org/wiki/Apache_OpenJPA) [EсlipseLink](http://en.wikipedia.org/wiki/EclipseLink) [TopLink](http://en.wikipedia.org/wiki/TopLink)
  * Hibernate VS JDBC  [first site](https://habiletechnologies.com/blog/reasons-to-choose-hibernate-over-jdbc)
  * O/R Mismatch  [first site](https://uk.wikipedia.org/wiki/%D0%9E%D0%B1%27%D1%94%D0%BA%D1%82%D0%BD%D0%BE-%D1%80%D0%B5%D0%BB%D1%8F%D1%86%D1%96%D0%B9%D0%BD%D0%B8%D0%B9_%D1%80%D0%BE%D0%B7%D1%80%D0%B8%D0%B2)
  * JPA vs. Hibernate  [first site](https://dzone.com/articles/what-is-the-difference-between-hibernate-and-sprin-1) [second site]()
  * Schema Management   [first site](https://stackoverflow.com/questions/2585641/hibernate-jpa-db-schema-generation-best-practices) [second site](https://docs.jboss.org/hibernate/orm/5.2/userguide/html_single/chapters/schema/Schema.html)  [Flyway vs. Liquibase](https://habr.com/ru/company/haulmont/blog/440696/)
* Connection Management
  * Hibernate Connection Lifecycle, Open Session In View  [first site](http://java-latte.blogspot.com/2014/10/how-hibernate-works-and-its-architecture-and-Persistence-Lifecycle-of-hibernate.html) [second site](https://stackoverflow.com/questions/1103363/why-is-hibernate-open-session-in-view-considered-a-bad-practice) [third site](https://stackoverflow.com/questions/8724259/spring-hibernate-session-lifecycle)
  * Connection Monitoring  [first site](https://stackoverflow.com/questions/3522051/hibernate-monitoring-solution) [second site](https://vladmihalcea.com/connection-monitoring-jpa-hibernate/)
  * Hibernate Statistics  [first site](https://vladmihalcea.com/hibernate-statistics/)
* Types and Identifiers
  * JPA and Hibernate Types  [first site](https://vladmihalcea.com/a-beginners-guide-to-hibernate-types/) [second site](https://docs.jboss.org/hibernate/stable/core.old/reference/en/html/mapping-types.html)
  * Custom Hibernate Types  [first site](https://vladmihalcea.com/how-to-implement-a-custom-basic-type-using-hibernate-usertype/) [second site](https://stackoverflow.com/questions/35227986/implementing-custom-hibernate-type)
  * JPA and Hibernate Identifiers  [first site](https://vladmihalcea.com/jpa-entity-identifier-sequence/) [second site](https://thorben-janssen.com/jpa-generate-primary-keys/)
  * Hibernate Identifier Optimizers (e.g. hilo, pooled, pooled-lo)  [first site](https://stackoverflow.com/questions/25204019/how-to-use-the-pooled-lo-optimizer-with-hibernate) [second site](https://vladmihalcea.com/hibernate-hidden-gem-the-pooled-lo-optimizer/)
* Relationships
  * JPA and Hibernate Relationships  [first site](https://stackabuse.com/a-guide-to-jpa-with-hibernate-relationship-mapping/) [second site](https://thorben-janssen.com/ultimate-guide-association-mappings-jpa-hibernate/)
  * Equals and Hashcode  [first site](https://stackoverflow.com/questions/1638723/how-should-equals-and-hashcode-be-implemented-when-using-jpa-and-hibernate) [second site](https://vladmihalcea.com/the-best-way-to-implement-equals-hashcode-and-tostring-with-jpa-and-hibernate/) [third site](https://thorben-janssen.com/ultimate-guide-to-implementing-equals-and-hashcode-with-hibernate/)
  * ManyToOne  [first site](https://vladmihalcea.com/manytoone-jpa-hibernate/) [second site](https://qna.habr.com/q/62258)
  * OneToMany  [first site](https://vladmihalcea.com/the-best-way-to-map-a-onetomany-association-with-jpa-and-hibernate/) [second site](https://medium.com/@rajibrath20/the-best-way-to-map-a-onetomany-relationship-with-jpa-and-hibernate-dbbf6dba00d3)
  * OneToOne  [first site](https://vladmihalcea.com/the-best-way-to-map-a-onetoone-relationship-with-jpa-and-hibernate/) [second site](https://stackoverflow.com/questions/21762328/java-hibernate-onetoone-mapping)
  * ManyToMany  [first site](https://thorben-janssen.com/best-practices-for-many-to-many-associations-with-hibernate-and-jpa/) [second site](https://www.baeldung.com/jpa-many-to-many)
  
* Inheritance  [first site](https://habr.com/ru/post/337488/)
  * JPA Inheritance Basics  [first site](https://vladmihalcea.com/the-best-way-to-use-entity-inheritance-with-jpa-and-hibernate/)
  * Single Table Inheritance   [first site](https://vladmihalcea.com/the-best-way-to-map-the-single_table-inheritance-with-jpa-and-hibernate/) [second site](https://stackoverflow.com/questions/63656497/jpa-repository-with-single-table-inheritance-hibernate)
  * Discriminator Column  [first site](https://vladmihalcea.com/the-best-way-to-map-the-discriminatorcolumn-with-jpa-and-hibernate/) [second site](https://stackoverflow.com/questions/16772370/when-to-use-discriminatorvalue-annotation-in-hibernate)
  * Joined Inheritance  [first site](https://habr.com/ru/post/337488/)
  * TablePerClass Inheritance  [first site](https://stackoverflow.com/questions/3557879/hibernate-and-inheritance-table-per-class)
* Persistence Context
  * Persistence Context and Flushing Basics  [first site](https://vladmihalcea.com/a-beginners-guide-to-jpahibernate-flush-strategies/) [second site](https://vladmihalcea.com/hibernate-facts-knowing-flush-operations-order-matters/)
  * The AUTO FlushModeType  [first site](https://stackoverflow.com/questions/18149876/what-to-use-flush-mode-auto-or-commit)
  * Dirty Checking Mechanism  [first site](https://vladmihalcea.com/the-anatomy-of-hibernate-dirty-checking/) [second site](https://vladmihalcea.com/how-to-customize-hibernate-dirty-checking-mechanism/) [third site](https://stackoverflow.com/questions/5268466/how-does-hibernate-detect-dirty-state-of-an-entity-object)
  * Bytecode Enhancement Dirty Checking  [first site](https://vladmihalcea.com/how-to-enable-bytecode-enhancement-dirty-checking-in-hibernate/)
* Batching and Statement Caching
  * Statement Lifecycle and Execution Plans  [first site](https://vladmihalcea.com/execution-plan-sql-server/)
  * Statement Caching  [first site](https://vladmihalcea.com/hibernate-performance-tuning-tips/) [second site](https://stackoverflow.com/questions/17764142/does-hibernate-use-preparedstatement-by-default)
  * Statement Batching and Cascade Operations  [first site](https://vladmihalcea.com/how-to-batch-delete-statements-with-hibernate/) [second site](https://vladmihalcea.com/how-to-optimize-the-merge-operation-using-update-while-batching-with-jpa-and-hibernate/)
  * Batching Update Operations  [first site](https://www.codejava.net/frameworks/hibernate/how-to-execute-batch-insert-update-in-hibernate)
  * SQL Injection  [first site](https://habr.com/ru/company/parallels/blog/272589/)
  * Hibernate Cache  [first site](http://habrahabr.ru/post/135176/) [second site](http://habrahabr.ru/post/136375/) [third site](http://www.tutorialspoint.com/hibernate/hibernate_caching.htm) [fourth site](http://stackoverflow.com/questions/3663979/how-to-use-jpa2s-cacheable-instead-of-hibernates-cache) [fifth site](http://vladmihalcea.com/2015/06/08/how-does-hibernate-query-cache-work/) [sixth](https://www.javacodegeeks.com/2014/06/pitfalls-of-the-hibernate-second-level-query-caches.html)
* Fetching
  * Direct and Natural id fetching  [first site](https://vladmihalcea.com/the-best-way-to-map-a-naturalid-business-key-with-jpa-and-hibernate/)
  * DTO projections vs Entity queries  [first site](https://vladmihalcea.com/the-best-way-to-map-a-projection-query-to-a-dto-with-jpa-and-hibernate/) [second site](https://thorben-janssen.com/entities-dtos-use-projection/)
  * LAZY vs. EAGER  [first site](https://stackoverflow.com/questions/2990799/difference-between-fetchtype-lazy-and-eager-in-java-persistence-api)

-  Ресурсы:
- <a href="https://dou.ua/lenta/articles/how-to-use-hibernate/">Как использовать Hibernate</a>
- <a href="https://dou.ua/lenta/articles/hibernate-fetch-types/">Стратегии загрузки коллекций в Hibernate</a>
- <a href="http://akorsa.ru/2016/08/kak-rabotaet-flush-v-hibernate/">Hibernate flush()</a>
- <a href="http://akorsa.ru/2016/08/kak-rabotaet-flush-v-hibernate/">Hibernate flush()</a>
- Open Session in View   [first site](https://coderoad.ru/1103363/%D0%9F%D0%BE%D1%87%D0%B5%D0%BC%D1%83-Hibernate-Open-Session-in-View-%D1%81%D1%87%D0%B8%D1%82%D0%B0%D0%B5%D1%82%D1%81%D1%8F-%D0%BF%D0%BB%D0%BE%D1%85%D0%BE%D0%B9-%D0%BF%D1%80%D0%B0%D0%BA%D1%82%D0%B8%D0%BA%D0%BE%D0%B9) [second site](https://habr.com/ru/post/440734/)
- <a href="http://habrahabr.ru/post/265061/">JPA и Hibernate в вопросах и ответах</a>
- <a href="https://habr.com/ru/post/416851/">Hibernate</a>
- <a href="https://stackoverflow.com/questions/9108224/can-someone-explain-mappedby-in-jpa-and-hibernate">mappedBy in JPA and Hibernate</a>
- [Hibernate — о чем молчат туториалы](https://habr.com/ru/post/416851/)
- [Наследование в Hibernate: выбор стратегии](https://habrahabr.ru/post/337488/)
- [Field vs property access](http://stackoverflow.com/a/6084701/548473)
- <a href="http://stackoverflow.com/questions/1069992/jpa-entitymanager-why-use-persist-over-merge">Merge vs Persist</a>
- <a href="https://developer.jboss.org/wiki/OpenSessionInView">Паттерн "открытие транзакции в фильтре"</a> и <a href="http://stackoverflow.com/questions/1103363/why-is-hibernate-open-session-in-view-considered-a-bad-practice">почему это bad-practice</a>

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








