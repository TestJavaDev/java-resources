---
layout: default
title: Challenge 5
parent: Arrays
grand_parent: Data Structures
nav_order: 5
permalink: /data_structures/arrays/ch5
---
<div align="center" markdown="1">
Challenge 5 / Java resources / Tutorial

{: .fs-8 .fw-400 }
</div>

## Challenge 5: Find Minimum Value in Array

## Problem Statement 
In this problem, you have to implement the int findMinimum(int[] arr) method, which will traverse the whole array and find the smallest number in the array.

## Method Prototype 
int findMinimum(int[] arr)

## Output 
The smallest number in the array.

## Sample Input 
arr = {9, 2, 3, 6}

## Sample Output 
2

![arr](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/arr/arr85.png)

## Coding Exercise

{% highlight java %}
class CheckMinimum {

  public static int findMinimum(int[] arr) {
    // Write your code here
    return Integer.MAX_VALUE;        
  }
}
{% endhighlight %}

## Solution Review: Find Minimum Value in an Array

{% highlight java %}
class CheckMinimum
{
  //Returns minimum value from given Array 
  public static int findMinimum(int[] arr) {

    int minimum = arr[0];

    //At every Index compare its value with minimum and if its less 
    //then make that index value new minimum value
    for (int i = 1; i < arr.length; i++) {

      if (arr[i] < minimum) {
        minimum = arr[i];
      }
    }
    return minimum;
  } //end of findMinimum

  public static void main(String args[]) {

    int[] arr = { 9, 2, 3, 6};

    System.out.print("Array : ");
    for(int i = 0; i < arr.length; i++)
      System.out.print(arr[i] + " ");
    System.out.println();

    int min = findMinimum(arr);
    System.out.println("Minimum in the Array: " + min);

  }

} 
{% endhighlight %}

## Explanation 
Start with the first element, which is 9 in this example, and save it in minimum as the smallest value. Then, iterate over the rest of the array and compare the minimum to each element. If any element is smaller than the minimum, then set the minimum to that element. By the end of the array, the number stored in the minimum will be the smallest integer in the whole array.

## Time Complexity 
Since the entire list is iterated over once, this algorithm is in linear time, O(n).