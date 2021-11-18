---
layout: default
title: Google Calendar
parent: Coding Interview
has_children: true
nav_order: 4
permalink: /coding_interview/google
---
<div align="center" markdown="1">
Google Calendar / Java resources / Tutorial

{: .fs-8 .fw-400 }
</div>

## Google Calendar

## Project Description for Google Calendar

## Introduction
The Google Calendar application is developed by Google as part of the GSuite. Google Calendar makes people’s everyday lives easier by helping them manage events and reminders. Companies especially benefit from it greatly because it can also be used to manage events across multiple calendars. This way, companies can track the availability of employees and rooms to schedule meetings efficiently.

In this chapter, we will discuss scenarios and problems that relate to developing and implementing meeting management features.

## Statement
Suppose you are a developer working for the team in charge of the Google Calendar application. Your team has decided to implement several productivity enhancing features. These features will enable individuals, pairs and larger groups of people to meet and collaborate more easily and efficiently.

## Features

We will need to introduce the following features to implement the functionalities we discussed above:
* Features #1: We have a schedule of meetings available. We want to determine and block the minimum number of meeting rooms for these meetings.
* Features #2: Some team leads have requested the ability to display the blocks of time during which they will be busy in meetings. This will help others who want to meet them efficiently request an appropriate meeting time as well as to avoid unnecessary walk-ins.
* Features #3: Before scheduling a meeting, check if the other person will be available during the specified time slot.
* Features #4: Some users have open agenda and open participant meetings so that two meetings can take place at overlapping time at the same venue. Add a new meeting to a user’s already busy schedule while merging the new meeting with existing meetings, if necessary.
* Features #5: Given the schedules of two users, find the time intervals when both of them are busy.
* Features #6: Find two sets of consecutive days to schedule a series of board meetings using the number of mutually free hours of the board members.
* Features #7: Given the schedule of a person, find the longest consecutive busy period.

Understanding these feature requests and designing their solutions will help us implement the requested functionality into the calendar application. In the upcoming lessons, we will discuss these features and their solutions in detail. By the end of the section, you’ll be able to map the solution to this scenario to different interview problems as well.

## Feature #1: Find Meeting Rooms

## Description
To develop this project’s first feature, we are given a set of meeting times. Our job is to implement a solution that can identify the number of meeting rooms needed to schedule the required meetings. Each meeting time will contain a startTime and an endTime that are both positive integers.

Our list of meetings times looks like the following: {{2, 8}, {3, 4}, {3, 9}, {5, 11}, {8, 20}, {11, 15}}. If we schedule each meeting in a separate room, that would require six rooms. However, we want to use the minimum number of rooms possible. In the example, we can see that the first three meetings, {2, 8}, {3, 4}, and {3, 9}, are overlapping. Therefore, each of them will require a separate meeting room.

Take a look at the illustration below to see how we can schedule all the meetings in just three rooms:

![cale](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/cale/cale1.png)

## Solution
We can use a heap or priority queue to keep the meeting timings, where the key would be the end_time of each meeting. This way, we can check if any room is free or not by simply checking the heap’s topmost element. The room at the top of the heap would get free the earliest out of all the other rooms currently occupied.

If the room we obtain from the top of the heap isn’t free yet, then this means no other room is free either. So, we can allocate a new room in this condition.

Here is how the implementation will take place:
* Sort the given meetings by their startTime.
* Allocate the first meeting to a room and add an entry in the heap with the meeting’s endTime.
* Traverse over the remaining meetings, and keep checking if the meeting at the top of the heap has ended or not. This will tell us if a room is free yet.
* If the room is free, then we extract this element and add it again in the heap with the ending time of the current meeting we are processing.
* If not, then we allocate a new room and add it to the heap.
* After processing all the meetings, the heap’s size will tell us the number of rooms allocated. This will be the minimum number of rooms needed to accommodate all the meetings.

{% highlight java %}
import java.util.Arrays; 
import java.util.PriorityQueue;
class Solution {

    public static int minMeetingRooms(int[][] meetingTimes){
        
        if(meetingTimes.length == 0){
            return 0;
        }

        Arrays.sort(meetingTimes, (a, b) -> Integer.compare(a[0], b[0]));       
        //min Heap keeps track of earliest ending meeting:
        PriorityQueue<Integer> minHeap = new PriorityQueue<>((A, B) -> A - B);
        
        minHeap.add(meetingTimes[0][1]);
        
        for (int i = 1; i < meetingTimes.length; i++) {
            int currStart = meetingTimes[i][0];
            int currEnding = meetingTimes[i][1];
            int earliestEnding = minHeap.peek();
            
            if (earliestEnding <= currStart) {
                minHeap.remove();
            } 
            //update heap with curr ending
            minHeap.add(currEnding);
        }
        return minHeap.size();
    }

    public static void main( String args[] ) {
        // Driver code
        int[][] meetingTimes = {{2, 8}, {3, 4}, {3, 9}, {5, 11}, {8, 20}, {11, 15}};
        System.out.print(minMeetingRooms(meetingTimes));
    }
}
{% endhighlight %}

![cale](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/cale/cale2.png)

## Feature #2: Show Busy Schedule

## Description
For the next feature, we want to find the times during which a user is busy. This feature is intended to show the busy hours of a user to other users without revealing the individual meeting slots. Therefore, if any meetings overlap or are back to back, then we want to merge their timings.

We will be provided a list of scheduled meetings, such as [[1, 4], [2, 5], [6, 8], [7, 9], [10, 13]]. In this schedule, [1, 4] and [2, 5], as well as [6, 8] and [7, 9], are overlapping. After merging these meetings, the schedule becomes [[1, 5], [6, 9], [10, 13]].

The illustration below shows a visual representation of the example.

![cale](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/cale/cale3.png)

Note: For simplicity, we are mapping the military timing to integers in the input. So, for example, 8:00 will be denoted by 8 in the code.

## Solution
To solve this problem, it is best to sort the meetings based on the startTime. Then, we can determine if two meetings should be merged or not by processing them simultaneously.

Here is how we’ll implement this feature:
* First, we will sort the meetings according to startTime.
* Considering two meetings at a time, we will then check if the startTime of the second meeting is less than the endTime of the first meeting.
* If the condition is true, merge the meetings into a new meeting and delete the existing ones.
* Repeat the above steps until all the meetings are processed.

{% highlight java %}
import java.util.Arrays;
import java.util.ArrayList; 
class Solution {
    public static int[][] mergeMeetings(int[][] meetingTimes){
        Arrays.sort(meetingTimes, (a, b) -> Integer.compare(a[0], b[0])); 
        
        ArrayList<int[]> merged = new ArrayList<>();
        for (int[] meeting: meetingTimes){
            int size = merged.size();
            if(size == 0 || merged.get(size - 1)[1] < meeting[0]){
                merged.add(meeting);
            }
            else{
                merged.get(size - 1)[1] = Math.max(merged.get(size - 1)[1], meeting[1]);
            }
        }
        return merged.toArray(new int[merged.size()][]);
    }
    public static void main( String args[] ) {
        int[][] meetingTimes1 = {{1, 4}, {2, 5}, {6, 8}, {7, 9}, {10, 13}};
        System.out.println(Arrays.deepToString(mergeMeetings(meetingTimes1)));
        int[][] meetingTimes2 = {{4, 7}, {1, 3}, {8, 10}, {2, 3}, {6, 8}};
        System.out.println(Arrays.deepToString(mergeMeetings(meetingTimes2)));
    }
}
{% endhighlight %}

![cale](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/cale/cale4.png)

## Feature #3: Check if Meeting is Possible

## Description
For this feature, we want to program a function that will let User A know if it is possible to schedule a meeting with User B or not. This decision will be made based on User B’s meeting schedule. If the new meeting’s time overlaps with an existing meeting in User B’s schedule, then the new meeting can not be scheduled.

Note: We will assume that User A is already free during the time of the new meeting, so no checks for this user are needed.

You will be given a list of start and end times of User B’s scheduled meetings, which are non-overlapping. Additionally, you will be given the start and end times for the proposed meeting, which we need to verify is schedulable.

Suppose that the list of timings is {{1, 3}, {4, 6}, {8, 10}, {10, 12}, {13, 15}}, and the new meeting is {7, 8}. In this example, you can see that the new meeting does not overlap with any existing meetings. Therefore, it can be scheduled, and the output will be True. Now, consider if the new meeting had been {9, 11}. It would have overlapped with {8, 10} and {10, 12}. Therefore, the output would have been false.

![cale](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/cale/cale5.png)

Note: For simplicity, we are mapping the military timing to integers in the input. So, for example, 8:00 will be denoted by 8 in the code.

## Solution

This feature can be implemented by brute force traversal. However, we can make it more efficient using a Binary Search Tree (BST). The main advantage is that we can insert all the meetings in a BST first, and then check if the new meeting can also be inserted without any clash. Placing the meetings in a BST in sorted order lets us verify whether the new meeting can be added in O(log(n))O(log(n)) time.

Here is how we will implement this feature:

* BST class: First, we will implement a simple BST class with a constructor, an insert function, and an addNode function.
   * constructor: The default constructor initializes the root of the node as null. Later on, this root will be of type Node.
   * insert() function: This function takes in the start and end timing of meetings and creates a new node. If the root is null, then the new node will become the root. Otherwise, the recursive helper function addNode will be called. The return type of this function is Boolean, as we will use it to determine if the node was added successfully.
   * addNode() function: This recursive helper function has two inputs: currentNode, which is initially the root node, and the newNode to be added. We will check if the newNode starts before the currentNode ends; this shows that there is no conflict up to this point. This means we will have to call the recursive function again to check for a conflict in the right child of the currentNode. If the previous check does not pass, we will check if the newNode starts after the currentNode and similarly call the recursive function for the left subtree if the check passes. If both of these conditions fail, this means that the new meeting overlaps with an existing meeting. Therefore, we will return false.
* checkMeeting() function: We initialize the BST with the user’s scheduled meetings in this function. Then, we will add the new meeting and return the result.

{% highlight java %}
class BST {
    class Node{
        int start;
        int end;
        Node leftChild;
        Node rightChild;
        Node(int start, int end){
            this.start = start;
            this.end = end;
        }
    }

    Node root;

    public BST(){
        this.root = null;
    } 

    public boolean insert(int start, int end) {
        
        if (this.root == null) {
            root = new Node(start, end);
            return true;
        }
        Node newNode = new Node(start, end);
        return addNode(this.root, newNode);
    }

    public boolean addNode(Node currentNode, Node newNode) {
        if(newNode.start >= currentNode.end){
            if(currentNode.rightChild == null){
                currentNode.rightChild = newNode;
                return true;
            }
            return addNode(currentNode.rightChild, newNode);
        }
        else if (newNode.end <= currentNode.start){
            if(currentNode.leftChild == null){
                currentNode.leftChild = newNode;
                return true;
            }
            return addNode(currentNode.leftChild, newNode);
        }
        else{
            return false;
        }
    }
}
class Solution {
    
    public static boolean checkMeeting(int[][] meetingTimes, int[] newMeeting){
        BST tree = new BST();
        for(int[] meeting: meetingTimes){
            tree.insert(meeting[0], meeting[1]);
        }
        return tree.insert(newMeeting[0], newMeeting[1]);
    }

    public static void main( String args[] ) {
        int[][] meetingTimes = {{1, 3}, {4, 6}, {8, 10}, {10, 12}, {13, 15}};
        int[] newMeeting = {7, 8};
        System.out.println(checkMeeting(meetingTimes, newMeeting));
        newMeeting = new int[] {9, 11};
        System.out.println(checkMeeting(meetingTimes, newMeeting));
    }
}
{% endhighlight %}

![cale](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/cale/cale6.png)

## Feature #4: Schedule a New Meeting

## Description
For this feature, we have a user who wants to add a new meeting to their tentative meeting schedule. First, we need to add the new meeting to the user’s schedule. Then, we want to make refinements in the schedule to merge some of the meetings. The user’s initial schedule will have no conflicts; however, the new meeting might overlap with one or more of the older ones. Therefore, we can save time by merging some of the meetings that can be held together in the same venue (this can be done for the tasks that can run simultaneously). The meetings can only be merged if the new meeting time overlaps or is adjacent to an existing meeting. We merge these meetings to eliminate conflict.

Suppose you are given a list of non-overlapping scheduled meetings, such as {{1, 3}, {4, 6}, {8, 10}, {10, 12}, {13, 15}, {16, 18}}. The new meeting, which we need to fit into this already busy schedule, is also given; it is {9, 13}. In this case, the new meeting overlaps with two meetings: {8, 10} and {10, 12}. After merging, the meeting is adjacent to the {13, 15} meeting, so {13, 15} will also be merged. Hence, the final schedule for the day will be: {{1, 3}, {4, 6}, {8, 15}, {16, 18}}.

The illustration below shows a visual representation of the example.

![cale](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/cale/cale7.png)

Note: For simplicity, we are mapping the military timing to integers in the input. So, for example, 8:00 will be denoted by 8 in the code.

## Solution
To implement this feature, we need to first sort the meetings based on startTime. Then, we will process the meetings that come before the new meeting, insert the new meeting, and merge the new meeting with the older ones if needed.

Here is how we will implement this feature:
* First, we need to sort the meetings according to the starting times.
* After the meetings are sorted, we will create a new list called output and add the meetings that start before the newMeeting to it.
* Then, we will add the newMeeting to the output and merge it with the previously added meeting (if the new meeting starts before the previously added meeting).
* Finally, we will add the remaining meetings to the output and merge it with the last added meeting (if the last added meeting starts before the previously added meeting).

{% highlight java %}
import java.util.Arrays;
import java.util.ArrayList; 
class Solution {
    public static int[][] insertMeeting(int[][] meetingTimes, int[] newMeeting){
        Arrays.sort(meetingTimes, (a, b) -> Integer.compare(a[0], b[0]));

        ArrayList<int[]> output = new ArrayList<>();
        int i = 0;
        int n = meetingTimes.length;
        int newStart = newMeeting[0];
        int newEnd = newMeeting[1];
        while(i < n && newMeeting[0] > meetingTimes[i][0]){
            output.add(meetingTimes[i]);
            i++;
        }
        
        if(output.size() == 0 || output.get(output.size() - 1)[1] < newMeeting[0]){
            output.add(newMeeting);
        }
        else{
            output.get(output.size() - 1)[1] = Math.max(output.get(output.size() - 1)[1], newMeeting[1]);
        }
        
        while(i < n){
            
            if(output.get(output.size() - 1)[1] < meetingTimes[i][0]){
                output.add(meetingTimes[i]);
            }
            else{
                output.get(output.size() - 1)[1] = Math.max(output.get(output.size() - 1)[1], meetingTimes[i][1]);
            }
            i++;
        }

        return output.toArray(new int[output.size()][]);
    }

    public static void main( String args[] ) {
        int[][] meetingTimes = {{1, 3}, {4, 6}, {8, 10}, {10, 12}, {13, 15}, {16, 18}};
        int[] newMeeting = {9, 13};
        System.out.println(Arrays.deepToString(insertMeeting(meetingTimes, newMeeting)));
    }
}
{% endhighlight %}

![cale](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/cale/cale8.png)

## Feature #5: Find Common Meeting Times

## Description
For the final part of this project, we want to implement a feature that lets us see when two users are busy at the same time. We will be given the meeting schedule of two users, and we have to find all the overlapping meetings to determine when both of them are unavailable.

We will also assume that each user’s schedule is free of conflicting meetings, meaning their schedules are non-overlapping. Moreover, the meetings have been already sorted based on their starting time.

Let’s say that we are given the following pairs of meeting schedules: {{1, 3}, {5, 6}, {7, 9}} and {{2, 3}, {5, 7}}. In this example, we can see that both of the users will be busy at the following times: {{2, 3}, {5, 6}}.

Take a look at the illustration given below:

![cale](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/cale/cale9.png)

Note: For simplicity, we are mapping the military timing to integers in the input. So, for example, 8:00 will be denoted by 8 in the code.

## Solution

Here is how we will implement this feature:
* We will use two indices, i and j, to traverse both of the meeting schedules, meetingsA and meetingsB, respectively.
* The indices i and j will both be zero at the beginning.
* Next, we will check if meetingsA[i] and meetingsB[j] overlap by comparing the start and end times.
* If the times overlap, the overlapping time interval will be added to the resultant list.
* Otherwise, we will keep incrementing the indices depending upon the end time of the next meeting. This means that if the next meeting in meetingsA ends before the next meeting in meetingsB we will only increment i. This is because the current meeting in meetingsB has the possibility to overlap with the next meeting. Similarly, vice versa is also true in case of incrementation in j.

{% highlight java %}
class Solution {

    public static int[][] meetingsIntersection(int[][] meetingsA, int[][] meetingsB){
        ArrayList<int []> intersection = new ArrayList<>();
        int i = 0;
        int j = 0;
        while (i < meetingsA.length && j < meetingsB.length) {
            int start = Math.max(meetingsA[i][0], meetingsB[j][0]);
            int end = Math.min(meetingsA[i][1], meetingsB[j][1]);
            if (start < end)
                intersection.add(new int[]{start, end});

            if (meetingsA[i][1] < meetingsB[j][1])
                i++;
            else
                j++;
        }

        return intersection.toArray(new int[intersection.size()][]);
    }
    public static void main( String args[] ) {
        int[][] meetingsA = {{1, 3}, {5, 6}, {7, 9}};
        int[][] meetingsB = {{2, 3}, {5, 7}};
        System.out.println(Arrays.deepToString(meetingsIntersection(meetingsA, meetingsB)));
    }
}
{% endhighlight %}

![cale](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/cale/cale10.png)

## Feature #6: Find Two Sets of Consecutive Days

## Description
An enterprise partner has asked us to create a feature for them. They want us to find two sets of consecutive days to schedule board meetings. They are selecting members for two teams from a candidate pool. Selecting each team takes k hours. We want to schedule two sets of meetings, one for each team, of duration k hours each. To ensure fairness, we want the selection committee meetings for a specific team to be done on consecutive days. This means that, once the interviews for a specific team start, there should be meetings every day until the interviews are over. The interviews for the second team cannot start on the last day of selections for the first team; they do not necessarily need to start the very next day, either. To best utilize everyone’s time, we want to fully utilize the mutually free hours on each day meetings are scheduled. We have already found the number of mutually free hours over a set of consecutive days for the members of the selection committee. Furthermore, we want each selection meeting to last as few days as possible. Your task is to find two sets of consecutive days for these selection board meetings that fulfill the above criteria and return the total number of days needed for the meetings.

For example, consider that the number of mutually free hours over a set of consecutive days are {1, 2, 2, 3, 2, 6, 7, 2, 1, 4, 8]}, and k is 5. In this case, the possible set of days with k free hours are {1, 2, 2}, {3, 2}, and {1, 4}. The requirements said that we want to select the sets that span the fewest days, so those are: {3, 2} and {1, 4}. Your function should return the total days that will be needed for both sets of meetings. Therefore, the output will be 4 for this example.

## Solution
To implement this solution, we can calculate the prefix sum for each index in the input array and use a hash table to store it. Then, we traverse the array and use the hash table to find the shortest subarrays with a sum equal to k.

The complete algorithm is given below:
* First, we will traverse through the input array once and store the key-value pairs in a hash table such that, for every ith index, the key is the sum of hoursPerDay[0] to hoursPerDay[i] and the value is i.
* We will also add (0, -1) to the hash table as the default.
* Now, we will traverse through the array again, and for every i, we will find the minimum value of the length of the subarray on the left or starting with i, whose value is equal to k.
* Then, we will find another subarray starting with i + 1, whose sum is k.
* We will update the result with the minimum value of the sum of both the subarrays. This is possible because all the values are positive, and the value of the sum is strictly increasing.

{% highlight java %}
class Solution {
    public static int twoSetsOfDays(int[] hoursPerDay, int k) {
        HashMap < Integer, Integer > hmap = new HashMap < >();
        int sum = 0;
        int lsize = Integer.MAX_VALUE;
        int result = Integer.MAX_VALUE;
        hmap.put(0, -1);
        for (int i = 0; i < hoursPerDay.length; i++) {
            sum += hoursPerDay[i];
            hmap.put(sum, i); 
            
        }
        sum = 0;
        for (int i = 0; i < hoursPerDay.length; i++) {
            sum += hoursPerDay[i];
            if (hmap.get(sum - k) != null) {
                // stores minimum length of sub-array ending with index<= i with sum k. This ensures non- overlapping property.
                lsize = Math.min(lsize, i - hmap.get(sum - k)); 
            }
            //searches for any sub-array starting with index i+1 with sum k.
            if (hmap.get(sum + k) != null && lsize < Integer.MAX_VALUE) {
        
                result = Math.min(result, hmap.get(sum + k) - i + lsize); 
            }
        }
        if (result == Integer.MAX_VALUE) return - 1;
        else return result;
    }
    public static void main( String args[] ) {
        int[] hoursPerDay = {1, 2, 2, 3, 2, 6, 7, 2, 1, 4, 8};
        int k = 5;
        System.out.println(twoSetsOfDays(hoursPerDay, k));
    }
}
{% endhighlight %}

![cale](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/cale/cale11.png)

## Feature #7: Longest Busy Period

## Description
A person has divided their workday into 15-minute time slots numbered as 1, 2, 3, ... n. People who want to schedule a meeting with this person choose any available time slot that suits them. Assume that this person’s calendar is now filled with jumbled up numbers that represent the time slots reserved for meetings. Your task is to find out what the longest consecutive time period in which this person will be busy is.

The following illustration shows how we will be mapping the 15-minute time slots to the numbers given in the input:

![cale](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/cale/cale12.png)

For example, you are given the following list of busy slots: [3, 1, 15, 5, 2, 12, 10, 4, 8, 9]. In this list, the longest sequence of consecutive slots is [1, 2, 3, 4, 5]. Since the length of this sequence is five, your function should return 5.

![cale](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/cale/cale13.png)

## Solution

The longest busy period can start from any of the array’s indexes, so we have to search the entire array. Additionally, for each slot, we need to look up the entire array for the next consecutive slot. We can use the set data structure and convert a linear time lookup to constant time to find the longest sequence of consecutive numbers.

Here is how the implementation will take place:
1. Initialize a set data structure and store the busy schedule in it.
2. Traverse the input array, and for each time slot, check if the next consecutive slot is in the array or not.
3. If the above condition is true, keep incrementing the slot number until we get a slot that is not in the set.
4. We will keep the count of consecutive slots in a variable. If the current longest slot count is greater than the previously calculated one, we will replace it with the current one.
5. Return the largest slot count at the end.

{% highlight java %}
class Solution {
    public static int lengthOfLongestBusyPeriod(Integer[] schedule){
        int longestBusyPeriod = 0;
        Set<Integer> slotSet = new HashSet<Integer>(Arrays.asList(schedule));
        for(int slot : slotSet){
            if (!slotSet.contains(slot - 1)){
                int currentSlot = slot;
                int currentConsecutiveSlot = 1;
                while (slotSet.contains(currentSlot + 1)){
                    currentSlot++;
                    currentConsecutiveSlot++;
                }
                if (currentConsecutiveSlot > longestBusyPeriod)
                    longestBusyPeriod = currentConsecutiveSlot;
            }
        }

        return longestBusyPeriod;
    }
  
  
    public static void main( String args[] ) {
        Integer[] schedule = {3, 1, 8, 5, 2, 12, 10, 4, 8, 9};
        System.out.println(lengthOfLongestBusyPeriod(schedule));
    }
}
{% endhighlight %}

![cale](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/cale/cale14.png)
