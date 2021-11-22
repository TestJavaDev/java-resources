---
layout: default
title: Challenge 3
parent: Arrays
grand_parent: Data Structures
nav_order: 3
permalink: /data_structures/arrays/ch3
---
<div align="center" markdown="1">
Challenge 3 / Java resources / Tutorial

{: .fs-8 .fw-400 }
</div>

## Challenge 3: Find Two Numbers that Add up to "n"

Problem Statement#
In this problem, you have to implement the int[] findSum(int[] arr, int n) method, which will take a number n, and an array arr as input and returns an array of two integers that add up to n in an array. You are required to return only one such pair. If no such pair is found then simply return the array.

Method Prototype#
int[] findSum(int[] arr, int n)
Output#
An array with two integers a and b that add up to a given number or the original array in case a pair is not found.

Sample Input#
arr = {1, 21, 3, 14, 5, 60, 7, 6}
value = 27
Sample Output#
arr = {21, 6} or {6, 21}

![arr](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/arr/arr82.png)

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

## Solution #1: Brute Force

{% highlight java %}
class CheckSum{   

  public static int[] findSum(int[] arr, int n) 
  {    
    int[] result = new int[2]; // to store the pair of values.
    
    for (int i = 0; i < arr.length; i++) { //traverse arr
      for (int j = i + 1; j < arr.length; j++) { //traverse arr again
        if (arr[i] + arr[j] == n) { // find where sum is equal to n
          result[0] = arr[i];
          result[1] = arr[j];
          return result; // return the pair of numbers
        }
      }
    }
    return arr;  
  }

  public static void main(String args[]) {

    int n = 9;
    int[] arr1 = {2, 4, 5, 7, 8};
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

Explanation#
This is the most time-intensive but intuitive solution. Traverse the whole array of the given size. For each element in the array, check if it can add up with any element after it to give the number n. Use a nested for-loop for this purpose and iterate over the entire array for each element.

Time Complexity#
Since we iterate over the entire array in a nested loop, the time complexity is O(n^2)

## Solution #2: Sorting the array

{% highlight java %}
class CheckSum{ 

  //Helper Function to sort given Array (Quick Sort)          
  public static int partition(int[] arr, int low, int high) { 
    int pivot = arr[high];  
    int i = (low - 1); // index of smaller element 
    for (int j = low; j < high; j++) { 
      // If current element is <= to pivot 
      if (arr[j] <= pivot) { 
        i++; 

        // swap arr[i] and arr[j] 
        int temp = arr[i]; 
        arr[i] = arr[j]; 
        arr[j] = temp; 
      } 
    } 

    // swap arr[i+1] and arr[high] (or pivot) 
    int temp = arr[i + 1]; 
    arr[i + 1] = arr[high]; 
    arr[high] = temp; 

    return i + 1; 
  } 

  public static void sort(int[] arr, int low, int high) { 
    if (low < high) { 
      int pi = partition(arr, low, high); 
      sort(arr, low, pi - 1); 
      sort(arr, pi + 1, high); 
    } 
  } 

  //Return 2 elements of arr that sum to the given value
  public static int[] findSum(int[] arr, int n) {
    //Helper sort function that uses the Quicksort Algorithm
    sort(arr, 0, arr.length - 1);   //Sort the array in Ascending Order

    int Pointer1 = 0;    //Pointer 1 -> At Start
    int Pointer2 = arr.length - 1;   //Pointer 2 -> At End

    int[] result = new int[2];
    int sum = 0;

    while (Pointer1 != Pointer2) {

      sum = arr[Pointer1] + arr[Pointer2];  //Calulate Sum of Pointer 1 and 2

      if (sum < n) 
        Pointer1++;  //if sum is less than given value => Move Pointer 1 to Right
      else if (sum > n) 
        Pointer2--; 
      else {
        result[0] = arr[Pointer1];
        result[1] = arr[Pointer2];
        return result; // containing 2 number 
      }
    }
    return arr; 
  } 

  public static void main(String args[]) {

    int n = 9;
    int[] arr1 = {1,2,3,4,5};
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

Explanation #
While solution #1 is very intuitive, it is not very time efficient. A better way to solve this is by first sorting the array. Here,QuickSort is used to sort the array first. Then using two variables, one starting from the first index of the array and second from size-1size−1 index of the array. If the sum of the elements on these indexes of the array is smaller than given value n, then increment index from the start else decrement index from the end until the given value n is equal to the sum. Store the elements on these indexes in result array and return it.

Time Complexity #
Since the sorting function used in this code takes O(nlogn)O(nlogn) and the algorithm to find two numbers takes O(n) time, the overall time complexity of this code is O(nlognO(nlogn).
