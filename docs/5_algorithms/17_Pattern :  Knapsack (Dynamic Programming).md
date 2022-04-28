---
layout: default
title: Knapsack 
parent: Algorithms
nav_order: 17
permalink: /algorithms/knapsack 
---
<div align="center" markdown="1">
Knapsack  / Java resources / Tutorial

{: .fs-8 .fw-400 }
</div>

## Pattern : 0/1 Knapsack (Dynamic Programming)

## Introduction
0/1 Knapsack pattern is based on the famous problem with the same name which is efficiently solved using Dynamic Programming (DP).

In this pattern, we will go through a set of problems to develop an understanding of DP. We will always start with a brute-force recursive solution to see the overlapping subproblems, i.e., realizing that we are solving the same problems repeatedly.

After the recursive solution, we will modify our algorithm to apply advanced techniques of Memoization and Bottom-Up Dynamic Programming to develop a complete understanding of this pattern.

Let’s jump onto our first problem.

## Introduction
Given the weights and profits of ‘N’ items, we are asked to put these items in a knapsack with a capacity ‘C.’ The goal is to get the maximum profit out of the knapsack items. Each item can only be selected once, as we don’t have multiple quantities of any item.

Let’s take Merry’s example, who wants to carry some fruits in the knapsack to get maximum profit. Here are the weights and profits of the fruits:

Items: { Apple, Orange, Banana, Melon }
Weights: { 2, 3, 1, 4 }
Profits: { 4, 5, 3, 7 }
Knapsack capacity: 5

Let’s try to put various combinations of fruits in the knapsack, such that their total weight is not more than 5:

Apple + Orange (total weight 5) => 9 profit
Apple + Banana (total weight 3) => 7 profit
Orange + Banana (total weight 4) => 8 profit
Banana + Melon (total weight 5) => 10 profit

This shows that Banana + Melon is the best combination as it gives us the maximum profit, and the total weight does not exceed the capacity.

## Problem Statement
Given two integer arrays to represent weights and profits of ‘N’ items, we need to find a subset of these items which will give us maximum profit such that their cumulative weight is not more than a given number ‘C.’ Each item can only be selected once, which means either we put an item in the knapsack or we skip it.

## Basic Solution
A basic brute-force solution could be to try all combinations of the given items (as we did above), allowing us to choose the one with maximum profit and a weight that doesn’t exceed ‘C’. Take the example of four items (A, B, C, and D), as shown in the diagram below. To try all the combinations, our algorithm will look like:

![alg](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/alg/gg10.png)

Here is a visual representation of our algorithm:

![alg](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/alg/gg11.png)

All green boxes have a total weight that is less than or equal to the capacity (7), and all the red ones have a weight that is more than 7. The best solution we have is with items [B, D] having a total profit of 22 and a total weight of 7.

## Code

Here is the code for the brute-force solution:

{% highlight java %}
class Knapsack {

  public int solveKnapsack(int[] profits, int[] weights, int capacity) {
    return this.knapsackRecursive(profits, weights, capacity, 0);
  }

  private int knapsackRecursive(int[] profits, int[] weights, int capacity, int currentIndex) {
    // base checks
    if (capacity <= 0 || currentIndex >= profits.length)
      return 0;

    // recursive call after choosing the element at the currentIndex
    // if the weight of the element at currentIndex exceeds the capacity, we shouldn't process this
    int profit1 = 0;
    if( weights[currentIndex] <= capacity )
        profit1 = profits[currentIndex] + knapsackRecursive(profits, weights,
                capacity - weights[currentIndex], currentIndex + 1);

    // recursive call after excluding the element at the currentIndex
    int profit2 = knapsackRecursive(profits, weights, capacity, currentIndex + 1);

    return Math.max(profit1, profit2);
  }

  public static void main(String[] args) {
    Knapsack ks = new Knapsack();
    int[] profits = {1, 6, 10, 16};
    int[] weights = {1, 2, 3, 5};
    int maxProfit = ks.solveKnapsack(profits, weights, 7);
    System.out.println("Total knapsack profit ---> " + maxProfit);
    maxProfit = ks.solveKnapsack(profits, weights, 6);
    System.out.println("Total knapsack profit ---> " + maxProfit);
  }
}

{% endhighlight %}

![alg](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/alg/gg12.png)

![alg](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/alg/gg13.png)

We can clearly see that ‘c:4, i=3’ has been called twice. Hence we have an overlapping sub-problems pattern. We can use Memoization to solve overlapping sub-problems efficiently.

## Top-down Dynamic Programming with Memoization
Memoization is when we store the results of all the previously solved sub-problems and return the results from memory if we encounter a problem that has already been solved.

Since we have two changing values (capacity and currentIndex) in our recursive function knapsackRecursive(), we can use a two-dimensional array to store the results of all the solved sub-problems. As mentioned above, we need to store results for every sub-array (i.e., for every possible index ‘i’) and every possible capacity ‘c.’

## Code
Here is the code with memoization (see changes in the highlighted lines):

{% highlight java %}
class Knapsack {

  public int solveKnapsack(int[] profits, int[] weights, int capacity) {
    Integer[][] dp = new Integer[profits.length][capacity + 1];
    return this.knapsackRecursive(dp, profits, weights, capacity, 0);
  }

  private int knapsackRecursive(Integer[][] dp, int[] profits, int[] weights, int capacity,
      int currentIndex) {

    // base checks
    if (capacity <= 0 || currentIndex >= profits.length)
      return 0;

    // if we have already solved a similar problem, return the result from memory
    if(dp[currentIndex][capacity] != null)
      return dp[currentIndex][capacity];

    // recursive call after choosing the element at the currentIndex
    // if the weight of the element at currentIndex exceeds the capacity, we shouldn't process this
    int profit1 = 0;
    if( weights[currentIndex] <= capacity )
        profit1 = profits[currentIndex] + knapsackRecursive(dp, profits, weights,
                capacity - weights[currentIndex], currentIndex + 1);

    // recursive call after excluding the element at the currentIndex
    int profit2 = knapsackRecursive(dp, profits, weights, capacity, currentIndex + 1);

    dp[currentIndex][capacity] = Math.max(profit1, profit2);
    return dp[currentIndex][capacity];
  }

  public static void main(String[] args) {
    Knapsack ks = new Knapsack();
    int[] profits = {1, 6, 10, 16};
    int[] weights = {1, 2, 3, 5};
    int maxProfit = ks.solveKnapsack(profits, weights, 7);
    System.out.println("Total knapsack profit ---> " + maxProfit);
    maxProfit = ks.solveKnapsack(profits, weights, 6);
    System.out.println("Total knapsack profit ---> " + maxProfit);
  }
}

{% endhighlight %}

![alg](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/alg/gg14.png)

![alg](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/alg/gg15.png)

![alg](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/alg/gg16.png)

Let’s draw this visually and start with our base case of zero capacity:

![alg](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/alg/gg17.png)
![alg](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/alg/gg18.png)
![alg](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/alg/gg19.png)
![alg](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/alg/gg20.png)
![alg](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/alg/gg21.png)
![alg](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/alg/gg22.png)
![alg](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/alg/gg23.png)
![alg](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/alg/gg24.png)
![alg](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/alg/gg25.png)
![alg](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/alg/gg26.png)
![alg](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/alg/gg27.png)
![alg](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/alg/gg28.png)
![alg](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/alg/gg29.png)
![alg](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/alg/gg30.png)
![alg](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/alg/gg31.png)
![alg](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/alg/gg32.png)
![alg](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/alg/gg33.png)
![alg](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/alg/gg34.png)
![alg](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/alg/gg35.png)
![alg](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/alg/gg36.png)
![alg](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/alg/gg37.png)
![alg](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/alg/gg38.png)
![alg](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/alg/gg39.png)

## Code

Here is the code for our bottom-up dynamic programming approach:

{% highlight java %}
class Knapsack {

  public int solveKnapsack(int[] profits, int[] weights, int capacity) {
    // basic checks
    if (capacity <= 0 || profits.length == 0 || weights.length != profits.length)
      return 0;

    int n = profits.length;
    int[][] dp = new int[n][capacity + 1];

    // populate the capacity=0 columns, with '0' capacity we have '0' profit
    for(int i=0; i < n; i++)
      dp[i][0] = 0;

    // if we have only one weight, we will take it if it is not more than the capacity
    for(int c=0; c <= capacity; c++) {
      if(weights[0] <= c)
        dp[0][c] = profits[0];
    }

    // process all sub-arrays for all the capacities
    for(int i=1; i < n; i++) {
      for(int c=1; c <= capacity; c++) {
        int profit1= 0, profit2 = 0;
        // include the item, if it is not more than the capacity
        if(weights[i] <= c)
          profit1 = profits[i] + dp[i-1][c-weights[i]];
        // exclude the item
        profit2 = dp[i-1][c];
        // take maximum
        dp[i][c] = Math.max(profit1, profit2);
      }
    }

    // maximum profit will be at the bottom-right corner.
    return dp[n-1][capacity];
  }

  public static void main(String[] args) {
    Knapsack ks = new Knapsack();
    int[] profits = {1, 6, 10, 16};
    int[] weights = {1, 2, 3, 5};
    int maxProfit = ks.solveKnapsack(profits, weights, 7);
    System.out.println("Total knapsack profit ---> " + maxProfit);
    maxProfit = ks.solveKnapsack(profits, weights, 6);
    System.out.println("Total knapsack profit ---> " + maxProfit);
  }
}
{% endhighlight %}

![alg](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/alg/gg40.png)

## How can we find the selected items?
As we know, the final profit is at the bottom-right corner. Therefore, we will start from there to find the items that will be going into the knapsack.

As you remember, at every step, we had two options: include an item or skip it. If we skip an item, we take the profit from the remaining items (i.e., from the cell right above it); if we include the item, then we jump to the remaining profit to find more items.

Let’s understand this from the above example:

![alg](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/alg/gg41.png)

1. ‘22’ did not come from the top cell (which is 17); hence we must include the item at index ‘3’ (which is item ‘D’).
2. Subtract the profit of item ‘D’ from ‘22’ to get the remaining profit ‘6’. We then jump to profit ‘6’ on the same row.
3. ‘6’ came from the top cell, so we jump to row ‘2’.
4. Again, ‘6’ came from the top cell, so we jump to row ‘1’.
5. ‘6’ is different from the top cell, so we must include this item (which is item ‘B’).
6. Subtract the profit of ‘B’ from ‘6’ to get profit ‘0’. We then jump to profit ‘0’ on the same row. As soon as we hit zero remaining profit, we can finish our item search.
7. Thus, the items going into the knapsack are {B, D}.

Let’s write a function to print the set of items included in the knapsack.

{% highlight java %}
import java.util.*;

class Knapsack {

  public int solveKnapsack(int[] profits, int[] weights, int capacity) {
    // base checks
    if (capacity <= 0 || profits.length == 0 || weights.length != profits.length)
      return 0;

    int n = profits.length;
    int[][] dp = new int[n][capacity + 1];

    // populate the capacity=0 columns, with '0' capacity we have '0' profit
    for(int i=0; i < n; i++)
      dp[i][0] = 0;

    // if we have only one weight, we will take it if it is not more than the capacity
    for(int c=0; c <= capacity; c++) {
      if(weights[0] <= c)
        dp[0][c] = profits[0];
    }

    // process all sub-arrays for all the capacities
    for(int i=1; i < n; i++) {
      for(int c=1; c <= capacity; c++) {
        int profit1= 0, profit2 = 0;
        // include the item, if it is not more than the capacity
        if(weights[i] <= c)
          profit1 = profits[i] + dp[i-1][c-weights[i]];
        // exclude the item
        profit2 = dp[i-1][c];
        // take maximum
        dp[i][c] = Math.max(profit1, profit2);
      }
    }

    printSelectedElements(dp, weights, profits, capacity);
    // maximum profit will be at the bottom-right corner.
    return dp[n-1][capacity];
  }

 private void printSelectedElements(int dp[][], int[] weights, int[] profits, int capacity){
   System.out.print("Selected weights:");
   int totalProfit = dp[weights.length-1][capacity];
   for(int i=weights.length-1; i > 0; i--) {
     if(totalProfit != dp[i-1][capacity]) {
       System.out.print(" " + weights[i]);
       capacity -= weights[i];
       totalProfit -= profits[i];
     }
   }

   if(totalProfit != 0)
     System.out.print(" " + weights[0]);
   System.out.println("");
 }

  public static void main(String[] args) {
    Knapsack ks = new Knapsack();
    int[] profits = {1, 6, 10, 16};
    int[] weights = {1, 2, 3, 5};
    int maxProfit = ks.solveKnapsack(profits, weights, 7);
    System.out.println("Total knapsack profit ---> " + maxProfit);
    maxProfit = ks.solveKnapsack(profits, weights, 6);
    System.out.println("Total knapsack profit ---> " + maxProfit);
  }
}
{% endhighlight %}
