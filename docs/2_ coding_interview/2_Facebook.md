---
layout: default
title: Facebook
parent: Coding Interview
has_children: true
nav_order: 2
permalink: /coding_interview/facebook
---
<div align="center" markdown="1">
Facebook / Java resources / Tutorial

{: .fs-8 .fw-400 }
</div>

## Facebook

## Project Description for Facebook

## Introduction
Facebook is the biggest social media company in the world. The company also owns other social media platforms like Instagram as well, and the engineering team at Facebook keeps trying to find better ways to connect people among all their platforms. This allows users to share and view content by their connections throughout all the platforms.

The scenario and the problems discussed in this chapter relate to Facebook’s content sharing and viewing functionality across different platforms and how we can improve them.

## Statement
Let’s say you are a developer on the Facebook engineering team. Your team needs to improve the integration among the sister platforms. An important concern in this integration is achieving operational efficiency through not only efficient code, but also API rate limiters and elimination of similar requests by the same user on different platforms. Your team has also been requested to take this opportunity to implement features to detect potentially objectionable content.

## Features

We will need to introduce the following features to implement the functionalities we discussed above:
* Feature #1: Find all the people on Facebook that are in a user’s friend circle.
* Feature #2: We want all the user’s friends on Facebook to be suggested on Instagram as well. Since Instagram is a different platform, all of its connections need to be copied to a separate database.
* Feature #3: Sync the Facebook stories list with Instagram.
* Feature #4: Limit the request rate from users. The same request cannot be sent from the other platform until a specified amount of time has elapsed since the request from the first platform.
* Feature #5: Identify the morphed versions of abused and profane words so posts containing them can be flagged inappropriate.
* Feature #6: Group the similar gibberish posts together so a decoding pattern can be observed.
* Feature #7: Mining for patterns in posts by a user needs to be done on a high-performance cluster. You need to suggest an optimal assignment of posts to cluster nodes so that their processing power is optimally utilized.

Understanding these feature requests and designing their solutions will help us implement the requested functionality into Facebook’s system.

In the next few lessons, we’ll discuss the recommended implementations of these features. Before we start, we suggest that you think about how you would implement these features. You may realize some of the underlying problems that you’ll need to solve. The solutions to these basic problems are also applicable to other common coding interview questions.

## Feature #1: Friend Circles

## Description
First, we need to find all the people that are in each user’s friends circle on Facebook. Your individual friend circle is defined as a group of users who are directly or indirectly friends with you. Assume there are a total of n users on Facebook. Some of them are your friends and others are not. The friendship/connection is transitive in nature. For example, if Shaw is a direct friend of Andy, and Andy is a direct friend of Noah, then Shaw is an indirect friend of Noah. Getting the total number of friend circles that exist on Facebook helps us suggest connections on Instagram for every user.

We’ll be provided with an n x n square matrix, where n is the number of users on Facebook. A cell [i,j] will hold the value 1 if user i and user j are friends. Otherwise, the cell will hold the value 0. For example, consider the input:

![code](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/code/code54.png)

There are two friend circles in the above example. Shaw is friends with Andy only, but Andy is friends with both​ Shaw and Noah. These three users make one friend circle. Dana, alone, makes another friend circle.

## Solution
We can think of the symmetric input matrix as an undirected graph. All the friends (both direct and indirect) who should be in one friend circle are also in one connected component​ in the graph. So, the number of connected components in the graph will give us the number of friend circles. We can treat our input matrix as an adjacency matrix; our task is to find the number of connected components.

Here is how we will implement this feature.
1. Initialize an array, called visited, to keep track of the visited vertices of size n with 0 as the initial value at each index.
2. For every vertex v, traverse the graph using DFS if visited[v] is 0. Otherwise, move to the next v.
3. Set visited[v] to 1 for every v that the DFS traversal encounters.

When the DFS traversal terminates, increment the friend circles counter by 1. This means that​ one whole connected component has been traversed.

Let’s look at this solution’s code:

{% highlight java %}
class Solution {

  public static void DFS (boolean[][] friends, int n, boolean[] visited, int v) {
    for (int i = 0; i < n; ++i) {

        // A user is in the friend circle if he/she is friends with the user represented by
        // user index and if he/she is not already in a friend circle
        if (friends[v][i] == true && !visited[i] && i != v) {
            visited[i] = true;
            DFS(friends, n, visited, i);
        }
    }
  }

  public static int friendCircles(boolean[][] friends, int n) {
    if (n == 0) {
        return 0;
    }
 
    int numCircles = 0;     //Number of friend circles
    
    //Keep track of whether a user is already in a friend circle
    boolean visited[] = new boolean[n];

    for (int i=0;i < n; i++){
      visited[i] = false;
    }
    
    //Start with the first user and recursively find all other users in his/her
    //friend circle. Then, do the same thing for the next user that is not already
    //in a friend circle. Repeat until all users are in a friend circle. 
    for (int i = 0; i < n; ++i) {
        if (!visited[i]) {
            visited[i] = true;
            DFS(friends, n, visited, i); //Recursive step to find all friends
            numCircles = numCircles + 1;
        }
    }
    
    return numCircles;
  }

  public static void main(String args[]) 
  { 
      int n = 4;
      boolean[][] friends = {
        {true,true,false,false},
        {true,true,true,false},
        {false,true,true,false},
        {false,false,false,true}
      };
     System.out.println("Number of friends circles: " + friendCircles(friends, n)); 
  } 

}
{% endhighlight %}

![code](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/code/code55.png)

## Feature #2: Copy Connections

## Description
After identifying every user’s friend circles, we need to duplicate this data to Instagram’s servers so it can be easily accessed and modified there as well. As the user’s name can be the same, so every user on Facebook gets assigned a unique id. Each Facebook user’s connections are represented and stored in a graph-like structure. We will first have to make an exact copy of this structure before storing it on Instagram’s servers.

Let’s say we want to duplicate the data for the following users:

![code](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/code/code56.png)

For each user, we’ll be provided with a node and its information. This node will point to other nodes, and from that one node, we need to reach and make an exact clone of every other node. An edge between two nodes means that they are friends with each other. A bi-directional edge means that both users follow each other, whereas a uni-directional edge means that only one user follows the other.

Below is an illustration of this:

![code](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/code/code57.png)

## Solution
We can use depth-first traversal and create a copy of each node while traversing the graph. To avoid getting stuck in cycles, we’ll use a hashtable to store each completed node, and we will not revisit nodes that exist in the hashtable. The hashtable key will be a node in the original graph, and its value will be the corresponding node in the cloned graph.

For the above graph, let’s assume the root (the randomly selected node from which we start the cloning process) is node 0. We’ll start with the root node 0.

![code](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/code/code58.png)
![code](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/code/code59.png)
![code](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/code/code60.png)
![code](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/code/code61.png)
![code](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/code/code62.png)
![code](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/code/code63.png)
![code](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/code/code64.png)
![code](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/code/code65.png)
![code](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/code/code66.png)
![code](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/code/code67.png)

Let’s look at the code for the solution:

{% highlight java %}
class Node {
  public int data;
  public List<Node> friends = new ArrayList<Node>();
  public Node(int d) {data = d;}
}

class Solution {
  private static Node clone_rec(Node root, HashMap<Node, Node> nodes_completed) {
    if (root == null) {
      return null;
    }

    Node newNode = new Node(root.data);
    nodes_completed.put(root, newNode);

    for (Node p : root.friends) {
      Node x = nodes_completed.get(p);
      if (x == null){
        newNode.friends.add(clone_rec(p, nodes_completed));
      } else {
        newNode.friends.add(x);
      }
    }
    return newNode;
  }

  public static Node clone(Node root) {
    HashMap<Node, Node> nodes_completed = new HashMap<Node, Node>();
      
    return clone_rec(root, nodes_completed);
  }

  public static void main(String[] args) {
    ArrayList<Node> vertices = CloneGraph.createTestGraphDirected(7, 18);

    CloneGraph.printGraph(vertices.get(0));

    Node cp = clone(vertices.get(0));
    System.out.println();
    System.out.println("After copy.");
    CloneGraph.printGraph(cp);

    HashSet<Node> set = new HashSet<Node>();
    System.out.println(CloneGraph.are_graphs_equal_rec(vertices.get(0), cp, set));
  }  
}

import java.util.*;
import java.lang.*;

class Pair<X, Y> {
  public X first;
  public Y second;
  public Pair(X first, Y second) {
    this.first = first;
    this.second = second;
  }
}

class CloneGraph {
// if there is an edge from x to y
// that means there must be an edge from y to x
// and there is no edge from a node to itself
// hence there can maximim of (nodes * nodes - nodes) / 2 edgesin this graph
  static ArrayList<Node> createTestGraphDirected(int nodes_count, int edges_count) {
    ArrayList<Node> vertices = new ArrayList<Node>();
    for (int i = 0; i < nodes_count; ++i) {
      vertices.add(new Node(i));
    }

    List<Pair<Integer, Integer>> all_edges = new ArrayList<Pair<Integer, Integer>>();
    for (int i = 0; i < vertices.size(); ++i) {
      for (int j = i + 1; j < vertices.size(); ++j) {
        all_edges.add(new Pair<Integer, Integer>(i, j));
      }
    }

    Collections.shuffle(all_edges);

    for (int i = 0; i < edges_count && i < all_edges.size(); ++i) {
      Pair<Integer, Integer> edge = all_edges.get(i);
      vertices.get(edge.first).friends.add(vertices.get(edge.second));
      vertices.get(edge.second).friends.add(vertices.get(edge.first));
    }

    return vertices;
  }

  static void printGraph(List<Node> vertices) {
    for (Node n : vertices) {
      System.out.print(n.data + ": {");
      for (Node t : n.friends) {
        System.out.print(t.data + " ");
      }
      System.out.println();
    }
  }

  static void printGraph(Node root, HashSet<Node> visited_nodes) {
    if (root == null || visited_nodes.contains(root)) {
      return;
    }

    visited_nodes.add(root);

    System.out.print(root.data + ": {");
    for (Node n : root.friends) {
      System.out.print(n.data + " ");
    }
    System.out.println("}");

    for (Node n : root.friends) {
      printGraph(n, visited_nodes);
    }
  }

  static void printGraph(Node root) {
    HashSet<Node> visited_nodes = new HashSet<Node>();
    printGraph(root, visited_nodes);
  }

  static boolean are_graphs_equal_rec(Node root1, Node root2, HashSet<Node> visited) {
    if (root1 == null && root2 == null) {
      return true;
    }

    if (root1 == null || root2 == null) {
      return false;
    }

    if (root1.data != root2.data) {
      return false;
    }

    if (root1.friends.size() != root2.friends.size()) {
      return false;
    }

    for (Node nbr1 : root1.friends) {
      boolean found = false;
      for (Node nbr2 : root2.friends) {
        if (nbr1.data == nbr2.data) {
          if (!visited.contains(nbr1)) {
            visited.add(nbr1);
            are_graphs_equal_rec(nbr1, nbr2, visited);
          }
          found = true;
          break;
        }
      }
      if (!found) {
        return false;
      }
    }

    return true;
  }
}
{% endhighlight %}

![code](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/code/code68.png)

## Feature #3: Find Story ID

## Description
This feature will allow us to watch or re-watch stories on Instagram that are uploaded through Facebook. Every story uploaded by a user on Facebook gets assigned a unique incrementing id. On Instagram, a user can only watch one story at a time. These stories will be accessed from Facebook in ascending id order. When a story is watched, the story array rotates to accommodate unwatched stories at the start and watched stories at the end. Since stories are fetched from Facebook, so whenever a user wants to rewatch a story on Instagram, our system has to search for its id in the Facebook story array.

Observe this behavior in the illustration below:

![code](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/code/code69.png)
![code](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/code/code70.png)

We’ll have an array containing the story id’s. Some of the stories will be watched and will be at the end of the array, and some will be unwatched and will be at the start of the array. If a user clicks a story, we need to search for its id in the array and return the index of that id.

## Solution
The solution is essentially a binary search with some modifications. If we look at the array in the example closely, we notice that at least one half of the array is always sorted. We can use this property to our advantage. If the number n lies within the sorted half of the array, our problem is a basic binary search. Otherwise, we’ll discard the sorted half and keep examining the unsorted half.

Let’s assume we have the following array and we have to find 6.

![code](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/code/code71.png)
![code](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/code/code72.png)
![code](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/code/code73.png)
![code](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/code/code74.png)

Let’s look at the code for the solution:

{% highlight java %}
class Solution{
  public static int Search(int[] arr, int start, int end, int key) {
    
    if (start > end) {
      return -1;
    }

    int mid = start + (end - start) / 2;

    if (arr[mid] == key) {
       return mid;
    }

    if (arr[start] <= arr[mid] && key <= arr[mid] && key >= arr[start]) {
      return Search(arr, start, mid - 1, key);
    }

    else if (arr[mid] <= arr[end] && key >= arr[mid] && key <= arr[end]) {
      return Search(arr, mid + 1, end, key);
    }

    else if (arr[end] <= arr[mid]) {
      return Search(arr, mid + 1, end, key);
    }

    else if (arr[start] >= arr[mid]) {
      return Search(arr, start, mid - 1, key);
    }
    
    return -1;
  }

  static int FindStoryId(int[] arr, int key) {
    return Search(arr, 0, arr.length - 1, key);
  }
  
  public static void main(String []args){
    int[] v1 = {6, 7, 1, 2, 3, 4, 5};
    System.out.println("Key(3) found at: " + FindStoryId(v1, 3));
    System.out.println("Key(6) found at: " + FindStoryId(v1, 6));
    
    int[] v2 = {4, 5, 6, 1, 2, 3};
    System.out.println("Key(3) found at: " + FindStoryId(v2, 3));
    System.out.println("Key(6) found at: " + FindStoryId(v2, 6));    
  }
}
{% endhighlight %}

![code](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/code/code75.png)

## Feature #4: Request Limiter

## Description
The Facebook Status API queues requests using the requested Status ID and a timestamp. We want to implement a throttling mechanism on the requests that limits one request for a particular Status ID at a pre-configured time interval. Any additional requests for the same Status ID in this interval will be dropped. Multiple requests for different Status IDs can occur at the same time.

We’ll be provided with the name of the request and the time it arrived. Our system will have to decide whether to accept the request or reject it based on its arrival time. In this scenario, we’ll use a time limit of five days before a similar request can be sent from the same or different platform.

## Solution
The hashtable data structure will be used to implement this feature. This data structure can uniquely store all of the incoming requests while simultaneously taking care of the duplicate requests. The requests will be stored as keys and the request’s timestamp will be stored as corresponding values in the hashtable.

Here is how we will implement this feature:
1. Initialize the hashtable.
2. When a request arrives, check if it’s a new request or a repeated request that came after the assigned time limit.
3. If either of the above conditions is satisfied, accept the request and update the entry associated with that request in the hashtable.
4. If not, reject the request.

![code](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/code/code76.png)

As you can see, the HashMap above has an entry with a request #2 and a timestamp T4. A new request arrives with the same number and a timestamp of T12 because the first request was made eight days ago. This exceeds our time limit. Therefore, we can allow this request to proceed, and as a result, the timestamp of request #2 will be updated to T12.

Let’s look at the code for the solution:

{% highlight java %}
import java.util.*;

class RequestLimiter {
  private HashMap<String, Integer> requests;

  public RequestLimiter() {
    requests = new HashMap<String, Integer>();
  }


  // Returns true if the request should be printed in the given timestamp, 
  //otherwise returns false.
  
  public boolean RequestApprover(int timestamp, String request) {

    if (!this.requests.containsKey(request)) {
      this.requests.put(request, timestamp);
      System.out.println("Request Accepted");
      return true;
    }

    Integer oldTimestamp = this.requests.get(request);

    if (timestamp - oldTimestamp >= 5) {
      this.requests.put(request, timestamp);
      System.out.println("Request Accepted");
      return true;
    } 
    else
      System.out.println("Request Rejected");
      return false;
  }

  public static void main(String[] args){
    // Driver code
    
    RequestLimiter obj = new RequestLimiter();

    obj.RequestApprover(1, "send_message");
    obj.RequestApprover(2, "block");
    obj.RequestApprover(3, "send_message");
    obj.RequestApprover(8, "block");
    obj.RequestApprover(10, "send_message");
    obj.RequestApprover(11, "send_message");
  }
}
{% endhighlight %}

![code](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/code/code77.png)

## Feature #5: Flag Words

## Description
Facebook recently conducted a survey on the techniques people use to hide offensive or profane words. The goal was to flag such words in the posts and messages of users. The most observable pattern was that the characters of a word were repeated multiple times to avoid detection. A single character in a word was observed to be repeated at least 3 times. This means that characters repeated less than 3 times will be ignored in the detection process.

We’ll be provided with a string, S, representing the profane or offensive input word and another string, W, representing the original word. We have to determine if the original word, W, can be modified into S following the above-mentioned rules.

![code](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/code/code78.png)

Since we have to observe letters of two strings at a time, we can follow a two-pointer approach to solve this problem.

Here is how we will implement this feature:
1. Initialize two pointers, i and j, to start traversing from S and W, respectively.
2. Check if letters currently pointed to by i and j of both words are equal. Otherwise, return False.
3. For each equal letter found:
   * Get the length of the repeating sequences of the equal letter found in both words.
   * The length of the repeating sequence of W letters should be less than or equal to the length of the repeating sequence of S letters.
   * The length of the repeating sequence of S letters should be greater than or equal to 3.
4. If any of the conditions mentioned in step 3 fails, return false.
5. If the ends of both strings are reached, return true.

Let’s look at this solution’s code:

{% highlight java %}
class Solution {
    public static boolean flagWords(String S, String W) {
        if (S == null || W == null) {
            return false;
        }
        int i = 0;
        int j = 0;
        while (i < S.length() && j < W.length()) {
            if (S.charAt(i) == W.charAt(j)) {
                int len1 = repeatedLetters(S, i);
                int len2 = repeatedLetters(W, j);
                if (len1 < 3 && len1 != len2 || len1 >= 3 && len1 < len2) {
                    return false;
                }
                i += len1;
                j += len2;
            } else {
                return false;
            }
        }
        return i == S.length() && j == W.length();
    }
    
    public static int repeatedLetters(String s, int ind) {
        int temp = ind;
        while (temp < s.length() && s.charAt(temp) == s.charAt(ind)) {
            temp++;
        }
        return temp - ind;
    }
    public static void main( String args[] ) {
        // Driver code

        String S = "mooooronnn"; // modified word
        String W = "moron"; // original word
        
        if (flagWords(S, W)){
            System.out.println("Word Flagged");
            System.out.println("The Word " + '"' + S + '"' + " is a possible morph of " + '"' + W + '"');
        }
        else
            System.out.println("Word Safe");
    }
}
{% endhighlight %}

![code](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/code/code79.png)

## Feature #6: Combine Similar Messages

## Description
Someone is posting messages on Facebook that are apparently gibberish. Research has indicated that the author picks every word and mutates it by adding a fixed offset value to each letter in the word. For example, they may mutate hy to iz by adding 1 to each letter of hy. Similarly, they may mutate hy to ja by adding 2 to each letter of hy, etc. We want to decode these messages. The first step is to group all the words that may be mutations of each order to make further analysis easier.

We’ll be provided with an array of strings in which each string represents a garbled message. Our task is to group all the messages that differ by the same number of offsets in each of their characters.

Here is an illustration of this process:

![code](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/code/code80.png)

## Solution
From the above example, we can see that the difference between consecutive characters of each word is equal for each set. Consider the words lmn and mno from Set 1 of the example above. The difference between the ASCII values of each pair of consecutive characters of lmn is (1, 1), respectively, and the difference between each character of mno is also (1, 1). Words that are shifted versions of each other have identical character code differences. Using this, we can combine shifted words into separate sets. We can use a HashMap in which the keys can be represented by the differences between adjacent characters. The words that have these differences between their characters will be mapped as the values of these keys. For example, (1,1) will be a key with lmn and mno as its values. When all words are processed, the values of our HashMap will be the different groups.

In Set 2 of the above example, a wrap-around case occurs. In the string azb and bac, z(122) - a(97) gives us 25, but a(97) - b(98) gives us -1. If we don’t take care of this case, these two messages would end up being in two different sets. So, if any difference is less than zero, simply add 26 to it. For our case, -1 + 26 gives us 25, which is correct since, in reality, a is 25 steps away from b moving in a forward direction.

Here is how we will implement this feature:
1. Create a generateKey() function that takes a string and returns their character differences. This function will start traversing from the second character and will compute all the subsequent differences in a string.
2. Initialize a HashMap called messageGroup.
3. Traverse the array of strings, and for each string, compute the key value using the generateKey() function.
4. If a key is present in messageGroup, append the current string to it. Otherwise, add the key and then append the string to it.
5. Return messageGroup when the iteration ends.

The following illustration shows us the key-value structure in which the groups are formed against their difference in characters:

![code](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/code/code81.png)

Let’s look at this solution’s code:

{% highlight java %}
import java.util.*;
class Solution {
    
    public static List<List<String>> combineMessages(String[] messages) {
        Map<String, List<String>> messageGroup = new HashMap<>();

        for(String message : messages) {
            // Get key for current message
            String key = generateKey(message);
            // Assign value to keys
            List<String> list = messageGroup.getOrDefault(key, new ArrayList<>());
            list.add(message);
            messageGroup.put(key, list);
        }
        return new ArrayList<>(messageGroup.values());
    }
    // Function to generate keys
    public static String generateKey(String message) {
        char[] chars = message.toCharArray();
        String key = "";

        for(int i = 1; i < chars.length; i++) {
            // Compute difference of adjacent characters
            int diff = chars[i] - chars[i-1];
            
            // Handle the wrap around case and construct the key string
            key += diff < 0 ? diff + 26 : diff;
            key += ",";
        }
        return key;
    }
    public static void main( String args[] ) {
        // Driver code
        
        String[] messages = {"lmn", "mno", "azb", "bac", "yza", "bdfg"};
        List<List<String>> groups = combineMessages(messages);

        System.out.println("The Grouped Messages are:\n");
        for (List<String> group : groups)
            System.out.println(group);  
    }
}
{% endhighlight %}

![code](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/code/code82.png)

## Feature #7: Divide Posts

## Description
Several users made a number of Facebook posts every day last month. We have stored the number of daily posts in an array. We want to mine these posts for information. We have k worker nodes to process the data. For optimally exploiting the temporal relationship between the posts, each worker node must process posts from one or more consecutive days. There will be a master node among our k worker nodes. This node will be in charge of distributing posts to other nodes, as well as mining the posts itself. Given an allocation of tasks to workers and the master node, the master node should get the smallest task. To efficiently utilize our resources, we want an allocation of tasks that maximizes the task allocation to the master node, so we have optimal utilization of worker nodes processing power. There can be a lot of posts a day, so input posts for each day would be in thousands.

We’ll be provided with an array of integers representing the daily number of posts on several consecutive days. Additionally, we’ll have the number of worker nodes, and our task will be to determine the maximum total posts that can be assigned to the master node.

Let’s understand this behavior in the illustration below:

![code](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/code/code83.png)

In the above example, the 4 thousand posts from Day 3 will be assigned to the master node. This is the maximum number of posts that the master node can handle while assigning a greater number of posts than itself to the other worker nodes.

## Solution
We have to search for the maximum number of posts that can be assigned from an array of integers. We can use the binary search with some modifications to compute this value. In a typical binary search, we compute the middle value in the array. If our target value is greater than this middle value, we move to the right portion of the array. Otherwise, we move to the left portion. We have found the element at which our target becomes equal to the middle value.

For this problem, our target is to optimally divide the number of posts into k nodes. This is a two-step process:
* First, use binary search to maximize the minimum sum of subarrays in a split.
* Then, figure out if such a split is possible.

What’s the maximum possible sum that any split could have? One extreme is everything gets assigned to one node, sum(days). No one gets anything to do. However, we know that this isn’t a valid split because it isn’t a split at all. Can we do better than this? Sure. How about the average, sum(days)/k? That’s a good starting point. The minimum subarray sum will definitely be smaller than or equal to the mean. We can assign the lower bound to 1 since, at minimum, the master node will be assigned a single post to process.

So, start with low = 1 and high = sum(days)/k. Then, binary search for the maximum sum of the smallest subarray sum over all the splits. We first check if it is possible to get a k-way split such that the smallest subarray has a sum less than or equal to mid = (high + low) / 2. If possible, we check if we can find a split with an even higher minimum subarray sum by setting low = mid. If not, we check if a smaller minimum subarray sum is possible by setting high = mid - 1.

How do we check if a split is possible for a given target minimum subarray sum? We just iterate over the array’s elements and keep accumulating elements into a single subarray as long as the sum doesn’t exceed mid. As soon as that happens, we declare the current subarray “closed” and “open” the next sub-array. We are splitting the array into subarrays such that their sum doesn’t exceed mid. If the number of such subarrays is less than k, we were aiming too high. Otherwise, we were aiming too low. We’ll keep doing this until our search condition low < high returns False as at that stage the mid value will have converged to the optimal one.

Here is how we will implement this feature:
1. Initialize low and high, as described above. Also, initializing the variables target and division to zero as target would denote the posts we currently have because we traverse over the array and division will tell us how many days we would get after dividing the array in mid amount of posts.
2. As long as low < high, compute the middle value as (low + high + 1) / 2. Here, +1 includes the mid in our range. If we don’t include +1, we’ll be stuck in an infinite loop because we’ll always pick the same mid, which will be low.
3. Traverse the array and keep adding the posts until the target becomes greater than or equal to our mid, and do the following:
   * Increment divisions by 1.
   * Assign target to 0.
4. At the end of traversal, assign low = mid if the divisions are greater than or equal to the number of nodes. Otherwise, assign high to mid - 1.
5. When low < high returns False, return either low or high as they would have converged to the optimal value.

Let’s look at this solution’s code:

{% highlight java %}
import java.util.*;
class Solution {
    
    public static int dividePosts(int[] days, int k) {
        int left = 1, right = Arrays.stream(days).sum() / k;

        while (left < right) {
            int mid = (left + right + 1) / 2;
            
            // This would denote the posts we currently have 
            // as we are traversing over the array
            int target = 0;
            
            // This would tell us how many days we would get after dividing 
            // the array in `mid` amount of posts
            int divisions = 0;
            for (int posts : days) {
                target += posts;
                if (target >= mid) {
                    divisions++;
                    target = 0;
                }
            }
            if (divisions >= k)
                left = mid;
            else
                right = mid - 1;
        }
        return left;
    }
    public static void main( String args[] ) {
        // Driver code
        
        int[] dayss = {1000,2000,3000,4000,5000};
        int nodes = 3;
        System.out.println("The master node was assigned " +  dividePosts(dayss, nodes) + " posts");
    }
}
{% endhighlight %}

![code](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/code/code84.png)