---
layout: default
title: Depth-first Search
parent: Algorithms
grand_parent: Data Structures and Algorithms
nav_order: 2
permalink: /data_structures/algorithms/depth_first_search
---
<div align="center" markdown="1">
Depth-first Search / Java resources / Tutorial

{: .fs-8 .fw-400 }
</div>

With a solid understanding of recursion under our belt, we are now ready to tackle one of the most useful techniques in coding interviews: Depth-first Search (DFS). We go as deep as we can to look for a value, and when there is nothing new to discover, we retrace our steps to find something new. To put it in a term we already know, the pre-order traversal of a tree is DFS. Let’s look at a simple problem of searching for a node in a binary tree whose value is equal to the target.

![dfs](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/dfs/dfs1.png)
![dfs](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/dfs/dfs2.png)
![dfs](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/dfs/dfs3.png)
![dfs](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/dfs/dfs4.png)
![dfs](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/dfs/dfs5.png)
![dfs](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/dfs/dfs6.png)
![dfs](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/dfs/dfs7.png)
![dfs](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/dfs/dfs8.png)
![dfs](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/dfs/dfs9.png)
![dfs](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/dfs/dfs10.png)
![dfs](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/dfs/dfs11.png)
![dfs](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/dfs/dfs12.png)
![dfs](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/dfs/dfs13.png)
![dfs](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/dfs/dfs14.png)
![dfs](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/dfs/dfs15.png)
![dfs](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/dfs/dfs16.png)

Being able to visualize recursion and call stack of a DFS function in your mind is extremely important. Please take a minute to make sure you internalize it and come back to this page anytime you need to look at it.

The example above also introduces two other concepts: backtracking and divide and conquer. The action of retracing steps is called backtracking (e.g. from 2 we first visited 3 depth-first and retraced back and visit the other child 4). Backtracking and DFS are similar concepts and essentially the same thing since in DFS you always “backtrack” after exploring a deeper node. It’s like saying I program computers by doing coding. If we really want to make the distinction, then backtracking is the concept of retracing and DFS is the algorithm that implements it. In computer science textbooks[1, 2, 3], backtracking is often mentioned and associated with combinatorial search problems. We will do the same in this course.

We have two recursive calls dfs(root.left) and dfs(root.right) and return based on results from the recursive calls. This is also a divide and conquer algorithm, i.e. splitting into sub-problems of the same type (search in left and right children) until they are simple enough to be solved directly (null nodes or found target) and combining the results from these sub-problems (return non-null node). We’ll investigate divide and conquer more in a later module.

When to use DFS#
Tree#
DFS is essentially pre-order tree traversal.

Traverse and find/create/modify/delete node
Traverse with return value (finding max subtree, detect balanced tree)
Combinatorial problems#
DFS/backtracking and combinatorial problems are a match made in heaven (or silver bullet and werewolf 😅). As we will see in the Combinatorial Search module, combinatorial search problems boil down to searching in trees.

How many ways are there to arrange something
Find all possible combinations of …
Find all solutions to a puzzle
Graph#
Trees are special graphs that have no cycle. We can still use DFS in graphs with cycles. We just have to record the nodes we have visited and avoid re-visiting them and going into an infinite loop.

Find a path from point A to B
Find connected components
Detect cycles

DFS on a Tree: Introduction

Think like a node#
The key to solving tree problems using DFS is to think from the perspective of a node instead of looking at the whole tree. This is in line with how recursion is written. Reason from a node’s perspective, make sure you consider all the cases, and let recursion take care of the rest. Provided you have a good understanding of the problem at hand, there are two things you want to think about:

1. Return value#
What do we want to return after visiting a node? For example, for the max depth problem, this is the max depth for the current node’s subtree. If we are looking for a node in the tree, we’d want to return that node if found, else return null. Use the return value to pass information from children to parent.

2. Identify states#
What states do we need to maintain to compute the return value for the current node? For example, to know if the current node’s value is larger than its parent we have to maintain the parent’s value as a state. State becomes DFS’s function arguments. Use states to pass information from parent to children.

The common template for DFS on tree is:

{% highlight java %}

def dfs(root, state):
    if not root:
        ...
        return 

    left = dfs(root.left, state)
    right = dfs(root.right, state)
      
        ...

    return ...
{% endhighlight %}

The time complexity of depth-first search on trees is O(N)O(N) since each node is visited once.

This may sound abstract at the moment. Let’s do a couple of concrete problems.

The Max Depth of Binary Tree

The max depth of a binary tree is the longest root-to-leaf path. Given a binary tree, find its max depth.

Example#

![dfs](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/dfs/dfs17.png)

Explanation#
1. Decide on the return value#
The problem asks for the total max depth, so we return the depth for the current subtree after we visit a node.

2. Identify states#
To decide the depth of the current node, we only need depth from its children and don’t need any additional state.

Having decided on the state and return value, we can now write the DFS.

The time complexity is O(N)O(N) since each node is visited once.

{% highlight java %}

class Node {
    int val;
    Node left, right;

    public Node(int val) {
        this.val = val;
    }

    public static Node buildTree(Iterator<String> iter) {
        String nxt = iter.next();
        if (nxt.equals("x")) return null;
        Node node = new Node(Integer.parseInt(nxt));
        node.left = buildTree(iter);
        node.right = buildTree(iter);
        return node;
    }
}
class Solution {
    public static int getMaxTreeDepth(Node root) {
        // Null node adds no depth
        if (root == null) return 0;
        // Depth of current node's subtree = max depth of the two subtrees + 1 provided by current node
        return Math.max(getMaxTreeDepth(root.left), getMaxTreeDepth(root.right)) + 1;
    }

    // Driver code  
	public static void main(String[] args) {

		String[] inputs ={"5 4 3 x x 8 x x 6 x x", "1 x x", "x", "6 x 9 x 11 x 7 x x"};
        int[] expected_outputs = {3, 1, 0, 4};
		for (int i = 0; i<inputs.length; i++) {
			Node root = Node.buildTree(Arrays.stream(inputs[i].split(" ")).iterator());
			System.out.println("Get map tree depth " + Solution.getMaxTreeDepth(root));
		}
	}
}
{% endhighlight %}

## Visible Tree Node

In a binary tree, a node is considered “visible” if no node on the root-to-itself path has a greater value. The root is always “visible” since there are no other nodes between the root and itself. Given a binary tree, count the number of “visible” nodes.

Example#

![dfs](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/dfs/dfs18.png)

Explanation#
We can perform DFS on the tree and keep track of the max value as we go.

1. Decide on the return value#
The problem asks for the total number of visible nodes, so we return the total number of visible nodes for the current subtree after we visit a node.

2. Identify states#
The definition for a “visible” node is the following: its value is greater than any other node’s value on the root-to-itself path. To determine whether the current node is visible or not, we need to know the max value from the root to it. We can carry this as a state as we traverse down the tree.

The time complexity is O(N)O(N) since each node is visited once.

Having decided on the state and return value, we can now write the DFS.

{% highlight java %}

class Node {
    int val;
    Node left, right;

    public Node(int val) {
        this.val = val;
    }

    public static Node buildTree(Iterator<String> iter) {
        String nxt = iter.next();
        if (nxt.equals("x")) return null;
        Node node = new Node(Integer.parseInt(nxt));
        node.left = buildTree(iter);
        node.right = buildTree(iter);
        return node;
    }
}

class Solution {
    public static int countVisibleNodes(Node root) {
        // Start maxSoFar with smallest integer value possible so any value root has is smaller than it
        return dfs(root, Integer.MIN_VALUE);
    }
    private static int dfs(Node root, int maxSoFar) {
        if (root == null) return 0;
        int total = 0;
        if (root.val >= maxSoFar) {
            total++;
        }
        // maxSoFar of the child node is the larger value of previous max and current node val
        total += dfs(root.left, Math.max(maxSoFar, root.val));
        total += dfs(root.right, Math.max(maxSoFar, root.val));

        return total;
    }
    // Driver code
    public static void main(String[] args) {     
	    String[] inputs ={"5 4 3 x x 8 x x 6 x x", "-100 x -500 x -50 x x", "9 8 11 x x 20 x x 6 x x"};
        int[] expected_outputs = {3, 2, 3};
        for(int i = 0; i < inputs.length; i++) {
            Node root = Node.buildTree(Arrays.stream(inputs[i].split(" ")).iterator());
            System.out.println("Visible tree node : "+Solution.countVisibleNodes(root));
        }
    }
}
{% endhighlight %}

## Lowest Common Ancestor

## Problem statement

The lowest common ancestor (LCA) of two nodes v and w in a tree is the lowest (i.e. deepest) node that has both v and w as descendants. We also define each node to be a descendant of itself, so if v has a direct connection from w, w is the lowest common ancestor.

Given two nodes of a binary tree, find their lowest common ancestor.

Explanation#
Intuition#
When we think as a node, there could be five scenarios of how we are relative to the LCA and two target nodes.

![dfs](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/dfs/dfs19.png)
![dfs](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/dfs/dfs20.png)

Current node is the LCA:

One target node is on the left subtree and the other target node is on the right subtree, so the current node itself is the LCA.
Current node is one of the targets and the other node is in a subtree.
Current node is not the LCA:

Current node is not a target node and its subtrees have no target node.
Current node is in the path between the LCA and a target node in case 2.
LCA is in the subtree of the current node.
1. Decide on the return value#
To return the LCA to the root, we obviously have to return it after we find it. If the current node is not the LCA, we also have to return the information back to the parent. If the current node is one of the target nodes, we return it. Otherwise, we return null.

2. Identify states#
To decide whether the current node is the LCA, we need to know which of the above scenarios we are in. We can determine that from the return value of subtrees. Therefore, no states are needed!

The time complexity is O(N)O(N).

Having decided on the state and return value, we can now write the DFS.

{% highlight java %}

class Solution {
    public static Node lca(Node root, Node node1, Node node2) {
        if (root == null) return null;

        // case 2 in above figure
        if (root.equals(node1) || root.equals(node2)) return root;
        Node left = lca(root.left, node1, node2);
        Node right = lca(root.right, node1, node2);

        // case 1
        if (left != null && right != null) return root;

        // at this point, left and right can't be both non-null
        // case 4 and 5, report target node or LCA back to parent
        if (left != null) return left;
        if (right != null) return right;

        // case 4, not found return null
        return null;
    }
    // Driver code  
	public static void main(String[] args) {

        String[] inputs ={"6 4 3 x x 5 x x 8 x x", "6 4 3 x x 5 x x 8 x x", "6 4 3 x x 5 x x 8 x x", "x"};
        int[] inputs1 ={4, 4, 3, 3};
        int[] inputs2 ={8, 6, 5, 2};
		for (int i = 0; i<inputs.length; i++) {
			Node root = Node.buildTree(Arrays.stream(inputs[i].split(" ")).iterator());
            Node node1 = Node.findNode(root, inputs1[i]);
            Node node2 = Node.findNode(root, inputs2[i]);
            Node actual_output = Solution.lca(root, node1, node2);
			System.out.println("Lowest common ancestor : " + Node.getValue(actual_output));
		}
	}
}
// Driver code
class Node {
    int val;
    Node left, right;

    public Node(int val) {
        this.val = val;
    }

    public static Node buildTree(Iterator<String> iter) {
        String nxt = iter.next();
        if (nxt.equals("x")) return null;
        Node node = new Node(Integer.parseInt(nxt));
        node.left = buildTree(iter);
        node.right = buildTree(iter);
        return node;
    }

    public static Node findNode(Node root, int target) {
        if (root == null) return null;
        if (root.val == target) return root;
        Node leftSearch = findNode(root.left, target);
        if (leftSearch != null) {
            return leftSearch;
        }
        return findNode(root.right, target);
    }

    public static boolean compareNode(Node root, String target){
      if (root == null) return "null" == target;
      if (Integer.toString(root.val) == target) return true;
      return false;
    }
    public static String getValue(Node root){
      if (root == null) return "null";
      return String.valueOf(root.val);
    }
}
{% endhighlight %}

