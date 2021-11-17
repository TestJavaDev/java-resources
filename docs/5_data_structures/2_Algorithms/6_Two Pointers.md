---
layout: default
title: Two Pointers
parent: Algorithms
grand_parent: Data Structures and Algorithms
nav_order: 6
permalink: /data_structures/algorithms/two_pointers
---
<div align="center" markdown="1">
Two Pointers / Java resources / Tutorial

{: .fs-8 .fw-400 }
</div>

## Two Pointers
## Remove Duplicates [Same Direction]

## Problem statement
Given a sorted list of numbers, remove duplicates and return the new length. You must do this in-place and without using extra memory.

Input: [0, 0, 1, 1, 1, 2, 2]

Your function should modify the list in-place so the first 3 elements become [0, 1, 2].

Example#
Input: [0, 0, 1, 1, 1, 2, 2]

Output: 3

After modifying the array in place, the array becomes [0, 1, 2, 1, 1, 2, 2] and we return the new length without duplicate 3.

## Explanation

## Intuition
If we could have used extra memory, this could be easily solved by going through the list once and using a “HashSet” to record elements we had seen.

But we are not allowed extra memory so we have to look at the conditions and see if there’s anything we can use. An important condition is that the numbers are sorted, which means that the same numbers are next to each other. This means that as we go through the list, once we see a number A, we will see all occurrences of A together and will not see A again after we see B. Using this key observation, we can devise a fast/slow pointer solution.

## Draw a figure

![two](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/two/two1.png)
![two](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/two/two2.png)
![two](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/two/two3.png)
![two](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/two/two4.png)
![two](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/two/two5.png)
![two](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/two/two6.png)
![two](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/two/two7.png)
![two](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/two/two8.png)
![two](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/two/two9.png)

## Implementation
{% highlight java %}

class Solution {
    public static int removeDuplicates(int[] nums) {
        int slow = 0;
        for (int fast = 0; fast < nums.length; ++fast) {
            if (nums[fast] != nums[slow]) {
                slow++;
                nums[slow] = nums[fast];
            }
        }
        return slow + 1;
    }
    public static void main(String[] args) {
        //Driver code
        String[] inputs = {"0 0 1 1 1 2 2","1 2 3","1 1 1 1 1 1 1 1 1 1 1 1"};
        for(int i = 0; i < inputs.length; i++) {
            int[] nums = Arrays.stream(inputs[i].split(" ")).mapToInt(Integer::parseInt).toArray();
            int count = Solution.removeDuplicates(nums);
            String actual_output = Arrays.toString(Arrays.stream(nums).limit(count).mapToObj(Integer::toString).toArray());

            System.out.println("Remove duplicates : "+actual_output);
        }
    }
}
{% endhighlight %}
The time complexity is O(N) since we traverse the array once.

## Middle of Linked List

## Problem statement
Find the middle node of a linked list.

## Example
Input: 0 1 2 3 4

Output: 2

## Explanation

## Intuition
If it was an array, we could get its length and middle element trivially. For a linked list, we have to traverse it to find its length l. We can find l by traversing the list once and then find the middle element by traversing it again and stop on the l/2th element.

Is there any way to traverse only once? We can use two pointers:
* a fast pointer that moves 2 nodes at a time and
* a slow pointer that moves 1 node at a time

Since the speed of the fast pointer is 2x of the slow pointer, by the time the fast pointer reaches the end, the slow pointer should be at the exact middle of the list.

## Draw a figure

![two](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/two/two10.png)
![two](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/two/two11.png)
![two](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/two/two12.png)

## Review
Notice that
1. We have to check the existence of fast and fast.next in the while loop condition. We have to do this because if list length is odd (illustrated above), the fast pointer would reach the last node. If list length is even (illustrated below), the fast pointer would land on null (Node 6’s next).

![two](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/two/two13.png)
![two](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/two/two14.png)
![two](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/two/two15.png)
![two](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/two/two16.png)
{% highlight java %}

class Solution {
    public static ListNode middleOfLinkedList(ListNode head) {
        ListNode slow = head;
        ListNode fast = head;
        while (fast != null && fast.next != null) {
            fast = fast.next.next;
            slow = slow.next;
        }
        return slow;
    }
    // Driver code  
	public static void main(String[] args) {

        String[] inputs = {"2 1", "5 5"};
		for (int i = 0; i<inputs.length; i++) {
            ListNode dummy = new ListNode(-1);
            ListNode cur = dummy;
			for (String val : inputs[i].split(" ")) {
                ListNode node = new ListNode(Integer.parseInt(val));
                cur.next = node;
                cur = node;
            }
			System.out.println("Middle of linked list : " + Solution.middleOfLinkedList(dummy.next).val);
		}
	}
}

class ListNode {
    int val;
    ListNode next;

    public ListNode(int val) {
        this.val = val;
    }
}
{% endhighlight %}
The time complexity is O(N) since we traverse the linked list once.

## Two Sum Sorted [Opposite Direction]

## Problem statement
Given an array of integers sorted in ascending order, find two numbers that add up to a given target. Return the indices of the two numbers in ascending order. You can assume elements in the array are unique and that there is only one solution. Do this in O(n) time and with constant auxiliary space.

Example#
Input: [2, 3, 4, 5, 8, 11, 18], 8

Output: 1 3

## Explanation

## Intuition
Provided that we understand the problem, the first step to finding a solution is to solve it by brute force.

Since the problem asks for two elements that sum to target, we can simply try every pair of numbers and see if they sum to it. This would take O(n^2) time.
![two](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/two/two17.png)
To improve the brute force solution, two questions to ask are “can we skip any pairs?” and “have we used all the unknowns?”

We noticed that the array is sorted. This means the smallest two sum we can get is the sum of the first two numbers 2 + 3 of input array [2, 3, 4, 5, 8, 11, 18], and the largest two sum we can get is the sum of the last two numbers 11 + 18 of input array [2, 3, 4, 5, 8, 11, 18]. If we sort all two sum pairs by their sum value, the middle point is the smallest number + largest number 2 + 18. From this point, we can compare with our target 8 in the input array [2, 3, 4, 5, 8, 11, 18].
* If our sum equals the target, then we’re done.
* If our sum is less than the target, we need to exchange one of the numbers for a bigger number. Since 18 is already the bigger number available, we have to exchange 2 for a bigger number. We go to 3.
* If our sum is greater than the target, we need to exchange one of the numbers for a smaller number. Since 2 is the smallest number available, we have to exchange 18 for a smaller number. We go to 11.
* Repeat the process until the sum is equal to our target.

![two](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/two/two18.png)

{% highlight java %}

class Solution {

    public static int[] twoSumSorted(int[] arr, int target) {
        int l = 0;
        int r = arr.length - 1;
        while (l < r) {
            int twoSum = arr[l] + arr[r];
            if (twoSum == target) {
                return new int[] {l, r};
            } else if (twoSum < target) {
                l++;
            } else {
                r--;
            }
        }
        return new int[2];
    }
    //Driver code
    public static void main(String[] args){
        String[] inputs = {"2 3 4 5 8 11 18","2 5 10 12 30 100","1 2 3 10 20 30 50 100","1 2", "100 1000 2001 3000 4000 5000"};
        String[] inputs1 = {"8","22","101","3","5001"};
        for(int i = 0; i < inputs.length; i++) {
            int[] arr = Arrays.stream(inputs[i].split(" ")).mapToInt(Integer::parseInt).toArray();
            int target = Integer.parseInt(inputs1[i]);
            int[] actual_output = Solution.twoSumSorted(arr, target);

            System.out.println("Two sum sorted : " + Arrays.toString(actual_output));
        }

    }
}
{% endhighlight %}

## Valid Palindrome

## Problem statement
Determine whether a string is a palindrome (ignoring non-alphanumeric characters and case).

## Examples 1:
Input: Do geese see God?

Output: True

## Examples 2:
Input: Was it a car or a cat I saw?

Output: True

## Examples 3:
Input: A brown fox jumping over

Output: False

## Explanation
## Intuition
This is a straightforward two-pointer problem. We have two pointers, l and r, starting from the leftmost and rightmost positions and moving towards each other. At each step, if the elements they point to are the same, we move each pointer one position towards each other. If the elements under the pointers are different at any step, then the string is not a palindrome.

Note that the problem asks us to ignore all non-alphanumeric characters. So, any time we see one, we have to skip it by incrementing the corresponding pointer only.
![two](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/two/two19.png)
![two](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/two/two20.png)
![two](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/two/two21.png)
![two](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/two/two22.png)
![two](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/two/two23.png)
![two](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/two/two24.png)
![two](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/two/two25.png)
![two](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/two/two26.png)
![two](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/two/two27.png)
![two](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/two/two28.png)

## Implementation
The implementation is relatively straightforward.

Note that:
1. We need a while loop here because there could be multiple non-alphanumeric characters in a row and we want to skip all of them.
2. We also need to do bound checking in the inner while loop too since while incrementing l/decrementing r, the outer loop condition l < r could be broken and the next line if s[l].lower() != s[r].lower() would be invalid when l < r does not hold.

The time complexity is O(N) since we only look at each character at most once. Space complexity is O(1) since we didn’t allocate a dynamic amount of memory.

## Alternative solution: removing non-alphanumeric characters first
An easier and less error-prone way is to filter the non-alphanumeric characters first and then validate if it’s a palindrome.

The time complexity is still O(N). Since strings are immutable in most mainstream languages, filtering requires allocating a new string and thus space complexity will be O(N) where NN is the length of the string.
{% highlight java %}

class Solution {
    public static boolean isPalindrome(String s) {
        char[] arr = s.toCharArray();
        int l = 0;
        int r = arr.length - 1;
        while (l < r) {
            while (l < r && !Character.isLetterOrDigit(arr[l])) {  // Note 1, 2
                l++;
            }
            while (l < r && !Character.isLetterOrDigit(arr[r])) {
                r--;
            }
            // ignore case
            if (Character.toLowerCase(arr[l]) != Character.toLowerCase(arr[r])) return false;
            l++;
            r--;
        }
        return true;
    }
    //Driver code
    public static void main(String[] arg){
        String[] inputs = {"Do geese see God","Was it a car or a cat I saw?","A brown fox jumping over"};
        for(int i = 0; i < inputs.length; i++) {
            System.out.println("Valid palindrome : "+Solution.isPalindrome(inputs[i]));
        }
    }
}
{% endhighlight %}
The time complexity is O(N)O(N) since we stop when the two pointers meet in the middle and each element is visited once.

##  Subarray Sum

## Problem statement
Given an array of integers and an integer target, find a subarray that sums to target and returns the start and end indices of the subarray. It’s guaranteed to have a unique solution.

## Example:
Input: [1 -20 -3 30 5 4], 7

Output: 1 4

Explanation: -20 - 3 + 30 = 7. The indices for subarray [-20,-3,30] is 1 and 4 (right exclusive).

## Explanation

## Intuition
The brute force way is to find the sum of each subarray and compare it with the target. Let NN be the number of elements in the array. There are N subarrays with size 1, N-1 subarrays with size 2, and 1 subarray with size N. . Time complexity is ![two](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/two/two29.png)

A key observation is that the sum of a subarray [i, j] is equal to the sum of [0, j] minus the sum of [0, i - 1].

![two](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/two/two30.png)

The sum of elements from index 0 to i is called the prefix sum. If we have the subarray sum for each index, we can find the sum of any subarray in constant time.

With the knowledge of the prefix sum under our belt, the problem boils down to Two Sum. We keep a dictionary of prefix_sum: index while going through the array calculating prefix_sum. If at any point, prefix_sum - target is in the dictionary, we have found our subarray.
{% highlight java %}

class Solution {

    public static int[] subarraySum(int[] arr, int target) {
        int[] res = new int[2];
        HashMap<Integer, Integer> prefixSums = new HashMap<>();
        // prefix_sum 0 happens when we have an empty array
        prefixSums.put(0, 0);
        int curSum = 0;
        for (int i = 0; i < arr.length; i++) {
            curSum += arr[i];
            int compliment = curSum - target;
            if (prefixSums.containsKey(compliment)) {
                res[0] = prefixSums.get(compliment);
                res[1] = i + 1;
                return res;
            }
            prefixSums.put(curSum, i + 1);
        }
        return res;
    }
    // Driver code
    public static void main(String[] arg){
        String[] inputs = {"1 3 -3 8 5 7","1 1 1","1 -20 -3 30 5 7"};
        String[] inputs1={"5","3","7"};
        for(int i = 0; i < inputs.length; i++) {
            int[] arr = Arrays.stream(inputs[i].split(" ")).mapToInt(Integer::parseInt).toArray();
            int target = Integer.parseInt(inputs1[i]);
            int[] res = Solution.subarraySum(arr, target);
            System.out.println("Subarray sum : "+res[0] + " " + res[1]);
        }
    }
}   
{% endhighlight %}
The time complexity is O(N) since we traverse the array twice –– once to calculate prefix sum and the other time to find the solution.

## Subarray Sum Divisible by K [Prefix Sum]

## Problem statement
Given an array of integers and an integer K, find the number of subarrays whose sums are divisible by K.

## Example:
Input: [3,1,2,5,1], 3

Output: 6

Explanation: the six subarrays are[3], [3,1,2], [1,2], [5,1], [3,1,2,5,1], [1,2,5,1]

## Explanation

## Intuition
This problem is very similar to the previous Subarray Sum problem. Instead of saving the prefix_sum, we save the remainder prefix_sum % K.
{% highlight java %}
class Solution {

    public static int subarraySumDivisible(int[] nums, int k) {
        HashMap<Integer, Integer> remainders = new HashMap<>();
        remainders.put(0, 1);
        int curSum = 0;
        int count = 0;
        for (int i = 0; i < nums.length; i++) {
            int num = nums[i];
            curSum += num;
            int remainder = curSum % k;
            int compliment = (k - remainder) % k;
            if (remainders.containsKey(compliment)) {
                count += remainders.get(compliment);
            }
            if (remainders.containsKey(compliment)) {
                remainders.replace(compliment, remainders
                .get(compliment) + 1);
            } else {
                remainders.put(compliment, 1);
            }
        }
        return count;
    }
    //Driver code
    public static void main(String[] arg){
        String[] inputs = {"3 1 2 5 1"};
        String[] inputs1 = {"3"};
        for(int i = 0; i < inputs.length; i++) {
            int[] nums = Arrays.stream(inputs[i].split(" "))
            .mapToInt(Integer::parseInt).toArray();
            int k = Integer.parseInt(inputs1[i]);
            System.out.println("Subarray sum divisible :"+
            Solution.subarraySumDivisible(nums, k));
        }
    }
    
}  
{% endhighlight %}

