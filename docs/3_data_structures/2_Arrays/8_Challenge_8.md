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

## Challenge 8: Right Rotate the Array by One Index

Problem Statement #
In this problem, you have to implement the void rotateArray(int[] arr) method, which takes an arr and rotate it right by 1. This means that the right-most elements will appear at the left-most position in the array.

Method Prototype #
void rotateArray(int[] arr)
Output #
Array rotated by one element from right to left

Sample Input #
arr = {1, 2, 3, 4, 5}
Sample Output #
arr = {5, 1, 2, 3, 4}

![arr](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/arr/arr88.png)

## Coding Exercise

{% highlight java %}
class CheckRotateArray{
  
  public static void rotateArray(int[] arr){

        // Write - Your - Code    
    }
}
{% endhighlight %}

## Solution Review: Right Rotate the Array by One Index

{% highlight java %}
class CheckRotateArray
{
  //Rotates given Array by 1 position
  public static void rotateArray(int[] arr) {

    //Store last element of Array.
    //Start from the Second last and Right Shift the Array by one.
    //Store the last element saved on the first index of the Array.
    int lastElement = arr[arr.length - 1];

    for (int i = arr.length - 1; i > 0; i--) {

      arr[i] = arr[i - 1];
    }

    arr[0] = lastElement;
  } //end of rotateArray

  public static void main(String args[]) {

    int[] arr = {3, 6, 1, 8, 4, 2};

    System.out.print("Array before rotation: ");
    for(int i = 0; i < arr.length; i++) {
      System.out.print(arr[i] + " ");
    }
    System.out.println();

    rotateArray(arr);

    System.out.print("Array after rotation: ");
    for(int i = 0; i < arr.length; i++) {
      System.out.print(arr[i] + " ");
    }
  }

} 
{% endhighlight %}

Explanation #
To rotate the array towards the right, we have to move the array elements towards the right by one index. This means every element stored at index i will be moved to i + 1 position. However, if we start shifting elements from the first element of the array, then the element at last index arr[arr.length - 1] is overwritten. Hence first, we save the last element in the variable lastElement. Then we start shifting elements from index i - 1 to i, where the initial value of i will be arr.length - 1, and we will keep shifting the elements until i is greater than 0. When the loop ends, we store the value of lastElement in arr[0].

Time Complexity #
Since the entire array is iterated over once, the time complexity of this solution is O(n)O(n).