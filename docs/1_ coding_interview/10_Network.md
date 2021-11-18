---
layout: default
title: Network
parent: Coding Interview
has_children: true
nav_order: 10
permalink: /coding_interview/network
---
<div align="center" markdown="1">
Network / Java resources / Tutorial

{: .fs-8 .fw-400 }
</div>

## Network

## Project Description for Network

## Introduction
A Network is an interconnection of computers, routers, or switches spanning a geographic area. The devices in a network communicate with each other through different protocols. Corporations typically use LAN to set up private networks for their employees. It can be used to simultaneously send data and messages to all devices available in the network. Most often, a network is connected to the global Internet so that devices on the same network can access resources on the Internet, too.

The scenario and the problems we will discuss in this chapter relate to data propagation in a network and how we can improve it.

## Statement
You work for a company that develops devices for LANs, high-performance compute clusters and overlay networks. Your team develops software for features in these devices, efficient communication protocols as well as analytics on network data. These devices enable efficient scientific as well as enterprise networks.

## Features

We will need to introduce the following features to implement the functionalities we discussed above:
* Feature #1: A message is transmitted from the server to the clients. Given the delays for each hop in the network, we want to determine the earliest time at which the message will be received by all the clients, assuming there are no errors along the way.
* Feature #2: Given that a specific Time-to-live (TTL) has been set in a message, find all the nodes on the network where the packet can travel from the current device.
* Feature #3: Each router in a linear virtual network topology can send a packet a certain maximum hops forward. We need to determine the minimum number of transmissions required to get a packet from the first router to the last.
* Feature #4: Disseminate an important packet to the maximum number of routers in a grid topology, subject to certain forwarding constraints.
* Feature #5: Efficiently update the VLAN IDs of network switches in a grid topology.
* Feature #6: A pair of machines have a request-response message exchange. Identify if the request and response packets used the same path.
* Feature #7: Distribute files over a network to high-performance cluster nodes to minimize communication overhead.
* Feature #8: Identify the most out of sync routers in a network topology.
* Feature #9: Determine the time for an update request to propagate through all routers in a grid topology.
* Feature #10: Determine the longest stretch of days for which a customer’s traffic variation was within a specified threshold.

Understanding these feature requests and designing their solutions will help us implement the requested functionality into the network.

In the next few lessons, we’ll discuss the recommended implementations of these features. Before we start, think about how you would implement these features. As you do, you’ll realize some of the underlying problems that you’ll need to solve. The solutions to these basic problems are also applicable to other common coding interview questions.

## Feature #1: Total Time

## Description
An Ethernet LAN topology is built with redundant connections between switches. However, an Ethernet can only work in a loop-free topology. Therefore, Ethernet switches run the Spanning Tree Protocol (STP), which computes a minimum spanning tree for the underlying topology. STP disables some of the network links to obtain a loop-free spanning tree. Messages on the LAN are forwarded only on network links that are part of the spanning tree.

The server is at the root of the spanning tree, and the clients are at the leaves of the spanning tree. All the other nodes in the spanning tree are Ethernet switches that forward messages from the server to the clients. The nodes are labeled with weights representing the time(in seconds) it takes a message to go from the device on one end of the link to reach the device on the other. The delays will always be positive. For simplicity, we will assume that the link weights are integers. In addition, the main server on the root node will also experience a transmission delay when it broadcasts the message. Considering the time required for a message to pass through a single device, we have to find the total time required by a message to reach all devices on a network.

Let’s try to understand this better with an illustration:

![net](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/net/net1.png)

We’ll be provided with two arrays: parents and delays. Each index of the parents array will be the device_id, and the value for that index will be the id for the device from which it receives the message. The delays array will contain the delays for each device corresponding to their id’s in the parents array.

For the example above, the two arrays will be:

parents : {-1,0,0,1,1,2,2,3,3,4,4,5,5,6,6}

delays : {1,1,1,1,1,1,1,0,0,0,0,0,0,0,0}

In the above slides, since nodes 7 through 14 are the destination nodes, or the clients, there is 0 transmission delay associated with them. For other nodes, indices 0 through 7 contain the value 1 because the example shows a delay of 1. In general, the delays for non-leaf nodes can be unequal. Additionally, the main server’s id will be provided separately. In the parents array, this will be represented by -1.

## Solution
We need to visit the children of each node of our tree structure to compute the total time from the root node to each leaf node. Eventually, we want to find the maximum value over all the root-to-leaf paths. We’ll keep summing the maximum of each level as we move down the tree. We can use the BFS algorithm here to traverse the tree after converting it into an adjacency list.

Let’s see how we might implement this functionality:
1. Build the adjacency list, where each server node points to its children in the spanning tree.
2. Create a tuple containing the main-server id and its delay time as (ID, Time), and insert it into a queue.
3. Traverse over the nodes while summing the maximum value at each level. Keep inserting each node and the sum until the node we just inserted into the queue.
4. Return the computed sum.

The following illustration might clarify this process.

![net](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/net/net2.png)
![net](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/net/net3.png)
![net](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/net/net4.png)
![net](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/net/net5.png)
![net](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/net/net6.png)
![net](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/net/net7.png)
![net](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/net/net8.png)
![net](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/net/net9.png)
![net](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/net/net10.png)

Let’s look at the code for the solution:

{% highlight java %}
class Solution {
    public static int totalTime(int mainServerId, int[] parents, int[] delays) {
        int n = parents.length;
        if (n <= 1)
            return 0;
        
        int res = 0;
        HashMap<Integer, List<Integer>> children = new HashMap<>();

        List<Integer> numbers = new ArrayList<>();
        for (int i = 0; i < parents.length; i++)
        {
            numbers.add(parents[i]);
        }

        ListIterator<Integer> it = numbers.listIterator();
        while (it.hasNext()) {
            int val = it.next();
            int index = it.nextIndex() - 1;
            List<Integer> temp_list = children.getOrDefault(val, new ArrayList<>());
            temp_list.add(index);
            children.put(val, temp_list);
        }

        Queue<Pair<Integer, Integer>> queue = new LinkedList<>();
        queue.add(new Pair(mainServerId, delays[mainServerId]));

        while (!queue.isEmpty()) {
            Pair<Integer, Integer> node = queue.remove();
            int curId = node.getKey();
            int curTime = node.getValue();
            // calculate max
            res = Math.max(res, curTime);

            for (int child : children.getOrDefault(curId, new ArrayList<>())) {

                queue.add(new Pair(child, curTime + delays[child]));
            }
        }
        
        return res;
    }


    public static void main( String args[] ) {
        // Driver code

        int mainServerId = 0;
        int[] parents = new int[] {-1,0,0,1,1,2,2,3,3,4,4,5,5,6,6};
        int[] delays = new int[] {1,1,1,1,1,1,1,0,0,0,0,0,0,0,0};

        System.out.println("Time required by message to reach all devices is " + totalTime(mainServerId, parents, delays) + " units!");
    }
}
{% endhighlight %}

![net](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/net/net11.png)

## Feature #2: TTL Expiry

## Description
To limit the number of messages flooding onto the network, we will set a TTL(Time-to-live) on each message. The number of hops a message will propagate away from the server will not exceed the value of the message’s TTL. In this problem, the server can be at any node in the tree. We want to determine which nodes will successfully receive a message from the server, given a specific TTL value. The network structure is represented by n-ary trees.

We’ll be provided with an n-ary tree network structure, the server device from where the message needs to propagate, and the TTL value for the message. We need to return the nodes after which the TTL value of the message will expire.

Let’s try to understand this better with an illustration:

![net](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/net/net12.png)

We are using small TTL values for demonstration purposes. Actual TTL values are usually high.

## Solution
We can solve this problem using a combination of DFS and BFS algorithms. First, we’ll do a DFS on the tree and store every node’s parent and children in an adjacency list. Then, we can perform BFS on the adjacency list to find the required nodes.

Let’s see how we might implement this functionality:
1. Initialize the adjacency list.
2. Perform DFS on the root node and add every node’s parents and children to the adjacency list.
3. Mark the server node as the result and iterate ttl times over the adjacency list starting from the server node.
4. During iteration, we will get all the parents and children nodes of the current node and mark them as the result.
5. When the loop ends, you’ll have the nodes that are ttl distance from the server as the result.

Let’s look at the code for the solution:

{% highlight java %}
import java.util.*;

class TreeNode {
  int val;
  List<TreeNode> children;

  TreeNode(int x) {
    val = x;
    children = new ArrayList<>();
  }
};

class Solution {
    public static List<Integer> getDevices(TreeNode root, TreeNode server, int ttl) {
      
      HashMap<Integer, List<Integer>> neighbors = new HashMap<>(); // Adjacency list
      dfs(null, root, neighbors);

      // BFS to find nodes
      List<Integer> bfs = new ArrayList<>();
      bfs.add(server.val);
      Set<Integer> lookup = new HashSet<Integer>(bfs);

      for (int i = 0; i < ttl; i++) {
        List<Integer> temp = new ArrayList<>();
        for (int node : bfs)
          for (int nei : neighbors.get(node))
            if (lookup.contains(nei) == false)
              temp.add(nei);
        
        bfs = temp;
        lookup.addAll(bfs);
      }
      
      return bfs;
    }

    private static void dfs(TreeNode parent, TreeNode child, HashMap<Integer, List<Integer>> neighbors) {
      // DFS to build adjacency list
      if (child == null){
        return;
      }

      if (parent != null) {

        if (!neighbors.containsKey(parent.val))
          neighbors.put(parent.val, new ArrayList<>());
        if (!neighbors.containsKey(child.val))
          neighbors.put(child.val, new ArrayList<>());

        neighbors.get(parent.val).add(child.val);
        neighbors.get(child.val).add(parent.val);
      }

      for (int i = 0; i < (child.children).size(); i++)
        dfs(child, child.children.get(i), neighbors);
    }

    public static void main(String[] args) {
      // Driver Code

      TreeNode root = new TreeNode(1);
      root.children.add(new TreeNode(2));
      root.children.add(new TreeNode(3));
      root.children.add(new TreeNode(4));
      root.children.get(0).children.add(new TreeNode(5));
      root.children.get(0).children.get(0).children.add(new TreeNode(10));
      root.children.get(0).children.add(new TreeNode(6));
      root.children.get(0).children.get(1).children.add(new TreeNode(11));
      root.children.get(0).children.get(1).children.add(new TreeNode(12));
      root.children.get(0).children.get(1).children.add(new TreeNode(13));
      root.children.get(2).children.add(new TreeNode(7));
      root.children.get(2).children.add(new TreeNode(8));
      root.children.get(2).children.add(new TreeNode(9));

      TreeNode server = root.children.get(0).children.get(1);
      int ttl = 2;
      System.out.println("The TTL value will expire on node IDs: " + getDevices(root, server, ttl));

    }
}
{% endhighlight %}

![net](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/net/net13.png)

## Feature #3: Minimum Hops

## Description
We have created a linear network topology by placing routers in a straight chain. Each router has a specific TTL (Time To Live) value associated with it. Hence, a router is able to send a packet to a downstream neighbor at most h[i] hops away (you may think of this as one to the right). Here, h[i] denotes the TTL value of the ith router. A packet has arrived at the first router, h[0], and it needs to be sent to the last router in the chain. You want to get the packet to the destination in the fewest possible transmissions, which means using the fewest possible intermediate routers.

We’ll be provided with an array containing the TTL values of each router. The router’s position in the chain will be denoted by array indexes. For example, the TTL of the first router in the chain is at index 0 of the input array, the second router is at index 1, and so on. We have to compute the minimum number of hops to transmit the packet from the initial to the final router.

Let’s try to understand this better with an illustration:

![net](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/net/net14.png)

We are using small TTL values for demonstration purposes. Actual TTL values are usually high.

## Solution
At each index of our array, we can choose to cover the longest possible distance, which is the maximum reachable position/index in our array from the current index. At an index i, the longest possible distance we can cover is i + value[i].

Start from the initial index i and hop to the furthest position i + value[i]. Keep track of this position using a currReach variable. Next, we’ll iterate the array until currReach, after which we’ll need to hop again. We won’t just hop from our current index because there can be indexes before our current position that can provide a bigger hop. Therefore, as we iterate until currReach, we’ll store the maximum reachable index (if exists) as maxReach from the positions that are less than currReach. The maxReach from a given index is the furthest that a packet can be sent by a router at or before its current position. Finally, we’ll make the hop to the stored maximum position and repeat until we reach the end of the array.

![net](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/net/net15.png)
![net](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/net/net16.png)
![net](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/net/net17.png)
![net](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/net/net18.png)

Let’s see how we might implement this functionality:
1. Initialize the maximum position that one could reach and the maximum position reachable during the first hop as maxReach = nums[0] and currRreach = nums[0] respectively.
2. If the size of our array is greater than 1, then initialize the hops variable to 1.
3. Start iterating over the array.
4. In each iteration, update the maxReach so it contains the maximum position one could reach from the current index i as max of maxReach and i + value[i].
5. During iteration, if currReach < i, it means that we are ready for another hop. Increment hop by 1 and assign currReach to the current maximum position, which is maxReach.
6. Return the number of hops when the loop exits.

The following illustration might clarify this process.

![net](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/net/net19.png)
![net](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/net/net20.png)
![net](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/net/net21.png)
![net](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/net/net22.png)
![net](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/net/net23.png)
![net](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/net/net24.png)
![net](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/net/net25.png)
![net](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/net/net26.png)

Let’s look at the code for the solution:

{% highlight java %}
class Solution {
    public static int minimumHops(int[] values) {
        
        if (values.length < 2) 
            return 0;


        int maxReach = values[0];
        int currReach = values[0];
        
        int hops = 1;
        for (int i = 1; i < values.length; ++i) {
            // Another jump needed if reach this clause
            if (currReach < i) {
                ++hops;
                currReach = maxReach;
            }
            maxReach = Math.max(maxReach, values[i] + i);
        }
        return hops;
    }

    public static void main( String args[] ) {
        // Driver code

        int[] switch_array = {4,1,1,3,1,1,1};
        System.out.println("Minimum hops to final router are: " + minimumHops(switch_array));
    }
}
{% endhighlight %}

![net](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/net/net27.png)

## Feature #4: Maximum Routers

## Description
We have several routers interconnected in a rectangular grid. Each router has an ID, and all router IDs are stored in a 2D array. Any router may forward a packet to any of its neighbors above it, below it, to its right or left, in the array, if the neighbor’s ID is higher than its own. We have an important packet that can be injected into any single router in the network. The goal is to have the packet forwarded to as many routers in the network as possible. No router should receive the packet more than once.

We’ll be provided with an m x n matrix containing the IDs for each router. Our task will be to forward the packet to the maximum number of routers.

Let’s try to understand this better with an illustration:

![net](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/net/net28.png)

If the packet is inserted into the router with ID 1, then it is transmitted through the maximum number of routers according to the above-defined criteria. In our case, this is 4.

## Solution
From the above example, we can see that, from every cell, we can move in at most four directions: up, down, left, and right. We will choose to move in the direction whose cell’s value is greater than the current one. We can use Depth First Search (DFS) algorithm on each cell of the matrix to calculate the maximum number of routers that can be reached from the current cell. We will keep updating the maximum reachable distance for each cell and return this value when the complete matrix has been traversed.

While effective, this approach is not very efficient as its time complexity can reach up to 2^{m+n}. This is because we keep performing duplicate calculations as the value for the same cell can get computed again in a different DFS call. To optimize this DFS, we can cache the results for each cell when its value gets computed. This way, if we encounter the same cell again, instead of calling an expensive DFS function on it, we can simply return its value from the cache. This technique is also known as Memoization.

Let’s see how we might implement this functionality:
1. Initialize a res variable and assign it a value 0.
2. Recursively call DFS on each cell of the matrix, and update res if the result of the DFS call is greater than the current res value.
3. During a DFS call, keep visiting each of the four paths from the current cell if the value in the next cell is greater than the value in the current cell.
4. If the result for a visited cell is not calculated, we compute it and cache (or memoize) it.
5. Otherwise, we get it from the cache directly.
6. Finally, return the res variable.

The following illustration might clarify this process.

![net](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/net/net29.png)
![net](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/net/net30.png)
![net](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/net/net31.png)
![net](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/net/net32.png)
![net](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/net/net33.png)
![net](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/net/net34.png)
![net](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/net/net35.png)
![net](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/net/net36.png)
![net](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/net/net37.png)
![net](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/net/net38.png)
![net](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/net/net39.png)
![net](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/net/net40.png)
![net](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/net/net41.png)

Let’s look at the code for the solution:

{% highlight java %}
class Solution {

     public static int maximumRouters(int[][] grid) {
        if(grid.length==0)
            return 0;

        int res = 0;
        int[][] cache = new int[grid.length][grid[0].length];

        for(int i = 0; i < grid.length; i++){
            for(int j = 0; j < grid[0].length; j++){

                if (cache[i][j] == 0){
                    int prev_val = grid[i][j];
                    dfs(grid,i,j,prev_val, cache);
                    res = Math.max(cache[i][j], res);
                }
            }
        }
        return res;
    }
    
    public static int dfs(int[][] grid, int i, int j, int prev_val, int[][] cache){
        
        if(i < 0 || j < 0 || i > grid.length-1 || j > grid[0].length-1)
            return 0;

        else if(prev_val > grid[i][j])
            return 0;

        else if(cache[i][j] != 0)
            return cache[i][j];
        
        // Up
        int path_up =  dfs(grid,i-1,j,grid[i][j], cache); 
        // Down
        int path_down =  dfs(grid,i+1,j,grid[i][j], cache); 
        // Left
        int path_left =  dfs(grid,i,j-1,grid[i][j], cache); 
        // Right
        int path_right =  dfs(grid,i,j+1,grid[i][j], cache); 
         

        int max1 = Math.max(path_up,path_down);
        int max2 = Math.max(path_left,path_right);
        
        cache[i][j] = 1 + Math.max(max1,max2);
          
        
        return cache[i][j]; 
    }

    public static void main( String args[] ) {
        // Driver code
        int[][] grid = {
            {2,9,6},
            {8,4,7},
            {5,3,1}
        };
        System.out.println("Maximum Routers are " + maximumRouters(grid));
    }
}

{% endhighlight %}

![net](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/net/net42.png)

## Feature #5: Update VLAN ID

## Description
We have a network topology in which several network switches are interconnected in a rectangular grid fashion. The switches are configured with VLAN IDs that are stored in a 2D array. Periodically, VLAN IDs need to be changed. At a specific switch, we will initiate a VLAN ID change request. This request will be propagated to its neighbors with the same VLAN ID, which will then forward it to their neighbors, and so on, until all switches in the topology are covered. The security is configured so that a switch will accept a VLAN ID change request only if the request is sent from a switch with the same VLAN ID and is above, below, to its right or left, or in the array. A VLAN ID change request is started at a switch in row r and column c, with a new VLAN ID specified. All the switches’ VLAN IDs need to be updated under the given constraints.

We’ll be provided with a 2D matrix of integers representing the VLAN IDs of switches at each index. We’ll also have the index of the starting switch and the new VLAN ID. Our task is to determine the VLAN IDs for all of the switches after the change messages have finished propagating.

Let’s try to understand this better with an illustration:

![net](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/net/net43.png)
![net](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/net/net44.png)

## Solution
Just like the previous feature, we can move in at most four directions from each cell, i.e., up, down, left, and right. To move to another cell, the neighboring cell must have a VLAN ID equal to the current cell’s ID. In this case, we’ll simply call DFS on the provided cell, and it will recursively assign the new ID to its neighbors. We also need to make sure that we don’t process a cell whose ID has already been changed.

Let’s look at the code for the solution:

{% highlight java %}
import java.util.*;

class Solution {
    public static int[][] updateVLAN(int[][] matrix, int r, int c, int newID) {
        
        int currID = matrix[r][c];
        if (currID == newID) 
            return matrix;
        
        dfs(matrix, r, c, currID, newID);
        return matrix;
    }
    public static void dfs(int[][] matrix, int r, int c, int currID, int newID) {
        // Check bounds of the matrix
        if (r < 0 || c < 0 || r >= matrix.length || c >= matrix[0].length || 
            matrix[r][c] != currID) // check if ID has already been changed
        {
            return;
        }
        // Assign new ID
        matrix[r][c] = newID;
        
        // Up 
        dfs(matrix, r-1, c, currID, newID);
        // Down
        dfs(matrix, r+1, c, currID, newID);
        // Left
        dfs(matrix, r, c-1, currID, newID);
        // Right
        dfs(matrix, r, c+1, currID, newID);
    }
    public static void main( String args[] ) {
        // Drive code

        int[][] matrix = {
            {1,1,1,1,1},
            {1,1,1,1,0},
            {1,1,1,0,0},
            {1,1,0,1,0},
            {1,1,0,0,1}
        };
        int r = 1, c = 1, newID = 2;

        System.out.println("Swtches with Updated VLAN IDs:\n " + Arrays.deepToString(updateVLAN(matrix, r, c, newID)));
    }
}
{% endhighlight %}

![net](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/net/net45.png)

## Feature #6: Transmission Error

## Description
In our network protocol, response packets take the same route (in reverse) back to the source as the request packet did to the destination. Sometimes the path may differ due to errors, and we can tolerate at most one diversion router. The path, in terms of IDs of routers along the way, is recorded in an array present inside the packet. We need to identify the paths with more than one diversion router, so our topology remains intact and transmission error occurs.

We’ll be provided with an array of integers representing the router IDs. The routers at the start and end of the path will always be the same. The first half of the array will show the request packet’s path from source to destination, while the second half will show the response packet’s path from the destination back to the source. We need to determine whether the same path is followed from source to destination and from destination to source, except for possibly one additional router ID in either the request or response packet’s paths.

The following illustration might clarify this behavior:

![net](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/net/net46.png)
![net](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/net/net47.png)
![net](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/net/net48.png)

## Solution
From the above examples, we can see that if we move towards the middle from each end of the array, the elements at each of those ends are the same. This is the definition of a palindromic sequence. Since our topology allows one diversion router, we can check for the first position of a mismatch as we move towards the middle from both ends. If we ignore the mismatched value once, the original array should still form a palindromic sequence.

For traversal, we’ll use two pointers, left and right, for each end, respectively. We’ll keep traversing until we find a mismatch. We can ignore one router ID, so we can have two possible cases here for a mismatch:
1. Ignore the ID pointed to by the left pointer.
2. Ignore the ID pointed to by the right pointer.

We’ll assess both of these cases. Since we have traversed an equal number of elements from each end, if we ignore the mismatched elements, the resulting elements should form a palindromic sequence. So, we check the first case by ignoring the element pointed to by the left pointer. If the remaining elements do not form a palindrome, we check the second case by ignoring the element pointed to by the right pointer. After both cases, the resulting elements still do not form a palindrome, it means more than one diversion routers are present.

Let’s see how we might implement this functionality:
1. Initialize the left and right pointers at each end of the array, respectively.
2. Traverse the array until left is less than right.
3. If the element pointed to by the left pointer is equal to the element pointed to by the right pointer, do the following:
   * Increment the left pointer by one position.
   * Decrement the right pointer by one position.
4. If the element pointed to by the left pointer is not equal to the element pointed to by the right pointer, do the following:
   * Ignore the ID at the left pointer by checking if the elements at indexes left + 1 to right form a palindrome or not. If they do, return 1; this indicates the presence of only one diversion router.
   * Ignore the ID at the right pointer by checking if the elements at indexes left to right - 1 form a palindrome or not. If they do, return 1; this indicates the presence of only one diversion router.
5. If both of the above cases fail, return -1; this indicates the presence of multiple diversion routers.
6. If no mismatch occurs, return 0; this indicates the presence of a zero-diversion router.

The following illustration might clarify this process.

![net](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/net/net49.png)
![net](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/net/net50.png)
![net](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/net/net51.png)
![net](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/net/net52.png)
![net](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/net/net53.png)
![net](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/net/net54.png)

Let’s look at the code for the solution:

{% highlight java %}
class Solution { 
    static int transmissionError(int[] arr) { 

        // Initialize left and right at each end
        int left = 0, right = arr.length - 1; 
  
        while (left < right)  
        { 
            // Clause if elemetns at both ends are same
            if (arr[left] == arr[right])  { 
                left++; 
                right--; 
            }  
            // Clause when mismatch occurs
            else{
                // Check if ignoring left gives a palindromic sequnce 
                if (isPalindrome(arr, left + 1, right)) 
                    return 1; 

                // Check if ignoring right gives a palindromic sequnce
                if (isPalindrome(arr, left, right - 1)) 
                    return 1; 
                
                // Multiple routers exist
                return -1; 
            } 
        } 
        // No diversion router was used
        return 0; 
    }
    public static boolean isPalindrome(int[] arr, int left, int right) 
    { 
        while (left < right)  
        { 
            if (arr[left] != arr[right]) 
                return false; 

            left++; 
            right--; 
        } 
        return true; 
    }
    public static void main(String args[]) {

        int[] arr = {1, 2, 3, 3, 4, 2, 1};
        int res = transmissionError(arr);
        if (res == 1 || res == 0)
            System.out.println("Network Sustained. No Transmission Error Occurred!");
        else
            System.out.println("Network Broke. Transmission Error Occurred!");
    }
}
{% endhighlight %}

![net](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/net/net55.png)

## Feature #7: Divide Files Over the Network

## Description
We need to perform multiple operations on a large number of files over our network. Each file is represented by a lowercase English letter. The complete file list will be provided to us in the form of a string like "abacdc". The position of each letter tells us the sequence in which the files need to be processed. If multiple instances of a file are present, it means that multiple operations will be performed on that file. The file name mapping to characters is shown below:

![net](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/net/net56.png)

The number of files is so large that we deployed a high-performing cluster on the server to handle it. The cluster is supposed to divide the files among its worker nodes so more work can be done in less time. Each node must be assigned a set of contiguous file operations from the input string. In order to minimize the communication overhead, the files will be divided so that they utilize the maximum number of worker nodes and no two nodes process the same file. This will help us remove the dependency of files resulting in communication overhead between nodes. For example, the string "abacdc" will be divided into two worker nodes as "aba" and "cdc".

We’ll be provided with a string of characters representing the number of files in the sequence they need to be processed. Our task is to divide the files according to the defined criteria and return the number of nodes needed to process them.

The following illustration might also clarify this:

![net](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/net/net57.png)

## Solution
We can only have one particular letter in one particular part of our split. From the example, we can see that whenever there is a letter at index i, we split our string after the last occurrence of that letter. The letters between the first and last occurrence of our letter at index i can’t be in any other split, so we have to split after their last occurrence as well.

For each letter, we’ll add it to a split and then traverse to the last occurrence of it in the string. If we don’t traverse to the last occurrence, that letter might get added to another split. We’ll keep updating the maximum last occurrence because we traverse and stop when we reach the last occurrence of each letter, marking the end of one split.

In the string "abacdc", the last occurrence of its first letter, a, is at position 2. The last occurrence of letter b, which resides in between the first and last occurrence of a, is at position 1. So, by computing the maximum last occurrence at each index, the end of our split will update until our split is as long as it needs to be. In our example, the last position of a is 2, which will is decided during the traversal of index 0. We will also compute the last occurrence of b, which is 1. However, but our maximum is already higher than 1. When we eventually reach index 2 in our traversal, one split will occur and the next split will start at the next index. We’ll use two pointers start and end to manage the start and end of our splits, respectively.

Let’s see how we might implement this functionality:
1. Compute the last occurrence of each letter in the string.
2. Initialize the start and end pointers to zero to denote the start of the string. Also, initialize a count variable to zero.
3. Keep updating the end pointer to the maximum last occurrence value for each character until we reach end during the traversal.
4. Increment the value of count by 1 when the above condition is fulfilled.
5. Assign the start pointer to end + 1 to denote the start of the next split.

The following illustration might clarify this process:

![net](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/net/net58.png)
![net](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/net/net59.png)
![net](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/net/net60.png)
![net](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/net/net61.png)
![net](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/net/net62.png)
![net](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/net/net63.png)
![net](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/net/net64.png)
![net](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/net/net65.png)

Let’s look at the code for the solution:

{% highlight java %}
import java.util.*;

class Solution {
    public static int partitionLabels(String files) {
        // Compute the last occurences of each letter
        int[] last = new int[26];
        for (int i = 0; i < files.length(); ++i)
            last[files.charAt(i) - 'a'] = i;
        
        int start = 0, end = 0, count = 0;

        // Traverse the string
        for (int i = 0; i < files.length(); ++i) {
            // Compute the highest last occurence position
            end = Math.max(end, last[files.charAt(i) - 'a']);
            
            // Clause for when we reach the highest last occurence position
            if (i == end) {
                count++;
                start = i + 1;
            }
        }
        return count;
    }
    public static void main( String args[] ) {
        // Driver code

        String files = "abacdc";
        System.out.println("The files " + '"' + files + '"' + " will be divided into " + partitionLabels(files) + " worker nodes!");
    }
}
{% endhighlight %}

![net](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/net/net66.png)

## Feature #8: Maximum Clock Skew

## Description
Our network topology consists of routers interconnected in a tree structure. Messages are forwarded in this structure from ancestor nodes to descendant nodes. A system’s clock time value is stored in tree nodes representing the routers. We want to tune a distributed consensus algorithm that is parameterized by the maximum clock skew in a forwarding path. The clock skew can be defined as the difference between the time values of two routers in a network. The messages are forwarded over our tree from ancestors to descendants or vice versa. We want to find the maximum clock skew that we can encounter while forwarding the messages in the tree.

It is established that these time values cannot be the same, and clock skew is unavoidable. Therefore, obtaining the maximum skew value will highlight the two ancestor-descendant router pairs that are most out of sync. We’ll be provided with an n-ary tree structure, and our task is to identify the nodes that have the maximum difference in their time values.

Let’s understand this better with an illustration:

![net](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/net/net67.png)

## Solution
For a given node n, all of the nodes above it, upto the root node, are considered ancestors of node n. Since any two nodes can be the most synced out nodes, we have to process the complete tree from top to bottom. We need to traverse the tree height-wise; so we will use a DFS algorithm.

As we recursively traverse down the tree from the root, we can maintain a maximum and minimum time value for each node in maxiVal and miniVal, respectively. The maxiVal represents the maximum value over all the node values, which are above our current node. This includes the maximum among parents, the parent of the parent, and so on until the root node. Similarly, miniVal represents the minimum value over all node values, which are above our current node.

Now, to check the out of sync metric for node n and its ancestor, we can simply compute the absolute difference of n.val with maxiVal and miniVal and choose the largest one. Since the maximum difference value can be between any of the tree’s two ancestor-descendant pairs, the above computation will be done for each node and the maximum will be updated at each stage. When the recursive call ends, we will have the final maximum difference value between a certain ancestor and descendant node.

Let’s see how we might implement this functionality:
1. Initialize a maxDiff variable to zero. Its value will be updated in each recursive call.
2. Call the DFS function on the root of the tree, and every node will automatically be traversed.
3. The DFS function will have the following three parameters:
   * A current node that needs to be processed
   * The maxiVal variable
   * The miniVal variable
4. In the DFS function, update the maxDiff variable with the maximum value of maxiVal or miniVal. Then, call the DFS again on each subtree of the n-ary tree.
5. Return the maxDiff variable.

Let’s look at the code for the solution:

{% highlight java %}
import java.util.*;

class TreeNode {
  int val;
  List<TreeNode> children;

  TreeNode(int x) {
    val = x;
    children = new ArrayList<>();
  }
};

class Solution {
    // store the required maximum difference
    public static int maxDiff = 0;

    public static int maxClockSkew(TreeNode root) {
        if (root == null) {
            return 0;
        }

        maxDiff = 0;
        
        dfs(root, root.val, root.val);
        return maxDiff;
    }

    public static void dfs(TreeNode node, int maxiVal, int miniVal) {
        if (node == null) {
            return;
        }
        // update `maxDiff`
        int possiblemaxDiff = Math.max(Math.abs(maxiVal - node.val), Math.abs(miniVal - node.val));
        maxDiff = Math.max(maxDiff, possiblemaxDiff);
        
        // update the maxiVal and miniVal
        maxiVal = Math.max(maxiVal, node.val);
        miniVal = Math.min(miniVal, node.val);
        
        for (TreeNode child : node.children){
            dfs(child, maxiVal, miniVal);
        }
        return;
    }

    public static void main(String[] args) {
      // Driver Code

      TreeNode root = new TreeNode(8);
      root.children.add(new TreeNode(3));
      root.children.add(new TreeNode(10));
      root.children.add(new TreeNode(12));
      root.children.get(0).children.add(new TreeNode(6));
      root.children.get(0).children.get(0).children.add(new TreeNode(1));
      root.children.get(0).children.add(new TreeNode(5));
      root.children.get(0).children.get(1).children.add(new TreeNode(2));
      root.children.get(0).children.get(1).children.add(new TreeNode(3));
      root.children.get(0).children.get(1).children.add(new TreeNode(4));
      root.children.get(2).children.add(new TreeNode(8));
      root.children.get(2).children.add(new TreeNode(7));
      root.children.get(2).children.add(new TreeNode(9));

      System.out.println("The maximum clock skew we'll encounter is: " + maxClockSkew(root) + " seconds");
    }
}
{% endhighlight %}

![net](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/net/net68.png)

## Feature #9: Update Configuration

## Description
We have a network topology in which several network routers are interconnected in a rectangular grid. A router has four neighboring routers: up,\ right,\ left,up, right, left, and downdown. A router transmits a configuration update control message to its 4 directionally adjacent neighbors in response to a configuration change. The routers exchange control messages with their adjacent neighbors at one-minute intervals.

A router accepts the configuration change only if it receives a configuration update from its four neighbors, mentioned above, and then it updates its configuration.

We will be provided an m * n matrix of integers ranging from 0 to 2. The ranged integers represent the state of the configuration flow:
* 0 represents a router with VLAN ID 0.
* 1 represents a router with VLAN ID 1; it has yet to receive the configuration update.
* 2 represents a router with VLAN ID 2; it has received the transmission and has updated its configuration.

Our task will be to determine the minimum minutes before the configuration changes stop propagating, given that the configuration has been updated in some routers.

We can assume that there are no isolated\ routersisolated routers (all the routers have at least one router in their neighbors with a VLAN ID greater than zero), and configuration updates will flow to all the routers without failing.

Let’s try to understand this better with an illustration:

![net](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/net/net69.png)
![net](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/net/net70.png)
![net](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/net/net71.png)
![net](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/net/net72.png)
![net](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/net/net73.png)
![net](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/net/net74.png)
![net](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/net/net75.png)

## Solution
Since the updated routers can only transmit to their neighbors, we can map this 2D traversal problem to a tree or graph traversal problem. In a tree or graph, we reach out to the child or parent nodes, and these nodes, in turn, reach out to their parents and children.

These problems are commonly solved using the Breadth-First Search(BFS) and Depth First Search(DFS) strategies.

The most intuitive approach for our problem is BFS because the updated routers transmit the control message to their 4 directionally adjacent neighbors before the newly updated routers further send it.

Let’s try to visualize the transmission process with a graph below:

![net](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/net/net76.png)
![net](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/net/net77.png)
![net](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/net/net78.png)
![net](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/net/net79.png)

The graph nodes in the above illustration contain the (i, j) index of the corresponding grid cells, and the edges represent the neighbors.

We can observe that the transmission propagates from the root (the initially configured router) to the farthest router level by level.

The number of elapsed minutes is equivalent to the number of levels in the graph.

Now, let’s review how we can use BFS to implement the solution.

We will use a queue data structure to store the nodes to be explored. We will iterate over the queue, popping the element from the head (front) of the queue. We process and update the popped node’s configuration. Then, we append the pair (i, j) to the queue to keep the BFS running.

The following are the optimizations we can apply to this solution:
1. Usually, an additional data structure, like a table, is required to store the visited nodes to avoid repetitive visits. However, we can update the grid in-place by altering the status from 1(yet-to-receive) to 2(updated).
2. We use the delimiter (-1, -1) in the queue to separate the grid cells on different levels.

Review the implementation below:

{% highlight java %}
class Pair{
    public int key;
    public int value;
    public Pair(int key, int value){
        this.key = key;
        this.value = value;
    }
}

class Solution {
    public static int updateConfiguration(int[][] grid){
        // Pair with both key and value as integers
        Queue<Pair> queue = new ArrayDeque<Pair>();

        // Step 1). build the initial set of updated routers
        int rows = grid.length, cols = grid[0].length;

        for (int r = 0; r < rows; ++r)
            for (int c = 0; c < cols; ++c)
                if (grid[r][c] == 2)
                    queue.offer(new Pair(r, c));

        // Mark the round / level, _i.e_ the ticker of timestamp
        queue.offer(new Pair(-1, -1));

        // Step 2). start the transmitting process via BFS
        int minutesElapsed = -1;
        // Four Neigbors, up, right, down and left
        int[][] directions = { {-1, 0}, {0, 1}, {1, 0}, {0, -1}};

        while (!queue.isEmpty()) {
            Pair p = queue.poll();
            int row = p.key;
            int col = p.value;
            if (row == -1) {
                // We finish one round of processing
                minutesElapsed++;
                // to avoid the endless loop
                if (!queue.isEmpty())
                    queue.offer(new Pair(-1, -1));
            } else {
                // this is an updated router
                // then it would transmit the update to its neighbors
                for (int[] d : directions) {
                    int neighborRow = row + d[0];
                    int neighborCol = col + d[1];
                    if (neighborRow >= 0 && neighborRow < rows && 
                        neighborCol >= 0 && neighborCol < cols) {
                        if (grid[neighborRow][neighborCol] == 1) {
                            // this router would be updated
                            grid[neighborRow][neighborCol] = 2;
                            // this router would then transmit to other routers
                            queue.offer(new Pair(neighborRow, neighborCol));
                        }
                    }
                }
            }
        }

        // return elapsed minutes
        return minutesElapsed;
    }

    public static void main( String args[] ) {
        // Driver Code
        int[][] grid = {{1, 1, 0, 0, 1}, {0, 1, 0, 1, 1}, {1, 1, 2, 0, 1}, {1, 0, 1, 1, 1}, {1, 1, 0, 1, 1}};
        System.out.println(updateConfiguration(grid));
    }
}
{% endhighlight %}

![net](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/net/net80.png)

## Feature #10: Minimum Variation

## Description
We monitored a network for several days and stored the daily traffic rates the network handled in an array. When billing customers for network traffic, we want to offer a discount to the traffic profiles for which traffic the rate stays more or less constant, meaning it does not vary too much. To this end, we want to find the longest stretch of consecutive days on which the traffic variation was the least on our array. Here, we define variation in a sub-array v[i..j] as the absolute difference between the maximum element and the minimum element in the sub-array, max(t[i..j]) - min(t[i..j]). We will define the threshold minimum value against which the variation will be compared. If the traffic variation is below this threshold (for at least x number of days), we will offer a discount on the bill. Therefore, we are looking for the days on which traffic variation is less than or equal to the defined threshold. For example, if a customer’s traffic changes by less than or equal to 5 Gbps in a five-day window, then they get a discount.

We’ll be provided with an array of integers representing the traffic while the index will represent the days. An additional threshold value will be provided. We have to return the length of the longest sub-array for which traffic variation is less than or equal to this certain threshold.

The following illustration might clarify this behavior:

![net](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/net/net81.png)
![net](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/net/net82.png)

## Solution
Since we need to compute a sub-array, we can use two pointers, start and end, to maintain the subarrays as we traverse over the array. Using these two pointers, we’ll keep track of the maximum and minimum elements in the sub-array currently being traversed. For each sub-array that comes under the range of the start and end pointers (inclusive), we’ll compute the maximum and minimum values for that sub-array. Now that we have the maximum and minimum values, we can compute the variation. If this max-min difference is greater than the limit, increment the start pointer. If this max-min difference is smaller or equal to the limit, increment the end pointer and update the current max sub-array size because another element was selected for our sub-array.

At the end of the traversal, we’ll have the size of the maximum sub-array in which variation is minimum. The only issue is computing the max and min value for each probable sub-array. We can use the deque data structure for this purpose because it provides O(1)O(1) lookup. The deque data structure also provides push and pop operations at both of its ends in O(1)O(1) time. We’ll maintain two deques, one increasing and one decreasing. The increasing deque will have the minimum element at its front, and the decreasing deque will have the maximum element at its front. Whenever we see a new value, we’ll compare it with the last value of both deques to maintain their monotonic properties.

Let’s see how we might implement this functionality:
1. Initialize the start and end pointers to the beginning of our input array. Also, initialize two empty deques, minDeque and maxDeque. Then, append the first index pointed by the end pointer to both deques.
2. Start traversing the array and keep inserting each new index to both the deques. Perform the following checks before this insertion:
   * Remove all values that are greater than the value at the current index from the end of the minDeque.
   * Remove all values that are smaller than the value at the current index from the end of the maxDeque.
3. Keep incrementing the end pointer and the max sub-array size while inserting elements in both deques. We do this until the max absolute difference (variation) within the sub-array exceeds the mentioned limit.
4. Now, we keep incrementing the start pointer until the maximum absolute difference (variation) falls back within the limit. Each time the start pointer gets incremented, we remove the smaller index value from the front of both the deques.
5. Return the max sub-array size at the end.

The following illustration might clarify this process. We’ll use array values instead of indexes to clearly visualize the algorithm.

![net](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/net/net83.png)
![net](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/net/net84.png)
![net](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/net/net85.png)
![net](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/net/net86.png)
![net](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/net/net87.png)
![net](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/net/net88.png)
![net](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/net/net89.png)
![net](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/net/net90.png)

Let’s look at the code for the solution:

{% highlight java %}
import java.util.*;
class Solution {
    public static int miniVariationLength(int[] nums, int threshold) {
        
        Deque<Integer> maxDeque = new ArrayDeque<>();
        Deque<Integer> minDeque = new ArrayDeque<>();
        int start = 0, end = 0;
        int ans = 0;

        while (end < nums.length){
            // All elements greater than current index element gets removed from minDeque
            while(!minDeque.isEmpty() && nums[end] < nums[minDeque.peekLast()])
                minDeque.pollLast(); // pop from end
            
            // All elements smaller than current index element gets removed from minDeque
            while(!maxDeque.isEmpty() && nums[end] > nums[maxDeque.peekLast()])
                maxDeque.pollLast(); // pop from end
            
            // append at end of both deques
            minDeque.add(end);
            maxDeque.add(end);

            int variation = nums[maxDeque.peek()] - nums[minDeque.peek()];
            if (variation > threshold){
                start++;
                // A new sub-array is starting so elements from previous one should
                // be removed from both the deques
                if (start > minDeque.peek())
                    minDeque.poll(); // pop from front
                if (start > maxDeque.peek())
                    maxDeque.poll(); // pop from front
            }
            
            ans = Math.max(ans, (end - start + 1));
            end++;
        }
        return ans;
    }
    public static void main( String args[] ) {
        // Driver code
        
        int[] trafficRates = {10,1,2,4,7,2};
        int thresholdMiniVal = 5;

        System.out.println("The traffic of this customer changes by less than or equal to " + thresholdMiniVal + " Gbps in a " + miniVariationLength(trafficRates, thresholdMiniVal) + " day window");
    }
}
{% endhighlight %}

![net](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/net/net91.png)
