---
layout: default
title: Trees
parent: Coding Interview
has_children: true
nav_order: 20
permalink: /coding_interview/trees
---
<div align="center" markdown="1">
Trees / Java resources / Tutorial

{: .fs-8 .fw-400 }
</div>

## Trees

## Invert Binary Tree

## Description
In this lesson, your task is to invert a given a binary tree, T.

Let’s look at an example below:

![tree](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/tree/tree1.png)
![tree](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/tree/tree2.png)

## Solution
We can solve this problem using depth-first search (DFS).

The inverse of an empty tree is the empty tree. To invert tree T with root and subtrees left and right, we keep root the same and invert the right and left subtrees.

Let’s review the implementation below:

{% highlight java %}
public class TreeNode {
    public int val;
    public TreeNode left;
    public TreeNode right;
    public TreeNode() {}
    public TreeNode(int val) { this.val = val; }
    public TreeNode(int val, TreeNode left, TreeNode right) {
          this.val = val;
          this.left = left;
          this.right = right;
    }
}

class Solution {
    public static TreeNode invertTree(TreeNode root) {
        if (root == null) {
        return root;
    }
        TreeNode right = invertTree(root.right);
        TreeNode left = invertTree(root.left);
        root.left = right;
        root.right = left;
        return root;
    }
    public static void main(String args[]){
        TreeNode root = new TreeNode(1);
        root.left = new TreeNode(2);
        root.right = new TreeNode(3);
        root.left.left = new TreeNode(4);
        root.left.right = new TreeNode(5);

        root.right.left = new TreeNode(6);
        root.right.right = new TreeNode(7);
        Utility.print(invertTree(root));
    }
}
{% endhighlight %}

![tree](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/tree/tree3.png)

## Flip Equivalent Binary Trees

## Description
Let’s start by defining what a flip operation for a binary tree is. We can define it as:

“Choosing any node and swapping the right and left child subtrees.”

A binary tree, T, is flip equivalent to another binary tree, S, if we can make T equal to S after some number of flip operations.

Given the roots of two binary trees, root1 and root2, you have to find out whether the trees are flip equivalent to each other or not. The flipEquiv function should return True if the binary trees are equivalent. Otherwise, it will return False.

## Example
Let’s look at the example below:

![tree](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/tree/tree4.png)

## Solution
We implement the flipEquiv function using recursion. Like any recursive function, we start by defining the base conditions. We have two base conditions:
1. If root1 or root2 is null, they are equivalent if and only if they are both null.
2. If root1 and root2 have different values, they aren’t equivalent.

Lastly, we move on to the recursive part and check whether the children of root1 are equivalent to the children of root2. We pair the children in two different ways:
1. Compare the left subtree of root1 with the left subtree of root2 and the right subtree of root1 with the right subtree of root2.
2. Compare the left subtree of root1 with the right subtree of root2 and the right subtree of root1 with the left subtree of root2.

{% highlight java %}
public class TreeNode {
      public int val;
      public TreeNode left;
      public TreeNode right;
      public TreeNode() {
      }
      public TreeNode(int val) { 
          this.val = val; 
      }
      public TreeNode(int val, TreeNode left, TreeNode right) {
          this.val = val;
          this.left = left;
          this.right = right;
      }
}

class Solution {
    public static boolean flipEquiv(TreeNode root1, TreeNode root2) {
        if (root1 == null && root2 == null)
            return true;
        if (root1 == null || root2 == null || root1.val != root2.val)
            return false;

        return (flipEquiv(root1.left, root2.left) && flipEquiv(root1.right, root2.right) ||
                flipEquiv(root1.left, root2.right) && flipEquiv(root1.right, root2.left));
    }

    public static void main( String args[] ) {
        TreeNode root1 = null;
        TreeNode root2 = null;
        System.out.println(flipEquiv(root1, root2));

        root1 = new TreeNode(1);
        root1.right = new TreeNode(3);
        root1.left = new TreeNode(2);
        root1.right.left = new TreeNode(6);
        root1.right.right = new TreeNode(9);
        root1.left.left = new TreeNode(4);
        root1.left.right = new TreeNode(5);
        root1.left.right.left = new TreeNode(7);
        root1.left.right.right = new TreeNode(8);

        root2 = new TreeNode(1);
        root2.left = new TreeNode(3);
        root2.right = new TreeNode(2);
        root2.left.right = new TreeNode(6);
        root2.left.left = new TreeNode(9);
        root2.right.left = new TreeNode(4);
        root2.right.right = new TreeNode(5);
        root2.right.right.right = new TreeNode(7);
        root2.right.right.left = new TreeNode(8);

        System.out.println(flipEquiv(root1, root2));

        TreeNode root3 = new TreeNode(1);
        root3.right = new TreeNode(4);
        root3.left = new TreeNode(3);

        TreeNode root4 = new TreeNode(1);

        System.out.println(flipEquiv(root3, root4));
    }
}
{% endhighlight %}

![tree](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/tree/tree5.png)

## Binary Tree Maximum Path Sum

## Description
A path in a binary tree is defined as:

A sequence of nodes such that each pair of adjacent nodes must have an edge connecting them. A node can only be included in a path at most once. Moreover, including the root in the path is not compulsory.

The path sum can be calculated by adding up all nodes’ values in the path. To solve this problem, we will calculate the maximum path sum given the root of a binary tree so that there won’t be any greater path than it in the tree.

## Example
Let’s discuss the example below:

![tree](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/tree/tree6.png)
![tree](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/tree/tree7.png)

## Solution
We’ll start by simplifying the problem and looking at the implementation of the maxContrib(node) function which takes a node as an argument and computes a maximum contribution that this node and one or none of its subtrees can add.

For example:

![tree](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/tree/tree8.png)
![tree](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/tree/tree9.png)
![tree](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/tree/tree10.png)
![tree](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/tree/tree11.png)
![tree](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/tree/tree12.png)
![tree](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/tree/tree13.png)
![tree](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/tree/tree14.png)

Now, if we are sure that the root is also included in the maximum path, the problem can be solved using maxContrib(root), and then adding both the maxContrib of the left child if its greater than zero, and same for the right child. Unfortunately, this isn’t always the case, and maximum path can exclude root. Therefore, we need to make a few additions to the solution to check whether to continue with the current path or to start a new path with the current node as the highest node at each step.

First, we need to initialize a maxSum as a global variable of negative infinity.

We’ll start by calling maxContrib with root as its parameter.

Second, we need to implement the maxContrib(node) function with a check to decide whether to continue with the old path or start a new path. Here’s how we will implement it:
1. This is a recursive function, so the base case states that the maxContrib is 0 if the node is null.
2. Call maxContrib recursively for the node’s children to calculate the max gain for the left and right subtrees. We also need to check if this value is greater than zero or not to avoid adding any negative values.
3. Now, check whether to continue with the old path or start a new path. To start a new path, the sum of this path will be node.val + leftSubtree + rightSubtree. Update maxSum if it’s better to start a new path.
4. We will return the max gain to the node, and one or none of its subtrees can be added to the current path: node.val + max(leftSubtree, rightSubtree).

{% highlight java %}
public class TreeNode {
  int val;
  TreeNode left;
  TreeNode right;

  TreeNode(int x) {
    val = x;
  }
}

class Solution {
  static int max_sum = Integer.MIN_VALUE;

  public static int maxContrib(TreeNode node) {
    int leftSubtree = 0;
    int rightSubtree = 0;
    
    if (node == null) 
      return 0;

    // max sum on the left and right sub-trees of node
    if (maxContrib(node.left) > 0)
      leftSubtree = maxContrib(node.left);

    if (maxContrib(node.right) > 0)
      rightSubtree = maxContrib(node.right);

    // the price to start a new path where `node` is a highest node
    int price_newpath = node.val + leftSubtree + rightSubtree;

    // update maxSum if it's better to start a new path
    max_sum = Math.max(max_sum, price_newpath);

    // for recursion :
    // return the max contribution if continue the same path
    return node.val + Math.max(leftSubtree, rightSubtree);
  }

  public static int maxPathSum(TreeNode root) {
    maxContrib(root);
    int temp = max_sum;
    max_sum = Integer.MIN_VALUE;
    return temp;
  }

  public static void main( String args[] ) {
    TreeNode root = new TreeNode(-8);

    root.left = new TreeNode(2);
    root.right = new TreeNode(17);
    root.left.left = new TreeNode(1);
    root.left.right = new TreeNode(4);
    root.right.left = new TreeNode(19);
    root.right.right = new TreeNode(5);

    System.out.println(maxPathSum(root));

    TreeNode root2 = new TreeNode(7);

    root2.left = new TreeNode(3);
    root2.right = new TreeNode(4);
    root2.right.left = new TreeNode(-1);
    root2.right.right = new TreeNode(-3);

    System.out.println(maxPathSum(root2));
  }
}
{% endhighlight %}

![tree](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/tree/tree15.png)

## Binary Tree Zigzag Level Order Traversal

## Description
Given a binary tree T, you have to find its nodes’ zigzag level order traversal. The zigzag level order traversal corresponds to traversing nodes from left to right and then right to left for the next level, alternating between.

You have to return the element in each level in a two-dimensional array.

Let’s look at an example:

![tree](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/tree/tree16.png)
![tree](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/tree/tree17.png)
![tree](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/tree/tree18.png)
![tree](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/tree/tree19.png)

## Solution
As per the problem statement, we need to traverse the tree in a level-by-level zigzag order. An intuitive approach for this problem would be to use Breadth-First Search (BFS). By default, BFS provides ordering from left to right within a single level.

We will need to modify BFS a little to get our desired output, a zigzagzigzag order. We can maintain a dequedeque (double-ended queue) data structure to add elements at both ends.

For each level, we alternate between first-in-first-out (FIFO) and last-in-first-out (LIFO). To ensure FIFO ordering, we append new elements to the deque’s tail. For LIFO, we append the new elements to the head of the deque.

Let’s review the steps to implement the solution:
1. Initially, add the root of the tree to the deque and initialize the order flag reverse to alternate between LIFO and FIFO.
2. Iterate over the deque as long as it is not empty—the outer loop iterates over each level of the tree.
3. For each level, append an array to the results array.
4. Iterate over the elements for a single level in a nested manner.
5. Pop the deque from the back or front on an alternate basis. Append the current node’s value to the last element of the 2d results array.
6. Alternate between the order by appending nodes to the front or back of the deque.

![tree](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/tree/tree20.png)
![tree](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/tree/tree21.png)
![tree](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/tree/tree22.png)
![tree](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/tree/tree23.png)
![tree](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/tree/tree24.png)
![tree](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/tree/tree25.png)
![tree](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/tree/tree26.png)
![tree](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/tree/tree27.png)
![tree](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/tree/tree28.png)
![tree](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/tree/tree29.png)
![tree](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/tree/tree30.png)
![tree](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/tree/tree31.png)
![tree](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/tree/tree32.png)
![tree](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/tree/tree33.png)
![tree](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/tree/tree34.png)

{% highlight java %}
public class TreeNode {
    public int val;
    public TreeNode left;
    public TreeNode right;
    public TreeNode() {}
    public TreeNode(int val) { this.val = val; }
    public TreeNode(int val, TreeNode left, TreeNode right) {
          this.val = val;
          this.left = left;
          this.right = right;
    }
}

class Solution {
    public static List<List<Integer>> zigzagLevelOrder(TreeNode root) {
      if (root == null) {
        return new ArrayList<List<Integer>>();
      }
      Deque<TreeNode> dq = new LinkedList<TreeNode>();
      dq.add(root);
      List<List<Integer>> results = new ArrayList<List<Integer>>();
      // To iterate the tree in a zigzag order
      boolean reverse = false;
      while(!dq.isEmpty()){
        int size = dq.size();
        results.add(new ArrayList<Integer>());
        for(int i = 0; i < size; i++){
            if(!reverse){
                TreeNode node = dq.pollFirst();
                results.get(results.size() - 1).add(node.val);
                if(node.left != null)  dq.addLast(node.left);
                if(node.right != null)  dq.addLast(node.right);
            }
            else{
                TreeNode node = dq.pollLast();
                results.get(results.size() - 1).add(node.val);
                if(node.right != null)  dq.addFirst(node.right);
                if(node.left != null)  dq.addFirst(node.left);                   
            }
        }
        // Alternate between left and right
        reverse = !reverse;
      }
      return results;
    }

    public static void main(String args[]){
        TreeNode root = new TreeNode(3);
        root.right = new TreeNode(9);
        root.left = new TreeNode(6);
        root.right.left = new TreeNode(15);
        root.right.right = new TreeNode(12);
        System.out.println(zigzagLevelOrder(root));
    }
}
{% endhighlight %}

![tree](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/tree/tree35.png)

## Binary Tree Right Side View

## Description
You are given a binary tree T. Imagine you are standing to the right of it; you have to return the value of the nodes you can see from top to bottom.

You have to return the rightmost nodes on their respective levels in the form of an array.

Let’s discuss an example below:

![tree](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/tree/tree36.png)

## Solution
We can use a depth-first search (DFS) to solve this problem. The intuition here is to traverse the tree level by level recursively, starting from the rightmost node for each recursive call.

Let’s review the implementation below:

{% highlight java %}
public class TreeNode {
    public int val;
    public TreeNode left;
    public TreeNode right;
    public TreeNode() {}
    public TreeNode(int val) { this.val = val; }
    public TreeNode(int val, TreeNode left, TreeNode right) {
          this.val = val;
          this.left = left;
          this.right = right;
    }
}

class Solution {    
    public static void DFS(TreeNode node, int level, List<Integer> rightside) {
        if (level == rightside.size()) 
            rightside.add(node.val);
        
        if (node.right != null) 
            DFS(node.right, level + 1, rightside);  
        if (node.left != null) 
            DFS(node.left, level + 1, rightside);
    }    
    
    public static List<Integer> rightSideView(TreeNode root) {
        List<Integer> rightside = new ArrayList<Integer>();

        if (root == null) return rightside;
        DFS(root, 0, rightside);
        return rightside;
    }

    public static void main(String args[]){
        TreeNode root = new TreeNode(1);
        root.left = new TreeNode(2);
        root.right = new TreeNode(3);
        root.left.left = new TreeNode(4);
        root.left.right = new TreeNode(5);

        root.right.left = new TreeNode(6);
        root.right.right = new TreeNode(7);
        root.right.right.left = new TreeNode(8);
        System.out.println("" + rightSideView(root));
    }
}
{% endhighlight %}

![tree](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/tree/tree37.png)

## Binary Tree Vertical Order Traversal

## Description
The goal is to find the binary tree vertical order traversal of the binary tree when the root of this binary tree is given. In other words, you have to return the values of the nodes from top to bottom in each column, column by column from left to right. If there is more than one node in the same column and row, return the values from left to right. Let’s go over some examples:

![tree](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/tree/tree38.png)
![tree](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/tree/tree39.png)

## Solution
The solution we will implement follows a breadth-first search. The intuition behind BFS is that it guarantees that nodes at the top will be visited first and the nodes at the bottom will be visited last. As for the traversal of the tree from left to right, we need to maintain a HashMap that contains the list of all the nodes in a specific column. We will denote these columns by their index, where the column of the root will be index 0, the columns on the left side of the root will have a negative index, and the columns on the right side of the root will have a positive index. The index of each column will be a key.

We also need to store the value of the minimum and maximum indexes in two variables, so we can iterate over the indices to get the nodes in the right order.

Let’s go over the algorithm in detail:
1. We need to create a HashMap called nodesList in which the key will be the index of the column and the value will be the list of nodes in that column.
2. We initialize two variables to store the minimum and maximum values of the index.
3. During BFS, we also maintain a queue to keep track of the order of nodes that need to be visited. We will initialize the queue by adding the root to it along with the column index of the root, which is 0.
4. Next, we carry out BFS using a loop until the queue is empty. In the loop, we iterate over the values of the queue, and we pop the values in the queue. The values in the queue consist of a node and the index of the column.
5. If the queue contains a node that is not null, we add the value of the node to nodesList along with the index of the column. We also keep updating the minimum and maximum values of the index. Then, we append the children of this node to the queue with their index values; the left child has an index value of the current index - 1 and the right child has a value of the current index + 1.
6. At the end of all the iterations, the nodesList HashMap contains the values of all the nodes in all the columns, but the values of each column are not in the correct order.
7. After BFS, we will iterate over the index range using the variables that stored the minimum and maximum indexes. Finally, we return the values of the nodes in the correct order.

![tree](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/tree/tree40.png)
![tree](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/tree/tree41.png)
![tree](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/tree/tree42.png)
![tree](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/tree/tree43.png)
![tree](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/tree/tree44.png)
![tree](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/tree/tree45.png)
![tree](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/tree/tree46.png)
![tree](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/tree/tree47.png)

{% highlight java %}
public class TreeNode {
  int val;
  TreeNode left;
  TreeNode right;

  TreeNode(int x) {
    val = x;
  }
}

import java.util.*;

class Solution {
  @SuppressWarnings("unchecked")
  public static List<List<Integer>> verticalOrder(TreeNode root) {
    List<List<Integer>> output = new ArrayList<List<Integer>>();
    if (root == null) {
      return output;
    }

    Map<Integer, ArrayList<Integer>> columnTable = new HashMap<Integer, ArrayList<Integer>>();
    // Map of node and its column offset
    Queue<Map.Entry<TreeNode, Integer>> queue = new ArrayDeque<>();
    int column = 0;
    queue.offer(new AbstractMap.SimpleEntry(root, column));

    int minColumn = 0;
    int maxColumn = 0;

    while (!queue.isEmpty()) {
      Map.Entry<TreeNode, Integer> p = queue.poll();
      root = p.getKey();
      column = p.getValue();

      if (root != null) {
        if (!columnTable.containsKey(column)) {
          columnTable.put(column, new ArrayList<Integer>());
        }
        columnTable.get(column).add(root.val);
        minColumn = Math.min(minColumn, column);
        maxColumn = Math.max(maxColumn, column);

        queue.offer(new AbstractMap.SimpleEntry(root.left, column - 1));
        queue.offer(new AbstractMap.SimpleEntry(root.right, column + 1));
      }
    }

    for(int i = minColumn; i < maxColumn + 1; ++i) {
      output.add(columnTable.get(i));
    }

    return output;
  }

  
  public static void main( String args[] ) {
    TreeNode root = new TreeNode(7);

    root.left = new TreeNode(11);
    root.right = new TreeNode(6);
    root.left.left = new TreeNode(13);
    root.left.right = new TreeNode(8);
    root.right.left = new TreeNode(19);
    root.right.right = new TreeNode(5);

    
    System.out.println(verticalOrder(root));

    // TreeNode root2 = new TreeNode(7);

    // root2.left = new TreeNode(3);
    // root2.right = new TreeNode(4);
    // root2.right.left = new TreeNode(-1);
    // root2.right.right = new TreeNode(-3);

    // System.out.println(maxPathSum(root2));
  }
}
{% endhighlight %}

![tree](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/tree/tree48.png)

## Boundary of Binary Tree

## Description
Let’s start by defining what a boundary of a binary tree is. We can define it as:

The boundary of a binary tree is the concatenation of the root, the left boundary, the leaves ordered from left-to-right, and the reverse order of the right boundary. Take a look at the example given below:

Take a look at the example given below:

![tree](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/tree/tree49.png)

As mentioned above, the boundary can be divided into four categories; the following explains these categories:

## Root node

## Left boundary
* The root node’s left child is in the left boundary. If the root does not have a left child, the left boundary is empty.
* If a node in the left boundary has a left child, the left child is in the left boundary.
* If a node in the left boundary has a right child but no left child, the right child is in the left boundary.
* The leftmost leaf is not in the left boundary.

## Right boundary
* The right boundary is similar to the left boundary, except it is on the right side of the root's right subtree.
* The leaf is not part of the right boundary.
* The right boundary is empty if the root does not have a right child.

## Leaves
* The leaves are nodes that do not have any children. For this problem, we can assume that the root is not a leaf.

Considering the definition of the boundary of a binary tree, implement a function that returns the boundary when the root of a binary tree is given as input.

## Solution
We can divide this problem into subproblems and solve each of them independently. We will implement separate functions for finding the left boundary, right boundary, and leaves. Let’s take a look at the complete algorithm:
* First, we will add the root node to the output.
* Then, we will use a recursive helper function called leftboundary() to find the leftmost nodes of the tree. In this function, we will recursively traverse the tree towards the left and keep adding the nodes in the output array. If at any point we can’t find the left child of a node, but its right child exists, we will traverse the right child. We reach the base when we encounter a leaf node.
* Then, to find all the leaf nodes, we will use a recursive helper function called leaves(). This function will use the pre-order traversal to traverse the complete tree. At each node, it will check if the current node is a leaf or not.
* Lastly, for the right boundary, we will use a recursive helper function called rightboundary() to find the tree’s rightmost nodes. This function’s implementation is very similar to the leftboundary() function if we just swap the left subtree with the right one. However, an important thing to note is that we want the right boundary in reverse order. For this, we will add the node to the output after the recursive calls. This way, we will use the system stack to print the results in reverse order.

{% highlight java %}
public class TreeNode {
    public int val;
    public TreeNode left;
    public TreeNode right;
    public TreeNode() {}
    public TreeNode(int val) { this.val = val; }
    public TreeNode(int val, TreeNode left, TreeNode right) {
          this.val = val;
          this.left = left;
          this.right = right;
    }
}

class Solution {
    public static void leftBoundary(TreeNode node, List<Integer> boundary){
        if (node == null || (node.left == null && node.right == null))
            return;
        boundary.add(node.val);
        if (node.left != null)
            leftBoundary(node.left, boundary);
        else
            leftBoundary(node.right, boundary);
    }

    public static void leaves(TreeNode node, TreeNode root, List<Integer> boundary){
        if (node == null){
            return;
        }
        leaves(node.left, root, boundary);
        if (node != root && node.left == null && node.right == null)
            boundary.add(node.val);
        leaves(node.right, root, boundary);
    }

    public static void rightBoundary(TreeNode node, List<Integer> boundary){
        if (node == null || (node.left == null && node.right == null))
            return;
        if (node.right != null)
            rightBoundary(node.right, boundary);
        else
            rightBoundary(node.left, boundary);
        boundary.add(node.val);
    }
    public static List<Integer> boundary(TreeNode root){
        List<Integer> boundary = new ArrayList<Integer>();
        if (root == null)
            return boundary;
        boundary.add(root.val);
        leftBoundary(root.left, boundary);
        leaves(root, root, boundary);
        rightBoundary(root.right, boundary);
        return boundary;
    }
    public static void main(String args[]) {
        // Driver Code
        TreeNode bt = new TreeNode(1);
        bt.left = new TreeNode(2);
        bt.left.left = new TreeNode(3);
        bt.left.right = new TreeNode(4);
        bt.left.right.left = new TreeNode(5);
        bt.right = new TreeNode(6);
        bt.right.left = new TreeNode(7);
        bt.right.left.right = new TreeNode(9);
        bt.right.right = new TreeNode(8);
        bt.right.right.right = new TreeNode(10);
        System.out.println(boundary(bt));
    }
}
{% endhighlight %}

![tree](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/tree/tree50.png)