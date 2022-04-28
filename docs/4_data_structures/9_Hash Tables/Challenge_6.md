---
layout: default
title: Challenge 6
parent: Hash Tables
grand_parent: Data Structures
nav_order: 6
permalink: /data_structures/hash_tables/ch6
---
<div align="center" markdown="1">
Challenge 6 / Java resources / Tutorial

{: .fs-8 .fw-400 }
</div>

## Challenge 6: Find If a Subarray with a Sum Equal to 0 Exists

Given an array with positive and negative integers, can you extract a contiguous sub-array from it which adds up to zero? A solution is placed in the "solution" section to help you, but we would suggest you try to solve it on your own first.

## Problem Statement
In this problem, you have to implement the findSubZero() function to check whether a given array has a contiguous subarray with a sum equal to zero. An illustration is also provided for your understanding.

## Function Prototype:
boolean findSubZero(int[] arr);
Here, arr is an Integer array.

## Output:
It returns true if a contiguous subarray exists with a sum equal to 0, or else the function returns false.

## Sample Input
arr = {6, 4, -7, 3, 12, 9}

## Sample Output
true

## Explanation
The SubArray from index 1 to 3 has sums equal to zero, i.e.

arr[1] + arr[2] + arr[3] = 0

4 - 7 + 3 = 0

![has](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/has/has34.png)

## Coding Exercise

{% highlight java %}
//Hash Set  =>  HashSet<Integer> hSet = new HashSet<>();
//HashMap   =>  HashMap<Integer,String> hMap = new HashMap<>();  
//HashTable =>  Hashtable<Integer,String> hTable = new Hashtable<>();  
//Hash Set Functions => {add(), remove(), contains()}
//Hash Map and Table Functions => {put(key,value), get(key), remove(key), containsKey(key), containsValue(value)}
class CheckSubZero {

  public static boolean findSubZero(int[] arr) {

    // Write - Your - Code    
    return false;
  }
}
{% endhighlight %}

## Solution Review: Find if a subarray with a sum equal to 0 exists.

## Solution: Iterative Hashing

{% highlight java %}
//Hash Set  =>  HashSet<Integer> hSet = new HashSet<>();
//HashMap   =>  HashMap<Integer,String> hMap = new HashMap<>();  
//HashTable =>  Hashtable<Integer,String> hTable = new Hashtable<>();  
//Hash Set Functions => {add(), remove(), contains()}
//Hash Map and Table Functions => {put(key,value), get(key), remove(key), containsKey(key), containsValue(value)}
class CheckSubZero {

  public static boolean findSubZero(int[] arr) {

    //Use HashMap to store Sum as key and index i as value till sum has been calculated.
    //Traverse the array and return true if either 
    //arr[i] == 0 or sum == 0 or HashMap already contains the sum
    //If you completely traverse the array and havent found any of the above three
    //conditions then simply return false.
    HashMap < Integer,Integer > hMap = new HashMap < >();

    int sum = 0;

    // Traverse through the given array
    for (int i = 0; i < arr.length; i++) {
      sum += arr[i];

      if (arr[i] == 0 || sum == 0 || hMap.get(sum) != null) return true;

      hMap.put(sum, i);
    }

    return false;
  }

  public static void main(String args[]) {

    int[] arr = {6, 4, -7, 3, 12, 9};
    System.out.println(findSubZero(arr));

  }
}
{% endhighlight %}

![has](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/has/has35.png)