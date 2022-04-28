---
layout: default
title: Challenge 1
parent: Heaps
grand_parent: Data Structures
nav_order: 1
permalink: /data_structures/heaps/ch1
---
<div align="center" markdown="1">
Challenge 1 / Java resources / Tutorial

{: .fs-8 .fw-400 }
</div>

## Challenge 1: Convert a Max-Heap to a Min-Heap

If you are given a Max Heap, can you convert it into a Min Heap? A solution is placed in the "solution" section to help you, but we would suggest you try to solve it on your own first.

## Problem Statement
In this problem, you have to implement the convertMax() function to convert a Binary Max Heap into a Binary Min Heap. An illustration is also provided for your understanding.

## Function Prototype:
void convertMax(int []maxHeap);
Here, maxHeap is an array which is given in maxHeap format, i.e. the parent is greater than its children. It’s a Binary Max Heap, meaning that for a particular node there can be a max. of 2 children (left and right respectively).

## Output
It does not return anything. The maxHeap array is manipulated and changed to a min-heap.

## Sample Input
[9,4,7,1,-2,6,5];

## Sample Output
[-2,1,5,9,4,6,7]

## Explanation

![heap](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/heap/res50.png)

![heap](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/heap/res51.png)

## Coding Exercise

{% highlight java %}
class CheckConvert {

  public static void convertMax(int[] maxHeap) {

    //Write Your Code Here
  }
}
{% endhighlight %}

## Solution Review: Convert a Max-Heap to a Min-Heap

## Solution

{% highlight java %}
class CheckConvert {

  public static void convertMax(int[] maxHeap) {

    //Consider maxHeap just an ordinary unsorted array 
    //Build minHeap of the given array. (We already covered that in previous lesson)
    //Return converted array in String format
    buildMinHeap(maxHeap, maxHeap.length);

  }

  private static void buildMinHeap(int[] heapArray, int heapSize) {

    // swap smallest child to parent node 
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

      if (smallest != index) { // swap parent with smallest child
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
    int[] heapArray = {9,4,7,1,-2,6,5};
    System.out.println("Max Heap: " + Arrays.toString(heapArray));
    convertMax(heapArray);
    System.out.println("Min Heap: " + Arrays.toString(heapArray));

  }
}
{% endhighlight %}

![heap](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/heap/res52.png)

