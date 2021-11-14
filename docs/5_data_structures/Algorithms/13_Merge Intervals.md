---
layout: default
title: Merge Intervals
parent: Algorithms
grand_parent: Data Structures and Algorithms
nav_order: 13
permalink: /data_structures/algorithms/merge_intervals
---
<div align="center" markdown="1">
Merge Intervals / Java resources / Tutorial

{: .fs-8 .fw-400 }
</div>

## Merge Intervals

## Problem statement
Given a collection of intervals, merge all overlapping intervals.

## Example: 1
Input: [[1,3],[2,6],[8,10],[15,18]]

Output: [[1,6],[8,10],[15,18]]

Explanation: Since intervals [1,3] and [2,6] overlaps, merge them into [1,6].

## Example: 2
Input: intervals = [[1,4],[4,5]]

Output: [[1,5]]

Explanation: Intervals [1,4] and [4,5] are considered overlapping.

Constraints:

intervals[i][0] <= intervals[i][1]

## Intuition
To merge the intervals, we have to establish an order so that the intervals that are close to each other are ordered next to each other so we can merge them. Since an interval is represented by a start time and an end time, we really only have two ways to order them by start time or end time.

Here we sort them by start time and go through each interval. We keep a list of final intervals. For each interval in the sorted interval list, if it has an overlap with the last interval in the final interval list, we update the last interval’s end position. Otherwise, we append the interval to the final interval list. The illustration below should make it very clear how this works.

![quick](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/interval/interval3.png)
![quick](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/interval/interval4.png)
![quick](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/interval/interval5.png)
![quick](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/interval/interval6.png)
![quick](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/interval/interval7.png)
![quick](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/interval/interval8.png)
![quick](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/interval/interval9.png)
![quick](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/interval/interval10.png)
![quick](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/interval/interval11.png)
![quick](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/interval/interval12.png)

While this works, one question you may ask is why we only have to check the last interval and not the second last or the ones before?

It’s because the intervals are sorted by their start time. If a new interval overlaps with the second last interval, then its start time would be smaller than the last interval’s start time. This contradicts the pre-condition that the intervals are sorted by start time and the new interval’s start is always greater than previously processed intervals.

## Implementation
We can check whether two intervals overlap with each other using the technique introduced in the intro section.
{% highlight java %}
class Solution {
    public static int[][] mergeInterval(int[][] intervals) {
      if (intervals.length <= 1)
          return intervals;

      // Sort by ascending starting point
      Arrays.sort(intervals, (i1, i2) -> Integer.compare(i1[0], i2[0]));

      int n = intervals.length;
        List<int[]> r = new ArrayList<>();
        for (int[] inter : intervals){            
            if (r.isEmpty() || !overlap(r.get(r.size() - 1), inter)) {
                r.add(inter);
            } else {
                int[] lastInterval = r.get(r.size() - 1);
                lastInterval[1] = Math.max(lastInterval[1], inter[1]);                
            }
        }

      return r.toArray(new int[r.size()][]);
    }

    public static boolean overlap(int[] a, int[] b){
        return !(a[1] < b[0] || a[0] > b[1]);
    }
        
    //Driver code
    public static void main(String[] arg){
        int[][][] inputs = {{{1, 3}, {2, 6}, {8, 10}, {15,18}},{{1, 4}, {4, 5}}};
        for(int i = 0; i < inputs.length; i++) {
            System.out.println("Merge intervals: "+  Arrays.deepToString(Solution.mergeInterval(inputs[i])));
        }
    }
}
{% endhighlight %}
The time complexity is O(Nlog(N)) because sorting takes O(Nlog(N)) and the traversal is O(N).