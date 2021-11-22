---
layout: default
title: Challenge 1
parent: Arrays
grand_parent: Data Structures
nav_order: 1
permalink: /data_structures/arrays/ch1
---
<div align="center" markdown="1">
Challenge 1 / Java resources / Tutorial

{: .fs-8 .fw-400 }
</div>

## Challenge 11: Find the Sum of Maximum Sum Subarray

Maximum Sum Subarray#
Given an unsorted array AA, the maximum sum sub-array is the sub-array (contiguous elements) from AA for which the sum of the elements is maximum. In this challenge, we want to find the sum of the maximum sum sub-array. This problem is a tricky one because the array might have negative integers in any position, so we have to cater to those negative integers while choosing the contiguous subarray with the largest positive values.

Here is an example:

![arr](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/arr/arr91.png)
![arr](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/arr/arr92.png)
![arr](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/arr/arr93.png)
![arr](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/arr/arr94.png)
![arr](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/arr/arr95.png)
![arr](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/arr/arr96.png)
![arr](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/arr/arr97.png)
![arr](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/arr/arr98.png)

Problem statement#
Given an integer array, return the maximum subarray sum. The array may contain both positive and negative integers and is unsorted.

Method Prototype#
int findMaxSumSubArray(int[] arr)
Output#
An integer value equal to the maximum sum of subarray found in arr.

Sample Input#
arr = {1, 7, -2, -5, 10, -1}
Sample Output#
11

## Coding Exercise

{% highlight java %}
class FindMax {
    public static int findMaxSumSubArray(int[] arr) {
        // Write - Your - Code
        return 0;
    }
}
{% endhighlight %}

## Solution Review: Find the Sum of Maximum Sum Subarray

## Solution: Kadane’s Algorithm

{% highlight java %}
class FindMax {
    public static int findMaxSumSubArray(int[] arr) {
        if (arr.length < 1) {
            return 0;
        }

        int currMax = arr[0];
        int globalMax = arr[0];
        int lengtharray = arr.length;
        for (int i = 1; i < lengtharray; i++) {
            if (currMax < 0) {
            currMax = arr[i];
            } else {
            currMax += arr[i];
            }

            if (globalMax < currMax) {
            globalMax = currMax;
            }
        }
        return globalMax;
    }
    public static void main( String args[] ) {
        int[] arr1 = {1, 7, -2, -5, 10, -1};
        System.out.println("Array: "+ Arrays.toString(arr1));
        System.out.println("Sum: " + findMaxSumSubArray(arr1));
    }
}
{% endhighlight %}

The basic idea of Kadane’s algorithm is to scan the entire array and at each position find the maximum sum of the subarray ending there. This is achieved by keeping a currMax for the current array index and a globalMax. The algorithm is as follows:

![arr](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/arr/arr99.png)

![arr](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/arr/arr100.png)

![arr](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/arr/arr101.png)
![arr](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/arr/arr102.png)
![arr](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/arr/arr103.png)
![arr](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/arr/arr104.png)
![arr](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/arr/arr105.png)
![arr](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/arr/arr106.png)
![arr](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/arr/arr107.png)
![arr](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/arr/arr108.png)
![arr](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/arr/arr109.png)
![arr](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/arr/arr110.png)