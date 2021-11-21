---
layout: default
title: Challenge 1
parent: Hash Tables
grand_parent: Data Structures
nav_order: 1
permalink: /structures/hash_tables/ch1
---
<div align="center" markdown="1">
Challenge 1 / Java resources / Tutorial

{: .fs-8 .fw-400 }
</div>

## Challenge 1: Find whether an array is a subset of another array

Can you find whether a given array is a subset of another by using a built-in Hash Table? A solution is placed in the "solution" section to help you, but we would suggest you try to solve it on your own first.

## Problem Statement
In this problem, you have to implement the isSubset() function to take two arrays as input and check whether an array is a subset of another given array.

Note: Both of these arrays represent sets, therefore, they do not contain duplicate values.

Use the built-in HashSet() class. It works like a Hash Table at the back-end and comes in handy during Java interviews.

An illustration of the problem is also provided for your understanding.

## Function Prototype:
boolean isSubset(int []arr1,int[]arr2);
Here, arr1 and arr2 are integer arrays.

## Output:
It returns true if arr2 is a subset of arr1, or else it returns false

## Sample Input
arr1 = [9,4,7,1,-2,6,5]
arr2 = [7,1,-2]
Arrays representing sets.

## Sample Output
true

## Explanation
[7,1,-2] is present in arr1 from index 2 to 4, therefore arr2 is a subset of arr1.

![has](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/has/has23.png)

## Coding Exercise

{% highlight java %}
//Hash Set  =>  HashSet<Integer> hSet = new HashSet<>();
//HashMap   =>  HashMap<Integer,String> hMap = new HashMap<>();  
//HashTable =>  Hashtable<Integer,String> hTable = new Hashtable<>();  
//Hash Set Functions => {add(), remove(), contains()}
//Hash Map and Table Functions => {put(key,value), get(key), remove(key), containsKey(key), containsValue(value)}
class CheckSubset {
  public static boolean isSubset(int[] arr1, int[] arr2) {
    // write your code here	
    return false;
  }
}
{% endhighlight %}

## Solution Review: Find whether an array is a subset of another array

## Solution: Lookup in a Hash Table

{% highlight java %}
class CheckSubset {
  static boolean isSubset(int arr1[], int arr2[]) {
    HashSet<Integer> hset= new HashSet<>(); 
    // hset stores all the values of arr1 
    for(int i = 0; i < arr1.length; i++) { 
      if(!hset.contains(arr1[i])) 
        hset.add(arr1[i]); 
    } 

    // loop to check if all elements of arr2 also 
    // lies in arr1 
    for(int i = 0; i < arr2.length; i++) { 
      if(!hset.contains(arr2[i])) 
        return false; 
    } 
    return true; 
  }
  
  public static void main(String args[]) {
    
    int[] arr1 = {9, 4, 7, 1, -2, 6, 5};
    int[] arr2 = {7, 1, -2};
    int[] arr3 = {10, 12};

    System.out.println(isSubset(arr1, arr2));
    System.out.println(isSubset(arr1, arr3));
  }
}
{% endhighlight %}

![has](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/has/has24.png)