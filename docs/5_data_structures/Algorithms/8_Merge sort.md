---
layout: default
title: Merge sort
parent: Algorithms
grand_parent: Data Structures and Algorithms
nav_order: 8
permalink: /data_structures/algorithms/merge_sort
---
<div align="center" markdown="1">
Merge sort / Java resources / Tutorial

{: .fs-8 .fw-400 }
</div>

## Merge sort
Merge sort is a recursive divide and conquer algorithm that essentially divides a given array into two halves, sorts those halves, and merges them together in order. The base case merges two arrays of size 1 so that, eventually, the single elements are merged in order; the merge part is where most of the heavy lifting happens.

{% highlight java %}

class Merge {
 public static void merge(int arr[], int left, int mid, int right) {
  int i, j, k;

  // Initialzing the sizes of the temporary arrays
  int sizeLeft = mid - left + 1;
  int sizeRight = right - mid;

  // Initializing temporary arrays
  int leftArr[] = new int[sizeLeft];
  int rightArr[] = new int[sizeRight];

  // Copying the given array into the temporary arrays
  for (i = 0; i < sizeLeft; i++)
   leftArr[i] = arr[left + i];
  for (j = 0; j < sizeRight; j++)
   rightArr[j] = arr[mid + 1 + j];

  // Merging the temporary arrays back into the given array
  i = 0; // Initial index of first subarray 
  j = 0; // Initial index of second subarray 
  k = left; // Initial index of the given array

  // This is the main part of the algorithm
  // Iterate over both arrays and copy the element that is smaller to the
  // given array. 
  while (i < sizeLeft && j < sizeRight) {
   if (leftArr[i] <= rightArr[j]) {
    arr[k] = leftArr[i];
    i++;
   } else {
    arr[k] = rightArr[j];
    j++;
   }
   k++;
  }

  // Copying the remaining elements of leftArr[], if there are any
  while (i < sizeLeft) {
   arr[k] = leftArr[i];
   i++;
   k++;
  }

  // Copy the remaining elements of rightArr[], if there are any
  while (j < sizeRight) {
   arr[k] = rightArr[j];
   j++;
   k++;
  }
 }

 public static void mergeSort(int arr[], int leftIndex, int rightIndex) {
  // Sanity checks
  if (leftIndex < 0 || rightIndex < 0)
   return;

  if (rightIndex > leftIndex) {
   // Equivalent to (leftIndex+rightIndex)/2, but avoids overflow
   int mid = leftIndex + (rightIndex - leftIndex) / 2;

   // Sorting the first and second halves of the array
   mergeSort(arr, leftIndex, mid);
   mergeSort(arr, mid + 1, rightIndex);

   // Merging the array
   merge(arr, leftIndex, mid, rightIndex);
  }
 }

 public static void main(String args[]) {
  int arr[] = {5,4,1,0,5,95,4,-100,200,0};
  int arrSize = 10;
  mergeSort(arr, 0, arrSize - 1);
  Helper obj = new Helper();
  obj.printArray(arr, arrSize);
 }
}

class Helper
{
  static void printArray(int[]arr, int arrSize) 
  {
    for(int i = 0; i < arrSize; i++)
      System.out.print(arr[i] + " ");
    System.out.println();
  } 
  static int findMin(int[] arr, int start, int end) {
    if(end<=0 || start < 0)
      return 0; 

    int minInd = start;
    for(int i = start+1; i <= end; i++) {
      if(arr[minInd] > arr[i])
        minInd = i;
    }
    return minInd;     
  } 
  int findMax(int[] arr, int start, int end) {
    if(end<=0 || start < 0)
      return 0; 

    int maxInd = start;
    for(int i = start+1; i <= end; i++) {
      if(arr[maxInd] < arr[i])
        maxInd = i;
    }
    return maxInd;     
  }
}
{% endhighlight %}

e mergeSort() function calls itself on the first and second halves of the given array, recursively. Once the base case is reached, i.e., when the condition that rightIndex > leftIndex becomes false, it returns. Then the merge function is called on the array. It works by dividing the given array into two subarrays and merging them by copying the greater element in one subarray back into the given array.

## Time complexity
The time complexity for this algorithm is O(n log n).

Here is an animation to clarify this:

## Merge: Animation

![merge](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/merge/merge1.png)
![merge](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/merge/merge2.png)
![merge](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/merge/merge3.png)
![merge](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/merge/merge4.png)
![merge](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/merge/merge5.png)
![merge](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/merge/merge6.png)
![merge](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/merge/merge7.png)
![merge](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/merge/merge8.png)
![merge](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/merge/merge9.png)
![merge](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/merge/merge10.png)
![merge](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/merge/merge11.png)
![merge](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/merge/merge12.png)
![merge](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/merge/merge13.png)
![merge](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/merge/merge14.png)

## Merge sort: Animation

Here’s how merge works in context:

![merge](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/merge/merge15.png)
![merge](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/merge/merge16.png)
![merge](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/merge/merge17.png)
![merge](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/merge/merge18.png)
![merge](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/merge/merge19.png)
![merge](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/merge/merge20.png)
![merge](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/merge/merge21.png)
![merge](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/merge/merge22.png)
![merge](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/merge/merge23.png)

