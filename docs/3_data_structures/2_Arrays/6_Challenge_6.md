---
layout: default
title: Challenge 6
parent: Arrays
grand_parent: Data Structures
nav_order: 6
permalink: /data_structures/arrays/ch6
---
<div align="center" markdown="1">
Challenge 6 / Java resources / Tutorial

{: .fs-8 .fw-400 }
</div>

## Challenge 6: First Non-Repeating Integer in an Array

Problem Statement #
In this problem, you have to implement the int findFirstUnique(int[] arr) method that will look for a first unique integer, which appears only once in the whole array. The function returns -1 if no unique number is found.

Method Prototype #
int findFirstUnique(int[] arr)
Output #
The first unique element in the array.

Sample Input #
arr = {9, 2, 3, 2, 6, 6}
Sample Output #
9

![arr](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/arr/arr86.png)

## Coding Exercise

{% highlight java %}
class CheckFirstUnique
{
 public static int findFirstUnique(int[] arr) 
 {
   int result = 0;
   // write your code here
   return result;
 }
}
{% endhighlight %}

## Solution Review: First Non-Repeating Integer in an Array

{% highlight java %}
//Returns first unique integer from array
class CheckFirstUnique {
  public static int findFirstUnique(int[] arr) {
    //Inside Inner Loop Check Each index of outerLoop If it's repeated in array
    //If it's not repeated then return this as first unique Integer
    boolean isRepeated = false;

    for (int i = 0; i < arr.length; i++) {

      for (int j = 0; j < arr.length; j++) {

        if (arr[i] == arr[j] && i != j) {
          isRepeated = true;
          break;
        }
      } //end of InnerLoop

      if (isRepeated == false) {
        return arr[i];
      }
      else {
        isRepeated = false;
      }
    
    } //end of OuterLoop
    return - 1;
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

  public static void  main(String args[]) {

    int[] arr = {2, 54, 7, 2, 6, 54};

    System.out.println("Array: " + arrayToString(arr));

    int unique = findFirstUnique(arr);
    System.out.print("First Unique in an Array: " + unique);

  }
}
{% endhighlight %}

Explanation #
We start from the first element and traverse through the whole array, comparing it with all the other elements to see if any element is equal to it. If so, we skip to the next element and repeat the above-mentioned steps. If not, then this is the first unique element in the array.

Time Complexity #
The time complexity of this solution is O(n^2)O(n
​2
​​ ) since the entire list is iterated for each element \rightarrow n \times n→n×n.