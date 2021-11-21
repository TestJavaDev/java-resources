---
layout: default
title: Challenge 3
parent: Heaps
grand_parent: Data Structures
nav_order: 3
permalink: /data_structures/heaps/ch3
---
<div align="center" markdown="1">
Challenge 3 / Java resources / Tutorial

{: .fs-8 .fw-400 }
</div>

## Challenge 3: Find the k Largest Elements in an Array

If you are given an array and any number "k", can you write a code to find the "k" largest elements using a Max Heap?

## Problem Statement
In this problem, you have to implement the findKlargest() function to take an array as input and find the “k” largest elements in the array using a Max Heap. An illustration is also provided for your understanding.

## Function Prototype
int[] findKLargest(int []arr,int k);
Here, arr is an unsorted integer array and k is an integer.

## Output:
It returns the integer array containing the first k largest elements from arr

## Sample Input
arr = [9,4,7,1,-2,6,5]           k = 3

## Sample Output
[9,7,6]

## Explanation
As “k” is 3, we need to find the top 3 maximum elements from the given array. 9 is the largest value in the array, while 7 is the second-largest, and 6 is the third-largest.

![heap](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/heap/res55.png)

## Coding Exercise

{% highlight java %}
class CheckLarge {
	public static int[] findKLargest(int[] arr,int k) 
  {
		int[] result = new int[k]; 
    // Write - Your - Code    
    return result;
	} 
}
{% endhighlight %}

## Solution Review: Find the k Largest Elements in an Array

## Solution: Creating a Max-Heap and removing max kk times

{% highlight java %}
//Build maxHeap of the given array. 
//Extract the maximum element/root and add it to the result
//Reduce the length of array and repeatedly build maxHeap till we reach K.
class CheckLarge 
{
  public static int[] findKLargest(int[] arr, int k) {
    int arraySize = arr.length;
    if ( k <= arraySize) {      
      int[] result = new int[k];	// build the result array of size = k
      for (int i = 0; i < k; i++) {
        buildMaxHeap(arr, arraySize);
        result[i] = arr[0];
        arr[0] = arr[--arraySize];
      }
      return result;
    }
    System.out.println("Value of k = " + k + "Out of Bounds");
    return arr;
  }

  private static void buildMaxHeap(int[] heapArray, int heapSize) {

    // swap largest child to parent node 
    for (int i = (heapSize - 1) / 2; i >= 0; i--) {
      maxHeapify(heapArray, i, heapSize);
    }
  }

  private static void maxHeapify(int[] heapArray, int index, int heapSize) {
    int largest = index;

    while (largest < heapSize / 2) { // check parent nodes only
      int left = (2 * index) + 1; //left child
      int right = (2 * index) + 2; //right child
      if (left < heapSize && heapArray[left] > heapArray[index]) {
        largest = left;
      }

      if (right < heapSize && heapArray[right] > heapArray[largest]) {
        largest = right;
      }

      if (largest != index) { // swap parent with largest child
        int temp = heapArray[index];
        heapArray[index] = heapArray[largest];
        heapArray[largest] = temp;
        index = largest;
      } else {
        break; // if heap property is satisfied
      }

    } // end of while
  }

  public static void main(String args[]) {
    int[] input = {9, 4, 7, 1, -2, 6, 5};
    int[] output = findKLargest(input, 2);

    for(int i = 0; i < output.length; i++) 
      System.out.println(output[i]);
  }

}
{% endhighlight %}

![heap](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/heap/res56.png)