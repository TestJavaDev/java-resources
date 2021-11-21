---
layout: default
title: Challenge 10
parent: Hash Tables
grand_parent: Data Structures
nav_order: 10
permalink: /data_structures/hash_tables/ch10
---
<div align="center" markdown="1">
Challenge 10 / Java resources / Tutorial

{: .fs-8 .fw-400 }
</div>

## Challenge 10: Find Two Numbers that Add up to "n"

Given an array and a number "n", find two numbers from the array that sums up to "n". Implement your solution in Java and see if your output matches with the correct output.

## Problem Statement 
In this problem, you have to implement the int[] findSum(int[] arr, int n) function, which will take a number n, and an array arr as input and returns an array of two integers that add up to n in an array. You are required to return only one such pair. If no such pair found then simply return the array.

## Function Prototype
int[] findSum(int[] arr, int n)

## Output 
An array with two integers a and b that add up to a given number.

## Sample Input 
arr = {1, 21, 3, 14, 5, 60, 7, 6}
value = 27

## Sample Output 
arr = {21, 6} or {6, 21}

![has](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/has/has45.png)

## Coding Exercise

{% highlight java %}
class CheckSum
{   
  public static int[] findSum(int[] arr, int n) 
  {
    int[] result = new int[2];
    // write your code here
    return result;   // return the elements in the array whose sum is equal to the value passed as parameter 
  }
}
{% endhighlight %}

## Solution Review: Find Two Numbers that Add up to "n"

## Solution Review: Using HashSet

{% highlight java %}
class CheckSum{   
  public static int[] findSum(int[] arr, int n) 
  {
    int[] result = new int[2];
    Set<Integer> set = new HashSet<Integer>();
    for(int i: arr) 
    {
      if(set.contains(n - i)){
          result[0] = i;
          result[1] = n - i;
          break;
      }
      set.add(i);
    }
    return result;   // return the elements in the array whose sum is equal to the value passed as parameter 
  }

  public static void main(String args[]) 
  {
    int n = 0;
    int[] arr1 = {};
    if(arr1.length > 0){
      int[] arr2 = findSum(arr1, n);
      int num1 = arr2[0];
      int num2 = arr2[1];

      if((num1 + num2) != n)
        System.out.println("Not Found");
      else {
        System.out.println("Number 1 = " + num1);
        System.out.println("Number 2 = " + num2);
        System.out.println("Sum = " +  (n) );

      }
    } else {
      System.out.println("Input Array is Empty!");
    }
  }
}
{% endhighlight %}

![has](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/has/has46.png)