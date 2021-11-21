---
layout: default
title: Challenge 3
parent: Hash Tables
grand_parent: Data Structures
nav_order: 3
permalink: /structures/hash_tables/ch3
---
<div align="center" markdown="1">
Challenge 3 / Java resources / Tutorial

{: .fs-8 .fw-400 }
</div>

## Challenge 3: Find symmetric pairs in an Array

If you are given a two-dimensional array, can you find a symmetric pair in that array? A solution is placed in the "solution" section to help you, but we would suggest you try to solve it on your own first.

## Problem Statement
In this problem, you have to implement the findSymmetric() function to find all the symmetric pairs in the given array. By definition, (a,b) and (c,d) are symmetric pairs if a = d and b = c. An illustration is also provided for your understanding.

## Function Prototype:
String findSymmetric(int [][]arr);
Here, arr is a 2D array containing pairs of integers.

## Output:
It returns a String containing the first occurance of all of the symmetric pairs of integers in the given array, arr.

## Sample Input
arr[][] = [{1, 2}, {3, 4}, {5, 9}, {4, 3}, {9, 5}]

## Sample Output
"{3,4}{5,9}"
Note: We will return {3, 4} and {5, 9} instead of {4, 3} and {9, 5} because the former occured first.

## Explanation
{ 3 , 4 } has a symmetrical pair to { 4 , 3 } in the given array, Similarly, { 5 , 9 } has a symmetrical pair to { 9 , 5 }.

![has](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/has/has27.png)

## Coding Exercise

{% highlight java %}
//Hash Set  =>  HashSet<Integer> hSet = new HashSet<>();
//HashMap   =>  HashMap<Integer,String> hMap = new HashMap<>();  
//HashTable =>  Hashtable<Integer,String> hTable = new Hashtable<>();  
//Hash Set Functions => {add(), remove(), contains()}
//Hash Map and Table Functions => {put(key,value), get(key), remove(key), containsKey(key), containsValue(value)}
class CheckSymmetric {

  public static String findSymmetric(int[][] arr) {

    String result = "";

    // Write - Your - Code    
    return result; 
  }
}
{% endhighlight %}

## Solution Review: Find symmetric pairs in an Array

## Solution: Using HashMap

{% highlight java %}
class CheckSymmetric {

  public static String findSymmetric(int[][] arr) {
    //Create an empty Hash Map
    //Traverse given Array
    //Look for second element of each pair in the hash. i.e for pair (1,2) look for key 2 in map.
    //If found then store it in the result array, otherwise insert the pair in hash
    HashMap < Integer,Integer > hashMap = new HashMap < Integer,Integer >();

    String result = "";

    //Traverse through the given array
    for (int i = 0; i < arr.length; i++) {
      int first = arr[i][0];
      int second = arr[i][1];

      Integer value = hashMap.get(second);

      if (value != null && value == first) {
        //Symmetric Pair found
        result += "{" + String.valueOf(second) + "," + String.valueOf(first) + "}";
      }
      else 
        hashMap.put(first, second);
    }
    return result;
  }

  public static void main(String args[]) {

    int[][] arr = { {1, 2}, {3, 4}, {5, 9}, {4, 3}, {9, 5} };
    String symmetric = findSymmetric(arr);
    System.out.println(symmetric);

  }

}
{% endhighlight %}

![has](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/has/has28.png)