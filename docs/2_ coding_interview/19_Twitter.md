---
layout: default
title: Twitter
parent: Coding Interview
has_children: true
nav_order: 19
permalink: /coding_interview/twitter
---
<div align="center" markdown="1">
Twitter / Java resources / Tutorial

{: .fs-8 .fw-400 }
</div>

## Twitter

## Project Description for Twitter

## Introduction
Twitter is a social media platform on which users post and interact with messages known as “Tweets.” Twitter is also considered a microblogging service because the text of a Tweet can only be up to 280 characters. The users on Twitter can interact with each other by following each other, which allows them to view each other’s Tweets. They can also Retweet, comment, or like other Tweets.

The scenario and the problems discussed in this chapter relate to Twitter’s Tweet management and recommendation system.

## Statement
Let’s say you are a developer on Twitter’s engineering team. The team has decided to implement APIs that can be exposed to partnered businesses and create modules that can be used for internal workings.

Some of the functionality relates to displaying feeds merged from multiple sources in chronological order. Other functionality relates to analytics and recommendation system.

Features
We will need to introduce the following features to implement the functionalities we discussed above:
* Feature #1: Create an API that calculates the total number of likes on a person’s Tweets.
* Feature #2: Implement a module that adds a user’s Tweets into an already populated Twitter feed in chronological order.
* Feature #3: Identify the time periods in which the maximum number of people interact with a user’s Tweets.
* Feature #4: Check if a group of people can be split into two groups such that no one in the same group follows anyone in the same group. Then, we will recommend people from the same group to each other.

Understanding these feature requests and designing their solutions will help us implement the requested functionality into Twitter’s system.

In the next few lessons, we’ll discuss the recommended implementations of these features. Before we start, we suggest that you think about how you would implement these features. You may recognize some of the underlying problems that you’ll need to solve. The solutions to these basic problems are also applicable to other common coding interview questions.

## Feature #1: Add Likes

## Description
For the first feature of the Twitter application, we are creating an API that calculates the total number of likes on a person’s Tweets. For this purpose, your team member has already extracted the data and stored it in a simple text file for you. You have to create a module that takes two numbers at a time and returns the sum of the numbers. The inputs were extracted from a text file, so they are in the form of strings. The limitation of the API is that we want all of the values to remain strings. We cannot even convert the string to numbers temporarily.

For example, let’s say you are given the strings "1545" and "67" as input. Your module should not convert these into integers while computing the sum and return "1612".

## Solution
To solve this problem, we will do digit-by-digit addition because we cannot convert the strings to integers. The algorithm for decimal addition is given below:
* First, we will initialize an empty res variable.
* Then, we will initialize the carry as 0.
* Next, we will set two pointers, p1 and p2, that point to the end of like1 and like2, respectively.
* We will traverse the strings from the end using p1 and p2 and stop when both strings are done.
* We will set x1 equal to a digit from string like1 at index p1. If p1 has reached the beginning of like1, we will set x1 to 0.
* We will do the same for x2, setting x2 equal to the digit from string like2 at index p2. If p2 has reached the beginning of like2, we will set x2 to 0.
* Now, we will compute the current value using value = (x1 + x2 + carry) % 10. Then, we will update the carry, like so: carry = (x1 + x2 + carry) / 10.
* We will append the current value to the result.
* If both of the strings are traversed but the carry is still non-zero, we will append the carry to res as well.
* At last, we will reverse the result, convert it to a string, and return that string.

![das](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/das/das30.png)
![das](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/das/das31.png)
![das](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/das/das32.png)
![das](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/das/das33.png)
![das](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/das/das34.png)

The implementation of this algorithm is given below:

{% highlight java %}
class Solution {
    public static String addLikes(String like1, String like2){
        StringBuilder res = new StringBuilder();

        int carry = 0;
        int p1 = like1.length() - 1;
        int p2 = like2.length() - 1;
        while (p1 >= 0 || p2 >= 0) {
            int x1, x2;
            if(p1 >= 0)
                x1 = like1.charAt(p1) - '0';
            else 
                x1 = 0;
            if(p2 >= 0)
                x2 = like2.charAt(p2) - '0';
            else 
                x2 = 0;
            int value = (x1 + x2 + carry) % 10;
            carry = (x1 + x2 + carry) / 10;
            res.append(value);
            p1--;
            p2--;    
        }
        
        if (carry != 0)
            res.append(carry);
        
        return res.reverse().toString();
    }
    public static void main(String args[]) {
        System.out.println(addLikes("1545", "67"));
    }
}
{% endhighlight %}

![das](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/das/das35.png)

## Feature #2: Merge Tweets In Twitter Feed

## Description
For the next feature, you have to implement a module that adds a user’s Tweets into an already populated Twitter feed in chronological order. Let’s assume that userA just started following userB. At this point, we want userB's Tweets to show up in userA's Twitter feed. We already have a chronologically sorted list of Tweets that will appear on userA's feed. Your job is to merge it with the list of userB's Tweets, which are also chronologically sorted.

As input, you will be given two sorted integer arrays, feed and tweets. The integers represent the posting time of the Tweets. You are also given the number of elements initialized in both of the arrays, which are m and n, respectively.

Note: Assume that feed has a size equal to m + n such that it has enough space to hold additional elements from tweets.

## Solution
We can solve this problem by comparing both arrays from the end and populating the result in the feed array. Take a look at the complete algorithm below:
* First, we will initialize two pointers, p1 and p2, that point to the last element of each array. (The last element of feed, or the element at the m-1 index, is the last initialized element.)
* Next, we will initialize another pointer called p, which will point to the m + n - 1 index of the feed. We will use this pointer to populate the result.
* Now, we will use the pointer p to traverse the feed array from the end.
* If the value at p1 is less than the value at p2, the result at p will be equal to the value at p1. Otherwise, the result at p will be set equal to the value at p2. We will decrement the pointer for the list that the entry was copied from.
* The traversal will continue until tweet is merged.

![das](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/das/das36.png)
![das](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/das/das37.png)
![das](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/das/das38.png)
![das](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/das/das39.png)
![das](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/das/das40.png)
![das](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/das/das41.png)
![das](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/das/das42.png)
![das](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/das/das43.png)
![das](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/das/das44.png)

{% highlight java %}
class Solution {
    public static void mergeTweets(int[] feed, int m, int[] tweets, int n) {
        int p1 = m - 1;
        int p2 = n - 1;
        
        for (int p = m + n - 1; p >= 0; p--) {
            if (p2 < 0) {
                break;
            }
            if (p1 >= 0 && feed[p1] > tweets[p2]) {
                feed[p] = feed[p1--];
            } else {
                feed[p] = tweets[p2--];
            }
        }
    }
    public static void main(String args[]){
        int[] feed = {23, 33, 35, 41, 44, 47, 56, 91, 105, 0, 0, 0, 0, 0, 0};
        int m = 9;
        int[] tweets = {32, 49, 50, 51, 61, 99};
        int n = 6;
        mergeTweets(feed, m, tweets, n);
        System.out.println(Arrays.toString(feed));
    }
}

{% endhighlight %}

![das](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/das/das45.png)

## Feature #3: Identify Peak Interaction Times

## Description
For this next Twitter feature, the company has decided to create an API that can be used by business accounts on Twitter. This API will identify three disjoint time intervals in which the most users followed or interacted with the businesses’ Tweets. You will be given the historical data of user interaction per hour for a particular business’ Twitter account. The API will have another parameter for hours. Your goal is to find three continuous intervals of a size equal to hours such that the sum of all the entries is the greatest. These time intervals should not overlap with each other.

Consider a Twitter profile with the following history of user interactions: {0, 2, 1, 3, 1, 7, 11, 5, 5} and hours = 2. The interaction array represents that this particular business’ account received no interactions during the first hour, 2 in the second hour, and so on. In this case, we want three intervals of size 2 with the maximum sum. These intervals will be {1, 3}, {7, 11}, and {5, 5}. Your function should return the indices of the first elements in the intervals. Therefore, the output will be: {2, 5, 7}.

Note: If there are multiple answers, you need to return the chronologically earliest one.

## Solution
To solve this problem, we can start by calculating the sum of n intervals for each index, where n = hours. We can store these sums in an array called sums. Then, all that’s left will be to find the lexicographically smallest tuple of indices {a, b, c} that maximizes sums[a] + sums[b] + sums[c].

Let’s take a look at the algorithm to find the solution:
* First, we need to calculate the sums at each index and store them in the array called sums. We can calculate sums using a sliding window.
* When the sums are calculated, we need to find the {a, b, c} indices. We know that we can assume some constraints for the lexicographically smallest trio of indices.
* If we consider b to be fixed, a should be in between 0 and b - n. Similarly, c should be between b + n and sums.length -1. We can deduce these constraints considering we want non-overlapping intervals. We can now find these indices using dynamic programming.
* We will create two arrays, left and right. These arrays will store the maximum starting index from the left and right, respectively. The left[i] will contain the first occurrence of the largest value of W[a] on the interval a \in [0, i]a∈[0,i]. Similarly, the right[i] will be the same but on the interval a \in [i, \text{len}(sums) - 1]a∈[i,len(sums)−1].
* Finally, for each value of b, we will check whether the corresponding left and right values are in the above-mentioned constraints or not. Out of all the trios that fulfill the constraints, we will choose the one that produces the maximum sums[a] + sums[b] + sums[c].

{% highlight java %}
class Solution {
    public static int[] peakInteractionTimes(int[] interactions, int hours) {
        
        int[] sums = new int[interactions.length - hours + 1];
        int currSum = 0;
        for (int i = 0; i < interactions.length; i++) {
            currSum += interactions[i];
            if (i >= hours) {
                currSum -= interactions[i - hours];
            }
            if (i >= hours - 1) {
                sums[i - hours + 1] = currSum;
            }
        }

        int[] left = new int[sums.length];
        int best = 0;
        for (int i = 0; i < sums.length; i++) {
            if (sums[i] > sums[best]) best = i;
            left[i] = best;
        }

        int[] right = new int[sums.length];
        best = sums.length - 1;
        for (int i = sums.length - 1; i >= 0; i--) {
            if (sums[i] >= sums[best]) {
                best = i;
            }
            right[i] = best;
        }
        
        int[] output = new int[]{-1, -1, -1};
        for (int j = hours; j < sums.length - hours; j++) {
            int i = left[j - hours], l = right[j + hours];
            if (output[0] == -1 || sums[i] + sums[j] + sums[l] > sums[output[0]] + sums[output[1]] + sums[output[2]]) {
                output[0] = i;
                output[1] = j;
                output[2] = l;
            }
        }
        return output;
    }

  
    public static void main(String args[]) {
        int[] interaction = {0, 2, 1, 3, 1, 7, 11, 5, 5};
        int hours = 2;
        int[] output = peakInteractionTimes(interaction, hours);
        System.out.println(Arrays.toString(output));
    }
}
{% endhighlight %}

![das](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/das/das46.png)

## Feature #4: Split Users into Two Groups

## Description
In this feature, the company has decided that they want to show people “follow” recommendations. For this purpose, we have been given the “following” relationship information for a group of users in the form of a graph. We want to see if these people can be split into two groups such that no one in the group follows or is followed-by anyone in the same group. We will then recommend people from the same group to each other.

The “following” relationship graph is given in the form of an undirected graph. So, if UserA follows UserB, or the other way around, it does not matter. This graph will be given to you as an input in the form of a 2D array called graph. In this array, each graph[i] will contain a list of indices, j, for which the edge between nodes i and j exists. Each node in the graph will represent a person and will be denoted by an integer ID from 0 to graph.length-1.

For example, the graph can be { {3}, {2, 4}, {1}, {0, 4}, {1, 3} }. This can be illustrated as:

![das](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/das/das47.png)

The nodes in this graph can be split into two groups:

![das](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/das/das48.png)

As we can see, this graph can be split into two groups such that no one in the same group follows or is followed-by anyone in the same group. Therefore, in this case, your function should return True.

## Solution
As mentioned above, a graph that can be split is also called a bipartite graph. To check if a graph is bipartite, we will color a node blue if it is part of the first set; otherwise, we will color it red. We can color the graph greedily if and only if it is bipartite. In a bipartite graph, all of a blue node’s neighbors must be red, and all of a red node’s neighbors must be blue.

The complete algorithm is given below:
* We’ll keep an array or HashMap to store each node’s color as color[node]. The possible values for colors can be 0, 1, or uncolored (-1 or null).
* We will search each node in the graph to ensure disconnected nodes are also visited. For each uncolored node, we’ll start the coloring process by doing DFS on that node.
* To perform DFS, we will first check if the nodes connected to the current node are colored or not. If a node is colored, we will check if the color is the same color as the current node. If the colors are the same, we return false.
* If the node is not colored, we will color it and call DFS on that node recursively. If the recursive call returns false, the current DFS should also return false because coloring will not be possible.
* If everything goes well and colors are assigned successfully, we will return true at the end.

{% highlight java %}
class Solution {
    public static boolean isSplitPossible(int[][] graph) {
        int[] color = new int[graph.length];			
				
        for (int i = 0; i < graph.length; i++) {             
            if (color[i] == 0 && !dfs(graph, color, 1, i)) {
                return false;
            }
        }
        return true;
    }
    
    public static boolean dfs(int[][] graph, int[] color, int currColor, int node) {
        if (color[node] != 0) {
            return color[node] == currColor;
        }       
        color[node] = currColor;       
        for (int i = 0; i < graph[node].length; i++){
            if (!dfs(graph, color, -currColor, graph[node][i])) {
                return false;
            }
        }
        return true;
    }
    public static void main(String args[]) {
        int[][] graph = { {3}, {2, 4}, {1}, {0, 4}, {1, 3} };
        System.out.println(isSplitPossible(graph));
    }
}
{% endhighlight %}

![das](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/das/das49.png)

