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

## Challenge 9: Re-arrange Positive & Negative Values

Problem Statement #
In this problem, you have to implement the void reArrange(int[] arr) method, which will sort the elements, such that all the negative elements appear at the left and positive elements appear at the right.

Note: Consider 0 as a positive number.

Method Prototype #
void reArrange(int[] arr)
Output #
A sorted array with negative elements at the left and positive elements at the right.

Sample Input #
arr = {10, -1, 20, 4, 5, -9, -6}
Sample Output #
arr = {-1, -9, -6, 10, 20, 4, 5}
Note: Order of the numbers doesn’t matter.

{-1, -9, -6, 10, 20, 4, 5} = {-9, -1, -6, 10, 4, 20, 5}

![arr](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/arr/arr89.png)

## Coding Exercise

{% highlight java %}
class CheckReArrange {

  public static void reArrange(int[] arr) {

    //Write - Your - Code        
  }
}
{% endhighlight %}

## Solution Review: Re-arrange Positive & Negative Values

## Solution# 1: Using New Array

{% highlight java %}
class CheckReArrange {

  //Re-Arrange Positive and Negative Values of Given Array 
  public static void reArrange(int arr[]) {

    int[] newArray = new int[arr.length];
    int newArray_index = 0;

    //Fill newArray with Negative Values first.
    //Then Fill it with Postive Values.
    //In the end, insert every element of newArray back into origional arr.
    for (int i = 0; i < arr.length; i++) {
      if (arr[i] < 0)
        newArray[newArray_index++] = arr[i];
    }

    for (int i = 0; i < arr.length; i++) {

      if (arr[i] >= 0)
        newArray[newArray_index++] = arr[i];
    }

    for (int j = 0; j < newArray_index; j++) {
      arr[j] = newArray[j];
    }
  }

  public static void main(String args[]) {
    
    int[] arr = {2, 4, -6, 8, -5, -10};

    System.out.print("Array before re-arranging: ");
    for(int i = 0; i < arr.length; i++)
      System.out.print(arr[i] + " ");
    System.out.println();

    reArrange(arr);

    System.out.print("Array after rearranging: ");
    for(int i = 0; i < arr.length; i++)
      System.out.print(arr[i] + " ");
  }
}
{% endhighlight %}

Explanation #
In this solution, we iterate over the entire given array and copy all negative numbers to a newly created array and then positive ones to this array. In the end, copy them into the original array.

Time Complexity #
Since the given array is iterated over thrice in non-nested loops, the time complexity of this solution is O(n)O(n). Space complexity increased in this case as the new array is created.

## Solution# 2: Re-arranging in Place

{% highlight java %}
class CheckReArrange
{
  //Re-Arrange Positive and Negative Values of Given Array 
  public static void reArrange(int[] arr) 
  {
    int j = 0; 
    for (int i = 0; i < arr.length; i++) { 
      if (arr[i] < 0) {   // if negative number found
        if (i != j) { 
          int temp = arr[i];
          arr[i] = arr[j]; // swapping with leftmost positive
          arr[j] = temp;
        }
        j++; 
      } 
    } 
  } //end of reArrange()

  public static void main(String args[]) {

    int[] arr = {2, 4, -6, 8, -5, -10};

    System.out.print("Array before re-arranging: ");
    for(int i = 0; i < arr.length; i++)
      System.out.print(arr[i] + " ");
    System.out.println();

    reArrange(arr);

    System.out.print("Array after rearranging: ");
    for(int i = 0; i < arr.length; i++)
      System.out.print(arr[i] + " ");
  }
}
{% endhighlight %}

Explanation#
In this solution, we keep two variables i and j. Both of them are 0 initially. i iterates over the array while j keeps track of the position where next encountered negative number should be placed. When we come across a negative number, the values at i and j indexes are swapped, and j is incremented. This continues until the end of the array is reached.
