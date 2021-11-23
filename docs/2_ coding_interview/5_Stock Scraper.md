---
layout: default
title: Stock Scraper
parent: Coding Interview
has_children: true
nav_order: 5
permalink: /coding_interview/stock
---
<div align="center" markdown="1">
Stock Scraper / Java resources / Tutorial

{: .fs-8 .fw-400 }
</div>

## Stock Scraper

## Project Description for Stock Scraper

## Introduction
Extracting data from a website is known as scraping. The main component of scraping is fetching data from the HTML DOM structure after receiving a response from the website. You can think of web scraping as a spider crawling over every corner of an HTML structure and retrieving information of interest.

The scenario and problems we will discuss in this chapter relate to scraping stock data from websites.

## Statement
You are a developer on a trading company’s engineering team. The company wants you to build a program that will dynamically scrape stock data from different websites, and then perform a profit analysis on the extracted data.

Since websites are represented as a DOM tree of HTML tags, we’ll first have to find a way to traverse this structure. Identifying stock data in an arbitrary HTML will be challenging because every website has a different structure and stock price data can be anywhere on the page.

## Features

We will need to introduce the following features to implement the functionalities discussed above:
* Feature #1: Develop a way to parse the DOM tree structure of different stock websites.
* Feature #2: Assign a confidence score to each HTML tag in the DOM to represent the likelihood that the tag contains stock price data. Then, filter the minimal subtree of the DOM that has stock price data.
* Feature #3: Stock price data at the same level of the DOM tree is closely related. Develop a new way to efficiently parse the DOM tree structure by introducing a next pointer in each tree node, pointing to the next node in the same level.
* Feature #4: Retrieve the stock increase and decrease percentages from the DOM tree and calculate the maximum profit we could obtain from it.

Understanding these feature requests and designing their solutions will help us implement the requested functionality into the scraper.

In the next few lessons, we’ll discuss the recommended implementations of these features. Before we start, think about how you would implement these features. As you do, you’ll realize some of the underlying problems that you’ll need to solve. The solutions to these basic problems are also applicable to other common coding interview questions.

## Feature #1: Traversing DOM Tree

## Description
First, we need to figure out a way to traverse the DOM structure that we obtain from a single web page. The HTML can be represented in a tree structure where the children of the HTML tag become the children of a node in the tree. Each level of the tree can have any number of nodes depending upon the number of nested HTML tags. We need to traverse the nodes in the tree level by level, starting at the root node.

![cale](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/cale/cale15.png)

We’ll be provided with a root node of an n-ary tree. The root node in our case will be the body tag. This root node will have the complete web page nested within its children. We have to return the values of each levels’ nodes from left to right in separate subarrays. This way we can separately analyze their content for further data processing.

Let’s try to understand this better with an illustration:

![cale](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/cale/cale16.png)

## Solution
Since we need to traverse all the nodes of each level before moving onto the next level, we can use the Breadth First Search (BFS) technique to solve this problem. We can use a queue to efficiently traverse in BFS fashion.

Let’s see how we might implement this functionality:
1. Start by enqueuing the root node to the queue.
2. Iterate until the queue is empty.
3. During each iteration, first count the elements in the queue (let’s call it queue_size). We will have this many nodes in the current level.
4. Next, remove queue_size nodes from the queue and enqueue their value in a list to represent the current level.
5. After removing each node from the queue, insert all of its children into the queue. If the queue is not empty, repeat from step 3 for the next level.

The following illustration might clarify this process.

![cale](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/cale/cale17.png)
![cale](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/cale/cale18.png)
![cale](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/cale/cale19.png)
![cale](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/cale/cale20.png)
![cale](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/cale/cale21.png)
![cale](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/cale/cale22.png)
![cale](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/cale/cale23.png)

Let’s look at the code for the solution:

{% highlight java %}
import java.util.*;

class TreeNode {
  String val;
  List<TreeNode> children;

  TreeNode(String x) {
    val = x;
    children = new ArrayList<>();
  }
};

class Solution {
  public static List<List<String>> traverse(TreeNode root) {
    List<List<String>> result = new ArrayList<List<String>>();
    if (root == null)
      return result;

    Queue<TreeNode> queue = new LinkedList<>();
    queue.offer(root);
    while (!queue.isEmpty()) {
      int levelSize = queue.size();
      List<String> currentLevel = new ArrayList<>(levelSize);
      for (int i = 0; i < levelSize; i++) {
        TreeNode currentNode = queue.poll();
        // add the node to the current level
        currentLevel.add(currentNode.val);
        // insert the children of current node in the queue
        queue.addAll(currentNode.children);

        // if (currentNode.left != null)
        //   queue.offer(currentNode.left);
        // if (currentNode.right != null)
        //   queue.offer(currentNode.right);
      }
      result.add(currentLevel);
    }

    return result;
  }

  public static void main(String[] args) {
    // Driver Code

    TreeNode root = new TreeNode("body");
    (root.children).add(new TreeNode("div"));
    (root.children).add(new TreeNode("h1"));
    (root.children).add(new TreeNode("div")); 
    (root.children.get(0).children).add(new TreeNode("h2"));
    (root.children.get(0).children.get(0).children).add(new TreeNode("ul"));
    (root.children.get(0).children).add(new TreeNode("h3"));
    (root.children.get(0).children.get(1).children).add(new TreeNode("a"));
    (root.children.get(0).children.get(1).children).add(new TreeNode("p"));
    (root.children.get(0).children.get(1).children).add(new TreeNode("table")); 
    (root.children.get(2).children).add(new TreeNode("p"));
    (root.children.get(2).children).add(new TreeNode("a"));
    (root.children.get(2).children).add(new TreeNode("p"));

    List<List<String>> result = traverse(root);
    System.out.println("Web nodes at each level: " + result);
  }
}
{% endhighlight %}

![cale](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/cale/cale24.png)

## Feature #2: Locating Stock Data

## Description
 Now, we need to identify which nodes of the website’s DOM tree contain the stock data. The data we are looking for is the dates on which a certain stock price went up or down. Identifying stock data in arbitrary HTML can be hard, so we’ll use the following technique.

Like the previous lesson we’ll traverse the DOM tree, assigning a score to nodes on how likely they are to be a date or a stock percentage based on the text inside of them. To make the process efficient, we also want to limit the DOM subtree that we are processing.

Here’s the scoring criteria for how likely a node is a date:
* A node whose text starts with a capital letter
* A node whose text ends in a number
* A node whose text contains the # symbol
* A node whose text is under ten characters

Here’s the scoring criteria for how likely a node is a stock percentage:
* A node whose text is short
* A node whose text contains a number
* A node whose text contains the + or - sign
* A node whose text contains the % sign

After this step, we’ll find two nodes: one node with a high date score and one with a high stock percentage score. We’ll calculate the LCA(Lowest Common Ancestor) of these two nodes. In most cases, the subtree of the LCA node will have all the dates and their respective stock percentages. This saves us time for searching the rest of the DOM tree.

Let’s try to understand this better with an illustration:

![cale](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/cale/cale25.png)
![cale](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/cale/cale26.png)

We’ll be provided with an n-ary tree in which each node will have a score associated with it. We’ll also be given two nodes representing the highest date and stock percentage scores. We have to find the LCA node of the provided two nodes inside the n-ary tree. Once the LCA node is found, we can easily extract the stock data from its sub-tree.

## Solution
Let’s say that our two identified nodes are a and b.

We can save the parent nodes of each node while traversing the tree. Then, we can store the parents of one of the nodes, say a, into a set. As we go from the node b towards the root, the first ancestor of b that we find in the set is the LCA. We can store the parent pointers in a dictionary for retrieval in constant time. For backtracking, we can use the set data structure.

Let’s see how we might implement this functionality:
1. First, we’ll traverse the tree starting from the root node.
2. Then, we’ll store the parent of each node in the dictionary until the nodes a and b are not found.
3. If the nodes a and b are found:
   * Traverse over the parents/ancestors of node a.
   * For each parent node, add it to the ancestors set.
4. Similarly, we will traverse through the ancestors of node b. If the ancestor is present in the ancestors set for a, this is the first ancestor common in between a and b (while traversing upwards), and this is the LCA node.

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
  public static int lowestCommonAncestor(TreeNode root, TreeNode a, TreeNode b) {
    Deque<TreeNode> stack = new ArrayDeque<>();

    Map<TreeNode, TreeNode> parent = new HashMap<>();

    parent.put(root, null);
    stack.push(root);

    while (!parent.containsKey(a) || !parent.containsKey(b)) {
      TreeNode node = stack.pop();

      // Save the parent pointers while iterating
      for (TreeNode child : node.children){
        parent.put(child, node);
        stack.push(child);
      }
    }

    Set<TreeNode> ancestors = new HashSet<>();

    while (a != null) {
      ancestors.add(a);
      a = parent.get(a);
    }

    // The first ancestor of b which appears in
    // a's ancestor set() is their lowest common ancestor.
    while (!ancestors.contains(b))
      b = parent.get(b);
    
    return b.val;
  }

  public static void main(String[] args){
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

    TreeNode a = root.children.get(0).children.get(1).children.get(2);
    TreeNode b = root.children.get(0).children.get(0).children.get(0);
    int LCA = lowestCommonAncestor(root, a, b);
    System.out.print("\"" + LCA + "\"" + " is the lowest common ancestor of the nodes " + "\"" + a.val + "\"" + " and " + "\"" + b.val + "\"");
  }

}
{% endhighlight %}

![cale](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/cale/cale27.png)

## Feature #3: Traversing DOM Tree II

## Description
The technique we used previously to traverse through the web tree used too much space. The number of web pages can be enormous, and traversing all of them will consume a lot of unnecessary space. Therefore, we have come up with a better approach in which we create a shadow tree for the DOM where each node has a pointer to the next node to its right on the same level. We’ll introduce an additional attribute, next, to our TreeNode structure. The next node will point to its immediate right node on the same level. If there is no right node to point, next will point to null. This next pointer will allow us to avoid the queue data structure that we used previously to traverse the tree, resulting in a space-efficient approach.

We’ll be provided with a root node of an n-ary tree. The root node in our case will again be the body tag. This root node will have the complete web page nested within its children. We have to go through each node and assign the next pointer to the node to its immediate right on the same level.

Let’s try to understand this better with an illustration:

![cale](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/cale/cale28.png)

## Solution
The tree structure that we get from the web is arbitrary, meaning a parent node can have any number of child nodes and the probability of a perfect tree is very low. So, we have no idea about the structure of the tree or its branches, and we want efficient access to all nodes that are on the same level.

If we are on a node N at a level L, we have access to all of its children on level L + 1. This is the perfect time to establish the children’s next pointers. If we decide to establish the next pointers after getting on level L + 1, there will be issues connecting the children of different parents. Therefore, we’ll only move down a level from a parent node when all of the children nodes have their next pointers established.

Let’s see how we might implement this functionality:
1. We will start our traversal from the root node. There is only one node at the first level whose next automatically points to null. So, we’ll not yet move to the next level but will first establish the next pointers of the children of the root node.
2. We now need to find the next level’s leftmost node to be the starting point for assigning the next pointers. The four candidate leftmost nodes for our varying tree structures are shown in the illustration to the right. After assigning the next pointers of each node for a level, the leftmost node will need to be updated for the next level.
3. We’ll also maintain a curr pointer that will be used to traverse current level’s nodes. Since the next pointers of the current level L were established on level L - 1, we can simply traverse these nodes like a linked list. For each curr node we traverse, we’ll update its children’s next pointers.
4. Now, we’ll use a prev pointer to establish the next pointers using the curr pointer. Initially, we’ll make it equal to the next level’s leftmost node. When the curr is updated, we assign prev.next to the first child of the curr if it exists. After this, the prev pointer is also updated to the same node, so the correct next pointer is assigned in the subsequent iterations.

![cale](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/cale/cale29.png)

Let’s look at the code for the solution:

{% highlight java %}
import java.util.*;

class TreeNode {
  String val;
  TreeNode next;
  List<TreeNode> children;

  TreeNode(String x) {
    val = x;
    next = null;
    children = new ArrayList<>();
  }
};

class Solution {

  public static TreeNode prev, leftmost;
  public static void processChild(TreeNode childNode) {
    if (childNode != null) {
        
      // If we found atleast one node on the new level,
      // setup its next pointer
      if (prev != null) {
        prev.next = childNode;
              
      } else {
        // It is the first node
        leftmost = childNode;
      }    
          
      prev = childNode; 
    }
  }
      
  public static TreeNode traversingDomTree(TreeNode root) {
      
    if (root == null) {
      return root;
    }

    leftmost = root;
    
    // Variable to keep track of nodes on the "current" level
    TreeNode curr = leftmost;
    
    // Traverse till last node
    while (leftmost != null) {
        
      // "prev" tracks the latest node on the "next" level
      // "curr" tracks the latest node on the current level
      prev = null;
      curr = leftmost;
      
      leftmost = null;
      
      // Iterate on the nodes of current level like a linked list
      while (curr != null) {
          System.out.println(curr.val);

        // Process all the children and update the prev
        // and leftmost pointers as necessary.
        for (TreeNode child : curr.children){
          processChild(child);
        }
        
        // Move onto the next node.
        curr = curr.next;
      }
    }
            
    return root ;
  }

  public static void main(String[] args) {
    // Driver Code

    TreeNode root = new TreeNode("body");
    (root.children).add(new TreeNode("div"));
    (root.children).add(new TreeNode("h1"));
    (root.children).add(new TreeNode("div")); 
    (root.children.get(0).children).add(new TreeNode("h2"));
    (root.children.get(0).children.get(0).children).add(new TreeNode("ul"));
    (root.children.get(0).children).add(new TreeNode("h3"));
    (root.children.get(0).children.get(1).children).add(new TreeNode("a"));
    (root.children.get(0).children.get(1).children).add(new TreeNode("p"));
    (root.children.get(0).children.get(1).children).add(new TreeNode("table")); 
    (root.children.get(2).children).add(new TreeNode("p"));
    (root.children.get(2).children).add(new TreeNode("a"));
    (root.children.get(2).children).add(new TreeNode("p"));

    TreeNode res = traversingDomTree(root);
  }
}
{% endhighlight %}

![cale](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/cale/cale30.png)

## Feature #4: Maximum Profit

## Description
We have now extracted the stock increase and decrease percentages over a number of consecutive days. This will be represented as an array of numbers, one for each consecutive day, holding the increase or decrease in stock price on the given day. We can use this data to find the maximum profit that could have been made for the given time period. Sometimes, the maximum profit might be negative, indicating a period of minimum loss. For simplicity and to avoid fractional values, we are rounding the increase and decrease percentages to their nearest value.

We’ll be provided with an array of positive and negative integers. The indexes will indicate the day number and the integer value will indicate the stock increase or decrease percentage on that day. We have to return the maximum value that can be obtained by adding the sub-array elements.

Let’s try to understand this better with an illustration:

![cale](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/cale/cale31.png)

## Solution
The basic idea is to scan the entire array and at each position find the maximum sum of the sub-array ending there. This is achieved by keeping a currentMax for the current array index and a globalMax.

Let’s see how we might implement this functionality:
1. Initialize a currentMax and a globalMax and assign them the first value of the array.
2. Traverse the array starting with the second element.
3. For each element, check whether currentMax is less than zero:
   * If it is less than zero, assign it the current element as its value
   * Otherwise, add the current element in the currentMax
4. Similarly, for each element check if globalMax is less than currentMax then assign globalMax equal to the value of currentMax

The following illustration might clarify this process.

![cale](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/cale/cale32.png)
![cale](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/cale/cale33.png)
![cale](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/cale/cale34.png)
![cale](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/cale/cale35.png)
![cale](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/cale/cale36.png)
![cale](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/cale/cale37.png)
![cale](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/cale/cale38.png)
![cale](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/cale/cale39.png)
![cale](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/cale/cale40.png)
![cale](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/cale/cale41.png)

Let’s look at the code for the solution:

{% highlight java %}
class Solution{
  public static int maxProfit(int[] A) {
    if (A.length < 1) {
      return 0;
    }

    int currMax = A[0];
    int globalMax = A[0];
    for (int i = 1; i < A.length; ++i) {

      if (currMax < 0)
        currMax = A[i];
      else
        currMax += A[i];

      if (globalMax < currMax)
        globalMax = currMax;
    }

    return globalMax;
  }
  
  public static void main(String[] args) {
    // Driver code
    
    int[] stocks = new int[]{-4, 2, -5, 1, 2, 3, 6, -5, 1};
    System.out.println("Maximum Profit: " + maxProfit(stocks) + "%");
  }
}  
{% endhighlight %}

![cale](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/cale/cale42.png)
