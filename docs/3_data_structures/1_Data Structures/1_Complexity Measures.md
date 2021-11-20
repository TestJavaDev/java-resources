---
layout: default
title: Complexity Measures
parent: Data Structures
grand_parent: Data Structures and Algorithms
nav_order: 1
permalink: /data_structures/structures/complexity_measures
---
<div align="center" markdown="1">
Complexity Measures / Java resources / Tutorial

{: .fs-8 .fw-400 }
</div>

## Comparing Algorithms

## Introduction
There are typically several different algorithms to solve a given computational problem. It is natural, then, to compare these alternatives. But how do we know if algorithm A is better than algorithm B?

## Important Criteria: Time and Space
One important factor that determines the “goodness” of an algorithm is the amount of time it takes to solve a given problem. If algorithm A takes less time to solve the same problem than does algorithm B, then algorithm A is considered better.

Another important factor in comparing two algorithms is the amount of memory required to solve a given problem. The algorithm that requires less memory is considered better.

## Comparing Execution Time
For the remainder of this lesson, we will focus on the first factor, i.e., execution time. How do we compare the execution time of two algorithms?

## Experimental Evaluation
Well, we could implement the two algorithms and run them on a computer while measuring the execution time. The algorithm with less execution time wins. One thing is for sure; this comparison must be made in a fair manner. Let’s try to punch holes into this idea:
* An algorithm might take longer to run on an input of greater size. Thus, algorithms being compared must be tested on the same input size. But that’s not all. Due to the presence of conditional statements, for a given input size, even the same algorithm’s running time may vary with the actual input given to it. This means that the algorithms being compared must be tested on the same input. Since one algorithm may be disadvantaged over another for a specific input, we must test the algorithms exhaustively on all possible input values. This is just not possible.
* The algorithms being compared must first be implemented. What if the programmer comes up with a better implementation of one algorithm than the other? What if the compiler optimizes one algorithm more than it does the other? There’s so much that can compromise the fairness at this stage.
* The programs implementing the two algorithms must be tested on exactly the same hardware and software environment. Far fetched as it may be, we could assign a single machine for all scientists to test their algorithms on. Even if we did, the task scheduling in modern-day operating systems involves a lot of randomness. What if the program corresponding to “the best” algorithm encounters an excessive number of the hardware interrupts? It is impossible to guarantee the same hardware/software environment to ensure a fair comparison.

## Analytical Evaluation
The above list highlights some of the factors that make fair experimental evaluation of algorithms impossible. Instead, we are forced to make an analytical/theoretical comparison. The two key points that we hold on to, from the previous discussion, is that we must compare algorithms for the same input size and consider all possible inputs of the given size. Here is how it is done.

We assume a hypothetical computer on which some primitive operations are executed in a constant amount of time. We consider a specific input size, say, n. We then count the number of primitive operations executed by an algorithm for a given input. The algorithm that results in fewer primitive operations is considered better.

What constitutes a primitive operation, though? You can think of these as simple operations that are typically implemented as processor instructions. These operations include assignment to a variable or array index, reading from a variable or array index, comparing two values, arithmetic operations, a function call, etc.

What is not considered a primitive operation? Consider a function call, for instance. When a function is called, all the statements in that function are executed. So, we can’t consider each function invocation as a single primitive operation. Similarly, displaying an entire array is not a primitive operation.

The number of times conditional statements run depends on the actual input values. Sometimes a code block is executed, some times it isn’t. So, how do we account for conditional statements? We can adopt one of three strategies: best case analysis, average-case analysis, and worst-case analysis.

## Best Case Analysis
In the best case analysis, we consider the specific input that results in the execution of the fewest possible primitive operations. This gives us a lower bound on the execution time of that algorithm for a given input size.

## Worst-Case Analysis
In the worst-case analysis, we consider the specific input that results in the execution of the maximum possible primitive operations. This gives us an upper bound on the execution time of that algorithm for a given input size.

## Average Case Analysis
In the average case analysis, we try to determine the average number of primitive operations executed for all possible inputs of a given size. This is not as easy as it may sound to the uninitiated. In order to compute the average-case running time of an algorithm, we must know the relative frequencies of all possible inputs of a given size. We compute the weighted average of the number of primitive operations executed for each input. But how can we accurately predict the distribution of inputs? If the algorithm encounters a different distribution of inputs in the field, our analysis is useless.

## The Verdict
The best-case analysis has limited value because what if you deploy that algorithm and the best case input rarely occurs. We feel that the worst-case analysis is more useful because whatever answer it gives you, you can be sure that no matter what, algorithm A wouldn’t incur more time than that. Unless otherwise specified, our analysis in this course will be worst-case running time.

The running time of an algorithm computed in the aforementioned way is also known as its time complexity. Another term that you will often hear is an algorithm’s space complexity. The space complexity of an algorithm is the amount of additional or auxiliary memory space that the algorithm requires. This is memory space other than the actual input itself. We will see examples of evaluating the space complexity of an algorithm later on in this course.

## Analyzing a Simple Java Program
Suppose that instead of an algorithm, we were given Java code. Here’s how we can analyze the algorithm underlying the given program. Let’s count the number of primitive operations in the program given below:

![arr](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/arr/arr6.png)

Let’s analyze the main() function. There is a variable assignment on line number 5, so that’s 1 primitive operation. A variable’s value is accessed, an addition is performed, and then an assignment takes place on line 6, so that’s three primitive operations. A variable’s value is accessed and then displayed on line 7, so that’s two primitive operations. So, overall there are 6 primitive operations in the above program. This analysis is also presented in the following table:

![arr](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/arr/arr7.png)

![arr](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/arr/arr8.png)
![arr](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/arr/arr9.png)
![arr](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/arr/arr10.png)
![arr](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/arr/arr11.png)

Note that there is no notion of input size in this simple example since there is no input to this program. Algorithms for which the time complexity is independent of the input size are known as constant-time algorithms.

## Example 1: Measuring Time Complexity of a Single Loop Algorithm

## A For Loop With n Iterations
Now, let’s consider what happens when a loop is involved. Consider the following Java program:

![arr](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/arr/arr12.png)

Let’s count the number of primitive operations in the above program. Let’s come to lines 4 and 5 where variable initializations are taking place, which account for one primitive operation, each.

Line 6 is a loop statement. To count the number of primitive operations on that line, we must dissect it into its constituents: the initialization, the increment, and the test. The initialization occurs only once and is counted as one primitive operation. The increment (i++i++) operation must read the current value of variable ii, add 11 to it and store the result back in variable ii. That’s three primitive operations. The test operation (i < ni<n) must read the current value of the variables ii and nn, then compare them. So, that’s three primitive operations as well.

Unlike the initialization in the loop, the increment and test parts are repeated in the iterations of the for loop. The comparison is performed n + 1 times, with the loop index at i = 0, 1, 2, ... , n. The increment operation, on the other hand, is performed nn times, when the loop index is at i = 0, 1, 2, ..., n - 1. When the index ii reaches nn, the loop terminates, and the increment is not performed. Thus, line 6 accounts for a total of 1 + 3\times( n + 1 ) + 3\times n = 6n + 4 primitive operations.

Line 7 involves reading a variable’s value, adding two integers, and assigning the result to a variable: 3 primitive operations. This line is repeated nn times since the loop is entered when index i = 0, 1, 2,... , n - 1. Thus, line 7 accounts for 3n primitive operations. Line 9 accounts for two primitive operations. This analysis is summarized in the following table:

![arr](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/arr/arr13.png)

![arr](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/arr/arr14.png)
![arr](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/arr/arr15.png)
![arr](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/arr/arr16.png)
![arr](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/arr/arr17.png)
![arr](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/arr/arr18.png)
![arr](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/arr/arr19.png)
![arr](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/arr/arr20.png)
![arr](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/arr/arr21.png)
![arr](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/arr/arr22.png)

## Example 2: Time Complexity of an Algorithm With Nested Loops

## A Program With Nested for Loops

Consider the following Java program:

![arr](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/arr/arr23.png)

It is a simple piece of code that prints the number of times the increment statement runs throughout the program. Let’s compute its time complexity.

## Time Complexity 
Let’s take the training wheels off and jump straight to line number 6. From the previous lesson, you would recall that it accounts for 6n + 46n+4 primitive operations: one for initialization, 3×(n+1) for the comparison, and 3\times n3×n for the increment.

Let’s move onto line number 7. Since this line is nested inside the for loop on line 6, it is repeated nn times. For a single iteration of the outer for loop, how many primitive operations does this line incur? You should be able to generalize from the last lesson that the answer is 6m + 4. That means that the total number of primitive operations on line 7 are n ( 6m + 4 ).

How about line number 8? Each time it is executed, it involves reading a variable’s value, adding two numbers, and assigning to a variable - that’s three primitive operations. Since. this line is nested inside the two loops, it is repeating n * mn∗m times. So, the total number of primitive operations contributed by line 8 are 3nm3nm. Lines 11 is executed only once and account for two primitive operations.

The analysis is summarized in the following table:

![arr](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/arr/arr24.png)

![arr](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/arr/arr25.png)
![arr](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/arr/arr26.png)
![arr](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/arr/arr27.png)
![arr](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/arr/arr28.png)
![arr](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/arr/arr29.png)
![arr](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/arr/arr30.png)
![arr](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/arr/arr31.png)
![arr](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/arr/arr32.png)
![arr](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/arr/arr33.png)
![arr](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/arr/arr34.png)
![arr](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/arr/arr35.png)
![arr](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/arr/arr36.png)
![arr](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/arr/arr37.png)

## Introduction to Asymptotic Analysis and Big O

We have seen that the time complexity of an algorithm can be expressed as a polynomial. To compare two algorithms, we can compare the respective polynomials. However, the analysis performed in the previous lessons is a bit cumbersome and would become intractable for bigger algorithms that we tend to encounter in practice.

## Asymptotic Analysis
One observation that helps us is that we want to worry about large input sizes only. If the input size is really small, how bad can a poorly designed algorithm get, right? Mathematicians have a tool for this sort of analysis called the asymptotic notation. The asymptotic notation compares two functions, say, f(n)f(n) and g(n)g(n) for very large values of nn. This fits in nicely with our need for comparing algorithms for very large input sizes.

![arr](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/arr/arr38.png)
![arr](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/arr/arr39.png)
![arr](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/arr/arr40.png)
![arr](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/arr/arr41.png)

![arr](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/arr/arr42.png)
![arr](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/arr/arr43.png)
![arr](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/arr/arr44.png)
![arr](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/arr/arr45.png)

## Other Common Asymptotic Notations and Why Big O Trumps Them

![arr](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/arr/arr46.png)
![arr](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/arr/arr47.png)

![arr](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/arr/arr48.png)
![arr](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/arr/arr49.png)

![arr](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/arr/arr50.png)
![arr](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/arr/arr51.png)

## Why Big ‘O’ is preferred over other notations 
All of these notations have a variety of applications in mathematics. However, in algorithm analysis, we tend to focus on the worst-case time and space complexity. It tends to be more useful to know that the worst-case running time of a particular algorithm will grow at most as fast as a constant multiple of a certain function than to know that it will grow at least as fast as some other function. In other words, Big Omega is often not very useful for use with worst-case running time.

What about Big Theta, though? Indeed it would be great to have a tight bound on the worst-case running time of an algorithm. Imagine that there is a complex algorithm for which we haven’t yet found a tight bound on the worst-case running time. In such a case, we can’t use Big Theta, but we can still use a loose upper bound (Big O) until a tight bound is discovered. It is common to see Big O being used to characterize the worst-case running time even for simple algorithms where a Big Theta characterization is easily possible. That is not technically wrong, because Big O is a subset of Big Theta.

The little o and little omega notations require a strict level of inequality (< or >) and the ability to show that there is a valid n_0 for any valid of choice of cc. This is not always easy to do.

For all the above reasons, it is most common to see Big O being used when talking about an algorithm’s time or space complexity.

## Useful Formulae

## Formulae 
Here is a list of handy formulas which can be helpful when calculating the Time Complexity of an algorithm:

![arr](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/arr/arr52.png)

## General Tips
Every time a list or array gets iterated over c×length times, it is most likely in O(n) time.
When you see a problem where the number of elements in the problem space gets halved each time, it will most probably be in O(log n)O(logn) runtime.
Whenever you have a single nested loop, the problem is most likely in quadratic time.

## Common Complexity Scenarios

![arr](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/arr/arr53.png)

Explanation: Java for loop increments the value x by 1 in every iteration from 0 till n-1 ([0, 1, 2, …, n-1]). So n is first 0, then 1, then 2, …, then n-1. This means the loop increment statement x++ runs a total of nn times. The comparison statement x < n ; runs n+1 times. The initialization x = 0; runs once. Summing them up, we get a running time complexity of the for loop of n + n + 1 + 1=2n+2. Now, the constant time statements in the loop itself each run nn times. Supposing the statements inside the loop account for a constant running time of cc in each iteration, they account for a total running time of cncn throughout the loop’s lifetime. Hence the running time complexity is (2n+2)+cn.

![arr](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/arr/arr54.png)

![arr](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/arr/arr55.png)

![arr](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/arr/arr56.png)

![arr](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/arr/arr57.png)

![arr](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/arr/arr58.png)

![arr](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/arr/arr59.png)

A pattern is hard to decipher here. So, let’s simplify things. In the outer loop, i is doubled and then incremented each time. If we ignore the increment part, we will be slightly over-estimating the number of iteration of the outer for loop. That is fine because we are looking for an upper bound on the worst-case running time (Big O).

![arr](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/arr/arr60.png)

![arr](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/arr/arr61.png)

![arr](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/arr/arr62.png)
