---
layout: default
title: Binary Search
parent: Algorithms
grand_parent: Data Structures and Algorithms
nav_order: 1
permalink: /data_structures/algorithms/binary_search
---
<div align="center" markdown="1">
Binary Search / Java resources / Tutorial

{: .fs-8 .fw-400 }
</div>

## Intuition
Binary search is an efficient array search algorithm. It works by narrowing down the search range by half each time. If you have ever looked up a word in a print dictionary, you have already used binary search in real life. Let’s look at a simple example:

Given a sorted array of integers and an integer called target, find the element that equals the target and return its index..

The key observation here is that the array is sorted. Let’s say we pick a random element in the array and compare it to the target.

* If we happen to pick the element that equals the target (how lucky!), then bingo. We don’t need to do any more work and just return its index.
* If the element is smaller than the target, we know the target cannot be found in the section to the left of the current element since everything to the left is even smaller. So we discard the current element and everything on the left from the search range.
* If the element is larger than the target, we know the target cannot be found in the section to the right of the current element since everything to the right is even larger. So we discard the current element and everything on the right from the search range.
We repeat this process until we find the target. Instead of picking a random element, we always pick the middle element in the current search range. This way we can discard half of the options and shrink the search range by half each time. This gives us O(log(N))O(log(N)) runtime.

## Implementation
The search range is represented by the left and right indices that start from both ends of the array and move towards each other as we search. When we move the index, we discard elements and shrink the search range.

![binary](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/binary/binary1.png)
![binary](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/binary/binary2.png)
![binary](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/binary/binary3.png)
![binary](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/binary/binary4.png)
![binary](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/binary/binary5.png)
![binary](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/binary/binary6.png)
![binary](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/binary/binary7.png)
![binary](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/binary/binary8.png)

{% highlight java %}

class Solution {
    public static int binarySearch(int[] arr, int target) {
        int left = 0;
        int right = arr.length - 1;

        while (left <= right) { // <= here because left and right could point to the same element, < would miss it
            int mid = left + (right - left) / 2; // use `(right - left) /2` to prevent `left + right` potential overflow
            // found target, return its index
            if (arr[mid] == target) return mid;
            if (arr[mid] < target) {
                // middle less than target, discard left half by making left search boundary `mid + 1`
                left = mid + 1;
            } else {
                // middle greater than target, discard right half by making right search boundary `mid - 1`
                right = mid - 1;
            }
        }
        return -1; // if we get here we didn't hit above return so we didn't find target
    }
    
    // Driver code
    public static void main(String[] args) {       
        System.out.println("Binary search : " + Solution.binarySearch(new int[] {1, 3, 5, 7, 8}, 5));
        System.out.println("Binary search : " + Solution.binarySearch(new int[] {1, 2, 3, 4, 5, 6, 7}, 0));
        System.out.println("Binary search : " + Solution.binarySearch(new int[] {2, 8, 89, 120, 1000}, 120));
    }
}
{% endhighlight %}

## Calculating mid
Note that if the number of elements is even when calculating mid, there are two elements in the middle. We normally follow the convention of picking the first one, which is equivalent to doing integer division (left + right) / 2.

## Deducing binary search
It’s important to understand and deduce the algorithm yourself instead of memorizing it. Interviewers may ask you additional questions to test your understanding, so simply having memorized the algorithm may not be enough to convince the interviewer.

Key elements in writing a correct binary search:

## 1. When to terminate the loop
Make sure your while loop has an equality comparison. Otherwise, — for the edge case of a one-element array, — you’d skip the loop and miss the potential match.

## 2. How to update left and right boundary in the if conditions
Consider which side to discard. If arr[mid] is already smaller than the target, we should discard everything on the left by making left = mid + 1.

## 3. Should I discard the current element?
For vanilla binary search, we can discard the current element since it can’t be the final answer if it is not equal to the target. There might be situations where you would want to think twice before discarding the current element. We’ll discuss these in the next module.

## When to use binary search
Interestingly, binary search works beyond sorted arrays. You can use binary search whenever you can make a binary decision to shrink the search range. We will learn about this in other modules.

# Finding the Boundary

## Problem statement
An array of boolean values is divided into two sections: the left section consists of all false, and the right section consists of all true. Find the boundary of the right section, i.e. the index of the first true element. If there is no true element, return -1.

## Example
Input: arr = [false, false, true, true, true]

Output: 2

Explanation: first true's index is 2.

## Explanation
The binary decisions we have to make when we look at an element are:

If the element is false, we discard everything to the left and the current element itself.
If the element is true, the current element could be the first that is true and there may be other true elements to the left. We discard everything to the right, but what about the current element?
We can either keep the current element in the range or record it somewhere and then discard it. Here we choose the latter. We’ll discuss the other approach in the alternative solution section.

We keep a variable boundary_index that represents the leftmost true's index currently recorded. If the current element is true, we update boundary_index with its index and discard everything to the right including the current element itself since its index has been recorded by the variable.

![binary](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/binary/finding1.png)
![binary](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/binary/finding2.png)
![binary](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/binary/finding3.png)
![binary](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/binary/finding4.png)
![binary](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/binary/finding5.png)
![binary](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/binary/finding6.png)
![binary](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/binary/finding7.png)
![binary](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/binary/finding8.png)

{% highlight java %}

class Solution {
    class Solution {
        public static int findBoundary(boolean[] arr) {
            int left = 0;
            int right = arr.length - 1;
            int boundaryIndex = -1;
            while (left <= right) {
                int mid = (left + right) / 2;
                if (arr[mid]) {
                    boundaryIndex = mid;
                    right = mid - 1;
                } else {
                    left = mid + 1;
                }
            }
            return boundaryIndex;
        }
    }
}
{% endhighlight %}

The good thing about this approach is that besides introducing a variable, we don’t have to modify the while loop logic in the vanilla binary search from the last module.

The time complexity is O(log(N))O(log(N)).

## Alternative approach
Another approach to handle case 2 above is to keep the current element in the search range instead of discarding it, i.e. if arr[mid]: right = mid instead of right = mid - 1. However, doing this without modifying the while condition will result in an infinite loop. This is because when left == right, right = mid will not modify right and thus not shrink the search range and we will be stuck in the while loop forever. To make this work, we have to remove the equality in the while condition. In addition, as mentioned in the last module, a while loop without equality will miss the single-element edge case, so we have to add an additional check after the loop to handle this case. Overall, we have to make three modifications to the vanilla binary search to make it work.

## Side note: how to not get stuck in an infinite loop
Make progress in each step
Have an exit strategy

## Summary
This problem is the major 🔑 in solving future binary search-related problems. As we will see in the following modules, many problems boil down to finding the boundary in a boolean array.

## First Element Not Smaller Than Target

## Problem statement
Given an array of integers sorted in increasing order and a target, find the index of the first element in the array that is larger or equal to the target. Assume that it is guaranteed to find a satisfying number.

## Example
Input: arr = [1, 3, 3, 5, 8, 8, 10],target = 2

Output: 1

Explanation: the first element larger than 2 is 3, which has index 1.

## Explanation
The problem is equivalent to finding the boundary of elements < 2 and elements >=2. If we apply a filter of arr[i] >= target, we would get:
![binary](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/binary/binary_first1.png)

Now the problem is reduced to finding the first true element in a boolean array. We already know how to do this from the Find the Boundary module.

The time complexity is O(log(N))O(log(N)).

{% highlight java %}

class Solution {
    public static int first_not_smaller(int[] arr, int target) {
        int left = 0;
        int right = arr.length - 1;
        int boundaryIndex = -1;
        while (left <= right) {
            int mid = left  + (right - left) / 2;
            if (arr[mid] >= target) {
                boundaryIndex = mid;
                right = mid - 1;
            } else {
                left = mid + 1;
            }
        }
        return boundaryIndex;
    }
}
{% endhighlight %}

## Find Minimum in Rotated Sorted Array

## Problem statement
A sorted array was rotated at an unknown pivot. For example, [10, 20, 30, 40, 50] becomes [30, 40, 50, 10, 20]. Find the index of the minimum element in this array.

## Example
Input: [30, 40, 50, 10, 20]

Output: 3

Explanation: The smallest element is 10 and its index is 3.

## Explanation
At first glance, it seems that there’s no way to do it in less than linear time. The array is not sorted.

But remember that binary search can work beyond sorted arrays as long as there is a binary decision we can use to shrink the search range.

Let’s draw a figure and see if there’s any pattern. If we plot the numbers against their index, we get:

![binary](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/binary/binary_min1.png)

Notice the numbers are divided into two sections: numbers larger than the last element of the array and numbers smaller than it. The minimum element is at the boundary between the two sections.

We can apply a filter of < the last element and get the boolean array that characterizes the two sections.
![binary](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/binary/binary_min2.png)

Now the problem is yet again reduced to finding the first true element in a boolean array. We already know how to do this from the “Finding the Boundary” module.

The time complexity is O(log(N))O(log(N)).

{% highlight java %}

class Solution {
    public static int findMinRotated(int[] arr) {
        int left = 0;
        int right = arr.length - 1;
        int boundaryIndex = -1;
        while (left <= right) {
            int mid = (left + right) / 2;
            // if <= last element, then belongs to lower half
            if (arr[mid] <= arr[arr.length - 1]) {
                boundaryIndex = mid;
                right = mid - 1;
            } else {
                left = mid + 1;
            }
        }
        return boundaryIndex;
    }
}
{% endhighlight %}



