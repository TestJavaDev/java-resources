---
layout: default
title: Cellular Operator
parent: Coding Interview
has_children: true
nav_order: 18
permalink: /coding_interview/operator
---
<div align="center" markdown="1">
Cellular Operator / Java resources / Tutorial

{: .fs-8 .fw-400 }
</div>

## Cellular Operator(AT&T)

## Project Description for Cellular Operator

## Introduction
Cellular networks provide us with much-needed connectivity. The cellular network market landscape in any region is generally very competitive. Cellular operators want to earn new customers and retain them with great services at low service charges. These companies survey major and minor areas of a region before setting up their towers. This survey helps them analyze which sites are best for maximum coverage.

The scenario and the problems discussed in this chapter also relate to site analysis for signal coverage and improving coverage.

## Statement
Assume you are a developer on AT&T’s engineering team. You have received survey reports detailing the signal strengths in different buildings and open areas. You have to analyze the data to identify low and high coverage points to assess the viability of operating in that place. Additionally, you have to program a vintage system to power up with minimum computation time.

## Features
We need to introduce the following features to implement the functionalities discussed above:
* Feature #1: Determine the furthest location in a rectangular grid beyond which a handset will receive the optimum signal to work.
* Feature #2: Determine the largest area in a rectangular grid in which signal coverage is minimum.
* Feature #3: Optimally power up a vintage system using dial turns.

Understanding these feature requests and designing their solutions will help us implement the requested functionality into AT&T’s system.

In the next few lessons, we’ll discuss these features’ recommended implementations. The solutions to these basic problems are also applicable to other common coding interview questions.

## Feature #1: Determine Location

## Description
Using a base station located in the top left corner, a cellular operator serves a rectangular region. They have done a road test where they measured the strength of the signal received from their network in a rectangular region. They recorded the loss in signal strength perceived at various parts of the region. The signal loss increases when you move towards the right of the region. The signal loss also increases as you move vertically towards the bottom of the region. To do this, the operator targets a specific handset that works as long as the signal strength does not fall below a certain threshold value. We want to determine the farthest point from the base station within this rectangular region where the handset will work.

We’ll be provided with a 2D matrix consisting of signal strength loss values and a threshold loss value. We need to determine the furthest location beyond which the handset will not work.

![das](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/das/das1.png)

## Solution
We can take advantage of the fact that the value of our matrix increases as we move right in the row and down the column, and we can perform a kind of binary search on this. We can observe that from a current value, cVal, in a column, all values above it will be smaller. So, if our cVal is already smaller than the target loss value, we know that all values above cVal in the current column will also be smaller than this loss value. Taking this observation into account, we can skip the current column and move one column to the right. A similar analysis can be done for rows as well.

Note: We cannot do our searching procedure from the top left or the bottom right corner since in both cases, the keys at either side of that corner are increasing or decreasing, respectively. We can also start the search from the top right corner, which would result in similar results as starting from the bottom left as we did.

Let’s see how we might implement this functionality:
1. Initialize a (row, col) pointer at the bottom-left of our matrix.
2. Traverse the matrix until we find the value or the (row, col) pointer points outside the matrix dimensions.
3. If the current value is larger than the target loss value, move one row up by decrementing the row value from our pointer.
4. Otherwise, if the current value is smaller than the target loss value, move one column right by incrementing the col value from our pointer.

The following illustration might clarify this process.

![das](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/das/das2.png)
![das](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/das/das3.png)
![das](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/das/das4.png)
![das](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/das/das5.png)
![das](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/das/das6.png)
![das](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/das/das7.png)
![das](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/das/das8.png)
![das](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/das/das9.png)
![das](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/das/das10.png)
![das](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/das/das11.png)

Let’s look at the code for the solution:

{% highlight java %}
import java.util.*;
class Solution {
    public static int[] determineLocation(int[][] region, int lossValue) {
        int row = region.length-1;
        int col = 0;

        while (row >= 0 && col < region[0].length) {
            if (region[row][col] > lossValue) {
                row--;
            } else if (region[row][col] < lossValue) {
                col++;
            } else {
                int[] temp = {row, col};
                return temp;
            }
        }
        int[] temp = {-1, -1};
        return temp;
    }

    public static void main( String args[] ) {
        // Driver code
        
        int[][] region = {{1,4,7,11,15},{2,5,8,12,19},{3,6,9,16,22},{10,13,14,17,24},{18,21,23,26,30}};
        int lossValue = 5;

        System.out.println("The coordinates of the loss value region are: " + Arrays.toString(determineLocation(region, lossValue)));
    }
}
{% endhighlight %}

![das](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/das/das12.png)

## Feature #2: Low Coverage Area

## Description
In a busy city center, our cellular operator has surveyed a mall, which happens to be rectangular in shape. They have identified locations within the mall where cellular network signals are unacceptably low. The result of the study is stored in the form of a rectangular matrix of 0s and 1s. Each cell in the matrix corresponds to a unit area in the mall. If the value in a cell of this array is 1, it means the corresponding location in the mall does not have good network coverage. The operator is considering deploying small radio sites inside the mall. These sites use beamforming technology, which enables providing coverage to a rectangular region. We need to determine the rectangle with the largest area with unacceptable coverage throughout.

We’ll be provided with an m x n matrix of 0s and 1s. We have to find the area of the largest rectangle containing only 1s since that will represent the largest, low coverage, rectangular part of the mall.

![das](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/das/das13.png)

## Solution
We will attempt to solve the smallest portion of the input in the original problem and gradually build to larger chunks of the input until we find the answer to the problem using the original input. To this end, we will first determine the area of the largest rectangle of 1s considering only the first row of the input. Then, we will find the area of the largest rectangle ending at the second row of input and including the first one. We will repeat this process on increasing subproblem sizes. As we keep increasing the subproblem size while maintaining the maximum area, we will find the area of the largest group of contiguous 1s in the original input.

To determine the maximum area rectangle within a subset of consecutive rows from the input, we will maintain a list, dp, with a size equal to the number of columns in the input matrix. After k iterations of our algorithm, the ith element in the dp list will hold the number of consecutive 1s in column i ending at the kth row of the input. For example, when we process the first row of the input shown above, [0 1 1], we want the list dp to hold [0 1 1]. How do we determine the maximum area of consecutive 1s in this list, meaning just the first row of the original input? We can again apply the divide and conquer strategy and look at a gradually increasing number of columns from the dp list.

As we process one column from dp, we determine the maximum area of consecutive 1s that that column is part of. For instance, if we consider the first column of dp, what’s the largest area of consecutive 1s? Since dp is [0 1 1], the answer is 0 because the first column has no 1s. How about the second column? If it were part of a rectangle of 1s, it would span the second and third column - with a width of 2, height of 1, and with an area(height * width) of 2. The same goes for the third column of dp as well. The maximum area we’ve seen so far is 2.

![das](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/das/das14.png)

Now, we process dp one column at a time as before. If the first column is part of a rectangle of consecutive 1s, its area will be 3 - with a height of 1 and spanning a width of 3. Now, let’s consider the second column of dp. If it were part of a maximally sized rectangle, it would have a height of 2 and span the second and third columns with an area of 4. This is greater than the previously-known maximum area of 3. So, we update our maximum sized rectangle area across the first two rows at 4. As we process the third row, the streak of 1s gets discontinued in the first and third column, while it continues to grow in the second column. So, we get dp =[0 3 0]. Again, we’ll process this one column at a time. The first and third columns have no contribution, and the second column can only contribute a rectangle of area 3. This is less than the maximum area seen so far, which is 4. Therefore, our answer remains 4.

Processing the dp array step by step is really simple. We initialize dp to [0 0 0]. Then, we read the first row from the input one value at a time. If the value in the input is 1, we increment the corresponding value in dp. Otherwise, we reset it to 0.

As we process each column of the dp list, how do we find the maximal rectangle from it?

We know that Area = height * widthArea=height∗width, and this needs to be calculated for each column in dp so we can return the maximum one. Let’s suppose we want to calculate the maximum rectangle of 1s from dp =[1 2 2], whose histogram representation we saw earlier. We have the heights metric for each point, but how do we calculate the width? Let’s suppose, we want to calculate the width at dp[1]. We’ll look to its left to find the first index(L), whose value is smaller than the value at dp[1]. Then, we’ll look at its right to find the first index(R) whose value is smaller than the value at dp[1]. Our width for dp[1] will come out to be width = (R - L) - 1 = (3 - 1) - 1 = 1width=(R−L)−1=(3−1)−1=1. Hence, the area at dp[1] will be Area = dp[1] * width = 2 * 1 = 1Area=dp[1]∗width=2∗1=1, which is the area of the rectangle at dp[1].

In this case, a valid L, existed but where did R come from? The R value was the size of the dp. How can we calculate the L and R if we encounter the smallest height in the list or the height equal to all the points either to its left or right? We can have boundary values for L and R if such cases occur. The L can be assigned -1, and R can be assigned to the length of the dp list.

We can use a stack-based solution in which we keep pushing the list’s indexes on the stack until we encounter an index whose value is less than the one currently on top of the stack. This new, smaller value will be our R value for the index currently on top of the stack. The L value for the top stack element will be the value second to the top because we are building a gradually increasing stack. If we reach the end of our list and the stack still has elements in it, no valid R values exist anymore since there are no more indexes to traverse. The above-mentioned R value will be used for this case. We’ll also keep updating the maximum area value if the current area comes out to be larger.

The following illustration might further clarify this process:

![das](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/das/das15.png)
![das](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/das/das16.png)
![das](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/das/das17.png)
![das](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/das/das18.png)
![das](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/das/das19.png)
![das](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/das/das20.png)
![das](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/das/das21.png)
![das](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/das/das22.png)

Let’s look at the code for the solution:

{% highlight java %}
import java.util.*;

class Solution {

    public static int maximumRowArea(int[] heights) {
        Stack <Integer> stack = new Stack<>();

        // Initialize stack with the default L value
        stack.push(-1);
        
        int maxArea = 0;
        for (int i = 0; i < heights.length; ++i) {

            while (stack.peek() != -1 && heights[stack.peek()] >= heights[i]){
                int height = heights[stack.pop()];
                int R = i;
                int L = stack.peek();
                int width = (R - L) - 1;
                int area = height * width;

                maxArea = Math.max(maxArea, area);
            }

            stack.push(i);

        }
        
        // Case when no valid R value exists anymore
        while (stack.peek() != -1)
        {
            int height = heights[stack.pop()];
            int R = heights.length;
            int L = stack.peek();
            int width = (R - L) - 1;
            int area = height * width;

            maxArea = Math.max(maxArea, area);
        }

        return maxArea;
    }
    
    public static void main( String args[] ) {
        // Driver code
        
        int[] heights = {2,1,5,6,2,3};

        System.out.println("Maximum Row Area: " + maximumRowArea(heights));
    }
}
{% endhighlight %}

Returning to the original problem, we now know how to calculate the area of subsequent rows. We simply need to traverse over the matrix computing area at every row and return the maximum area found.

Let’s see how we might implement this functionality:
1. Initialize a list of integers dp with zeros of size equal to the number of columns.
2. Start traversing the matrix. For each row, we’ll update the dp list values as follows:
   * If row[i] == 0, update dp as dp[i] = 0.
   * If row[i] == 1, update dp as dp[i] = dp[i] + 1.
3. Calculate the maximum area of each row using the maximum_row_area program explained above.
4. Keep updating the maximum area for each row, and return the largest area at the end.

The following illustration might further clarify this process:

![das](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/das/das23.png)
![das](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/das/das24.png)
![das](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/das/das25.png)
![das](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/das/das26.png)

Let’s look at the code for the solution:

{% highlight java %}
import java.util.*;

class Solution {

    public static int maximumRowArea(int[] heights) {
        Stack <Integer> stack = new Stack<>();

        // Initialize stack with the default L value
        stack.push(-1);
        
        int maxArea = 0;
        for (int i = 0; i < heights.length; ++i) {

            while (stack.peek() != -1 && heights[stack.peek()] >= heights[i]){
                int height = heights[stack.pop()];
                int R = i;
                int L = stack.peek();
                int width = (R - L) - 1;
                int area = height * width;

                maxArea = Math.max(maxArea, area);
            }

            stack.push(i);

        }
        
        // Case when no valid R value exists anymore
        while (stack.peek() != -1)
        {
            int height = heights[stack.pop()];
            int R = heights.length;
            int L = stack.peek();
            int width = (R - L) - 1;
            int area = height * width;

            maxArea = Math.max(maxArea, area);
        }

        return maxArea;
    }

    public static int lowCoverage(String[][] matrix) {

        if (matrix.length == 0) return 0;
        int maxArea = 0;
        int[] dp = new int[matrix[0].length];

        for(int i = 0; i < matrix.length; i++) {
            for(int j = 0; j < matrix[0].length; j++) {

                // update the state of this row's dp array using the last row's dp array
                // by keeping track of the number of consecutive ones
                if (matrix[i][j] == "1"){
                    dp[j] = dp[j] + 1;
                }
                else{
                    dp[j] = 0;
                }
            }
            // update maxArea with the maximum area from this row's dp array
            maxArea = Math.max(maxArea, maximumRowArea(dp));
        } return maxArea;
    }

    public static void main( String args[] ) {
        // Driver code
        
        String[][] mall = {
                        {"1","0","0","1","1","1"},
                        {"1","0","1","1","0","1"},
                        {"0","1","1","1","1","1"},
                        {"0","0","1","1","1","1"}
                    };

        System.out.println("Maximum Low coverage area is " + lowCoverage(mall) + " units");
    }
}
{% endhighlight %}

![das](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/das/das27.png)

## Feature #3: Power Up the Station

## Description
AT&T just acquired a cellular company in a small town that owns four base stations. The company they acquired owned vintage equipment with dials that must be rotated clockwise or counterclockwise by hand to power up the base stations. There’s one dial for each of the base stations. Each dial has numbers from 0 to 9 and does not stop at either extreme; this means you can rotate clockwise at 9 to go back to 0 or counterclockwise at 0 to go to 9.

Each position on a dial represents a particular state for the corresponding base station. To power up the base stations, the dials must be taken from state 0000 to a target state, say abcd, where a, b, c, and d are digits between 0 and 9. The constraints are that only one dial may be turned (clockwise or counterclockwise) one position at a time and certain dead states are prohibited and must be avoided at all costs. The system will get stuck and fail if we land in a dead state.

We’ll be provided with an array of dead states that we need to avoid and a target state that we need to reach. You want to power up the system in the minimum number of dial turns by avoiding the dead states.

## Solution
There are 10,000 digits starting from 0000 to 9999. We have to reach a target number in a minimum number of dial turns. We can consider the 10,000 digits to be nodes in a graph. If two nodes differ in one digit (wrapping around, so 0 and 9 also differ by 1) and both nodes are not dead states, there will be an edge between them. We can use BFS here to find the shortest path from the starting node 0000 to the target node.

We implement the BFS using a queue and a visited set. The main part will be generating the new nodes from the current one. Each digit on the dial can be moved forward or backward, so eight new states can be generated from a single state. We’ll keep adding the new states into the queue if they have not already been visited or explored. The new states should only be generated from nodes that are not part of the dead states.

The eight states will be generated by moving each of the four digits forward and backward once. Usually, we can simply subtract or add 1 to each number to get a new one, but the wrapping around between 0 and 9 is allowed. Therefore, we need to do something else.

We can explicitly check for the condition: if we are subtracting from 0, 9 should be returned. Similarly, if we are adding to 9, 0 should be returned.

![das](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/das/das28.png)

Let’s look at the code for the solution:

{% highlight java %}
import java.util.*;

class Solution {
    public static int powerUp(String[] deadStates, String target) {
        Queue<String> q = new LinkedList<>();
        Set<String> visited = new HashSet<>(Arrays.asList(deadStates));
        int depth = -1;
        q.addAll(Arrays.asList("0000"));
        //System.out.println(q.poll());
        while(!q.isEmpty()) {
            depth++;
            int size = q.size();
            for(int i = 0; i < size; i++) {
                String node = q.poll();
                if(node.equals(target))
                    return depth;
                if(visited.contains(node))
                    continue;
                visited.add(node);
                q.addAll(neighbors(node));
            }
        }
        return -1;
    }
	
    private static List<String> neighbors(String str) {
        List<String> res = new LinkedList<>();
        for (int i = 0; i < str.length(); i++) {
            // Calculate the new state by moving the current number in 
            // opposite direction
            res.add(str.substring(0, i) + (str.charAt(i) == '0' ? 9 :  str.charAt(i) - '0' - 1) + str.substring(i+1));
            
            // Calculate the new state by moving the current number in 
            // forward direction
            res.add(str.substring(0, i) + (str.charAt(i) == '9' ? 0 :  str.charAt(i) - '0' + 1) + str.substring(i+1));
        }
        return res;
    }
    
    public static void main( String args[] ) {
        // Driver code

        String[] deadStates = {"0201","0101","0102","1212","2002"};
        String target = "0202";
        System.out.println("The system will power up in " + powerUp(deadStates, target) + " dial turns");
    }
}
{% endhighlight %}

![das](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/das/das29.png)
