---
layout: default
title: Challenge 7
parent: Hash Tables
grand_parent: Data Structures
nav_order: 7
permalink: /data_structures/hash_tables/ch7
---
<div align="center" markdown="1">
Challenge 7 / Java resources / Tutorial

{: .fs-8 .fw-400 }
</div>

## Challenge 7: First Non-Repeating Integer in an Array

Given an array, find the first integer which is unique in the array using hashing technique. Implement your solution in Java and see if it runs correctly!

## Problem Statement
In this problem, you have to implement the int findFirstUnique(int[] arr) function that will look for a first unique integer which appears only once in the whole array. You must use hashing to implement this function in the most optimized way possible.

Note: We consider zero to be an integer for the premise of this challenge.

## Function Prototype
int findFirstUnique(int[] arr)

## Output
The first unique element in the array.

## Sample Input
arr = {9, 2, 3, 2, 6, 6}

## Sample Output
9

![has](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/has/has36.png)

Note: We already covered this problem in chapter 2, but the approach used was different. Previously, a brute-force strategy was used because Hash Tables had not been discussed then. That solution was inefficient and should not be used in a technical interview. Now, let us create an optimized solution for the same problem using hashing!

## Coding Challenge

{% highlight java %}
class CheckFirstUnique
{
  public static int findFirstUnique(int[] arr) 
  {
    int result = 0;
    // write your code here
    return result;
  }
}
{% endhighlight %}

## Solution Review: First Non-Repeating Integer in an Array

## Solution: Using a HashMap

{% highlight java %}
class CheckFirstUnique {
    public static int findFirstUnique(int[] arr) {

        Map<Integer, Integer> countElements = new HashMap<>();
        //If the element does not exist in the HashMap
        //Add that element with value = 0
        //or else update the number of occurrences of that element by adding 1
        for (int i = 0; i < arr.length; i++) {
            if(countElements.containsKey(arr[i])){
                int occurence = countElements.get(arr[i]) + 1;
                countElements.put(arr[i], occurence);
            }
            else
                countElements.put(arr[i], 0); 
        }
        //Traverse the array and check the number of occurrences
        //Return the first element with 0 occurences
        for (int i = 0; i < arr.length; i++) {
            if (countElements.get(arr[i]) == 0) {
                return arr[i];
            }
        }
        //If no such element is found, return -1
        return -1;
    }

    public static void main(String args[]) {

        int[] arr = {2, 54, 7, 2, 6, 54};

        System.out.println("Array: " + Arrays.toString(arr));

        int unique = findFirstUnique(arr);
        System.out.print("First Unique in an Array: " + unique);

    }
}
{% endhighlight %}

![has](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/has/has37.png)

## Solution: Using a TreeMap

{% highlight java %}
class CheckFirstUnique {
    public static int findFirstUnique(int[] arr) {

        Map<Integer, Integer> countElements = new TreeMap<>(); //TreeMap is sorted
        //If the element does not exist in the TreeMap
        //Add that element with value = 0
        //or else update the number of occurrences of that element by adding 1
        for (int i = 0; i < arr.length; i++) {
            if(countElements.containsKey(arr[i])){
                int occurence = countElements.get(arr[i]) + 1;
                countElements.put(arr[i], occurence);
            }
            else
                countElements.put(arr[i], 0); 
        }
        //Traverse the array and check the number of occurrences
        //Return the first element with 0 occurences
        for (int i = 0; i < arr.length; i++) {
            if (countElements.get(arr[i]) == 0) {
                return arr[i];
            }
        }
        //If no such element is found, return -1
        return -1;
    }

    public static void main(String args[]) {

        int[] arr = {2, 54, 7, 2, 6, 54};

        System.out.println("Array: " + Arrays.toString(arr));

        int unique = findFirstUnique(arr);
        System.out.print("First Unique in an Array: " + unique);

    }
}
{% endhighlight %}

![has](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/has/has38.png)