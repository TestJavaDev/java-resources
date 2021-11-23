---
layout: default
title: Meeting Room
parent: Algorithms
nav_order: 10
permalink: /algorithms/meeting_room
---
<div align="center" markdown="1">
Meeting Room / Java resources / Tutorial

{: .fs-8 .fw-400 }
</div>

## Meeting Room

## Problem statement
Given an array of meeting time intervals consisting of start and end times [[s1,e1],[s2,e2],...](si< ei), determine if a person could attend all meetings.

## Example: 1
Input: intervals = [[0,30],[5,10],[15,20]]

Output:false

## Example: 2
Input:intervals = [[7,10],[2,4]]

Output:true

## Intuition
This problem basically asks if there’s any overlap between adjacent intervals. We sort the intervals by start time and use the technique from the intro section to check overlap.

{% highlight java %}
class Solution {
    public static boolean mergeInterval(int[][] intervals) {
      Arrays.sort(intervals, new Comparator<int[]>(){
          public int compare(int[] a, int[] b){
              return a[0]-b[0];
          }
      });

      for(int i=0; i<intervals.length-1; i++){
          if(intervals[i][1]>intervals[i+1][0]){
              return false;
          }
      }

      return true;
    }
    //Driver code
    public static void main(String[] arg){
        int[][][] inputs = [[{0,30},{5, 10},{15,20}],[{7,10},
        {2, 4}]];
        for(int i = 0; i < inputs.length; i++) {
            System.out.println("Merge interval :"+
            Solution.mergeInterval(inputs[i]));
        }
    }
}
{% endhighlight %}

The time complexity is O(Nlog(N)) because sorting takes O(Nlog(N)) and the traversal is O(N).