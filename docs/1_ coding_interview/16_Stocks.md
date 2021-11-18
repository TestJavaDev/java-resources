---
layout: default
title: Stocks
parent: Coding Interview
has_children: true
nav_order: 16
permalink: /coding_interview/stocks
---
<div align="center" markdown="1">
Stocks / Java resources / Tutorial

{: .fs-8 .fw-400 }
</div>

## Stocks

## Project Description for Stocks

## Introduction
Stocks represent companies and individuals’ claims of the shares of public companies. These shares’ prices vary depending on various factors, including inflation, demand, and reputation. There are a lot of trading firms, which deal in the buying and selling of these stocks. These firms are always on the lookout for new traders to join their company.

The scenario and the problems discussed in this chapter also relate to the onboarding process and how we can improve it.

## Statement
Assume you are a developer in a stock trading company, and you’re working on their online trading platform. The company wants you to add functionalities to their onboarding feature for new hires.

The company has noticed that a lot of rookies mess up the buying and selling prices while making stock trades. Therefore, we need a validator in place to inform them of their probable mistakes. After a trade is made, we need to make sure the settling period is over before someone tries to make another trade. We also want to know whether everyone completed their assigned trading goals for the day or not. The rookies can make as many trades as they want but their daily minimum goals should be met. We also need to obtain the day and week these brokers reached specific trading milestones. All this data will eventually help us in decide their promotions at the time of performance evaluation.

## Features
We will need to introduce the following features to implement the functionalities we discussed above:
* Feature #1: Validate the price for buying and selling stocks according to the defined company’s criteria.
* Feature #2: Stock of the same company should not be traded again until the settling period is over.
* Feature #3: Store the trades for every rookie and evaluate whether everyone met their minimum criteria or not.
* Feature #4: Determine the day and week when a broker reached specific trading milestones.
* Feature #5: Determine the top brokers based on their frequency of trades.

Understanding these feature requests and designing their solutions will help us implement the requested functionality into the trading platform.

In the next few lessons, we’ll discuss the recommended implementations of these features. The solutions to these problems will also be applicable to other common coding interview questions.

## Feature #1: Validate Price

## Description
Stocks are being bought and sold every second in a trading company. It becomes common for new hires or interns with little experience to make mistakes while entering purchase or sale prices. The company has defined the fixed criteria for the purchasing and selling of stocks on its platform. In the trading section, if a price is entered with + sign, it means buy the stocks worth that amount. If a price is entered with - sign, it means sell the currently selected stock worth that amount. If no sign is entered with the price, that entry should be disregarded. Since stocks are traded in different currencies and we know that all currencies are not equal in value, prices can be fractional as well.

We’ll be provided with an input price in the form of a string. We have to validate this input so it can be either accepted or rejected. Some examples are mentioned below for reference:

+40.325 is a valid price.
-1.1.1 is NOT a valid price.
-222 is a valid price.
++22 is NOT a valid price.
10.1 is NOT a valid price.
+22.22 is a valid price.
100. is NOT a valid price.

## Solution
We’ll use the state machine below to check if a price is valid or not. The initial state is Start. We’ll process each character to identify the next state. The input string is not a valid price if we reach an UNKNOWN state at any point or if it ends in a DECIMAL point.

![bog](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/bog/bog35.png)

In the state machine, we are not looking at the sign (+ or -) at the start of a price. If there is a sign at the start of the input string, we start processing the string for the state machine after that sign character.

Let’s look at the code for the solution:

{% highlight java %}
class Solution{
    
  enum STATE { START, INTEGER, DECIMAL, UNKNOWN, AFTERDECIMAL};
  
  static STATE getNextState(STATE currentState, char ch) {
   switch(currentState) {
      case START:
      case INTEGER:
        if (ch == '.') {
        return STATE.DECIMAL;
        } else if (ch >= '0' && ch <= '9') {
          return STATE.INTEGER;
        } else {
          return STATE.UNKNOWN;
        }
      case DECIMAL:
        if (ch >= '0' && ch <= '9') {
          return STATE.AFTERDECIMAL;
        } else {
          return STATE.UNKNOWN;
       }
      case AFTERDECIMAL: 
       if (ch >= '0' && ch <= '9') {
          return STATE.AFTERDECIMAL;
        } else {
          return STATE.UNKNOWN;
       }
    }
    return STATE.UNKNOWN;
  }

  static boolean isPriceValid(String s) {
    if (s.isEmpty()) {
      return true;
    }
    int i = 0;
    if (s.charAt(i) == '+' || s.charAt(i) == '-') {
      ++i;

      STATE currentState = STATE.START;
      while (i < s.length()) {
        currentState = getNextState(currentState, s.charAt(i));
      
        if (currentState == STATE.UNKNOWN) {
          return false;
        }

        i = i + 1;
      }
      
      if (currentState == STATE.DECIMAL)
        return false;
      
      return true;
    }
    return false;
  }

  public static void main(String[] args) {

    System.out.println("Is the price valid +40.325? " + isPriceValid("+40.325"));
    System.out.println("Is the price valid -1.1.1? " + isPriceValid("-1.1.1"));
    System.out.println("Is the price valid -222? " + isPriceValid("-222"));
    System.out.println("Is the price valid ++22? " + isPriceValid("++22"));
    System.out.println("Is the price valid 10.1? " + isPriceValid("10.1"));
    System.out.println("Is the price valid +22.22.? " + isPriceValid("22.22."));
    System.out.println("Is the price valid .100? " + isPriceValid(".100"));   
  }
}
{% endhighlight %}

![bog](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/bog/bog36.png)

## Feature #2: Settling Period

## Description
The settling period is the time that must elapse before money changes hands after a stock trade is completed. We don’t want to allow another trade in the same stock before the expiry of the settling period. So, a person can’t trade more than one stock of the same company at once, and the user must wait for the settling period before another stock of the same company can be traded.

We are given a list of letters, where each letter represents the stock of a company for which a stock trade must be made. The stocks will be mapped to letters to form this input array. Letters can repeat to represent that multiple trades need to be made for the same company’s stocks. We want to make all the given trades as quickly as possible. The constraint is that two trades of the same company must be separated by at least k intervening periods; these could be trades of other companies or idle periods. The parameter k defines the settling period. We need to calculate the minimum amount of time required to trade all the stocks.

For example, if a user wants to trade four stocks of APPLE, two stocks of TESLA and one stock of MICROSOFT in the same transaction, an input array like ['A', 'A', 'A', 'T', 'T', 'M', 'A'] would be given.

This is an example of mapping of stocks to characters’ array:

![bog](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/bog/bog37.png)

This is an example of the input array:

![bog](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/bog/bog38.png)

## Solution
First, calculate and store the number of trades needed for each stock in a list named frequencies.

We will store the count of stocks of the company that will be traded the most in the transaction as fMax; after that, the fMax trades of the most traded company need to be separated by (fMax - 1) intervals equal to the settling period. If you have n items, there are n-1 intervals between them.

Initially, (fMax - 1) is multiplied by settling time, this gives the number of idle periods between the fMax trades of the most frequently traded item, and we assign this value to idleIntervals. Then, we keep updating the idleIntervals variable. We pick the next most frequently traded stock. If it is less frequent than the most frequently traded stock, it can be traded in the intervening periods between the trades of the latter. Otherwise, it will have to be traded one interval after the most traded stock. In the end, we need length stocks intervals for the actual trades and idleIntervals for the idle intervals

Let’s take a look at the example below:

![bog](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/bog/bog39.png)
![bog](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/bog/bog40.png)
![bog](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/bog/bog41.png)

Here is how we will implement this feature:
1. Calculate and store the frequencies of the trades for each company in an array called frequencies. Sort this array in descending order.
2. Then find the maximum value in frequencies. Store this max value as fMax to get the count of stock of the company traded the most.
3. Next, calculate the idle intervals between consecutive trades of the most frequent stock; to get that this value, we multiply settling time with fMax - 1.
4. Iterate over frequencies, and if the value at each index is less than (fMax - 1), subtract the value from idleIntervals. If the value is greater than (fMax - 1), we subtract (fMax - 1) from idleIntervals instead.
5. If idleIntervals is negative, we return stocks.length. Otherwise, we return idleIntervals + stocks.length.

{% highlight java %}

{% endhighlight %}

![bog](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/bog/bog42.png)

## Feature #3: Goals Fulfilled

## Description
Our stock trading company is hiring interns. Different interns start on different days. Each intern is given a target to close at least three trades on any given day and log these trades using automatically incrementing sequence numbers. Each intern will close trades numbered 1, 2, 3, .... Since different interns have spent a different number of days on the job at any given time, one may be closing trade number 2 while another is closing trade number 23.

Before you arrived, a developer wrote a logging application for the interns. The application accepts trades sequence numbers from the interns and stores them in a centralized log. The logs keep separate records for each day. Unfortunately, the developer didn’t include the intern IDs in the log records. To complicate matters further, the developer sorted the list of trade numbers before storing it in the log. For example, consider a day on which three interns were working. They logged the following trades: [1, 2, 3, 4], [4, 5, 6] and [10, 11, 12]. The log for this day would say [1, 2, 3, 4, 4, 5, 6, 10, 11, 12].

Given a day’s record log, we want you to figure out if every intern working on a given day submitted at least three deals for the day or not as accurately as possible. Note that if the log said [1, 2, 3, 4, 5, 6, 10, 11, 12], we can’t be certain if there were three interns working or two. However, all we are interested in is a true/false answer, which would be true in the above case. If on a given day, there is no way that any number of interns could have reported at least three deals, return false.

We’ll be provided with an array of sorted numbers representing trades. This array actually contains the different sets of trades made by interns organized in a sorted manner. Our task is to determine if subsequences/sets with at least three consecutive elements exist in them or not.

Here is an illustration to better understand this:

![bog](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/bog/bog43.png)
![bog](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/bog/bog44.png)

## Solution
We need to determine if valid subsequences can be made under the above-mentioned constraints. Each number can either be part of an existing subsequence, or it will make a new subsequence starting from itself. We’ll need two maps to store the count of our numbers. The first map, frequencyMap, will store the frequency with which a number occurs in our trades array. The second map, imaginedMap, will help us determine if a new number should be part of an existing subsequence or not.

When making a new sequence with a number n, we need to ensure there are at least two consecutive numbers in the array that follows n. We can use our frequencyMap to verify this. When a subsequence with at least 3 consecutive integers is found, we’ll add that sequence’s next number to our imaginedMap with its respective count. Initially, this count value is 1 because we are assuming the number for the first time. If we have to assume this number again, we’ll increment its count value. Currently, we are assuming that this number will only be part of our initial subsequence.

When we move to the next number in our array, we can check our imaginedMap to verify if this new number needs to join an existing subsequence or not.

Here is how we will implement this feature:
1. Initialize the two maps frequencyMap and imaginedMap.
2. Let frequencyMap[n] be the frequency of n and imaginedMap[n] be the next number of an existing sequence.
3. Traverse the trades array. If new subsequences are found, we will decrement their count and add the next assumed number in imaginedMap.
4. For every n, check if it exists in the imaginedMap. If it exists, we will decrement its count in both maps.
5. Otherwise, create a new sequence and repeat from step 3.

![bog](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/bog/bog45.png)
![bog](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/bog/bog46.png)
![bog](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/bog/bog47.png)
![bog](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/bog/bog48.png)
![bog](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/bog/bog49.png)
![bog](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/bog/bog50.png)
![bog](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/bog/bog51.png)
![bog](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/bog/bog52.png)
![bog](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/bog/bog53.png)
![bog](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/bog/bog54.png)

Let’s look at the code for the solution:

{% highlight java %}
import java.util.*;

class Solution {
  public static boolean goalsFulfilled(int[] trades) {
    Counter frequencyMap = new Counter();
    Counter imaginedMap = new Counter();

    for (int n: trades) frequencyMap.add(n, 1);

    for (int n: trades) {

      if (frequencyMap.get(n) == 0) {
        continue;
      } 

      else if (imaginedMap.get(n) > 0) {
        // Adding number to existing sequence
        imaginedMap.add(n, -1);
        imaginedMap.add(n+1, 1);
      } 

      else if (frequencyMap.get(n+1) > 0 && frequencyMap.get(n+2) > 0) {
        // Creating new subsequence
        frequencyMap.add(n+1, -1);
        frequencyMap.add(n+2, -1);
        imaginedMap.add(n+3, 1);
      } 

      else {
        return false;
      }

      frequencyMap.add(n, -1);
    }
    
    return true;
  }

  public static void main(String args[]) {
    // Driver code

    int[] trades = {1, 2, 3, 3, 4, 4, 5, 5};
    
    if (goalsFulfilled(trades) == false){
      System.out.println("The goals have not been fulfilled!");
    }
    else{
      System.out.println("The goals have been fulfilled!");
    }

  }
}

// extending class to get frequency of elements
class Counter extends HashMap<Integer, Integer> {
  public int get(int k) {
    return containsKey(k) ? super.get(k) : 0;
  }

  public void add(int k, int v) {
    put(k, get(k) + v);
  }
}
{% endhighlight %}

![bog](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/bog/bog55.png)

## Feature #4: Milestone Reached

## Description
Our company wants to display high achieving brokers in a hall of fame. They want to find out if a broker reached a milestone of making k trades and, if so, they want to know when they reached that milestone. Stockbrokers have been making trades and recording their tally of completed trades since the start of their career at the company. The data is being recorded into separate log files, each of which can be viewed as a matrix with 5 columns, one for each day of the week. There are r rows, representing the last r weeks of the year. We want to find out when a given broker reached the milestone of k trades in their career.

We’ll be provided with an m x 5 matrix and a target milestone value. Our task is to determine the day and week a stockbroker fulfilled their milestone.

## Solution
Each day stores the cumulative sum of all the trades, so we’ll have a matrix with an increasing number of values along each day. We can observed that the 2D matrix, with its unique properties, can be visualized as a sorted 1D array of size m x n. Since the array is sorted, we can simply apply the binary search algorithm on it to get the required value.

![bog](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/bog/bog56.png)

Since we are not actually converting the matrix into an array, we need a way to access the elements located at a (row, col) index. If we have an index, ind, from a linear array, it’s corresponding (row, col) pair can be obtained as follows

![bog](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/bog/bog57.png)

At each step of the binary search, convert the 1D index into row and column indices to look up the element in the 2D array.

Let’s see how we might implement this functionality:
1. Initialize two pointers left and right at each end of the array as left = 0 and right = m x n - 1.
2. Traverse the array until the value of the right pointer is greater than the value of the left pointer.
3. Select the index of the middle element of the array as middleInd = (left + right) / 2.
4. This selected index will give us the (row, col) pair (as explained above) to find the middle element of the matrix.
5. If our milestone value is less than the middle element, skip the entire array right of the middle element as right = middleInd - 1.
6. If our milestone value is greater than the middle element, skip the entire array left of the middle element as left = middleInd + 1.
7. If at any point the middle element becomes equal to milestone, return the index positions. Otherwise, return -1, -1.

![bog](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/bog/bog58.png)
![bog](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/bog/bog59.png)
![bog](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/bog/bog60.png)
![bog](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/bog/bog61.png)

Let’s look at the code for the solution:

{% highlight java %}
import java.util.*;
class Solution {
    
    public static int[] milestoneReached(int[][] matrix, int milestone) {
        
        int[] failed = {-1, -1};

        int m = matrix.length;
        if (m == 0)
            return failed;
        int n = matrix[0].length;

        // binary search
        int left = 0, right = m * n - 1;
        int middleIdx, middleElement;
        while (left <= right) {
            middleIdx = (left + right) / 2;
            middleElement = matrix[middleIdx / n][middleIdx % n];
            if (milestone == middleElement){
                int[] res = {middleIdx / n, middleIdx % n};
                return res;
            }
            else {
                if (milestone < middleElement)
                    right = middleIdx - 1;
                else
                    left = middleIdx + 1;
            }
        }
        
        return failed;
    }

    public static void main( String args[] ) {
        // Driver code

        int[][] matrix = {
            {0,2,4,6,8},
            {10,12,14,18,22},
            {24,30,34,60,64}
        };
        int milestone = 24;
        int[] res = milestoneReached(matrix, milestone);
        System.out.println("Milestone reached on day " + (res[1] + 1) + " of week " + (res[0] + 1));
    }
}
{% endhighlight %}

![bog](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/bog/bog62.png)

## Feature #5: Top Brokers

## Description
The company is doing performance evaluations. Each broker’s increments will be decided based on their level of activity throughout the last quarter. Each broker is assigned a unique ID that can be used to track their progress. Currently, this information is managed using an array. Every time a broker completes a trade, their ID is inserted into this array. Now, the company wants to promote its top k brokers. We have to implement a functionality that will automatically output the top k performers at the end of a quarter.

We’ll be provided with an array of integers representing the brokers’ IDs. Our task is to determine the top k most active brokers based on the number of times their ID occurs in the array.

![bog](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/bog/bog63.png)

## Solution
We need to find the top k IDs based on each number’s frequency count. In this problem, we first need to know the frequency of each number; we can do this using a, HashMap. Once we have the frequency map, the best data structure to keep track of the top k frequencies is heap. We’ll iterate through the frequency map and insert each element into our heap. If for an element, i, the size of our heap is k + 1, we do two things:
1. Take out the lowest frequency element from the heap.
2. Insert the element, i, into the heap.

This will ensure that we always have k maximum frequencies in the heap. The most efficient way to repeatedly find the smallest number among a set of numbers is using a min-heap.

Below is an illustration of this process:

![bog](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/bog/bog64.png)
![bog](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/bog/bog65.png)
![bog](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/bog/bog66.png)
![bog](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/bog/bog67.png)
![bog](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/bog/bog68.png)
![bog](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/bog/bog69.png)
![bog](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/bog/bog70.png)

Let’s look at the code for the solution:

{% highlight java %}
import java.util.*;
class Solution {
  public static List<Integer> topBrokers(int[] brokerIDs, int k) {
    // find the frequency of each number
    Map<Integer, Integer> numFrequencyMap = new HashMap<>();
    for (int n : brokerIDs)
      numFrequencyMap.put(n, numFrequencyMap.getOrDefault(n, 0) + 1);

    PriorityQueue<Map.Entry<Integer, Integer>> minHeap = new PriorityQueue<Map.Entry<Integer, Integer>>(
        (e1, e2) -> e1.getValue() - e2.getValue());

    // go through all numbers of the numFrequencyMap and push them in the minHeap, which will have 
    // top k frequent numbers. If the heap size is more than k, we remove the smallest (top) number 
    for (Map.Entry<Integer, Integer> entry : numFrequencyMap.entrySet()) {
      minHeap.add(entry);
      if (minHeap.size() > k) {
        minHeap.poll();
      }
    }
    
    // create a list of top k numbers
    List<Integer> topNumbers = new ArrayList<>(k);
    while (!minHeap.isEmpty()) {
      topNumbers.add(minHeap.poll().getKey());
    }
    return topNumbers;
  }
  public static void main(String[] args) {
    // Driver code

    List<Integer> result = topBrokers(new int[] { 1, 3, 5, 12, 11, 12, 11, 12, 5 }, 3);
    
    System.out.println("Here are the IDs of the top K brokers of the quarter: " + result);
  }
}

{% endhighlight %}

![bog](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/bog/bog71.png)
