---
layout: default
title: Challenge 2
parent: Heaps
grand_parent: Data Structures
nav_order: 2
permalink: /data_structures/heaps/ch2
---
<div align="center" markdown="1">
Challenge 2 / Java resources / Tutorial

{: .fs-8 .fw-400 }
</div>

## Challenge 2: Find the k Smallest Elements in an Array

If you are given an array and any number "k", can you write a code to find the "k" smallest elements using a Min Heap?

## Problem Statement
In this problem, you have to implement the findKSmallest() function to take an array as input and find the “k” smallest elements in the array using Min Heap. An illustration is also provided for your understanding.

## Function Prototype
int[] findKSmallest(int []arr,int k);
Here, arr is an unsorted integer array and k is an integer.

## Output
It returns the integer array containing first k smallest elements from arr

## Sample Input
    arr = [9,4,7,1,-2,6,5]        
    k = 3

## Sample Output
    [-2,1,4]

## Explanation
As “k” is 3, we need to find the top 3 minimum elements from the given array. -2 is minimum value in the array, while 1 is the second-minimum, and 4 is the third-minimum.

![heap](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/heap/res53.png)

## Coding Exercise

{% highlight java %}
class checkSmall {

	public static int[] findKSmallest(int[] arr,int k) {

		int[] result = new int[k]; 
    
        // Write - Your - Code   
		    return result;
	} 
}

{% endhighlight %}

## Solution Review: Find the k Smallest Elements in an Array

## Solution: removeMin() kk times

{% highlight java %}
//Build minHeap of the given array. 
//Extract the minimum element/root and add it to the result
//Keep removing elements and repeatedly build minHeap till we reach K.
class CheckSmall 
{
  public static int[] findKSmallest(int[] arr, int k) 
  {
    int arraySize = arr.length;
    if(k <= arraySize)
    {
      int[] result = new int[k];   
      for (int i = 0; i < k; i++) 
      {
        result[i] = removeMin(arr, arraySize);
        --arraySize;
      }
      return result;
    }
    System.out.println("Value of k = " + k+ "out of bounds!");
    return arr;
  }

  public static int removeMin(int[] heapArray, int heapSize)
  {
    buildMinHeap(heapArray, heapSize);
    int min = heapArray[0];
    heapArray[0] =  heapArray[heapSize-1];
    return min;
  }
  private static void buildMinHeap(int[] heapArray, int heapSize) {

    // swap largest child to parent node 
    for (int i = (heapSize - 1) / 2; i >= 0; i--) {
      minHeapify(heapArray, i, heapSize);
    }
  }

  private static void minHeapify(int[] heapArray, int index, int heapSize) {
    int smallest = index;

    while (smallest < heapSize / 2) { // check parent nodes only
      int left = (2 * index) + 1; //left child
      int right = (2 * index) + 2; //right child
      if (left < heapSize && heapArray[left] < heapArray[index]) {
        smallest = left;
      }

      if (right < heapSize && heapArray[right] < heapArray[smallest]) {
        smallest = right;
      }

      if (smallest != index) { // swap parent with largest child
        int temp = heapArray[index];
        heapArray[index] = heapArray[smallest];
        heapArray[smallest] = temp;
        index = smallest;
      } else {
        break; // if heap property is satisfied
      }

    } //end of while
  }

  public static void main(String args[]) {
    int[] input = {9, 4, 7, 1, -2, 6, 5};
    int[] output = findKSmallest(input, 2);

    for(int i = 0; i < output.length; i++) 
      System.out.println(output[i]);
  }

}
{% endhighlight %}

![heap](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/heap/res54.png)