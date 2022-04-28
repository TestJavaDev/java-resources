---
layout: default
title: Interval Problems
parent: Algorithms
nav_order: 12
permalink: /algorithms/interval_problems
---
<div align="center" markdown="1">
Interval Problems / Java resources / Tutorial

{: .fs-8 .fw-400 }
</div>

## Interval Problems

## Introduction
Interval problems typically involve a list of intervals, each represented by a start and end time/position. The goals are typically detecting or merging overlapping intervals.

These questions are often asked by FANNG. They are quite simple to explain but tricky to get right. The most important concept is how to find the overlap of two intervals.

## Fundamental concepts

## 1. Determine if there’s an overlap between two intervals:

First let’s think in the opposite direction, how would the intervals look like if they do NOT overlap?

End time of the first interval has to be earlier than the start time of the second interval.

![quick](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/interval/interval1.png)

i.e. x2 < y1 or y2 < x1

So the overlapping condition is the opposite

Not (x2 < y1 or y2 < x1)

## 2. Finding the overlap

The key formula here is the overlap of two interval is given by [max(x1, y1), min(x2, y2)].

![quick](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/interval/interval2.png)

Note that we can also answer question query #1 by comparing max(x1, y1) <= min(x2, y2).

As we will see in the examples, solving an interval problem becomes much easier if we can find the overlap.

## 3. Sort by start time
It’s very common to sort the intervals by start time as pre-processing for interval problems. We will see this in Merge Intervals.

## Problems:
* Merge Intervals
* Insert Interval

## Footnote:
For formula #1, If we want to go one-step further, we can reduce it by DeMorgan’s Law (Not (A or B) == Not A and Not B). This is equivalent to Not (x2 < y1) and Not (y2 < x1) which is equivalent to x2 >= y1 and y2 >= x1.
