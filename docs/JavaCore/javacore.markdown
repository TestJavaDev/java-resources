---
layout: default
title: JavaCore
nav_order: 1
permalink: /javacore
has_children: true
---
<div align="center" markdown="1">
JavaCore / Java resources / Articles

{: .fs-6 .fw-300 }
</div>

- <a href="https://habrahabr.ru/post/283290/">Сравнение EE и Spring в комментариях</a>
- [The Top 20 Most Popular Java Libraries](https://dzone.com/articles/the-top-100-java-libraries-in-2016-after-analyzing)
- [Guava Wiki](https://github.com/google/guava/wiki)
  - [Apache Commons](https://commons.apache.org/)
  - [Spring Boot cache providers](http://docs.spring.io/spring-boot/docs/current/reference/html/boot-features-caching.html#_supported_cache_providers)
- [Release 21.0: Java 8!](https://github.com/google/guava/wiki/Release21)
- [118 слайдов от Егора Чернышева](https://www.slideshare.net/echernyshev/guava-41982734)

- [Java](http://ru.wikipedia.org/wiki/Java), [JVM](http://ru.wikipedia.org/wiki/Виртуальная_машина_Java), [JIT-компиляция](http://ru.wikipedia.org/wiki/JIT) (wiki)
- [Что такое Java? История создания](http://www.intuit.ru/studies/courses/16/16/lecture/27105)
- [Что такое JDK? Введение в средства разработки Java](https://topjava.ru/blog/what-is-the-jdk)
- [Что такое JRE? Введение в среду выполнения Java](https://topjava.ru/blog/what-is-the-jre)
- [Programming languages TIOBE Index](http://www.tiobe.com/index.php/content/paperinfo/tpci/index.html)

![jvm](https://cloud.githubusercontent.com/assets/18701152/15219296/e6c67e86-186b-11e6-986f-651a87deec6c.png)

- [ME](http://ru.wikipedia.org/wiki/Java_Platform,_Micro_Edition), [SE](https://ru.wikipedia.org/wiki/Java_Platform,_Standard_Edition), [EE](http://ru.wikipedia.org/wiki/Java_Platform,_Enterprise_Edition) (wiki)
- [Java Microbenchmark JMH](http://openjdk.java.net/projects/code-tools/jmh/)
- [Oracle Java8 Home](http://docs.oracle.com/javase/8/docs/index.html)
- <a href="http://www.intuit.ru/studies/courses/16/16/info">Интуит. Программирование на Java</a>
- <a href="http://ggenikus.github.io/blog/2014/05/04/gc">Основы Java garbage collection</a>
- <a href="https://habrahabr.ru/post/134102/">Размер Java объектов</a>
- <a href="http://www.quizful.net/post/java-reflection-api">Введение в Java Reflection API</a>
- <a href="https://habrahabr.ru/users/tarzan82/topics/">Структуры данных в картинках</a>
- <a href="https://habrahabr.ru/company/luxoft/blog/157273/">Обзор java.util.concurrent.*</a>
- <a href="http://www.skipy.ru/technics/synchronization.html">Синхронизация потоков</a>
- <a href="http://java67.blogspot.ru/2014/08/difference-between-string-literal-and-new-String-object-Java.html">String literal pool</a>
- <a href="https://habrahabr.ru/post/132241/">Маленькие хитрости Java</a>
-  <a href="https://github.com/winterbe/java8-tutorial">A Guide to Java 8</a>
- [Implementing equals() and hashCode()](https://access.redhat.com/documentation/en-us/jboss_enterprise_application_platform/4.3/html/hibernate_reference_guide/persistent_classes-implementing_equals_and_hashcode)

- Оптимально использовать уникальные бизнес-поля, но обычно таких нет, и чаще всего используются PK с ограничением, что он может быть `null` у новых объектов, и нельзя объекты сравнивать через `equals() and hashCode()` в бизнес-логике (например, тестах).

- [equals() and hashcode() when using JPA and Hibernate](https://stackoverflow.com/questions/1638723)
- [Методы класса String, появившиеся в Java 11](https://topjava.ru/blog/java-11-string-api-additions)
- [Модификатор static](http://www.intuit.ru/studies/courses/16/16/lecture/27119)
- [10 заметок о модификаторе static в Java](http://info.javarush.ru/translation/2014/04/15/10-заметок-о-модификаторе-Static-в-Java.html)
- [Класс Object. Контракт equals/hashCode](http://www.intuit.ru/studies/courses/16/16/lecture/27129?page=1)
- [Абстрактные классы](https://www.youtube.com/watch?v=ZjiFL2Yo2fw) (youtube)
- [Интерфейсы](http://www.intuit.ru/studies/courses/16/16/lecture/27119?page=3)
- [Полиморфизм](http://www.intuit.ru/studies/courses/16/16/lecture/27119?page=4)
- [Отличия абстрактного класса от интерфейса](https://ru.stackoverflow.com/questions/235352/Отличия-абстрактного-класса-от-интерфейса-abstract-class-and-interface)
- [Что такое полиморфизм?](https://github.com/ichimax/Core-Java-Interview-Questions/blob/master/Questions/1.%20OOP.md#%D0%A7%D1%82%D0%BE-%D1%82%D0%B0%D0%BA%D0%BE%D0%B5-%D0%BF%D0%BE%D0%BB%D0%B8%D0%BC%D0%BE%D1%80%D1%84%D0%B8%D0%B7%D0%BC)
- [Ключевое слово static](https://www.youtube.com/watch?v=GZzVfeY7yEM) (youtube)
- [Интерфейсы, абстрактные классы, полиморфизм](https://www.youtube.com/watch?v=7NMFk2oj1-c&index=4&list=PLkKunJj_bZefB1_hhS68092rbF4HFtKjW) (youtube)
- [Разбираемся с hashCode() и equals()](https://habrahabr.ru/post/168195/)
- [Строки в Java](https://urvanov.ru/2016/04/20/java-8-строки/)
- [Кодировка в Java](http://www.skipy.ru/technics/encodings.html)
- [Ошибки при использовании строк](http://www.skipy.ru/technics/strings.html)
- [Обработка строк в Java](https://habrahabr.ru/post/260767/)
- [StringBuilder vs StringBuffer](https://stackoverflow.com/questions/355089/difference-between-stringbuilder-and-stringbuffer?rq=1)
- [String vs StringBuffer vs StringBuilder](https://www.journaldev.com/538/string-vs-stringbuffer-vs-stringbuilder)
- [String literal pool](http://java67.blogspot.ru/2014/08/difference-between-string-literal-and-new-String-object-Java.html)
- [Java 8 аннотации](https://urvanov.ru/2016/03/30/java-8-аннотации/)
- [Reflection для начинающих](https://youtu.be/XJQuBXWADZg) (youtube)
- [Руководство по Java Reflection API](http://javadevblog.com/polnoe-rukovodstvo-po-java-reflection-api-refleksiya-na-primerah.html)
- [Java Reflection Example Tutorial](https://www.journaldev.com/1789/java-reflection-example-tutorial)
- [The Reflection API](https://docs.oracle.com/javase/tutorial/reflect/)
- [What is reflection and why is it useful?](https://stackoverflow.com/questions/37628/what-is-reflection-and-why-is-it-useful) В нашем проекте Reflection используют JUnit и будут использовать библиотеки работы с XML и JSON
 - [Фреймворк для модульного тестирования JUnit](http://junit.org/)
 - [Тестирование с помощью JUnit (Test Case)](http://www.javenue.info/post/19)
 - [Тестирование кода Java с помощью фреймворка JUnit](https://www.youtube.com/watch?v=z9jEVLCF5_w) (youtube)
 - [Исключения (Exceptions)](http://proglang.su/java/exceptions)
 - [Статья про исключения](http://developer.alexanderklimov.ru/android/java/exception.php)
 - Про исключения также можно почитать в книге Джошуа Блоха - ["Java. Эффективное программирование"](https://www.ozon.ru/context/detail/id/21724143/)
 - [Конструктор](http://info.javarush.ru/javarush_articles/2015/12/04/Конструкторы-классов-Java-JDK-1-5-.html)
 - [Ключевые слова: this, super](http://info.javarush.ru/grishin/2015/03/31/Разница-между-ключевыми-словами-this-и-super-в-Java.html)
 - [Exceptions](https://docs.oracle.com/javase/tutorial/essential/exceptions/)
 - [Checked vs unchecked exception explanation](https://stackoverflow.com/questions/6115896/java-checked-vs-unchecked-exception-explanation)





