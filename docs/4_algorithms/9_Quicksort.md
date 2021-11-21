---
layout: default
title: Quicksort
parent: Algorithm
nav_order: 9
permalink: /algorithms/quicksort
---
<div align="center" markdown="1">
Quicksort / Java resources / Tutorial

{: .fs-8 .fw-400 }
</div>

## Quicksort

## Introduction

Quicksort is the fastest known comparison-based sorting algorithm for arrays in the average case.

Caveat: Merge sort works better on linked lists, and there are other non-comparison based algorithms that outperform quicksort.

## Quick sort algorithm
Start with an array of n elements.

Choose a pivot element from the array to be sorted.

Partition the array into two unsorted subarrays, such that all elements in one subarray are less than the pivot and all the elements in the other subarray are greater than the pivot.

Elements that are equal to the pivot can go in either subarray.

Sort each subarray recursively to yield two sorted subarrays.

Concatenate the two sorted subarrays and the pivot to yield one sorted array.

![quick](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/quick/quick.png)

## Median-of-three strategy

Pick three random elements from the array and find their median. This strategy ensures that the first element is not picked.

![quick](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/quick/quick1.png)
![quick](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/quick/quick2.png)
![quick](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/quick/quick3.png)
![quick](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/quick/quick4.png)
![quick](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/quick/quick5.png)
![quick](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/quick/quick6.png)
![quick](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/quick/quick7.png)
![quick](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/quick/quick8.png)
![quick](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/quick/quick9.png)
![quick](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/quick/quick10.png)
![quick](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/quick/quick11.png)
![quick](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/quick/quick12.png)

![quick](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/quick/quick13.png)

{% highlight java %}
class QuickSort {
 static Helper obj = new Helper();
 public static int choosePivot(int left, int right) {
  Random rand = new Random();
  // Pick 3 random numbers within the range of the array
  int i1 = left + (rand.nextInt(right - left + 1));
  int i2 = left + (rand.nextInt(right - left + 1));
  int i3 = left + (rand.nextInt(right - left + 1));

  // Return their median
  return Math.max(Math.min(i1, i2), Math.min(Math.max(i1, i2), i3));
 }

 public static int partition(int arr[], int left, int right) {
  int pivotInd = choosePivot(left, right); // Index of pivot
  obj.swap(arr, right, pivotInd); // self created function to swap two indices of an array
  int pivot = arr[right]; // Pivot 
  int i = (left - 1); // All the elements less than or equal to the
  // pivot go before or at i

  for (int j = left; j <= right - 1; j++) {
   if (arr[j] <= pivot) {
    i++; // increment the index 
    obj.swap(arr, i, j);
   }
  }
  obj.swap(arr, i + 1, right); // Putting the pivot back in place
  return (i + 1);
 }

 public static void quickSort(int arr[], int left, int right) {
  if (left < right) {
   // pi is where the pivot is at
   int pi = partition(arr, left, right);

   // Separately sort elements before and after partition 
   quickSort(arr, left, pi - 1);
   quickSort(arr, pi + 1, right);
  }
 }
 public static void main(String args[]) {
  int arr[] = {5,4,1,0,5,95,4,-100,200,0};
  int arrSize = 10;
  quickSort(arr, 0, arrSize - 1);
  System.out.print("Sorted array: ");
  obj.printArray(arr, arrSize);
 }
}

class Helper {
 static void swap(int[] array, int i, int j) {
  int temp = array[i];
  array[i] = array[j];
  array[j] = temp;
 }
 static void printArray(int[] arr, int arrSize) {
  for (int i = 0; i < arrSize; i++)
   System.out.print(arr[i] + " ");
  System.out.println();
 }
 static int findMin(int[] arr, int start, int end) {
  if (end <= 0 || start < 0)
   return 0;

  int minInd = start;
  for (int i = start + 1; i <= end; i++) {
   if (arr[minInd] > arr[i])
    minInd = i;
  }
  return minInd;
 }
 int findMax(int[] arr, int start, int end) {
  if (end <= 0 || start < 0)
   return 0;

  int maxInd = start;
  for (int i = start + 1; i <= end; i++) {
   if (arr[maxInd] < arr[i])
    maxInd = i;
  }
  return maxInd;
 }
}
{% endhighlight %}

![quick](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/quick/quick14.png)

![quick](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/quick/quick15.png)






