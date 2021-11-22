---
layout: default
title: Challenge 4
parent: Arrays
grand_parent: Data Structures
nav_order: 4
permalink: /data_structures/arrays/ch4
---
<div align="center" markdown="1">
Challenge 4 / Java resources / Tutorial

{: .fs-8 .fw-400 }
</div>

## Challenge 4: Array of Products of All Elements Except Itself

Given an array, return an array where each index stores the product of all numbers except the number on the index itself. Implement your solution in Java and see if your output matches the expected output!

Problem Statement#
In this problem, you have to implement the int[] findProduct(int[] arr) method which will modify arr in such a way that in the output, each index i will contain the product of all elements present in arr except the element stored on that index i.

Method Prototype#
int[] findProduct(int[] arr)
Input#
An array of integers. This array can be of any (valid) size and elements can be repeated.

Output#
An array with products stored at each position.

Sample Input#
arr = {1,2,3,4}
Sample Output#
arr = {24,12,8,6}

![arr](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/arr/arr83.png)

## Coding Exercise

{% highlight java %}
class ProductArray  
{  
  public static int[] findProduct(int arr[])  
  {    
    int [] result = { 0 };

    // write your code here

    return result; 
   } 
} 
{% endhighlight %}

## Solution Review: Array of Products of All Elements Except Itself

{% highlight java %}
class ProductArray  
{  
  public static int[] findProduct(int arr[])  
  { 
    int n = arr.length;
    int i, temp = 1; 

    // Allocation of result array
    int result[] = new int[n]; 

    // Product of elements on left side excluding arr[i]
    for (i = 0; i < n; i++)  
    { 
      result[i] = temp; 
      temp *= arr[i]; 
    } 

    // Initializing temp to 1 for product on right side
    temp = 1; 

    // Product of elements on right side excluding arr[i] 
    for (i = n - 1; i >= 0; i--)  
    { 
      result[i] *= temp; 
      temp *= arr[i]; 
    }

    return result; 
  } 
  public static String arrayToString(int arr[]){
    if (arr.length > 0){
      String result = "";
      for(int i = 0; i < arr.length; i++) {
        result += arr[i] + " ";
      }
      return result;
    }
    else {
      return "Empty Array!";
    }
  }

  public static void main(String args[]) {

    int[] arr = {-1, 2, -3, 4, -5};

    System.out.println("Array before product: " + arrayToString(arr));

    int[] prodArray = findProduct(arr);

    System.out.println("Array after product: " + arrayToString(prodArray));
  }
} 
{% endhighlight %}

Explanation#
The algorithm for this solution is to first create a new array result with products of all elements to the left of each element, as done on lines 12-16. With temp initially set to 1, in each iteration, the code:

sets the value of temp to the current index of the result array.
updates temp by multiplying it with the current element in the original array. This causes temp to be the product of the elements that the loop have traversed so far.
This will store the product from the start of array to the i-1 index.

We can then multiply each element in the result array to the product of all the elements to the right of the array by traversing it in reverse as done on lines 22-26. We set temp to 1 again and in each iteration we:

multiply the value of temp to the current index of the result array. It is important to multiply the value of temp here as this will ensure that all elements of the result array are products of elements to the right and the left of the original element.
update temp by multiplying it with the current element in the original array. This causes temp to be the product of the elements that the loop have traversed so far.

![arr](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/arr/arr84.png)