---
layout: default
title: Cyclic Sort
parent: Algorithms
nav_order: 15
permalink: /algorithms/sort
---
<div align="center" markdown="1">
Cyclic Sort / Java resources / Tutorial

{: .fs-8 .fw-400 }
</div>

## Cyclic Sort

Problem Statement#
We are given an array containing n objects. Each object, when created, was assigned a unique number from the range 1 to n based on their creation sequence. This means that the object with sequence number 3 was created just before the object with sequence number 4.

Write a function to sort the objects in-place on their creation sequence number in O(n)O(n) and without using any extra space. For simplicity, let’s assume we are passed an integer array containing only the sequence numbers, though each number is actually an object.

Example 1:

Input: [3, 1, 5, 4, 2]
Output: [1, 2, 3, 4, 5]
Example 2:

Input: [2, 6, 4, 3, 1, 5]
Output: [1, 2, 3, 4, 5, 6]
Example 3:

Input: [1, 5, 6, 4, 3, 2]
Output: [1, 2, 3, 4, 5, 6]

Solution#
As we know, the input array contains numbers from the range 1 to n. We can use this fact to devise an efficient way to sort the numbers. Since all numbers are unique, we can try placing each number at its correct place, i.e., placing 1 at index ‘0’, placing 2 at index ‘1’, and so on.

To place a number (or an object in general) at its correct index, we first need to find that number. If we first find a number and then place it at its correct place, it will take us O(N^2), which is not acceptable.

Instead, what if we iterate the array one number at a time, and if the current number we are iterating is not at the correct index, we swap it with the number at its correct index. This way, we will go through all numbers and place them at their correct indices, hence, sorting the whole array.

Let’s see this visually with the above-mentioned Example-2:

![alg](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/alg/qa4.png)
![alg](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/alg/qa5.png)

## Code

{% highlight java %}
class CyclicSort {

  public static void sort(int[] nums) {
    int i = 0;
    while (i < nums.length) {
      int j = nums[i] - 1;
      if (nums[i] != nums[j])
        swap(nums, i, j);
      else
        i++;
    }
  }

  private static void swap(int[] arr, int i, int j) {
    int temp = arr[i];
    arr[i] = arr[j];
    arr[j] = temp;
  }

  public static void main(String[] args) {
    int[] arr = new int[] { 3, 1, 5, 4, 2 };
    CyclicSort.sort(arr);
    for (int num : arr)
      System.out.print(num + " ");
    System.out.println();

    arr = new int[] { 2, 6, 4, 3, 1, 5 };
    CyclicSort.sort(arr);
    for (int num : arr)
      System.out.print(num + " ");
    System.out.println();

    arr = new int[] { 1, 5, 6, 4, 3, 2 };
    CyclicSort.sort(arr);
    for (int num : arr)
      System.out.print(num + " ");
    System.out.println();
  }
}

{% endhighlight %}

![alg](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/alg/qa6.png)

## Find the Missing Number

We are given an array containing ‘n’ distinct numbers taken from the range 0 to ‘n’. Since the array has only ‘n’ numbers out of the total ‘n+1’ numbers, find the missing number.

Example 1:

Input: [4, 0, 3, 1]
Output: 2
Example 2:

Input: [8, 3, 5, 2, 4, 6, 0, 1]
Output: 7

Solution#
This problem follows the Cyclic Sort pattern. Since the input array contains unique numbers from the range 0 to ‘n’, we can use a similar strategy as discussed in Cyclic Sort to place the numbers on their correct index. Once we have every number in its correct place, we can iterate the array to find the index which does not have the correct number, and that index will be our missing number.

However, there are two differences with Cyclic Sort:

In this problem, the numbers are ranged from ‘0’ to ‘n’, compared to ‘1’ to ‘n’ in the Cyclic Sort. This will make two changes in our algorithm:
In this problem, each number should be equal to its index, compared to index - 1 in the Cyclic Sort. Therefore => nums[i] == nums[nums[i]]
Since the array will have ‘n’ numbers, which means array indices will range from 0 to ‘n-1’. Therefore, we will ignore the number ‘n’ as we can’t place it in the array, so => nums[i] < nums.length
Say we are at index i. If we swap the number at index i to place it at the correct index, we can still have the wrong number at index i. This was true in Cyclic Sort too. It didn’t cause any problems in Cyclic Sort as over there, we made sure to place one number at its correct place in each step, but that wouldn’t be enough in this problem as we have one extra number due to the larger range. Therefore, we will not move to the next number after the swap until we have a correct number at the index i.
Code#

{% highlight java %}
class MissingNumber {

  public static int findMissingNumber(int[] nums) {
    int i = 0;
    while (i < nums.length) {
      if (nums[i] < nums.length && nums[i] != nums[nums[i]])
        swap(nums, i, nums[i]);
      else
        i++;
    }

    // find the first number missing from its index, that will be our required number
    for (i = 0; i < nums.length; i++)
      if (nums[i] != i)
        return i;

    return nums.length;
  }

  private static void swap(int[] arr, int i, int j) {
    int temp = arr[i];
    arr[i] = arr[j];
    arr[j] = temp;
  }

  public static void main(String[] args) {
    System.out.println(MissingNumber.findMissingNumber(new int[] { 4, 0, 3, 1 }));
    System.out.println(MissingNumber.findMissingNumber(new int[] { 8, 3, 5, 2, 4, 6, 0, 1 }));
  }
}

{% endhighlight %}

Time complexity#
The time complexity of the above algorithm is O(n)O(n). In the while loop, although we are not incrementing the index i when swapping the numbers, this will result in more than n iterations of the loop, but in the worst-case scenario, the while loop will swap a total of n-1 numbers and once a number is at its correct index, we will move on to the next number by incrementing i. In the end, we iterate the input array again to find the first number missing from its index, so overall, our algorithm will take O(n) + O(n-1) + O(n)O(n)+O(n−1)+O(n) which is asymptotically equivalent to O(n)O(n).

Space complexity#
The algorithm runs in constant space O(1)O(1).

## Find all Missing Numbers

Problem Statement#
We are given an unsorted array containing numbers taken from the range 1 to ‘n’. The array can have duplicates, which means some numbers will be missing. Find all those missing numbers.

Example 1:

Input: [2, 3, 1, 8, 2, 3, 5, 1]
Output: 4, 6, 7
Explanation: The array should have all numbers from 1 to 8, due to duplicates 4, 6, and 7 are missing.
Example 2:

Input: [2, 4, 1, 2]
Output: 3
Example 3:

Input: [2, 3, 2, 1]
Output: 4

olution#
This problem follows the Cyclic Sort pattern and shares similarities with Find the Missing Number with one difference. In this problem, there can be many duplicates whereas in ‘Find the Missing Number’ there were no duplicates and the range was greater than the length of the array.

However, we will follow a similar approach though as discussed in Find the Missing Number to place the numbers on their correct indices. Once we are done with the cyclic sort we will iterate the array to find all indices that are missing the correct numbers.

Code

{% highlight java %}
import java.util.*;

class AllMissingNumbers {

  public static List<Integer> findNumbers(int[] nums) {
    int i = 0;
    while (i < nums.length) {
      if (nums[i] != nums[nums[i] - 1])
        swap(nums, i, nums[i] - 1);
      else
        i++;
    }

    List<Integer> missingNumbers = new ArrayList<>();
    for (i = 0; i < nums.length; i++)
      if (nums[i] != i + 1)
        missingNumbers.add(i + 1);

    return missingNumbers;
  }

  private static void swap(int[] arr, int i, int j) {
    int temp = arr[i];
    arr[i] = arr[j];
    arr[j] = temp;
  }

  public static void main(String[] args) {
    List<Integer> missing = AllMissingNumbers.findNumbers(new int[] { 2, 3, 1, 8, 2, 3, 5, 1 });
    System.out.println("Missing numbers: " + missing);

    missing = AllMissingNumbers.findNumbers(new int[] { 2, 4, 1, 2 });
    System.out.println("Missing numbers: " + missing);

    missing = AllMissingNumbers.findNumbers(new int[] { 2, 3, 2, 1 });
    System.out.println("Missing numbers: " + missing);
  }
}

{% endhighlight %}

Time complexity#
The time complexity of the above algorithm is O(n)O(n).

Space complexity#
Ignoring the space required for the output array, the algorithm runs in constant space O(1)O(1).

## Find the Duplicate Number

Problem Statement#
We are given an unsorted array containing ‘n+1’ numbers taken from the range 1 to ‘n’. The array has only one duplicate but it can be repeated multiple times. Find that duplicate number without using any extra space. You are, however, allowed to modify the input array.

Example 1:

Input: [1, 4, 4, 3, 2]
Output: 4
Example 2:

Input: [2, 1, 3, 3, 5, 4]
Output: 3
Example 3:

Input: [2, 4, 1, 4, 4]
Output: 4

Solution#
This problem follows the Cyclic Sort pattern and shares similarities with Find the Missing Number. Following a similar approach, we will try to place each number on its correct index. Since there is only one duplicate, if while swapping the number with its index both the numbers being swapped are same, we have found our duplicate!

Code

{% highlight java %}
class FindDuplicate {

  public static int findNumber(int[] nums) {
    int i = 0;
    while (i < nums.length) {
      if (nums[i] != i + 1) {
        if (nums[i] != nums[nums[i] - 1])
          swap(nums, i, nums[i] - 1);
        else // we have found the duplicate
          return nums[i];
      } else {
        i++;
      }
    }

    return -1;
  }

  private static void swap(int[] arr, int i, int j) {
    int temp = arr[i];
    arr[i] = arr[j];
    arr[j] = temp;
  }

  public static void main(String[] args) {
    System.out.println(FindDuplicate.findNumber(new int[] { 1, 4, 4, 3, 2 }));
    System.out.println(FindDuplicate.findNumber(new int[] { 2, 1, 3, 3, 5, 4 }));
    System.out.println(FindDuplicate.findNumber(new int[] { 2, 4, 1, 4, 4 }));
  }
}

{% endhighlight %}

Time complexity#
The time complexity of the above algorithm is O(n)O(n).

Space complexity#
The algorithm runs in constant space O(1)O(1) but modifies the input array.

Similar Problems#
Problem 1: Can we solve the above problem in O(1)O(1) space and without modifying the input array?

Solution: While doing the cyclic sort, we realized that the array will have a cycle due to the duplicate number and that the start of the cycle will always point to the duplicate number. This means that we can use the fast & the slow pointer method to find the duplicate number or the start of the cycle similar to Start of LinkedList Cycle.

{% highlight java %}
class DuplicateNumber {

  public static int findDuplicate(int[] arr) {
    int slow = 0, fast = 0;
    do {
      slow = arr[slow];
      fast = arr[arr[fast]];
    } while (slow != fast);

    // find cycle length
    int current = arr[slow];
    int cycleLength = 0;
    do {
      current = arr[current];
      cycleLength++;
    } while (current != arr[slow]);

    return findStart(arr, cycleLength);
  }

  private static int findStart(int[] arr, int cycleLength) {
    int pointer1 = arr[0], pointer2 = arr[0];
    // move pointer2 ahead 'cycleLength' steps
    while (cycleLength > 0) {
      pointer2 = arr[pointer2];
      cycleLength--;
    }

    // increment both pointers until they meet at the start of the cycle
    while (pointer1 != pointer2) {
      pointer1 = arr[pointer1];
      pointer2 = arr[pointer2];
    }

    return pointer1;
  }

  public static void main(String[] args) {
    System.out.println(DuplicateNumber.findDuplicate(new int[] { 1, 4, 4, 3, 2 }));
    System.out.println(DuplicateNumber.findDuplicate(new int[] { 2, 1, 3, 3, 5, 4 }));
    System.out.println(DuplicateNumber.findDuplicate(new int[] { 2, 4, 1, 4, 4 }));
  }
}
{% endhighlight %}


## Find all Duplicate Numbers

Problem Statement#
We are given an unsorted array containing ‘n’ numbers taken from the range 1 to ‘n’. The array has some numbers appearing twice, find all these duplicate numbers without using any extra space.

Example 1:

Input: [3, 4, 4, 5, 5]
Output: [4, 5]
Example 2:

Input: [5, 4, 7, 2, 3, 5, 3]
Output: [3, 5]

Solution#
This problem follows the Cyclic Sort pattern and shares similarities with Find the Duplicate Number. Following a similar approach, we will place each number at its correct index. After that, we will iterate through the array to find all numbers that are not at the correct indices. All these numbers are duplicates.

Code

{% highlight java %}
import java.util.*;

class FindAllDuplicate {

  public static List<Integer> findNumbers(int[] nums) {
    int i = 0;
    while (i < nums.length) {
      if (nums[i] != nums[nums[i] - 1])
        swap(nums, i, nums[i] - 1);
      else
        i++;
    }

    List<Integer> duplicateNumbers = new ArrayList<>();
    for (i = 0; i < nums.length; i++) {
      if (nums[i] != i + 1)
        duplicateNumbers.add(nums[i]);
    }

    return duplicateNumbers;
  }

  private static void swap(int[] arr, int i, int j) {
    int temp = arr[i];
    arr[i] = arr[j];
    arr[j] = temp;
  }

  public static void main(String[] args) {
    List<Integer> duplicates = FindAllDuplicate.findNumbers(new int[] { 3, 4, 4, 5, 5 });
    System.out.println("Duplicates are: " + duplicates);

    duplicates = FindAllDuplicate.findNumbers(new int[] { 5, 4, 7, 2, 3, 5, 3 });
    System.out.println("Duplicates are: " + duplicates);
  }
}

{% endhighlight %}





{% highlight java %}

{% endhighlight %}