---
layout: default
title: Challenge 7
parent: Arrays
grand_parent: Data Structures
nav_order: 7
permalink: /data_structures/arrays/ch7
---
<div align="center" markdown="1">
Challenge 7 / Java resources / Tutorial

{: .fs-8 .fw-400 }
</div>

## Challenge 7: Find Second Maximum Value in an Array

## Problem Statement 
In this problem, you have to implement the int findSecondMaximum(int[] arr) method, which will traverse the whole array and return the second largest element present in the array.

Assumption: Array should contain at least two unique elements.

## Method Prototype 
int findSecondMaximum(int[] arr)

## Output 
Second largest element present in the array.

## Sample Input 
arr = {9,2,3,6}

## Sample Output 
6

![arr](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/arr/arr87.png)


## Coding Exercise

{% highlight java %}
class CheckSecondMax {
  
  public int findSecondMaximum(int[] arr)
  {
    // Write - Your - Code
    return -1;
  }
}
{% endhighlight %}

## Solution Review: Find Second Maximum Value in an Array

## Solution #1: Traversing the Array Twice

{% highlight java %}
class CheckSecondMax
{

  public static int findSecondMaximum(int[] arr) {

    int max = Integer.MIN_VALUE;;
    int secondmax = Integer.MIN_VALUE;

    // Find the maximum value in the array by comparing each index with max
    // If an element is greater than max then update max to be equal to it
    for (int i = 0; i < arr.length; i++) {
      if (arr[i] > max) 
        max = arr[i];

    }//end of for-loop

    // Find the second maximum value by comparing each index with secondmax
    // If an element is greater than secondmax and not equal to previously 
    // calculated max, then update secondmax to be equal to that element.
    for (int i = 0; i < arr.length; i++) {
      if (arr[i] > secondmax && arr[i] < max) 
        secondmax = arr[i];

    }//end of for-loop

    return secondmax;
  } 

  public static String arrayToString(int arr[]){
    if (arr.length > 0){
      String result = "";
      for(int i = 0; i < arr.length; i++) {
        result += arr[i] + " ";
      }
      return result;
    }
    else {
      return "Empty Array!";
    }
  }

  public static void main(String args[]) {

    int[] arr = {-2, -33, -10, -456};

    System.out.println("Array: " + arrayToString(arr));

    int secMax = findSecondMaximum(arr);

    System.out.println("Second maximum: " + secMax);

  }
}

{% endhighlight %}

## Explanation 
We traverse the array twice. In the first traversal, we find the maximum element. In the second traversal, find the greatest element less than the element obtained in the first traversal.

## Time Complexity 
The time complexity of the solution is in O(n) since the array is traversed twice but in separate loops. Which means O(n + n) \Rightarrow O(n)O(n+n)⇒O(n)

## Solution #2: Traversing the Array Only Once

{% highlight java %}
 class CheckSecondMax {
  //Returns second maximum value from given Array 
  public static int findSecondMaximum(int[] arr) {

    int max = Integer.MIN_VALUE;;
    int secondmax = Integer.MIN_VALUE;

    // Keep track of Maximum value, whenever the value at an array index is greater
    // than current Maximum value then make that max value 2nd max value and
    // make that index value maximum value  
    for (int i = 0; i < arr.length; i++) {
      if (arr[i] > max) {
        secondmax = max;
        max = arr[i];
      }
      else if (arr[i] > secondmax && arr[i] != max) {
        secondmax = arr[i];
      }
    }//end of for-loop

    return secondmax;
  } //end of findSecondMaximum
  
  public static String arrayToString(int arr[]){
    if (arr.length > 0){
      String result = "";
      for(int i = 0; i < arr.length; i++) {
        result += arr[i] + " ";
      }
      return result;
    }
    else {
      return "Empty Array!";
    }
  }

  public static void main(String args[]) {

    int[] arr = {-2, -33, -10, -456};

    System.out.println("Array: " + arrayToString(arr));

    int secMax = findSecondMaximum(arr);

    System.out.println("Second maximum: " + secMax);

  }
}
{% endhighlight %}

## Explanation 
We initialize two variables max and secondmax to Integer.MIN_VALUE having value -2147483648, which is the maximum integer negative value range. We then traverse the array, and if the current element in the array is greater than the maximum value, then set secondmax to max and max to the current element. If the current element is greater than the secondmax but less than max, then update secondmax to store the value of the current element. Finally, return the value stored in secondmax.

## Time Complexity 
This solution is in O(n) since the list is traversed once only.