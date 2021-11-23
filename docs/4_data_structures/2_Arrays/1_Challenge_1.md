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

## Challenge 1: Remove Even Integers from an Array

## Introduction 
Here is a short guide to these challenge lessons.

The method definition is always given in the problem statement with the expected arguments and method name to be used as is in the solution. If you change it, your code will not compile
When you do get compile-time errors, they will sometimes refer to line numbers and code, which you did not write. That is fine; that is just our evaluation code. Although, rest assured that our code compiles. When in doubt, refer to the solution given and paste that in.
Sometimes you are going to have to return from methods in a form that aligns with the test cases. Your solution may not be incorrect, but your form of returning might not be what the evaluation code expects. For example, you might return a number, but our test cases might expect an array. Watch out for that. Good luck! 🍀

## Problem Statement 
In this problem, you have to implement the int [] removeEven(int[] arr) method, which removes all the even elements from the array and returns back updated array.

## Method Prototype 
int[] removeEven(int[] arr);

## Input 
An array with integers.

## Output 
An array with only odd integers.

## Sample Input 
arr = {1, 2, 4, 5, 10, 6, 3}

## Sample Output 
arr = {1, 5, 3}

## Coding Exercise

![arr](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/arr/arr80.png)

{% highlight java %}
class CheckRemoveEven {

	public static int[] removeEven(int[] arr) {

		// Write - Your - Code- Here
		return arr; // change this and return the correct result array
	}
}
{% endhighlight %}

## Solution Review: Remove Even Integers from an Array

{% highlight java %}
class CheckRemoveEven {
  
	public static int[] removeEven(int[] arr) {
		int oddElements = 0;

		//Find number of odd elements in arr
		for (int i = 0; i < arr.length; i++) {
			if (arr[i] % 2 != 0) oddElements++;
		}

		//Create result array with the size equal to the number of odd elements in arr
		int[] result = new int[oddElements];
		int result_index = 0;

		//Put odd values from arr to the resulted array
		for (int i = 0; i < arr.length; i++) {
			if (arr[i] % 2 != 0) 
        result[result_index++] = arr[i];
		} //end of for loop

		return result;
	} //end of removeEven


  public static void main(String args[]) {
  
    int size = 10;
    int[] arr = new int[size]; //declaration and instantiation 
  
    System.out.print("Before removing Even Numbers: "); 
    for (int i = 0; i < arr.length; i++) {
      arr[i] = i; // assigning values
      System.out.print(arr[i] +  " ");
    }
    System.out.println();
  
    int[] newArr =  removeEven(arr); // calling removeEven
  
    System.out.print("After removing Even Numbers: "); 
    for (int i = 0; i < newArr.length; i++) {
      System.out.print(newArr[i] +  " "); // prinitng array
    }
  }
}
{% endhighlight %}

## Explanation 
This solution first finds the number of odd elements in the given array by iterating over it and incrementing a count variable if an element is odd.

Next, we initialize an array with a size oddElements, and store all the odd numbers in it.

## Time Complexity 
Since the entire array has to be iterated over, this solution is in O(n).