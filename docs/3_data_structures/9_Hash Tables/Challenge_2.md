---
layout: default
title: Challenge 2
parent: Hash Tables
grand_parent: Data Structures
nav_order: 2
permalink: /data_structures/hash_tables/ch2
---
<div align="center" markdown="1">
Challenge 2 / Java resources / Tutorial

{: .fs-8 .fw-400 }
</div>

## Challenge 2: Check if the given arrays are disjoint

If you are given two arrays, arr1 and arr2, can you check if these arrays are disjoint? A solution is placed in the "solution" section to help you, but we would suggest you try to solve it on your own first.

## Problem Statement
In this problem, you have to implement the isDisjoint() function to check whether two given arrays are disjoint or not. Disjoint arrays mean that their intersection returns nothing or there are no common elements in them. The assumption is that there are no duplicate elements in each array. An illustration is also provided for your understanding.

## Function Prototype:
boolean isDisjoint(int []arr1,int[]arr2);
Here, arr1 and arr2 are integer arrays.

## Output:
It returns true if arr1 and arr2 are disjoint, or else it returns false.

## Sample Input
arr1 = [9,4,3,1,-2,6,5]
arr2 = [7,10,8]

## Sample Output
true

## Explanation
arr1 and arr2 have no common elements, so both of them are disjoint arrays.

![has](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/has/has25.png)

## Coding Exercise

{% highlight java %}
//Hash Set  =>  HashSet<Integer> hSet = new HashSet<>();
//HashMap   =>  HashMap<Integer,String> hMap = new HashMap<>();  
//HashTable =>  Hashtable<Integer,String> hTable = new Hashtable<>();  
//Hash Set Functions => {add(), remove(), contains()}
//Hash Map and Table Functions => {put(key,value), get(key), remove(key), containsKey(key), containsValue(value)}
class CheckDisjoint {

  public static Object isDisjoint(int[] arr1,int[] arr2) {

    // Write - Your - Code    
    return 0;    
  } 
}
{% endhighlight %}

## Solution Review: Check if the given arrays are disjoint

## Solution: Use a HashSet

{% highlight java %}
class CheckDisjoint {

  public static boolean isDisjoint(int[] arr1, int[] arr2) {

    //Create an HashSet and store all values of arr1   
    HashSet < Integer > hSet = new HashSet < >();

    for (int i = 0; i < arr1.length; i++) {
      if (!hSet.contains(arr1[i])) hSet.add(arr1[i]);
    }

    //Traverse arr2 and check if arr1 contains any arr2 element
    for (int i = 0; i < arr2.length; i++) {
      if (hSet.contains(arr2[i])) return false;
    }
    return true;
  }
  
  public static void main(String args[]) {
   
    int[] arr1 = {9, 4, 3, 1, -2, 6, 5};
    int[] arr2 = {7, 10, 8};
    int[] arr3 = {1, 12};
    System.out.println(isDisjoint(arr1, arr2));
    System.out.println(isDisjoint(arr1, arr3));
    
  }
}
{% endhighlight %}

![has](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/has/has26.png)