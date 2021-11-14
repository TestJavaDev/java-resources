---
layout: default
title: Breadth-first Search on Trees
parent: Algorithms
grand_parent: Data Structures and Algorithms
nav_order: 4
permalink: /data_structures/algorithms/breadth_first_search_on_trees
---
<div align="center" markdown="1">
Breadth-first Search on Trees / Java resources / Tutorial

{: .fs-8 .fw-400 }
</div>

## Breadth-first search on trees

Hopefully, by this time, you’ve drunk enough DFS kool-aid to understand its immense power and seen enough visualization to create a call stack in your mind. Now let’s look at the companion spell: breadth-first search (BFS). The names are self-explanatory. While depth-first search reaches for depth-first (child nodes) before breadth (nodes in the same level/depth), breadth-first search visits all nodes in a level before starting to visit the next level.

While DFS uses recursion/stack to keep track of progress, BFS uses a queue (First In First Out). When we dequeue a node, we enqueue its children.

![bfs](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/bfs/bfs1.png)
![bfs](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/bfs/bfs2.png)
![bfs](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/bfs/bfs3.png)
![bfs](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/bfs/bfs4.png)
![bfs](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/bfs/bfs5.png)
![bfs](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/bfs/bfs6.png)
![bfs](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/bfs/bfs7.png)
![bfs](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/bfs/bfs8.png)
![bfs](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/bfs/bfs9.png)
![bfs](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/bfs/bfs10.png)
![bfs](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/bfs/bfs11.png)

## DFS vs BFS

A question naturally arises: which one should I use? Or more fundamentally, which tasks do they each excel at? Complexity-wise they are both O(N)O(N) since each node is visited once during the tree traversal. The differences come from the different order of traversal.

DFS is better at:
* Narrow but deep trees
* Finding nodes far away from the root

BFS is better for:
* Shallow but wide trees
* finding nodes close/closest to the root

## Template
We can implement BFS using a queue. Important things to remember:
* We need at least one element to kick start the process.
* Right after we dequeue an element, we’d want to enqueue its children if there are any.
{% highlight java %}

from collections import deque

def bfs_by_queue(root):
    queue = deque([root]) # at least one element in the queue to kick start bfs
    while len(queue) > 0: # as long as there is an element in the queue 
        node = queue.popleft() # dequeue
        for child in node.children: # enqueue children
            if OK(child): # early return if problem condition met
                return FOUND(child)
            queue.append(child)
    return NOT_FOUND
{% endhighlight %}

## Binary Tree Level Order Traversal

Given a binary tree, return its level order traversal. The input is the root node of the tree. The output should be a list of lists containing tree nodes at each level.
![bfs](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/bfs/bfs12.png)

## Explanation
We can use DFS for this problem by keeping track of the depth for each node. A better way though is to use BFS since it traverses the tree by level by default.

Applying the template, we use a queue to keep track of nodes to visit next.

## How to get a node’s level
When we dequeue a node from the queue, we need to know the level it sits in the tree to add it to the corresponding level in the result. But nodes in the queue do not have any information about level. How do we get a node’s level?

One observation is that the queue contains at most two levels of nodes. To see why, let’s assume our tree is three-level deep. Let’s call the nodes of the shallowest level “level 0” nodes and their children “level 1” nodes, whose children are “level 2” nodes. When we do a BFS, we first push “level 0” nodes into the queue, and as we process them, we push their children “level 1” nodes into the queue. To get “level 2” nodes onto the queue, we have to start dequeuing and processing “level 1” nodes, but we can’t dequeue any “level 1” nodes until we have finished dequeuing and processing “level 0” nodes. This is because a queue is a First-in-First-Out structure. Therefore, it’s impossible to have 3 levels in the queue at the same time. At most, we can have two levels in the queue.

Observe that we always push the leftmost node of a level into the queue first. When we dequeue the leftmost node (and before we add its children), the queue contains only one level of nodes. We can save the number of nodes in the queue in a variable n and dequeue the next n nodes.

The time complexity is O(N) since each node is visited once.
![bfs](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/bfs/bfs13.png)
![bfs](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/bfs/bfs14.png)
![bfs](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/bfs/bfs15.png)
![bfs](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/bfs/bfs16.png)
![bfs](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/bfs/bfs17.png)
![bfs](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/bfs/bfs18.png)
![bfs](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/bfs/bfs19.png)

{% highlight java %}
class Solution {
    public static List<List<Node>> levelOrderTraversal(Node root) {
        List<List<Node>> res = new ArrayList<>();
        if (root == null) return res;

        Deque<Node> queue = new ArrayDeque<>();
        queue.add(root);  // at least one element in the queue to kick start bfs
        while (queue.size() > 0) {  // as long as there is element in the queue
            int n = queue.size();
            List<Node> newLevel = new ArrayList<>();
            // dequeue each node in the current level
            for (int i = 0; i < n; i++) {
                Node node = queue.pop();
                newLevel.add(node);
                // enqueue non-null children
                if (node.left != null) queue.add(node.left);
                if (node.right != null) queue.add(node.right);
            }
            res.add(newLevel);
        }
        return res;
    }
    // Driver code  
	public static void main(String[] args) {

        String[] inputs = {"1 2 4 x 7 x x 5 x x 3 x 6 x x","0 x x"};
		for (int i = 0; i<inputs.length; i++) {
            Node root = Node.buildTree(Arrays.stream(inputs[i].split(" ")).iterator());
            List<List<Node>> actual_output = Solution.levelOrderTraversal(root);
            String[] result = new String[inputs.length];
            String actualData = "";
            for (int j = 0; j< actual_output.size() ;j++) {
                List<Node> level = actual_output.get(j);
                actualData  += "["+level.stream().map(node -> Integer.toString(node.val)).collect(Collectors.joining(","))+"]";
            }
			System.out.println("Binary tree level order traversal : [" +actualData+"]");
		}
	}
}

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
{% endhighlight %}

## Binary Tree ZigZag Level Order Traversal

## Problem statement

Given a binary tree, return its level order traversal but in alternate left to right order.
![bfs](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/bfs/bfs22.png)

## Explanation
This problem is almost the same as level order traversal. We just have to keep a flag to track if we are currently traversing left-to-right or right-to-left.
{% highlight java %}
class Solution {
    public static List<List<Node>> zigZagLevelOrderTraversal(Node root) {
        List<List<Node>> res = new ArrayList<>();
        if (root == null) return res;

        Deque<Node> queue = new ArrayDeque<>();
        queue.add(root); // at least one element in the queue to kick start bfs
        boolean leftToRight = true;
        while (queue.size() > 0) {  // as long as there is element in the queue        
            List<Node> level = new ArrayList<>();
            int size = queue.size();            
            for (int i = 0; i < size; i++) {                
                //poll from q
                Node node = queue.pop();                
                level.add(node);
                //check if left not null add to queue
                if (node.left != null) {
                    queue.add(node.left);
                }                    
                if (node.right != null) {
                    queue.add(node.right);
                }                
            }
            if (!leftToRight) {
                Collections.reverse(level);
            }
            res.add(level);
            leftToRight = !leftToRight;
        }
        return res;
    }
    // Driver code  
	public static void main(String[] args) {

        String[] inputs = {"1 2 4 x 7 x x 5 x 8 x x 3 x 6 x x"};
		for (int i = 0; i<inputs.length; i++) {
			Node root = Node.buildTree(Arrays.stream(inputs[i].split(" "))
			.iterator());
            List<List<Node>> actual_output = Solution.zigZagLevelOrderTraversal(root);
            String actualData = "";
    
            for (int j = 0; j< actual_output.size() ;j++) {   
                List<Node> level = actual_output.get(j);
                actualData  += "["+level.stream().map(node -> 
                Integer.toString(node.val)).collect(Collectors.joining(","))+"]";
            }
			System.out.println("Lowest common ancestor : [" + actualData+"]");
		}
	}
}
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
{% endhighlight %}

## Binary Tree Right Side View

Given a binary tree, return the rightmost node of each level.
![bfs](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/bfs/bfs23.png)

## Explanation
We can do a level order traversal and add the last node to return the result. The time complexity is O(N) since each node is visited at most once.

{% highlight java %}
class Solution {

    public static List<Node> getRightSideView(Node root) {
        List<Node> res = new ArrayList<>();
        if (root == null) return res;

        Deque<Node> queue = new ArrayDeque<>();
        queue.add(root);  // at least one element in the queue 
        to kick start bfs

        while (queue.size() > 0) {  // as long as there is element 
        in the queue
            int n = queue.size();  // number of nodes in current level
            res.add(queue.peek());  // only append the first node
             we encounter since it's the rightmost
            // dequeue each node in the current level
            for (int i = 0; i < n; i++) {
                Node node = queue.pop();
                // we add right children first so it'll pop out 
                of the queue first
                if (node.right != null) queue.add(node.right);
                if (node.left != null) queue.add(node.left);
            }
        }

        return res;
    }
      // Driver code  
	public static void main(String[] args) {

        String[] inputs ={"1 2 4 x 7 x x 5 x x 3 x 6 x x","0 x x"};
		for (int i = 0; i<inputs.length; i++) {
			Node root = Node.buildTree(Arrays.stream(inputs[i]
			.split(" ")).iterator());
			System.out.println("Binary tree right side : " + 
			Solution.getRightSideView(root)
            .stream().map(node -> Integer.toString(node.val))
            .collect(Collectors.joining(" ")));
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
}
{% endhighlight %}

## Binary Tree Min Depth
Given a binary tree, find the depth of the shallowest leaf node.
![bfs](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/bfs/bfs20.png)

## Explanation
We can solve this problem with either DFS or BFS. With DFS, we traverse the whole tree looking for leaf nodes, and record and update the minimum depth as we go. With BFS, since we search level by level, we are guaranteed to find the shallowest leaf node earlier than other leaf nodes. This is the biggest advantage of BFS over DFS. The time complexity is O(N)O(N) since each node is visited at most once.

{% highlight java %}

class Solution {
    public static int getBinaryTreeMinDepth(Node root) {
        Deque<Node> queue = new ArrayDeque<>();  // at least one element in the queue to kick start bfs
        int depth = -1;  // we start from -1 because popping root will add 1 depth
        queue.add(root);

        while (queue.size() > 0) {  // as long as there is element 
        in the queue
            depth++;
            int n = queue.size();
            for (int i = 0; i < n; i++) {
                Node node = queue.pop();
                if (node.left == null && node.right == null) {
                    // found leaf node, early return
                    return depth;
                }
                if (node.left != null) queue.add(node.left);
                if (node.right != null) queue.add(node.right);                
            }
        }

        return depth;
    }
      // Driver code  
	public static void main(String[] args) {

        String[] inputs ={"1 2 4 x 7 x x 5 x x 3 x 6 x x","0 x x"};
		for (int i = 0; i<inputs.length; i++) {
			Node root = Node.buildTree(Arrays.stream(inputs[i]
			.split(" ")).iterator());
			System.out.println("Binary tree min depth : " + 
			Solution.getBinaryTreeMinDepth(root));
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
}
{% endhighlight %}

## Binary Tree Distance K from Target Node

Given a binary tree, a target node, and an integer K, find all nodes whose depth (level) is K away from the target node’s depth. The order of returned nodes does not matter.
![bfs](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/bfs/bfs21.png)

## Explanation
To find the nodes distance K away from the target node, we have to first find the target node and its depth. We can do this with a simple BFS using the template in the intro module.

After we find the target node and its level l we can traverse the tree at a level order using BFS again and look for nodes on the l - k and l + k level.

In total, two BFSs are involved and the time complexity is O(N).

## Implementation

{% highlight java %}

class Solution {

    public static List<Node> getDistanceKNodes(Node root, 
    Node target, int k) {
        List<Node> res = new ArrayList<>();
        if (root != null) {
            int targetLevel = findTarget(root, target);
            bfs(root, targetLevel, k, res);
        }
        return res;
    }

    private static void bfs(Node root, int targetLevel, int k, 
    List<Node> res) {
        int level = 0;
        Deque<Node> queue = new ArrayDeque<>();
        queue.add(root);
        while (queue.size() > 0) {
            int n = queue.size();
            level++;
            for (int i = 0; i < n; i++) {
                Node node = queue.pop();
                // found nodes K away from target
                if (Math.abs(targetLevel - level) == k) 
                res.add(node);
                if (node.left != null) queue.add(node.left);
                if (node.right != null) queue.add(node.right);
            }
        }
    }

    private static int findTarget(Node root, Node target) {
        int level = 0;
        Deque<Node> queue = new ArrayDeque<>();
        queue.add(root);
        while (queue.size() > 0) {
            int n = queue.size();
            level++;
            for (int i = 0; i < n; i++) {
                Node node = queue.pop();
                // early exit if found target
                if (node.equals(target)) return level;
                if (node.left != null) queue.add(node.left);
                if (node.right != null) queue.add(node.right);
            }
        }
        return level;
    } 
    // Driver code  
    public static void main(String[] args) {

        String[] inputs ={"1 2 4 x 7 x x 5 x 8 x x 3 x 6 x x",
        "0 1 x x 2 x x"};
        String[] inputs1 ={"6","2"};
        String[] inputs2 ={"1","0"};
        for (int i = 0; i<inputs.length; i++) {
            Node root = Node.buildTree(Arrays.stream( inputs[i]
            .split(" ")).iterator());
            Node target = Node.findNode(root, 
            Integer.parseInt( inputs1[i]));
            int k = Integer.parseInt(inputs2[i]);
            String actual_output = Solution
            .getDistanceKNodes(root, target, k)
                .stream().map(node -> Integer.toString(node.val))
                .collect(Collectors.joining(" "));
            System.out.println("Binary tree distance 
            K from target node : " + actual_output);
        }
    }
}
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
        if (root == null || root.val == target) return root;
        Node leftSearch = findNode(root.left, target);
        if (leftSearch != null) return leftSearch;
        return findNode(root.right, target);
    }
}
{% endhighlight %}

## Binary Tree Distance K from Target Node

Given a binary tree, a target node, and an integer K, find all nodes whose depth (level) is K away from the target node’s depth. The order of returned nodes does not matter.

![bfs](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/bfs/bfs24.png)

## Explanation
To find the nodes distance K away from the target node, we have to first find the target node and its depth. We can do this with a simple BFS using the template in the intro module.

After we find the target node and its level l we can traverse the tree at a level order using BFS again and look for nodes on the l - k and l + k level.

In total, two BFSs are involved and the time complexity is O(N).

## Implementation
{% highlight java %}
class Solution {

    public static List<Node> getDistanceKNodes(Node root, 
    Node target, int k) {
        List<Node> res = new ArrayList<>();
        if (root != null) {
            int targetLevel = findTarget(root, target);
            bfs(root, targetLevel, k, res);
        }
        return res;
    }

    private static void bfs(Node root, int targetLevel, int k, 
    List<Node> res) {
        int level = 0;
        Deque<Node> queue = new ArrayDeque<>();
        queue.add(root);
        while (queue.size() > 0) {
            int n = queue.size();
            level++;
            for (int i = 0; i < n; i++) {
                Node node = queue.pop();
                // found nodes K away from target
                if (Math.abs(targetLevel - level) == k) res.add(node);
                if (node.left != null) queue.add(node.left);
                if (node.right != null) queue.add(node.right);
            }
        }
    }

    private static int findTarget(Node root, Node target) {
        int level = 0;
        Deque<Node> queue = new ArrayDeque<>();
        queue.add(root);
        while (queue.size() > 0) {
            int n = queue.size();
            level++;
            for (int i = 0; i < n; i++) {
                Node node = queue.pop();
                // early exit if found target
                if (node.equals(target)) return level;
                if (node.left != null) queue.add(node.left);
                if (node.right != null) queue.add(node.right);
            }
        }
        return level;
    } 
    // Driver code  
    public static void main(String[] args) {

        String[] inputs ={"1 2 4 x 7 x x 5 x 8 x x 3 x 6 x x",
        "0 1 x x 2 x x"};
        String[] inputs1 ={"6","2"};
        String[] inputs2 ={"1","0"};
        for (int i = 0; i<inputs.length; i++) {
            Node root = Node.buildTree(Arrays.stream( inputs[i]
            .split(" ")).iterator());
            Node target = Node.findNode(root, Integer.parseInt( inputs1[i]));
            int k = Integer.parseInt(inputs2[i]);
            String actual_output = Solution.getDistanceKNodes(root, target, k)
                .stream().map(node -> Integer.toString(node.val))
                .collect(Collectors.joining(" "));
            System.out.println("Binary tree distance K 
            from target node : " + actual_output);
        }
    }
}
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
        if (root == null || root.val == target) return root;
        Node leftSearch = findNode(root.left, target);
        if (leftSearch != null) return leftSearch;
        return findNode(root.right, target);
    }
}
{% endhighlight %}