---
layout: default
title: Challenge 5
parent: Hash Tables
grand_parent: Data Structures
nav_order: 5
permalink: /structures/hash_tables/ch5
---
<div align="center" markdown="1">
Challenge 5 / Java resources / Tutorial

{: .fs-8 .fw-400 }
</div>

## Challenge 5: Find two pairs in an Array such that a+b = c+d

If you are given an array, can you find two pairs such that their sum is equal? A solution is placed in the "solution" section to help you, but we would suggest you try to solve it on your own first.

## Problem Statement
In this problem, you have to implement the findPair() function to find two pairs or 4 elements (a,b,c,d) in an array, such that,

a+b = c+d

You only have to find first two pairs in the array which satisfies the above condition. An illustration is also provided for your understanding.

## Function Prototype: 
String findPair(int[] arr);
Here, arr is an Integer array.

## Output: 
It returns a String containing two pairs, (a,b) and (c,d), which satisfies a+b = c+d.

## Sample Input
arr = {3, 4, 7, 1, 12, 9}

## Sample Output
"{4,12}{7,9}"

## Explanation
4,12,7 and 9 follow the above condition, as 4+12 = 7+9. There are so many other possible pairs in the sample input that satisfy the above condition, but for this problem, we only have to find one of them.

![has](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/has/has32.png)

## Coding Exercise

{% highlight java %}
//Hash Set  =>  HashSet<Integer> hSet = new HashSet<>();
//HashMap   =>  HashMap<Integer,String> hMap = new HashMap<>();  
//HashTable =>  Hashtable<Integer,String> hTable = new Hashtable<>();  
//Hash Set Functions => {add(), remove(), contains()}
//Hash Map and Table Functions => {put(key,value), get(key), remove(key), containsKey(key), containsValue(value)}
class CheckPair {

  public static String findPair(int[] arr) {

    String result = "";

    // Write - Your - Code   
    return result; 
  }
}
{% endhighlight %}

## Solution Review: Find two pairs in an Array such that a+b = c+d

## Solution: Sums Stored as Hash Keys

{% highlight java %}
//Hash Set  =>  HashSet<Integer> hSet = new HashSet<>();
//HashMap   =>  HashMap<Integer,String> hMap = new HashMap<>();  
//HashTable =>  Hashtable<Integer,String> hTable = new Hashtable<>();  
//Hash Set Functions => {add(), remove(), contains()}
//Hash Map and Table Functions => {put(key,value), get(key), remove(key), containsKey(key), containsValue(value)}

class CheckPair {

  public static String findPair(int[] arr) {

    String result = "";

    // Create HashMap with Key being sum and value being a pair i.e key = 3 , value = {1,2}
    // Traverse all possible pairs in given arr and store sums in map
    // If sum already exist then print out the two pairs.
    HashMap < Integer,int[] > hMap = new HashMap < >();

    for (int i = 0; i < arr.length; ++i) {
      for (int j = i + 1; j < arr.length; ++j) {
        int sum = arr[i] + arr[j]; //calculate sum

        if (!hMap.containsKey(sum)) {
          // If sum is not present in Map then insert it alongwith pair
          hMap.put(sum, new int[] {arr[i],arr[j]});
        }
        else {
          //Sum already present in Map
          int[] prev_pair = hMap.get(sum);

          // Since array elements are distinct, we don't
          // need to check if any element is common among pairs
          result += "{" + prev_pair[0] + "," + prev_pair[1] + "}{" + arr[i] + "," + arr[j] + "}";

          return result;
        }
      }
    }//end of for
    return result;
  }
  
  public static void main(String args[]) {
   
     int[] arr = {3, 4, 7, 1, 12, 9};
     System.out.println(findPair(arr));
    
  }
}
{% endhighlight %}

![has](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/has/has33.png)