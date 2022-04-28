---
layout: default
title: Uber
parent: Coding Interview
has_children: true
nav_order: 6
permalink: /coding_interview/uber
---
<div align="center" markdown="1">
Uber / Java resources / Tutorial

{: .fs-8 .fw-400 }
</div>

## Uber

## Project Description for Uber

## Introduction
Uber is the largest ride-hailing company in the world. They provide services like food and items delivery in addition to the primary service of passenger pick up and drop off. Their user base in terms of consumers and drivers is growing significantly. So, the engineering team at Uber keeps trying to find better ways to efficiently allocate nearby drivers to users.

The scenario and the problems discussed in this chapter discuss efficient driver allocation functionality and how we can improve it.

## Statement
Imagine you are a developer on the Uber engineering team. The team is targeting some optimizations in driver allocation to rides as well as accessibility features for the client application. wants to optimize the process of driver allocation during rainy days. Whenever a user wants a ride, our system will first select the drivers closest to the user’s location. Then, it’ll plot a path from all the drivers’ locations to the user’s location and check whether it is possible for a driver to reach the pick-up location or not.

The map of a city is divided into several checkpoints, and there is a cost associated with the travel between each checkpoint. We’ll calculate the cost it’ll take for every driver to reach the user’s location through multiple checkpoints. The cost will depend on the amount of rainwater accumulated between checkpoints on each path. The driver having the least cost on their path will then get selected for the user. At the end of the ride, a fare will be calculated and we need to update the accessibility plugin to announce that fare aloud. Additionally, to facilitate new drivers we’ll provide them routes on which the probability and possibility of finding rides will be high. We’ll also tweak the rank system so drivers with low-rank also get a chance to become top-rated drivers.

## Features

We need to introduce the following features to implement the functionalities we discussed above:
* Feature #1: Select at least the n nearest drivers within the user’s vicinity, avoiding the drivers that are too far away.
* Feature #2: Calculate the max depth of water along the way between two points in a rain-affected city.
* Feature #3: Find a path from each driver’s location to the user’s location and calculate the cost of travel so we can choose the driver with the least cost.
* Feature #4: Convert the calculated fare to English words for our system to recognize.
* Feature #5: Implement the pool functionality in which drivers can pick up multiple customers. On picking up a pool customer, we will suggest a route to the driver on which they may find more pool customers.
* Feature #6: Introduce the longest route of the city that will maximize the possibility of finding customers.
* Feature #7: Instead of always picking the top-ranked drivers, smartly pair drivers to customers so that high-ranked drivers are more likely, but others are also picked sometimes.

Understanding these feature requests and designing their solutions will help us implement the requested functionality into Uber’s system.

In the next few lessons, we’ll discuss the recommended implementations of these features. Before we start, we suggest that you think about how you would implement these features. As you do, you’ll realize some of the underlying problems that you’ll need to solve. The solutions to these basic problems are also applicable to other common coding interview questions.

## Feature #1: Select Closest Drivers

## Description
The first functionality we’ll be building is to locate the nearest available drivers within the vicinity of a user. There are numerous Uber drivers roaming around in a city. For simplicity, we’ll consider the city as a Cartesian plane and assign the coordinates (0, 0) to the user’s location. When a user wants to book a ride, we’ll simply find k drivers with the shortest distance on the Cartesian plane. Here, k is the minimum threshold for choosing the closest drivers.

We’ll be provided a list containing a set of points on the Cartesian plane and a number k. Each set of points will represent the location of a driver. We need to find the k closest drivers from the user’s location.

## Solution
The Euclidean distance between a point P(x,y) and the origin can be calculated using the following formula: \sqrt{x^2 + y^2}√

​​Now that you can calculate the distance between a user and all nearby drivers, how will you find the K nearest drivers? The best data structure that comes to mind to track the nearest K drivers is Heap.

We iterate through the array and calculate the distance between each driver’s current location and the user. We’ll insert the distances of the first K drivers into the Heap. Each time we find a distance smaller than the maximum distance in the Heap, we do two things:
* Remove the maximum distance from the Heap
* Insert the smaller distance into the Heap

This will ensure that we always have K minimum distances in the Heap. The most efficient way to repeatedly find the maximum number among a set of numbers is to use a max-Heap.

Below is an illustration of this process. We have mapped the city of Seattle onto the cartesian plane to get simpler latitude and longitude values for the driver’s location.

![cale](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/cale/cale43.png)
![cale](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/cale/cale44.png)
![cale](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/cale/cale45.png)
![cale](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/cale/cale46.png)
![cale](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/cale/cale47.png)

Let’s look at the code for the solution:

{% highlight java %}
import java.util.*;

class Location {
  int x;
  int y;

  public Location(int x, int y) {
    this.x = x;
    this.y = y;
  }

  public int distFromOrigin() {
    // ignoring sqrt
    return (x * x) + (y * y);
  }
}

class Solution {

  public static List<Location> findClosestDrivers(Location[] locations, int k) {
    PriorityQueue<Location> maxHeap = new PriorityQueue<>((p1, p2) -> p2.distFromOrigin() - p1.distFromOrigin());
    // put first 'k' locations in the max heap
    for (int i = 0; i < k; i++)
      maxHeap.add(locations[i]);

    // go through the remaining locations of the input array, if a Location is closer to the origin than the top Location 
    // of the max-heap, remove the top Location from heap and add the Location from the input array
    for (int i = k; i < locations.length; i++) {
      if (locations[i].distFromOrigin() < maxHeap.peek().distFromOrigin()) {
        maxHeap.poll();
        maxHeap.add(locations[i]);
      }
    }

    // the heap has 'k' locations closest to the origin, return them in a list
    return new ArrayList<>(maxHeap);
  }

  public static void main(String[] args) {
    Location[] locations = new Location[] { new Location(1, 3), new Location(3, 4), new Location(2, -1) };
    List<Location> result = Solution.findClosestDrivers(locations, 2);
    System.out.print("Here are the k drivers locations closest to the user in the Seattle area: ");
    for (Location p : result)
      System.out.print("[" + p.x + " , " + p.y + "] ");
  }
}

{% endhighlight %}

![cale](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/cale/cale48.png)

## Feature #2: Path Cost

## Description
Now that some drivers have been selected, we need to calculate the cost required to travel between different checkpoints. The cost depends on the amount of water accumulated in different parts of the road. We know that water collects on roads that are either broken or uneven. We will use an API to access the data regarding water on the road, it will transform the 3D layout of the road into a nice 2D layout of water trapped between different parts of the road.

We’ll be given an array whose length is equal to the length of the road between two checkpoints. Each integer value in the array will represent the combined elevation(in cm) of the road at the points where it is broken. We need to find how much total water(in cm) will be accumulated in the spaces left between different elevations of the broken road.

Below is an illustration of this process:

![cale](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/cale/cale49.png)
![cale](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/cale/cale50.png)

## Solution
We need to calculate the amount of water that has accumulated above each road elevation and sum it up. At a single index/elevation (X), the amount of water depends on the heights of the highest bars to it left and right, regardless of how far apart they are. Upon further exploration, we also observe that the elevation (X) + the height of the water above this elevation, is equivalent to the minimum height of the highest bars around it. Therefore, the accumulation of the water, above a certain point (X), can be calculated using the formula:

![cale](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/cale/cale51.png)

Here is how implementation will take place:
* Traverse through the array once.
* Calculate the left_max for each point and save it in an array.
* Traverse the array again to do the same with right_max.
* Traverse the array once more, and use this data to find the amount of water above each point using the formula mentioned above.

Let’s look at the code for the solution:

{% highlight java %}
class Solution 
{ 
  //This method calculates the amount of water trapped. The only argument
  //passed is the elevation map, in form of an array.

	static int pathCost(int[] elevation_map) {
		int water = 0; //keeps track of the total water as we traverse the elevation map

		int n = elevation_map.length; //number of points on the map

		//arrays to store the leftMax and rightMax of each point in the map
		int leftMax[] = new int[n]; 
		int rightMax[] = new int[n]; 
	
		//default values
		leftMax[0] = elevation_map[0]; 
		rightMax[n-1] = elevation_map[n-1]; 

		//filling the leftMax array
		for (int i = 1; i < n; i++) 
			leftMax[i] = Math.max(leftMax[i-1], elevation_map[i]); 
		
		//filling the rightMax array
		for (int i = n-2; i >= 0; i--) 
		rightMax[i] = Math.max(rightMax[i+1], elevation_map[i]); 
	
    	//calculating the amount of water
		for (int i = 0; i < n; i++) 
		water += Math.min(leftMax[i],rightMax[i]) - elevation_map[i]; 
	
		return water; 
	} 
	
	public static void main(String[] args) {
		// Driver code

		int elevation_map[] = new int[]{1, 2, 1, 3, 1, 2, 1, 4, 1, 0, 0, 2, 1, 4};

		System.out.println("Accumulated water: " + pathCost(elevation_map) + "cm"); 
	} 
} 
{% endhighlight %}

![cale](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/cale/cale52.png)

## Feature #3: Plot and Select Path

## Description
After obtaining the closest drivers and calculating the cost of traveling on different roads, we need to build a functionality to select a path from the driver’s location to the user’s location. All the drivers have to pass through multiple checkpoints to reach the user’s location. Each road between checkpoints will have a cost, which we learned how to calculate in the previous lesson. It is possible that some of the k chosen drivers might not have a path to the user due to unavailability. Unavailability can occur due to a driver already being in a ride that has ended but not reached its location. In some cases, the driver can also get booked by another user and become unavailable. The driver that has the path to the user’s location with the minimum accumulated cost will be selected.

We’ll be given a city map G_map as a list of different checkpoints. Another list path_costs, at each index, will represent the cost of traveling between the corresponding checkpoints in G_map. We are also given some drivers, where each drivers[i] represents a single driver node. We need to determine whether a path from the driver node drivers[i] to a user node exists or not. If the path exists, return the accumulated sum of the checkpoints between the two nodes. Otherwise, return -1.

![cale](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/cale/cale53.png)

In the above example,

G_map has the values [["a","b"],["b","c"],["a","e"],["d","e"]].

path_costs has the values [12,23,26,18].

drivers has the values ["c", "d", "e", "f"].

user has a value "a".

After calculating the total cost of each driver’s route to the user, we’ll select that driver that has a path to the user with the lowest cost. Here, the driver f has no path to the user due to unavailability.

## Solution
The main problem comes down to finding a path between two nodes, if it exists. If the path exists, return the cumulative sums along the path as the result. Given the problem, it seems that we need to track the nodes where we come from. DFS (Depth-First Search), also known as the backtracking algorithm, will be applicable in this case.

Here is how the implementation will take place:
1. Build the graph using the city map list G_map.
2. Assign the cost to each edge while building the graph.
3. Once the graph is built, evaluate each driver’s path in the drivers list by searching for a path between the driver node and the user node.
4. Return the accumulated sum if the path exists. Otherwise, return -1.

Let’s look at the code for the solution:

{% highlight java %}
import java.util.*;
class Solution {
  
  public static double[] getTotalCost(List<List<String>> GMap, double[] pathCosts, List<String> drivers, String user) {
    HashMap<String, HashMap<String, Double>> city = new HashMap<>();

    // Step 1). build the city from the GMap
    for (int i = 0; i < GMap.size(); i++) {
      List<String> checkPoints = GMap.get(i);
      String sourceNode = checkPoints.get(0), destNode = checkPoints.get(1);
      double pathCost = pathCosts[i];

      if (!city.containsKey(sourceNode))
          city.put(sourceNode, new HashMap<String, Double>());
      if (!city.containsKey(destNode))
          city.put(destNode, new HashMap<String, Double>());

      city.get(sourceNode).put(destNode, pathCost);
      city.get(destNode).put(sourceNode, pathCost);
    }

    // Step 2). Evaluate each driver via bactracking (DFS)
    // by verifying if there exists a path from driver to user
    double[] results = new double[drivers.size()];
    for (int i = 0; i < drivers.size(); i++) {
      String driver = drivers.get(i);

      if (!city.containsKey(driver) || !city.containsKey(user))
          results[i] = -1.0;
      else {
          HashSet<String> visited = new HashSet<>();
          results[i] = backtrackEvaluate(city, driver, user, 0, visited);
      }
    }

    return results;
  }

  private static double backtrackEvaluate(HashMap<String, HashMap<String, Double>> city, String currNode, String targetNode, double accSum, Set<String> visited) {

      // mark the visit
      visited.add(currNode);
      double ret = -1.0;

      Map<String, Double> neighbors = city.get(currNode);
      if (neighbors.containsKey(targetNode))
          ret = accSum + neighbors.get(targetNode);
      else {
          for (Map.Entry<String, Double> pair : neighbors.entrySet()) {
              String nextNode = pair.getKey();
              if (visited.contains(nextNode))
                  continue;
              ret = backtrackEvaluate(city, nextNode, targetNode,
                      accSum + pair.getValue(), visited);
              if (ret != -1.0)
                  break;
          }
      }

      // unmark the visit, for the next backtracking
      visited.remove(currNode);
      return ret;
  }

  public static void main(String[] args) {

    // Driver code
    List<List<String>> GMap = Arrays.asList(Arrays.asList("a","b"), Arrays.asList("b","c"), Arrays.asList("a","e"), Arrays.asList("d","e"));
    double[] pathCosts = {12.0,23.0,26.0,18.0};
    List<String> drivers = Arrays.asList("c", "d", "e", "f");
    String user = "a";
    double[] allPathCosts = getTotalCost(GMap, pathCosts, drivers, user);

    System.out.print("Total cost of all paths " + Arrays.toString(allPathCosts));
  }
}
{% endhighlight %}

![cale](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/cale/cale54.png)
![cale](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/cale/cale55.png)

## Feature #4: Fare in Words

## Description
At the end of a ride, the Uber app displays the fare to the customer. For accessibility, we want the fare to be read out, should the customer so choose. Assuming that the ride fare is an integer and that a text to speech engine is available, all we need to do is to convert the fare to English words. For example, we need to change $120 to one hundred and twenty dollars. The fare may be as high as several billion depending on the country the ride is taken in.

We’ll be provided with an integer number, fare, which represents the fare. Our task will be to convert fare to its English word representation.

## Solution
We can solve this problem by dividing the initial number into a specific set of digits and then solving those sets. Initially, we can split the number into sets of three. For example, if we split the amount 1234567890 into sets of three digits, we’ll get 1 234 567 890. Now, the values are separated into billion, million, and thousand parts in the number. At this stage, our English representation will become 1 Billion 234 Million 567 Thousand 890.

The three digits from each set can be further divided into individual sets to obtain the values at the hundreds, tens, and ones places. For example, 567 can be split into 5 6 7. After splitting, 5 6 7 will be converted to the English word representation five Hundred sixty seven. We need to consider the values from 10 to 19 separately for conversion if they are present at the ones and tens places.

Let’s look at the code for the solution:

{% highlight java %}
class Solution {

    public static String ones(int fare) {
        switch(fare) {
            case 1: return "One";
            case 2: return "Two";
            case 3: return "Three";
            case 4: return "Four";
            case 5: return "Five";
            case 6: return "Six";
            case 7: return "Seven";
            case 8: return "Eight";
            case 9: return "Nine";
        }
        return "";
    }

    public static String teens(int fare) {
        switch(fare) {
            case 10: return "Ten";
            case 11: return "Eleven";
            case 12: return "Twelve";
            case 13: return "Thirteen";
            case 14: return "Fourteen";
            case 15: return "Fifteen";
            case 16: return "Sixteen";
            case 17: return "Seventeen";
            case 18: return "Eighteen";
            case 19: return "Nineteen";
        }
        return "";
    }

    public static String tens(int fare) {
        switch(fare) {
            case 2: return "Twenty";
            case 3: return "Thirty";
            case 4: return "Forty";
            case 5: return "Fifty";
            case 6: return "Sixty";
            case 7: return "Seventy";
            case 8: return "Eighty";
            case 9: return "Ninety";
        }
        return "";
    }

    public static String two(int fare) {
        if (fare == 0)
            return "";
        else if (fare < 10)
            return ones(fare);
        else if (fare < 20)
            return teens(fare);
        else {
            int tenner = fare / 10;
            int rest = fare - tenner * 10;
            if (rest != 0)
                return tens(tenner) + " " + ones(rest);
            else
                return tens(tenner);
        }
    }

    public static String three(int fare) {
        int hundred = fare / 100;
        int rest = fare - hundred * 100;
        String res = "";

        if (hundred*rest != 0)
            res = ones(hundred) + " Hundred " + two(rest);
        else if ((hundred == 0) && (rest != 0))
            res = two(rest);
        else if ((hundred != 0) && (rest == 0))
            res = ones(hundred) + " Hundred";
        
        return res;
    }

    public static String FareinWords(int fare) {
        if (fare == 0)
            return "Zero";

        int billion = fare / 1000000000;
        int million = (fare - billion * 1000000000) / 1000000;
        int thousand = (fare - billion * 1000000000 - million * 1000000) / 1000;
        int rest = fare - billion * 1000000000 - million * 1000000 - thousand * 1000;

        String result = "";
        
        if (billion != 0)
            result = three(billion) + " Billion";
        if (million != 0) {
            if (! result.isEmpty())
                result += " ";
            result += three(million) + " Million";
        }
        if (thousand != 0) {
            if (! result.isEmpty())
                result += " ";
            result += three(thousand) + " Thousand";
        }
        if (rest != 0) {
            if (! result.isEmpty())
                result += " ";
            result += three(rest);
        }
        
        return result;
    }


    public static void main( String args[] ) {
        // Driver code

        int fare = 5648;
        System.out.println( "The fare is: " +  FareinWords(fare) + " dollars");
    }
}
{% endhighlight %}

![cale](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/cale/cale56.png)

## Feature #5: Uber Pool

## Description
Uber pool allows a passenger to share the car with other passengers on their journey. In return, each passenger pays less than what they would pay for their own car. However, passengers in a pooled ride are not predetermined. As a pool customer is taking a ride, more pool ride requests may arrive. The driver will have the option to pick up those new passengers to pool the ride. It is quite possible that a customer gets the entire ride to themselves because no one else along their ride’s route requested an Uber pool.

Let’s say a driver has picked up a pool customer and is at a checkpoint. There are multiple routes to the passenger’s destination, and the likelihood of finding another pool customer on each route may be different. Based on these likelihoods, we have assigned metrics to each route to the destination. We don’t want to always suggest the route with the highest probability because it might not necessarily be the best option. Instead, we want to suggest a route randomly picked from the available routes to the destination in proportion to the metric assigned to the route. That way, high probability routes are more likely to be selected, but other routes will also be selected.

We’ll be provided with an array where the index represents a route that the driver can take for finding another pool customer. The values in the array represent the likelihood metrics assigned to each route. We want the route with a higher likelihood to get higher weightage during selection.

Let’s understand this better with an illustration:

![cale](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/cale/cale57.png)
![cale](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/cale/cale58.png)
![cale](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/cale/cale59.png)

On a number line, make marks at arr[0], arr[0] + arr[1], arr[0] + arr[1] + arr[2], ...., arr[0] + arr[1] + … arr[n-1]. This results in n line segments each corresponding to one of the entries in the array. Let the last mark be at a value k. Now, if we draw a random value between 0 and k, it will lie on one of these line segments. If the random value lies on the ith line segment, we’ll say that the ith array value has been picked. The likelihood of a random value between 0 and k falling on a specific line segment depends on the length of the line segment, which equals the value of the corresponding array element. This means that we have picked an array element using probability determined by its value.

Each point on this prob line is a running sum of all the previous numbers in the metric array plus the current number itself. Our running sum array is sorted as it is increasing, so we only need to fit the random value in this sorted array. Wherever our random number gets fitted, we can return the index that represents our chosen route.

Here is how the implementation will take place:
1. Generate an array of running sums from the given array of metrics in the constructor so that we don’t have to compute it again at every call.
2. The largest number of the running sums array will give us the range for generating the random number.
3. Create a pick_route() method that will find and return the index value.
4. Generate a random number between 0 and k.
5. Use binary search to find the index of the first running sum that is greater than the random value.
6. Return the index so we can choose the route associated with it.

Let’s look at the code for the solution:

{% highlight java %}
class Uber {
    private int[] cumSums;

    public Uber(int[] metrics) {
        this.cumSums = new int[metrics.length];

        int cumSum = 0;
        for (int i = 0; i < metrics.length; i++) {
            cumSum += metrics[i];
            this.cumSums[i] = cumSum;
        }
    }

    public int pickRoute() {
        double target = this.cumSums[this.cumSums.length - 1] * Math.random();

        // Binary search to find the target
        int low = 0, high = this.cumSums.length;
        while (low < high) {
            int mid = low + (high - low) / 2;
            if (target > this.cumSums[mid])
                low = mid + 1;
            else
                high = mid;
        }
        return low;
    }
    public static void main( String args[] ) {
        // Driver code

        int[] metrics = {1, 2, 3};
        Uber uber = new Uber(metrics);
        
        for (int i = 0; i < 10; i++)
            System.out.println("Randomly choose route " + uber.pickRoute());
    }
}
{% endhighlight %}

![cale](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/cale/cale60.png)

## Feature #6: Longest Route

## Description
A city cannot be represented by a single straight road because there are numerous intersections and crossings running throughout it. In our city, there are forks in the road, making binary-tree representation possible. The furthest checkpoints of the city are leaf nodes in this binary tree; these represent the Uber service area’s limits. We want the new drivers to have a fantastic first day to kick start their career at Uber. Therefore, we want to recommend these drivers a route that would maximize the possibility of finding customers. This route should be the longest possible route so that they are bound to find a customer eventually.

We’ll be provided with the root of a binary tree structure representing our city with each node as a checkpoint. We have to find the longest path/route so that drivers are likely to find more customers.

![cale](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/cale/cale61.png)

## Solution
As seen in the above example, the longest path is one in which there is a maximum number of edges between two nodes or checkpoints. The edges here represent the roads. As the city structure represents a binary tree, the longest path in the tree will either pass through the root node or not. Let’s explore both of these conditions.

The longest path that passes through the root of the tree:

We can use the height of the tree when the root node is included in the longest path. The height of a tree is the longest path from the root node to any leaf node in the tree. So, the height of a tree can be considered the longest path starting from the root. We can calculate the longest path of the complete tree as:

height(root -> left) + height(root -> right) + 1(root node itself)

The path passes through the root (the +1 at the end of the above expression). It includes the deepest node in the left subtree (accounted by the first term) and the deepest node in the right subtree (the second term).

Let’s look at an example of this case in the illustration below.

![cale](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/cale/cale62.png)

The longest path that does not pass through the root of the tree:

In this case, the longest path can exist in either the left subtree or the right subtree. Since the root will not be a part of our path, we can consider the two subtrees to be new individual trees. The longest path for each of these trees needs to be calculated separately, and the longest one will be chosen.

max(l_path(root -> left), r_path(root -> right)), where l_path(x) represents the length of the longest path in a tree rooted at x.

![cale](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/cale/cale63.png)

We can’t know for sure which of the two cases we’ll encounter, so we’ll calculate both of the above metrics and choose the one with the maximum value as the longest path.

max( l_height+r_height+1, max(l_path, r_path) )

We can follow a simple recursive approach to calculate the above metrics for each node. For the second case, the longest path between two newly obtained trees can again either pass through the root or not. The tree will keep getting divided until we get a path that includes the root. We can then return from that point. We’ll first compute the height metric and then the path metric.

Let’s look at the code for the solution:

{% highlight java %}
import java.util.*;

class TreeNode {
  String val;
  TreeNode left;
  TreeNode right;

  TreeNode(String x) {
    val = x;
  }
};

class Solution {
  public static int longestRoute(TreeNode root) {
    if (root == null) 
      return 0;
    
    int lHeight = height(root.left);
    int rHeight = height(root.right);

    int lPath = longestRoute(root.left);
    int rPath = longestRoute(root.right);

    int res = Math.max(lHeight + rHeight + 1, Math.max(lPath, rPath));

    return res;
  }
  
  public static int height(TreeNode node) {
    if (node == null) 
      return 0;
    else{
      // Compute the height of each subtree
      int lh = height(node.left);
      int rh = height(node.right);

      // Use the larger one 
      return Math.max(lh, rh) + 1;
    }
  }

  public static void main(String args[]) {
    // Driver code

    TreeNode root = new TreeNode("a");
    root.left = new TreeNode("b");
    root.right = new TreeNode("c");
    root.left.left = new TreeNode("d");
    root.right.left = new TreeNode("e");
    root.right.right = new TreeNode("f");
    System.out.println("The longest route will pass through " + longestRoute(root) + " checkpints");
  }
}
{% endhighlight %}

![cale](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/cale/cale64.png)

## Feature #7: Highest Rank

## Description
At Uber, each driver is assigned a rank based on the reviews they receive from their passengers. Currently, the system prioritizes drivers with the highest rank and assigns them instant rides. We want to change this driver selection criterion such that drivers with lower ranks don’t get starved while the drivers with high ranks keep getting rides. The drivers’ ranks are maintained in an unsorted array. We’ll call a hidden API that will provide us with a number k. The value of this k can range from 1 to the size of our rank array. Once we have a value k, we need to find the kth highest driver rank.

We’ll be provided with an unsorted array of integers representing the divers’ ranks. The drivers are represented by the index of this array. The value of k will be made available from the hidden API. Our task will be to determine the kth highest rank, so the driver associated with that rank can be selected.

![cale](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/cale/cale65.png)

## Solution
Just like in Feature #1, we can use a heap to obtain the kth highest rank from our unsorted array. We now have to select the largest number, so we’ll use a min-heap. We’ll insert ranks of the first k drivers into the min-heap.

As we know, the root is the smallest element in a min-heap. So, since we want to keep track of the kth highest element, we can compare every number with the root while iterating through all the numbers in the array. If any number is greater than the root element, we’ll take the root out and insert the greater number. This will ensure that we always have the k highest ranks in the Heap. In the end, we can simply return the root element as the kth highest rank.

Below is an illustration of this process:

![cale](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/cale/cale66.png)
![cale](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/cale/cale67.png)
![cale](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/cale/cale68.png)
![cale](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/cale/cale69.png)
![cale](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/cale/cale70.png)
![cale](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/cale/cale71.png)
![cale](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/cale/cale72.png)
![cale](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/cale/cale73.png)

Let’s look at the code for the solution:

{% highlight java %}
import java.util.*;
class Solution {
  public static int kthHighestRank(int[] ranks, int k) {
    
    PriorityQueue<Integer> minHeap = new PriorityQueue<Integer>((n1, n2) -> n1 - n2);
    // Put first k ranks in the min heap
    for (int i = 0; i < k; i++)
      minHeap.add(ranks[i]);

    // Go through the remaining ranks of the array, if the rank from the array is greater than the
    // top (smallest) rank of the heap, remove the top rank from heap and add the rank from array
    for (int i = k; i < ranks.length; i++) {
      if (ranks[i] > minHeap.peek()) {
        minHeap.poll();
        minHeap.add(ranks[i]);
      }
    }

    // The root of the heap has the Kth largest rank
    return minHeap.peek();
  }

  public static void main(String[] args) {
    // Driver code

    int[] driverID = {1, 5, 12, 2, 11, 9, 7, 30, 20};
    int k = 3; // Supplied by a hidden API

    System.out.println("Driver with the rank " + kthHighestRank(driverID, k) + " is selected!"); 
  }
}

{% endhighlight %}

![cale](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/cale/cale74.png)
