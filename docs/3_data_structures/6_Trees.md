---
layout: default
title: Trees
parent: Data Structures
nav_order: 6
permalink: /data_structures/trees
---
<div align="center" markdown="1">
Trees / Java resources / Tutorial

{: .fs-8 .fw-400 }
</div>

## What is a Tree?

## Introduction
In this chapter, we will learn a hierarchical data structure known as a Tree. A tree consists of nodes (vertices) that are connected using pointers (edges). Trees are similar to Graphs; the key differentiating point is that a cycle cannot exist in a Tree.

The basic structure of a tree consists of the following components:
* Nodes: Hold data
* Root: The uppermost node of a tree
* Parent Node: A node which is connected to one or more nodes on the lower level (Child Nodes).
* Child Node: A node which is linked to an upper node (Parent Node)
* Sibling Node: Nodes that have the same Parent Node
* Leaf Node – A node that doesn’t have any Child Node

The figure below shows all the terminologies described above:

![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/a1.png)
![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/a2.png)
![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/a3.png)
![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/a4.png)
![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/a5.png)
![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/a6.png)
![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/a7.png)
![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/a8.png)
![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/a9.png)
![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/a10.png)
![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/a11.png)
![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/a12.png)
![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/a13.png)
![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/a14.png)
![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/a15.png)
![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/a16.png)
![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/a17.png)
![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/a18.png)
![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/a19.png)
![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/a20.png)
![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/a21.png)

## Explanation:
In the figure above, 1 is the Root as well as the parent node to child nodes 2, 3 and 4. Node 3 is a parent node to child nodes 6 and 7. As nodes 2,3, and 4 share the same parent node 1 -they are sibling nodes. Similarly, 6 and 7 are sibling nodes because they both have 3 for their parent node.

## Terminology Used in Trees
Here are some other common terminologies used in trees:

* Sub-tree:
A subtree is a portion of a tree that can be viewed as a complete tree on its own. Any node in a tree, together with all the connected nodes below it, comprise a subtree of the original tree. Think of the sub-tree as an analogy for the term, proper subset.
* Degree:
The degree of a node refers to the total number of sub-trees of a node
* Depth:
The number of connections (edges) from the root to a node is known as the depth of that node.
* Level:
(Depth Of Node) + 1
* Height of a Node:
The maximum number of connections between the node and a leaf node in its path is known as the height of that node.
* Height of a Tree:
The height of a tree is simply the height of its root node.

![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/b1.png)
![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/b2.png)
![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/b3.png)
![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/b4.png)
![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/b5.png)
![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/b6.png)
![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/b7.png)
![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/b8.png)
![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/b9.png)
![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/b10.png)
![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/b11.png)

There are a total of six sub-trees in the above tree, and each is marked with a number. Each node has two sub-trees, namely the left and right sub-tree. In a leaf node, the left and right sub-trees are null.

## Types of Trees

## Introduction
Trees being advanced data structures, offer a wide variety of types to provide an efficient solution, specific to a particular use. Trees are extensively used in Artificial Intelligence and complex algorithms to provide an efficient storage mechanism for problem-solving. Based on the structure, height, and other features like time/space complexity, there are different types of trees.

The most commonly used types are listed below:
* N-ary Tree
* Balanced Tree
* Binary Tree
* BinarySearchTree
* AVL Tree
* Red-Black Tree
* 2-3 Tree

Let’s take a look at N-ary and Balanced Trees in this lesson and the other types later in the chapter.

## N-ary Tree
In N-ary trees, each node can have child nodes anywhere from 0 to N. So if it’s a 2-ary tree, commonly known as a Binary Tree, it can have a max. of 0-2 child nodes. Can you guess the value of N in the figure shown below?

![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/b12.png)

![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/b13.png)

![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/b14.png)

## What Makes a Tree Balanced?

![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/b15.png)

![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/b16.png)

## Checking if a binary tree is balanced 
Try to guess if the following tree is balanced or not before looking at the answer!

![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/b17.png)

his tree is height-balanced! How did we determine that? Let’s go through and break our thought process down into a series of steps to find out.

## Steps to Check if Tree is Balanced 
This is the list of steps to follow to find out if a tree is balanced or not:
1. Start from the leaf nodes and move towards the root.
2. Along with traversing the tree, compute the heights of the left-subtree and right-subtree of each node. The height of a leaf node is always 0.
3. At each node, check if the difference in height between the left and right sub-tree is more than 1; if so, then it means that the tree is not balanced.
4. If you have completely traversed the tree and haven’t caught the above condition, then it shows that the tree is balanced. (The height difference between the left and right sub-trees is NOT more than 1.)

## Example
In the illustration below, we are implementing what we learned from the above four steps. Here, HLT means the height of the Left Tree and HRT means the height of the right tree:

![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/e1.png)
![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/e2.png)
![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/e3.png)
![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/e4.png)
![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/e5.png)
![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/e6.png)
![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/e7.png)
![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/e8.png)
![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/e9.png)
![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/e10.png)
![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/e11.png)

## What is a Binary Tree?

## Introduction
The only characteristic which separates Binary Tree from N-ary trees is that any internal-node (non-leaf node) can only contain a maximum of two child nodes. Each node strictly has reference to a left and a right node; we call them its left and right child. The figure below shows what a Binary Tree looks like:

![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/e12.png)

## Types of Binary Trees
The following are further variations of binary trees, based on the structure and other features:
* Complete Binary Tree
* Full Binary Tree
* Perfect Binary Tree

Starting with Complete Binary Tree, let’s discuss each one of them and look at their characteristics and structure.

![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/e13.png)

![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/e14.png)

![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/e15.png)

![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/e16.png)

![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/e17.png)

![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/e18.png)

There are many other advanced trees derived from the basic structure of binary trees. These types will be discussed in the upcoming lessons. Some of the most common ones are:
* Skewed Binary Tree
* Binary Search Tree
* AVL Tree
* Two-Three Tree

## More on Complete Binary Trees

![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/e19.png)

![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/e20.png)

![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/e21.png)

## Insertion in Complete Binary Tree
The following steps are involved in inserting a value in a Complete Binary Tree:
* Nodes are inserted level by level
* Fill in the left-subtree before moving to the right one

![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/e22.png)
![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/e23.png)
![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/e24.png)
![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/e25.png)
![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/e26.png)
![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/e27.png)
![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/e28.png)
![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/e29.png)
![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/e30.png)
![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/e31.png)

## Explanation
As you can see in the above animation, Node 4 was inserted as a left child of Node 2 to fill the property of the Complete Binary Tree. In a Complete Binary Tree, nodes don’t exist with the right child only. The right child exists only when the left child is also present. So during Insertion, make sure to insert a node as a left child first (if it’s empty in the left sub-tree) before moving to right sub-tree.

## Skewed Binary Tree

## Introduction
A Skewed Binary Tree is a type of Binary Tree where all nodes are shifted to either the left or right side. It can also be defined as a Binary Tree in which the number of children is firmly restricted to one at each node. Furthermore, the side at which that single child node is present, either left or right, is also fixed throughout the tree. This type of Binary Tree structure is avoided at all cost, as we will have to perform n number of comparisons to search for a node, where n is the total number of nodes in the tree.

## Types of Skewed Binary Tree
There are two types of Skewed Binary Trees based on which side is dominated:
* Left-Skewed Binary Tree
* Right-Skewed Binary Tree

![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/e32.png)

![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/e33.png)

## Note
Try your best to avoid such tree structures, especially in the case of a Binary Search Tree, as it will kill efficient searching (the core purpose of a Binary Search Tree).

## What is a Binary Search Tree (BST)?

![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/e34.png)

![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/e35.png)

For example, in the above tree Node Y is a parent node having two child nodes, SubTree 1 and SubTree 2 respectively. To convert a binary tree into a binary search tree, we need to follow a general rule. According to that rule, all nodes in SubTree 1 will have a value less than Node Y, and similarly, all nodes in SubTree 2 will have a value greater than Node Y.

Therefore, the value of Node Y will be less than X and the value of SubTree 3 is greater than Node X.

## Different b/w Binary Search Tree and Binary Tree
Not every Binary Tree is a Binary Search Tree. BST is simply a type of Binary Tree. For a Binary Tree to qualify as a Binary Search Tree, it needs to follow the general rule which we covered earlier.

Let’s see an example to understand why every Binary Tree is not always a Binary Search Tree?

![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/e36.png)

## Explanation
As you can see in the above figure, the first one is a Binary Tree because each node has a maximum of two children. But why isn’t it a Binary Search Tree? Because it does not follow the BST rule that Node 2 cannot be a left child of Node 1, and we would need to make Node 1 a left child of Node 2 to convert it into a Binary Search Tree.

Now that we have studied a Binary Search Tree and how it’s different from a simple Binary Tree, it is time to implement the basic operations –Insert(), Search() and Delete()–to see how efficient this BST is compared to a simple Binary Tree.

## Insertion in Binary Search Trees

## Implementing Insertion
To implement the insertion operation of a Binary Search Tree, we first need to build a simple Binary Tree. A basic class of Binary Tree is where every node holds the following information:
* Data/Key-Value
* Pointer to its left child
* Pointer to its right child

{% highlight java %}
class Node{
  
//Variables
  private  int data;
  private  Node leftChild;
  private  Node rightChild;
  
//Constructor  
  Node(int value){
    this.data=value;
    leftChild=null;
    rightChild=null;
  }
  
//Getter-Setter  
  public Node getLeftChild(){return leftChild;}
  public Node getRightChild(){return rightChild;}
  public int  getData(){return data;}
  public void setData(int value){this.data=value;}
  public void setLeftChild(Node left){this.leftChild=left;}
  public void setRightChild(Node right){this.rightChild=right;}
}
{% endhighlight %}

Since every tree has a root or a starting node, we can start from there to move to any internal or child node and add a tree node in the class.

![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/e37.png)

## Insert Function
The insertion functionality works according to the following steps. See the illustration below for better understanding.
1. Start from the root node.
2. Check if the value is greater than root/current node data.
3. If yes, then traverse the right sub-tree. Otherwise, if the value is less than or equal to the current node value, traverse its left sub-tree.
4. Repeat steps two and three until you find a leaf node, then insert the data and connect the new node with the leaf node, which will now become parent of that new node.

![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/w1.png)
![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/w2.png)
![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/w3.png)
![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/w4.png)
![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/w5.png)
![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/w6.png)
![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/w7.png)
![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/w8.png)
![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/w9.png)
![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/w10.png)
![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/w11.png)

## Explanation
While inserting 17 into the tree, we first traverse the nodes from the root by comparing every node value with 17. This happens until we reach the right node, which is 15 in this case. Now we know 15 is smaller than 17 so we will add the new node at the right child node of 15. We will insert 12 by performing the same series of steps, starting from the root node.

## Insertion in BST (Complete Implementation)

## Introduction
There are two techniques to code an Insertion Function:
* Iterative
* Recursive

First, let’s see how Iterative methodology works. The following tree is what we will build once we successfully implement the insertion functionality in Binary Search Tree code.

![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/w12.png)

{% highlight java %}
class binarySearchTree {

	private Node root;

	public Node getRoot() {
		return root;
    }
    
	public void setRoot(Node root) {
		this.root = root;
	}

	//Iterative Function to insert a value in BST
	public boolean add(int value) {

		//If Tree is empty then insert Root with the given value inside Tree   
		if (isEmpty()) {
			root = new Node(value);
			return true;
		}

		//Starting from root
		Node currentNode = root;

		//Traversing the tree untill valid position to insert the value
		while (currentNode != null) {

			Node leftChild = currentNode.getLeftChild();
			Node rightChild = currentNode.getRightChild();

			//If the value to insert is less than root value then move to left subtree
			//else move to right subtree of root
			//and before moving check if the subtree is null, if it's then insert the value.
			if (currentNode.getData() > value) {
				if (leftChild == null) {
					leftChild = new Node(value);
					currentNode.setLeftChild(leftChild);
					return true;
				}
				currentNode = leftChild;
			} else {
				if (rightChild == null) {
					rightChild = new Node(value);
					currentNode.setRightChild(rightChild);
					return true;
				}
				currentNode = rightChild;
			} //end of else
		} //end of while
		return false;
	}

	//Function to check if Tree is empty or not  
	public boolean isEmpty() 
    {
		return root == null; //if root is null then it means Tree is empty
	}

	//Just for Testing purpose 
	public void printTree(Node current) 
    {
		if (current == null) return;

		System.out.print(current.getData() + ",");
		printTree(current.getLeftChild());
		printTree(current.getRightChild());

	}
}

//Class for a binary tree Node
class Node {

    //Variables
    private int data;
    Node leftChild;
    Node rightChild;

    //Constructor  
    Node(int value) {
        this.data = value;
        leftChild = null;
        rightChild = null;
    }

    //Getter-Setter  
    public Node getLeftChild() {
        return leftChild;
    }

    public Node getRightChild() {
        return rightChild;
    }

    public int getData() {
        return data;
    }

    public void setData(int value) {
        this.data = value;
    }

    public void setLeftChild(Node left) {
        this.leftChild = left;
    }

    public void setRightChild(Node right) {
        this.rightChild = right;
    }
}

class binarySearchTreeDemo {

	public static void main(String args[]) 
    {
		binarySearchTree bsT = new binarySearchTree();

		bsT.add(6);
		bsT.add(4);
		bsT.add(9);
		bsT.add(5);
		bsT.add(2);
		bsT.add(8);
		bsT.add(12);
		bsT.add(10);
		bsT.add(14);
    
		bsT.printTree(bsT.getRoot());
	}
}
{% endhighlight %}

## Explanation
Add function takes an integer value and then traverses the BST tree for a valid position to insert a value. It starts from the root of the tree and traverses the leaf node. Traversing is based on the BST formula, i.e. if the current node’s value is less than key-value, then we will have to find an appropriate position in the right subtree of the current node before we try to find a position in the left subtree.

When we reach the leaf node, we will create a new node, assign it a given value, and link it with the leaf node. If the leaf node’s value is less than the given value then make the new node rightChild of leafNode, or else make it leftChild.

![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/w13.png)

## Insertion Implementation (Recursive)

{% highlight java %}
class binarySearchTree {

	private Node root;


	public Node getRoot() {
		return root;
    }
    
		
	public void setRoot(Node root) {
		this.root = root;
	}

	//Recursive function to insert a value in BST 
	public Node recursive_insert(Node currentNode, int value) {

		//Base Case
		if (currentNode == null) {
			return new Node(value);
		}

		if (value < currentNode.getData()) {
			//Iterate left sub-tree
			currentNode.setLeftChild(recursive_insert(currentNode.getLeftChild(), value));
		} else if (value > currentNode.getData()) {
			//Iterate right sub-tree
			currentNode.setRightChild(recursive_insert(currentNode.getRightChild(), value));
		} else {
			// value already exists
			return currentNode;
		}

		return currentNode;

	}

	//Function to call recursive insert
	public boolean add(int value) {

		root = recursive_insert(this.root, value);
		return true;
	}

	//Function to check if Tree is empty or not  
	public boolean isEmpty() 
    {
		return root == null; //if root is null then it means Tree is empty
	}

	//Just for Testing purpose 
	public void printTree(Node current) 
    {
		if (current == null) return;

		System.out.print(current.getData() + ",");
		printTree(current.getLeftChild());
		printTree(current.getRightChild());

	}
}

class Node{
  
//Variables
  private  int data;
  Node leftChild;
	Node rightChild;
  
//Constructor  
  Node(int value){
    this.data=value;
    leftChild=null;
    rightChild=null;
  }
  
//Getter-Setter  
  public Node getLeftChild(){return leftChild;}
  public Node getRightChild(){return rightChild;}
  public int  getData(){return data;}
  public void setData(int value){this.data=value;}
  public void setLeftChild(Node left){this.leftChild=left;}
  public void setRightChild(Node right){this.rightChild=right;}
}

class binarySearchTreeDemo {

	public static void main(String args[]) {

		binarySearchTree bsT = new binarySearchTree();
		bsT.add(6);
		bsT.add(4);
		bsT.add(9);
		bsT.add(5);
		bsT.add(2);
		bsT.add(8);
		bsT.add(12);
		bsT.add(10);
		bsT.add(14);
		bsT.printTree(bsT.getRoot());

	}
}
{% endhighlight %}

![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/w14.png)

![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/w15.png)

## Search in Binary Search Trees (Implementation)

## Introduction
In this lesson, we are going to implement the Search functionality by using the previously implemented BST class. The following are the steps which we perform to search for an element in BST.
1. Start from Root.
2. If the value is less than the current node value, then traverse the left sub-tree; if it is more, then traverse the right sub-tree.
3. Keep on doing the above step until you either find a node with that value or reach a leaf node—in which case the value doesn’t exist in the Binary Search Tree.

{% highlight java %}
class binarySearchTree {

	//Variables
	private Node root;
	//Getter for Root
	public Node getRoot() {
		return root;
	}
  
  public void setRoot(Node root) {
		this.root = root;
	}


	//Searches value in BST
	//Either returns the Node with that value or return null
	public Node search(int value) {

		if (isEmpty()) return null; // if tree is empty simply return null

		Node currentNode = this.root;

		while (currentNode != null) {

			if (currentNode.getData() == value) return currentNode; // compare data from current node
			
			if (currentNode.getData() > value) //if data from current node is greater than value
				currentNode = currentNode.getLeftChild(); // then move towards left subtree
			else 
				currentNode = currentNode.getRightChild(); //else move towards right subtree
		}

		System.out.println(value + " Not found in the Tree!");
		return null;
	}
	//Recursive function to insert a value in BST 
	public Node recursive_insert(Node currentNode, int value) {

		//Base Case
		if (currentNode == null) {
			return new Node(value);
		}

		if (value < currentNode.getData()) {
			//Iterate left sub-tree
			currentNode.setLeftChild(recursive_insert(currentNode.getLeftChild(), value));
		} else if (value > currentNode.getData()) {
			//Iterate right sub-tree
			currentNode.setRightChild(recursive_insert(currentNode.getRightChild(), value));
		} else {
			// value already exists
			return currentNode;
		}

		return currentNode;

	}

	//Function to call recursive insert
	public boolean add(int value) {

		root = recursive_insert(this.root, value);
		return true;
	}

	//Function to check if Tree is empty or not  
	public boolean isEmpty() {
		return root == null; //if root is null then it means Tree is empty
	}

	//Just for Testing purpose 
	public void printTree(Node current) {

		if (current == null) return;

		System.out.print(current.getData() + ",");
		printTree(current.getLeftChild());
		printTree(current.getRightChild());

	}
}


class Node{
  
//Variables
  private  int data;
  Node leftChild;
	Node rightChild;
  
//Constructor  
  Node(int value){
    this.data=value;
    leftChild=null;
    rightChild=null;
  }
  
//Getter-Setter  
  public Node getLeftChild(){return leftChild;}
  public Node getRightChild(){return rightChild;}
  public int  getData(){return data;}
  public void setData(int value){this.data=value;}
  public void setLeftChild(Node left){this.leftChild=left;}
  public void setRightChild(Node right){this.rightChild=right;}
}

class binarySearchTreeDemo {
	public static void main(String args[]) {

		binarySearchTree bsT = new binarySearchTree();

		bsT.add(6);
		bsT.add(4);
		bsT.add(9);
		bsT.add(5);
		bsT.add(2);
		bsT.add(8);
		bsT.add(12);
		bsT.add(10);
		bsT.add(14);
		System.out.println(">> Tree <<");
		bsT.printTree(bsT.getRoot());

		Node temp = bsT.search(5);
		if (temp != null) {
			System.out.println("\n" + temp.getData() + " found in Tree !");
		}
		temp = bsT.search(51);
		if (temp != null) {
			System.out.println("\n" + temp.getData() + " found in Tree !");
		}
  }
}
{% endhighlight %}

![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/w16.png)

{% highlight java %}
class binarySearchTree {

	//Variables
	private Node root;
	//Getter for Root
	public Node getRoot() {
		return root;
	}
  
  public void setRoot(Node root) {
		this.root = root;
	}

	//Wrapper function for recursive search
	public Node search(int value) {

		if (isEmpty()) return null; // if tree is empty simply return null

		// return the output of the recursive search
		return searchRecursive(root, value);
	}

	//Recursive search function
	public Node searchRecursive(Node currentNode, int value){
		// if node is null or value is found then return node
		if (currentNode==null || currentNode.getData() == value) 
			return currentNode; 
		
		// if value is less than node's data then search left sub-tree 
		if (currentNode.getData() > value){
			return searchRecursive(currentNode.getLeftChild(), value);
		} 
		else{
		// if value is greater than node's data then search right sub-tree 
			return searchRecursive(currentNode.getRightChild(), value); 
		}
	}

	//Recursive function to insert a value in BST 
	public Node recursive_insert(Node currentNode, int value) {

		//Base Case
		if (currentNode == null) {
			return new Node(value);
		}

		if (value < currentNode.getData()) {
			//Iterate left sub-tree
			currentNode.setLeftChild(recursive_insert(currentNode.getLeftChild(), value));
		} else if (value > currentNode.getData()) {
			//Iterate right sub-tree
			currentNode.setRightChild(recursive_insert(currentNode.getRightChild(), value));
		} else {
			// value already exists
			return currentNode;
		}

		return currentNode;

	}

	//Function to call recursive insert
	public boolean add(int value) {

		root = recursive_insert(this.root, value);
		return true;
	}

	//Function to check if Tree is empty or not  
	public boolean isEmpty() {
		return root == null; //if root is null then it means Tree is empty
	}

	//Just for Testing purpose 
	public void printTree(Node current) {

		if (current == null) return;

		System.out.print(current.getData() + ",");
		printTree(current.getLeftChild());
		printTree(current.getRightChild());

	}
}


class Node{
  
//Variables
  private  int data;
  Node leftChild;
	Node rightChild;
  
//Constructor  
  Node(int value){
    this.data=value;
    leftChild=null;
    rightChild=null;
  }
  
//Getter-Setter  
  public Node getLeftChild(){return leftChild;}
  public Node getRightChild(){return rightChild;}
  public int  getData(){return data;}
  public void setData(int value){this.data=value;}
  public void setLeftChild(Node left){this.leftChild=left;}
  public void setRightChild(Node right){this.rightChild=right;}
}

class binarySearchTreeDemo {
	public static void main(String args[]) {

		binarySearchTree bsT = new binarySearchTree();

		bsT.add(6);
		bsT.add(4);
		bsT.add(9);
		bsT.add(5);
		bsT.add(2);
		bsT.add(8);
		bsT.add(12);
		bsT.add(10);
		bsT.add(14);
		System.out.println(">> Tree <<");
		bsT.printTree(bsT.getRoot());

		Node temp = bsT.search(5);
		if (temp != null) {
			System.out.println("\n" + temp.getData() + " found in Tree !");
		}
		else 
			System.out.println("\n Not found in Tree !");

		temp = bsT.search(51);
		if (temp != null) {
			System.out.println("\n" + temp.getData() + " found in Tree !");
		}
		else 
			System.out.println("\n Not found in Tree !");
  }
}
{% endhighlight %}

![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/w17.png)

## Deletion in Binary Search Trees

## Introduction
In this lesson, we are going to look at the three deletion cases and the steps required to perform deletion in each case.

The three cases are given below:
* Deletion at Leaf Node
* Deletion at Parent Node
   * Node has only one child
   * Node has two children

Now let’s look at all the case one by one.

## Deletion at Leaf Node
If the node we want to delete is present at the leaf node in a Binary Search Tree, we simply remove that leaf node. After deletion, its parent node will point to null. If the leaf node was the left child of Node X, then make leftChild of Node X null; if it was the right one, then make the rightChild pointer of node X point to null. See the following example for clarification:

![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/w18.png)
![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/w19.png)
![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/w20.png)
![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/w21.png)
![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/w22.png)
![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/w23.png)

## Deletion at Parent Node
Deletion at the Parent Node is further sub-divided into two cases:
* Parent node with only one child
* Parent node with two children

## Parent Node with only one Child
If the parent node that you want to delete has only one child, then delete the parent node first. After doing that, take the deleted parent-node’s child and link it with the parent node of the deleted node. Now the parent of the deleted node will become the parent of the child node.

It will be easier to understand visually, so take a look at the following illustration:

![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/w24.png)
![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/w25.png)
![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/w26.png)
![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/w27.png)
![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/w28.png)
![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/w29.png)
![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/w30.png)

## Parent Node has Two Children
It is a little more complex than the first two cases. Here’s the list of steps you perform when deleting a parent node with two children in a BST:
1. Start by traversing the right subtree of the soon-to-be deleted parent node in such a way that you reach the left-most value—the value that will appear to be the smallest value in the whole subtree.
2. Replace the value of the node, found in the last step, with the parent’s node value.
3. Finally, delete the leaf node.

![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/q1.png)
![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/q2.png)
![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/q3.png)
![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/q4.png)
![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/q5.png)
![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/q6.png)
![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/q7.png)
![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/q8.png)
![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/q9.png)
![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/q10.png)

## Deletion in Binary Search Trees (Implementation)

We will cover the implementation of deletion, including all the cases that we discussed previously: Node as a Leaf, Parent Node with one child, and Parent Node with two children.

## Deletion Cases
As discussed in the last lesson, the following are the three cases of deletion in a Binary Search Tree:
* Node is a leaf node
* Node has a one child
* Node has two children

## Implementation in Java
Look at the code snippet below and try to understand the code. If you don’t understand at​​ any point, you can just read the explanation below.

{% highlight java %}
class binarySearchTree {

	private Node root;

	public Node getRoot() {
		return root;
	}
  
  	public void setRoot(Node root) {
		this.root = root;
	}


	//3 conditions for delete
	//1.node is leaf node.
	//2.node has 1 child.
	//3.node has 2 children.
	boolean delete(int value, Node currentNode) {
       
        if (root == null) {
            return false;
        } 

        Node parent = null; //To Store parent of currentNode
        while(currentNode != null && (currentNode.getData() != value)) {
            parent = currentNode;
            if (currentNode.getData() > value)
                currentNode = currentNode.getLeftChild();
            else
                currentNode = currentNode.getRightChild();
            
        }
       
        if(currentNode == null) {
            return false;
        }
        else if(currentNode.getLeftChild() == null && currentNode.getRightChild() == null) {
            //1. Node is Leaf Node
            //if that leaf node is the root (a tree with just root)
            if(root.getData() == currentNode.getData()){
                setRoot(null);
                return true;
            }
            else if(currentNode.getData() < parent.getData()){
				parent.setLeftChild(null);
                return true;
             }
            else{
                parent.setRightChild(null);
                return true;
            }
        } else if(currentNode.getRightChild() == null) {
            
            if(root.getData() == currentNode.getData()){
                setRoot(currentNode.getLeftChild());
                return true;
            }
            else if(currentNode.getData() < parent.getData()){
                parent.setLeftChild(currentNode.getLeftChild());
                return true;
            }
            else{

                parent.setRightChild(currentNode.getLeftChild());
                return true;
            }

        }
        else if(currentNode.getLeftChild() == null) {
            
            if(root.getData() == currentNode.getData()){
                setRoot(currentNode.getRightChild());
                return true;
            }
            else if(currentNode.getData() < parent.getData()){
                parent.setLeftChild(currentNode.getRightChild());
                return true;
            }
            else{
                parent.setRightChild(currentNode.getRightChild());
                return true;
            }

        }
        else {
            //Find Least Value Node in right-subtree of current Node
            Node leastNode = findLeastNode(currentNode.getRightChild());
            //Set CurrentNode's Data to the least value in its right-subtree
            int temp = leastNode.getData();
            delete(temp, root);
            currentNode.setData(temp);
            //Delete the leafNode which had the least value
            return true;
        }

    }

	//Helper function to find least value node in right-subtree of currentNode
	private Node findLeastNode(Node currentNode) {

		Node temp = currentNode;

		while (temp.getLeftChild() != null) {
			temp = temp.getLeftChild();
		}

		return temp;

	}

	//Iterative Function to insert a value in BST
	public boolean add(int value) {

		//If Tree is empty then insert Root with the given value inside Tree   
		if (isEmpty()) {
			root = new Node(value);
			return true;
		}

		//Starting from root
		Node currentNode = root;

		//Traversing the tree untill valid position to insert the value
		while (currentNode != null) {

			Node leftChild = currentNode.getLeftChild();
			Node rightChild = currentNode.getRightChild();

      //If the value to insert is less than root value 
      //then move to left subtree else move to right subtree of root
      //and before moving check if the subtree is null, if it's then insert the value. 

			if (currentNode.getData() > value) {
				if (leftChild == null) {
					leftChild = new Node(value);
					currentNode.setLeftChild(leftChild);
					return true;
				}
				currentNode = leftChild;
			} else {
				if (rightChild == null) {
					rightChild = new Node(value);
					currentNode.setRightChild(rightChild);
					return true;
				}
				currentNode = rightChild;
			} //end of else
		} //end of while
		return false;
	}

	//Function to check if Tree is empty or not  
	public boolean isEmpty() {
		return root == null; //if root is null then it means Tree is empty
	}

	//Just for Testing purpose 
	public void printTree(Node current) {

		if (current == null) return;

		System.out.print(current.getData() + ",");
		printTree(current.getLeftChild());
		printTree(current.getRightChild());

	}
}

class Node{
  
//Variables
  private  int data;
  Node leftChild;
	Node rightChild;
  
//Constructor  
  Node(int value){
    this.data=value;
    leftChild=null;
    rightChild=null;
  }
  
//Getter-Setter  
  public Node getLeftChild(){return leftChild;}
  public Node getRightChild(){return rightChild;}
  public int  getData(){return data;}
  public void setData(int value) {this.data=value;}
  public void setLeftChild(Node left){this.leftChild=left;}
  public void setRightChild(Node right){this.rightChild=right;}
}

class binarySearchTreeDemo {
	public static void main(String args[]) {

		binarySearchTree bsT = new binarySearchTree();

		bsT.add(6);
		bsT.add(7);
		bsT.add(8);
		bsT.add(12);
		bsT.add(1);
		bsT.add(15);
		

		System.out.print("Tree : ");
		bsT.printTree(bsT.getRoot());


		System.out.print("\nDeleting Node 6: ");
		bsT.delete(6, bsT.getRoot());
		bsT.printTree(bsT.getRoot());

		System.out.print("\nDeleting Node 15: ");
		bsT.delete(15, bsT.getRoot());
		bsT.printTree(bsT.getRoot());

		System.out.print("\nDeleting Node 1: ");
		bsT.delete(1, bsT.getRoot());
		bsT.printTree(bsT.getRoot());

	}
}
{% endhighlight %}

## Explanation
Let’s break the above code down into different sections:
* Main function – Creates BST and calls the delete function.
* Delete function – Takes the node value to be deleted and the root node. It returns a boolean for successful/unsuccessful deletion.
* findLeastNode – Takes in the root node of the right sub-tree on the node to be deleted, and returns the least value node in that sub-tree.

Let’s take a look at these functions one by one.

## Main
1. We are creating an instance of a Binary Search Tree class.
2. We will be handling these three cases in our code:
   * Node at Leaf: Delete Node 15
   * Node is a Parent Node with two children: Delete Node 6
   * Node is a Parent Node with only one child: After deletion of first two nodes, deleting Node 1


## Delete (int value, Node start)
The delete function gets called whenever we want to delete a node from the tree. It searches from the start node, which is the root of the tree, looking for the node with the key value equal to the value variable given in the function argument. The function keeps traversing the nodes till it either finds the node to be deleted or reaches the end of the tree.

While Traversing the tree, we will keep track of current node and its parent node. We will be using them in the third case to link parent node with the new child. When the node to be deleted is found in the tree, we will perform the following steps:
* If the node to be deleted is a leaf node, simply set its parent to null.
* If the node to be deleted has only one child, link that node’s parent with its child.
* If the node to be deleted has two children, then search for the node with least value in the right sub-tree. We will be using a helper function called findLeastNode (root_of_right_subtree) for this purpose. After finding the leastNode, replace the currentNode value with the least node value, and then call the delete function for that least node (which will now be a leaf node) so our first case will be called.


## findLeastNode (Node start)
In this function, start will be the root of the right sub-tree on the node that we are planning to delete. We will iterate the left sub-tree of the start node recursively until we find the least value node.

## Time Complexity for Deletion
The worst case time complexity for the delete operation is O(h) where h is the height of the BST. In the worst case, we will have to traverse from the root to the deepest leaf node in the tree. If the height of the skewed tree becomes n then the time complexity will be O(n).

## Pre-Order Traversal in Binary Search Trees

## Pre-Order Traversal
In this type, the elements are traversed in “root-left-right” order. We first visit the root/parent node and then the children; First the left child and then the right one.

The following steps are required to perform Pre-Order Traversal, starting from the root node:
1. Visit the current node and display its data.
2. Traverse the left sub-tree of currentNode, recursively using the PreOrder() function.
3. Traverse the right sub-tree of currentNode, recursively using the PreOrder() function.

![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/q11.png)
![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/q12.png)
![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/q13.png)
![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/q14.png)
![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/q15.png)
![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/q16.png)
![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/q17.png)
![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/q18.png)
![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/q19.png)

## Implementation in Java
Now we will try to implement the same example in the code below, so have a look:

{% highlight java %}
class binarySearchTree {

  //Variables
  private Node root;
  //Getter for Root

  public Node getRoot() {
    return root;
  }

  public void setRoot(Node root) {
    this.root = root;
  }

  //Searches value in BST
  //Either returns the Node with that value or return null
  public Node search(int value) {

    if (isEmpty()) return null;

    Node currentNode = this.root;

    while (currentNode != null) {

      if (currentNode.getData() == value) return currentNode;

      if (currentNode.getData() > value) currentNode = currentNode.getLeftChild();
      else currentNode = currentNode.getRightChild();
    }

    System.out.println(value + " is not in Tree !");
    return null;
  }
  //Recursive function to insert a value in BST 
  public Node recursive_insert(Node currentNode, int value) {

    //Base Case
    if (currentNode == null) {
      return new Node(value);
    }

    if (value < currentNode.getData()) {
      //Iterate left sub-tree
      currentNode.setLeftChild(recursive_insert(currentNode.getLeftChild(), value));
    } else if (value > currentNode.getData()) {
      //Iterate right sub-tree
      currentNode.setRightChild(recursive_insert(currentNode.getRightChild(), value));
    } else {
      // value already exists
      return currentNode;
    }

    return currentNode;

  }

  //Function to call recursive insert
  public boolean add(int value) {

    root = recursive_insert(this.root, value);
    return true;
  }


  //Function to check if Tree is empty or not  

  public boolean isEmpty() {
    return root == null; //if root is null then it means Tree is empty
  }

  //Just for Testing purpose 
  public void printTree(Node current) {

    if (current == null) return;

    System.out.print(current.getData());
    printTree(current.getLeftChild());
    printTree(current.getRightChild());

  }
}

class binarySearchTree {

  //Variables
  private Node root;
  //Getter for Root

  public Node getRoot() {
    return root;
  }

  public void setRoot(Node root) {
    this.root = root;
  }

  //Searches value in BST
  //Either returns the Node with that value or return null
  public Node search(int value) {

    if (isEmpty()) return null;

    Node currentNode = this.root;

    while (currentNode != null) {

      if (currentNode.getData() == value) return currentNode;

      if (currentNode.getData() > value) currentNode = currentNode.getLeftChild();
      else currentNode = currentNode.getRightChild();
    }

    System.out.println(value + " is not in Tree !");
    return null;
  }
  //Recursive function to insert a value in BST 
  public Node recursive_insert(Node currentNode, int value) {

    //Base Case
    if (currentNode == null) {
      return new Node(value);
    }

    if (value < currentNode.getData()) {
      //Iterate left sub-tree
      currentNode.setLeftChild(recursive_insert(currentNode.getLeftChild(), value));
    } else if (value > currentNode.getData()) {
      //Iterate right sub-tree
      currentNode.setRightChild(recursive_insert(currentNode.getRightChild(), value));
    } else {
      // value already exists
      return currentNode;
    }

    return currentNode;

  }

  //Function to call recursive insert
  public boolean add(int value) {

    root = recursive_insert(this.root, value);
    return true;
  }


  //Function to check if Tree is empty or not  

  public boolean isEmpty() {
    return root == null; //if root is null then it means Tree is empty
  }

  //Just for Testing purpose 
  public void printTree(Node current) {

    if (current == null) return;

    System.out.print(current.getData());
    printTree(current.getLeftChild());
    printTree(current.getRightChild());

  }
}

class preOrderTraversal {

	public static void preTraverse(Node root) {

		if (root == null) return;

		System.out.print(root.getData() + ",");
    preTraverse(root.getLeftChild());
    preTraverse(root.getRightChild());

	}

	public static void main(String[] args) {

		binarySearchTree BST = new binarySearchTree();

		BST.add(6);
		BST.add(4);
		BST.add(2);
		BST.add(5);
		BST.add(9);
		BST.add(8);
		BST.add(12);

		preOrderTraversal.preTraverse(BST.getRoot());

	}

}
{% endhighlight %}

![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/q20.png)
![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/q21.png)

## In-Order Traversal in Binary Search Trees

## In-Order Traversal
In this type, the elements are traversed in a “left-root-right” order: we first visit the left node, then comes the turn of the root, and finally the right child. The following steps are required to perform In-Order Traversal, starting from the root node:
1. Traverse the left sub-tree of currentNode, recursively using the InOrder() function.
2. Visit the ​​​current node and read.
3. Traverse the right sub-tree of currentNode, recursively using the In-Order() function.

![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/r1.png)
![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/r2.png)
![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/r3.png)
![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/r4.png)
![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/r5.png)
![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/r6.png)
![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/r7.png)
![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/r8.png)
![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/r9.png)
![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/r10.png)
![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/r11.png)
![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/r12.png)

## Implementation in Java
Now we will try to implement the same example in the code below, so have a look:

{% highlight java %}
class binarySearchTree {

  //Variables
  private Node root;
  //Getter for Root

  public Node getRoot() {
    return root;
  }
  public void setRoot(Node root) {
    this.root = root;
  }

  //Searches value in BST
  //Either returns the Node with that value or return null
  public Node search(int value) {

    if (isEmpty()) return null;

    Node currentNode = this.root;

    while (currentNode != null) {

      if (currentNode.getData() == value) return currentNode;

      if (currentNode.getData() > value) currentNode = currentNode.getLeftChild();
      else currentNode = currentNode.getRightChild();
    }

    System.out.println(value + " is not in Tree !");
    return null;
  }
  //Recursive function to insert a value in BST 
  public Node recursive_insert(Node currentNode, int value) {

    //Base Case
    if (currentNode == null) {
      return new Node(value);
    }

    if (value < currentNode.getData()) {
      //Iterate left sub-tree
      currentNode.setLeftChild(recursive_insert(currentNode.getLeftChild(), value));
    } else if (value > currentNode.getData()) {
      //Iterate right sub-tree
      currentNode.setRightChild(recursive_insert(currentNode.getRightChild(), value));
    } else {
      // value already exists
      return currentNode;
    }

    return currentNode;

  }

  //Function to call recursive insert
  public boolean add(int value) {

    root = recursive_insert(this.root, value);
    return true;
  }


  //Function to check if Tree is empty or not  

  public boolean isEmpty() {
    return root == null; //if root is null then it means Tree is empty
  }

  //Just for Testing purpose 
  public void printTree(Node current) {

    if (current == null) return;

    System.out.print(current.getData());
    printTree(current.getLeftChild());
    printTree(current.getRightChild());

  }
}

class Node{

  //Variables
  private  int data;
  Node leftChild;
  Node rightChild;

  //Constructor  
  Node(int value){
    this.data=value;
    leftChild=null;
    rightChild=null;
  }

  //Getter-Setter  
  public Node getLeftChild(){return leftChild;}
  public Node getRightChild(){return rightChild;}
  public int  getData(){return data;}
  public void setData(int value){this.data=value;}
  public void setLeftChild(Node left){this.leftChild=left;}
  public void setRightChild(Node right){this.rightChild=right;}
}

class inOrderTraversal {

	public static void inTraverse(Node root) {

		if (root == null) return;

		inTraverse(root.getLeftChild());
		System.out.print(root.getData() + ",");
		inTraverse(root.getRightChild());

	}

	public static void main(String[] args) {

		binarySearchTree BST = new binarySearchTree();

		BST.add(6);
		BST.add(4);
		BST.add(9);
		BST.add(5);
		BST.add(8);
		BST.add(12);
		BST.add(2);

		inOrderTraversal.inTraverse(BST.getRoot());

	}

}
{% endhighlight %}

![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/r13.png)

![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/r14.png)

## Post-Order Traversal in Binary Search Tree

## Post-order Traversal
In this type, the elements are traversed in a “left-right-root” order: We first visit the left child node, then the right child, and then comes the turn of root/parent node.

Follow the steps below to perform Post-Order Traversal, starting from the root node:
* Traverse the left sub-tree of currentNode, recursively using PostOrder() function.
* Traverse the right sub-tree of currentNode, recursively using PostOrder() function.
* Visit current node and print its value.

![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/d1.png)
![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/d2.png)
![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/d3.png)
![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/d4.png)
![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/d5.png)
![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/d6.png)
![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/d7.png)
![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/d8.png)
![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/d9.png)
![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/d10.png)
![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/d11.png)
![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/d12.png)
![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/d13.png)
![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/d14.png)
![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/d15.png)

## Implementation in Java
Now we will try to implement the same example in the code below, so have a look:

{% highlight java %}
class binarySearchTree {

  //Variables
  private Node root;
  //Getter for Root

  public Node getRoot() {
    return root;
  }
  public void setRoot(Node root) {
    this.root = root;
  }

  //Searches value in BST
  //Either returns the Node with that value or return null
  public Node search(int value) {

    if (isEmpty()) return null;

    Node currentNode = this.root;

    while (currentNode != null) {

      if (currentNode.getData() == value) return currentNode;

      if (currentNode.getData() > value) currentNode = currentNode.getLeftChild();
      else currentNode = currentNode.getRightChild();
    }

    System.out.println(value + " is not in Tree !");
    return null;
  }
  //Recursive function to insert a value in BST 
  public Node recursive_insert(Node currentNode, int value) {

    //Base Case
    if (currentNode == null) {
      return new Node(value);
    }

    if (value < currentNode.getData()) {
      //Iterate left sub-tree
      currentNode.setLeftChild(recursive_insert(currentNode.getLeftChild(), value));
    } else if (value > currentNode.getData()) {
      //Iterate right sub-tree
      currentNode.setRightChild(recursive_insert(currentNode.getRightChild(), value));
    } else {
      // value already exists
      return currentNode;
    }

    return currentNode;

  }

  //Function to call recursive insert
  public boolean add(int value) {

    root = recursive_insert(this.root, value);
    return true;
  }


  //Function to check if Tree is empty or not  

  public boolean isEmpty() {
    return root == null; //if root is null then it means Tree is empty
  }

  //Just for Testing purpose 
  public void printTree(Node current) {

    if (current == null) return;

    System.out.print(current.getData());
    printTree(current.getLeftChild());
    printTree(current.getRightChild());

  }
}

class Node{

  //Variables
  private  int data;
  Node leftChild;
  Node rightChild;

  //Constructor  
  Node(int value){
    this.data=value;
    leftChild=null;
    rightChild=null;
  }

  //Getter-Setter  
  public Node getLeftChild(){return leftChild;}
  public Node getRightChild(){return rightChild;}
  public int  getData(){return data;}
  public void setData(int value){this.data=value;}
  public void setLeftChild(Node left){this.leftChild=left;}
  public void setRightChild(Node right){this.rightChild=right;}
}


class postOrderTraversal {

	public static void postTraverse(Node root) {

		if (root == null) return;

		postTraverse(root.getLeftChild());
		postTraverse(root.getRightChild());
		System.out.print(root.getData() + ",");

	}

	public static void main(String[] args) 
	{
		binarySearchTree BST = new binarySearchTree();
		BST.add(6);
		BST.add(4);
		BST.add(2);
		BST.add(5);
		BST.add(9);
		BST.add(8);
		BST.add(12);

		postOrderTraversal.postTraverse(BST.getRoot());

	}

}
{% endhighlight %}

![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/d16.png)
![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/d17.png)

## What is an AVL Tree?

## Introduction
AVL trees are a self-balanced special type of Binary Search Tree with just one exception:

For each Node, the maximum height difference between the left and right sub-trees can only be one.

If at any point their difference becomes more than one, then re-balancing is applied to make it a valid AVL tree.

## Time Complexity
As we studied earlier, in the case of BST, the Big(O) of all three basic operations (Insertion, Deletion, and Searching) takes O(h) time, where “h” is the height of a Binary Search Tree.

In the case of Skewed Trees, the complexity becomes O(n), where “n” is the number of nodes in the tree. Now to improve time complexity, We have to manage the height of the tree to improve time complexity, such that we can bring the time down to O(logn) for performing these basic operations.

## When to use AVL Trees?
As AVL are strictly balanced, AVL Trees are preferred in those applications where the lookup​ is the​ ​ most vital operation. The following is an example of a valid AVL Tree:

![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/d18.png)

The tree in the above figure is an AVL Tree, as its subtrees follow the property that each node has a maximum height difference of ​​one.

Given below is an example of an invalid AVL tree as the height between the sibling nodes exceeds one.

![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/d19.png)

## AVL Insertion

## Insertion in AVL Tree
Insertion for an AVL tree follows the same steps that we covered in BST insertion.

The main step comes after insertion when the tree gets unbalanced.

To re-balance the tree, we need to perform some kind of rotation (left or right). But before getting into the deeper concepts that’ll be a mess for you to understand at this point, let’s slowly cover one case at a time.

Let’s look at some of the terms which we will be using while re-balancing the tree.
* Node U – an unbalanced node
* Node C – child node of node U
* Node G – grandchild node of node U

## Insertion Cases
To rebalance the tree, we will perform rotations on the subtree with Node U as being the root node.

There are two types of rotations:
* left
* right

We came across four different scenarios based on the arrangements of Nodes U, C and, G.
* Left-Left: Node C is the left-child of Node U, and Node G is the left-child of Node C.
* Left-Right: Node C is the left-child of Node U, and Node G is the right-child of Node C.
* Right-Right: Node C is the right-child of Node U, and Node G is the right-child of Node C.
* Right-Left: Node C is the right-child of Node U, and Node G is the left-child of Node C.

## Case 1: Left-Left

![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/se1.png)
![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/se2.png)
![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/se3.png)
![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/se4.png)

As you can see in the left-left case, we only need to make a single rotation towards the right at Node U to balance the AVL tree. In the final balanced version, Node C becomes the parent node of Node G and U and its two subtrees become balanced.

## Case 2: Left-Right

![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/se5.png)
![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/se6.png)
![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/se7.png)
![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/se8.png)
![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/se9.png)
![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/se10.png)
![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/se11.png)

In the left-right case we need to make two rotations:
* First is a left rotation at Node C.
* Second is a right rotation at Node U.

These two rotations balance the AVL tree. In this case, Node G becomes the parent node of both Node C and U.

## Case 3: Right-Right

![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/qw1.png)
![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/qw2.png)
![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/qw3.png)
![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/qw4.png)

The right-right case is just like the left-left case. The only difference is that instead of rotating right, we ​need to make a ​single rotation towards the left at Node U to balance the AVL tree. In the final balanced version, Node C becomes the parent node of Node G and U and its two subtrees become balanced.

## Case 4: Right-Left

![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/qw5.png)
![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/qw6.png)
![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/qw7.png)
![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/qw8.png)
![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/qw9.png)
![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/qw10.png)
![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/qw11.png)
![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/qw12.png)

The right-left case is similar to the left-right case. The only difference is that the two rotations performed are as follows:
* First is a right rotation at Node C.
* Second is a left rotation at Node U.

These two rotations balance the AVL tree. In this case, Node G becomes the parent node of both Node C and U.

## Time Complexity
Considering that it takes constant time to do left-right rotation operations and update the height to get a balanced tree, the time complexity of an AVL insert remains the same as BST insert: O(h) where h is the height of the tree. However, since the AVL tree is balanced, the height is O(Logn); so time complexity of an AVL insert is O(Logn).

## AVL Deletion

## Deletion in AVL Tree
Deletion is similar to AVL’s insertion operation with just one exception:

The deletion operation adds an extra step after the insertion method’s rotation and balancing of the first unbalanced node.

After fixing the first unbalanced node through rotations, start moving up and fix the next unbalanced node. Keep on fixing the unbalanced nodes until you reach the root.

## Steps for Deletion
The following are the detailed steps for removing value from AVL Trees.

## Step 1: Delete currentNode
Delete the currentNode in the same way as we did in BST deletion. At this point, the tree will become unbalanced, and we would need to perform some kind of rotation (left or right) to rebalance the tree.

## Step 2: Traverse Upwards
Start traversing from currentNode upwards till you find the first unbalanced node.

Let’s look at some of the terms we will be using while re-balancing the tree.
* Node U — an unbalanced node
* Node C — child node of node U
* Node G — grandchild node of node U

## Step 3: Rebalance the Tree
To rebalance the tree, we will perform rotations on the subtree where U is the root node.

There are two types of rotations:
* left
* right

We came across four different scenarios based on the arrangements of Nodes U, C and, G.
* Left-Left: Node C is the left-child of Node U, and Node G is the left-child of Node C.
* Left-Right: Node C is the left-child of Node U, and Node G is the right-child of Node C.
* Right-Right: Node C is the right-child of Node U, and Node G is the right-child of Node C.
* Right-Left: Node C is the right-child of Node U, and Node G is the left-child of Node C.

After performing a successful rotation for the first unbalanced Node U, traverse up and find the next unbalanced node and perform the same series of operations to balance. Keep on balancing the unbalanced nodes from first Node U to ancestors of Node U until we reach the root. After that point, we will have a fully balanced AVL Tree.

## Case 1: Left-Left

![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/qw13.png)
![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/qw14.png)
![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/qw15.png)
![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/qw16.png)

When a node in our AVL tree is deleted, ​and the tree becomes unbalanced, we traverse upwards from that node till we find the first unbalanced node. In the example above, the first unbalanced node is Node U. If it is the left-left case, we only need to make a single rotation towards the right at the Node U to balance the AVL tree. In the final balanced version, Node C becomes the parent node of Node G and U and its two subtrees become balanced.

## Case 2: Left-Right

![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/qw17.png)
![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/qw18.png)
![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/qw19.png)
![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/qw20.png)
![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/qw21.png)
![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/qw22.png)
![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/qw23.png)

Again, in the example above, the first unbalanced node after performing the deletion operation is denoted as Node U.

It is the left-right case, so we need to make two rotations:
* First is a left rotation at Node C.
* Second is a right rotation at Node U.

These two rotations balance the AVL tree. In this case, Node G becomes the parent node of both Node C and U.

## Case 3: Right-Right

![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/qw24.png)
![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/qw25.png)
![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/qw26.png)
![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/qw27.png)

If the case after deletion is the right-right case, then we need to make a ​single rotation just like the left-left case. However​, in this case,​ it will be a left rotation at Node U to balance the AVL tree. In the final balanced version, Node C becomes the parent node of Node G and U and its two subtrees become balanced.

## Case 4: Right-Left

![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/dd1.png)
![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/dd2.png)
![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/dd3.png)
![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/dd4.png)
![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/dd5.png)
![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/dd6.png)
![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/dd7.png)
![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/dd8.png)

If the case after deletion is a right-left case, then (similar to the left-right case) we need to make two rotations as follows:
* First is a right rotation at Node C.
* Second is a left rotation at Node U.

These two rotations balance the AVL tree. In this case, Node G becomes the parent node of both Node C and U.

## Time Complexity
Considering that it takes constant time to do left-right rotation operations and update the height to get a balanced tree, the time complexity of an AVL insert remains the same as a BST insert: O(h) where h is the height of the tree. However, since AVL tree is balanced, the height is O(Logn). Therefore, the time complexity of AVL delete is O(Logn).

## What is a Red-Black Tree?

## Introduction
A Red-Black Tree is another type of self-balancing Binary Search Tree, just like the AVL Trees that we studied in the previous lesson, but with some additions. The nodes in a Red-Black Tree are colored to either red or black. Colored nodes help in re-balancing the tree after insertion or deletion. There are also some cases used to balance the Red-Black Trees. We will go through the insertion and deletion operations of the Red-Black Tree just like we did in the previous AVL Tree lessons.

## Properties of Red-Black Trees
* Every node has either Red or Black color.
* The root is always colored black.
* Two red nodes cannot be adjacent, i.e. no red parent can have a red child and vice versa.
* Every path from the root to a leaf must contain the exact same number of black-colored nodes.
* Every null node is considered to be black in color.

From the perspective of implementation, our node class will contain a boolean variable in addition that will store the information about the color of a node.

Given below is the basic structure of a Node which will be used to build a Red-Black Tree.

![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/aaa1.png)

The following is an example of a valid Red-Black Tree:

![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/aaa2.png)

## Time Complexity
Balancing the tree doesn’t result in a tree being perfectly balanced, but it is good enough to get the time complexity close to O(log n)O(logn) for basic operations like searching, deletion, and insertion.

## AVL vs Red-Black Trees
Although AVL Trees are more balanced than Red-Black Trees, AVL Trees take more rotations during insertion and deletion operations than Red-Black Trees. So, if you have a search intensive application where insertion and deletion are not that frequent, then use AVL Trees. Otherwise, use Red-Black Trees for those applications involving more insertions and deletions.

## Red-Black Tree Insertion

## Insertion in Red-Black Tree 
The following are the steps involved in inserting value into a Red-Black Tree:

1. Insert currentNode using the standard BST insertion technique that we studied earlier, and make currentNode red.
2. If currentNode is the root, then change the color of currentNode to black.
3. If currentNode is not the root, then we will have to perform some operations to make the tree follow the Red-Black property.

## Rebalancing the Tree 
To balance an unbalanced tree, we have two techniques which are used depending on some conditions that we will discuss shortly. The two techniques are:
* Recoloring Nodes.
* Rotating Nodes (left or right).

But before going deeper into the concepts that’ll be a mess for you to understand at this point, let’s slow down and go step by step.

First, we need to define the structure of the Red-Black Tree and some nodes relative to the currentNode, which is the node that we inserted in the Red-Black Tree.
* Node C – newly inserted node (currentNode)
* Node P – parent of currentNode
* Node G – grandparent of currentNode
* Node U – uncle of currentNode / sibling of Node P / child of Node G

If currentNode is not a root, and the parent of currentNode is not black, first, we will check Node U (the uncle of currentNode). Based on Node U’s color, we will perform some steps to make the tree balanced. If Node U is red, then do the following:
* Change the color of Node P and U to black
* Change the color of Node G to red
* Make Node G the currentNode and repeat the same process from step two

Disclaimer: The illustrations given in this lesson are providing the visual representation of one case at a time. Therefore, you may notice that the tree gets unbalanced at the end of some of the illustrations. These trees have dummy values. However, in the case of an actual tree with real values, if one step ends up unbalancing the tree, then we keep moving in a bottom-up manner and applying the next possible case until the tree gets balanced again.

![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/aaa3.png)
![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/aaa4.png)
![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/aaa5.png)
![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/aaa6.png)
![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/aaa7.png)
![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/aaa8.png)

If Node U (uncle) is black, then we come across four different scenarios based on the arrangements of Node P and G, just like we did in AVL trees. We will cover each of these scenarios and try to help you understand by using illustrations:
* Left-Left: Node P is the leftChild of Node G, and currentNode is the leftChild of Node P
* Left-Right: Node P is the leftChild of Node G, and currentNode is the rightChild of Node P
* Right-Right: Node P is the rightChild of Node G, and currentNode is the rightChild of Node P
* Right-Left: Node P is the rightChild of Node G, and currentNode is the leftChild of Node P

## Case 1: Left-Left
When Node P is the leftChild of Node G, and currentNode is the leftChild of Node P, we perform the following steps:
1. Rotate Node G towards the Right
2. Swap the colors of Nodes G and P

Look at the illustration below for a better understanding.

![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/aaa9.png)
![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/aaa10.png)
![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/aaa11.png)
![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/aaa12.png)
![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/aaa13.png)

## Case 2: Left-Right
When Node P is the leftChild of Node G, and currentNode is the rightChild of Node P, we perform the following steps:
1. Rotate Node P towards the Left
2. After that, repeat the steps that we covered in Left-Left case

Look at the illustration below for a better understanding.

![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/aaa14.png)
![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/aaa15.png)
![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/aaa16.png)
![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/aaa17.png)
![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/aaa18.png)
![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/aaa19.png)
![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/aaa20.png)
![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/aaa21.png)

## Case 3: Right-Right
When Node P is the rightChild of Node G, and currentNode is the rightChild of Node P, we perform the following steps:
1. Rotate Node G towards the Left
2. Swap the colors of Nodes G and P

Look at the illustration below for a better understanding.

![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/aaa22.png)
![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/aaa23.png)
![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/aaa24.png)
![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/aaa25.png)
![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/aaa26.png)

## Case 4: Right-Left
When Node P is the rightChild of Node G, and currentNode is the leftChild of Node P, we perform the following steps:
1. Rotate Node P towards Right
2. After that, repeat the steps that we covered in Right-Right case

Look at the illustration below for a better understanding.

![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/aaa27.png)
![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/aaa28.png)
![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/aaa29.png)
![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/aaa30.png)
![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/aaa31.png)
![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/aaa32.png)
![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/aaa33.png)
![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/aaa34.png)

## Red-Black Tree Deletion

## Deletion in Red-Black Tree 
Before we start discussing how deletion works in a Red-Black Tree, let’s see the main difference between insertion and deletion operations in Red-Black Trees.

In insertion, we may violate the property of a red parent having a red child. At the same time, in a deletion operation, we may end up deleting a black node which could violate the property of, “the same number of black nodes from root to the null for every path”.

In insertion, we check the color of the uncle node (uncle to currentNode), and based on the color we perform appropriate operations to balance the tree. In the deletion operation, we will check the color of the sibling node (sibling to currentNode), and based on its color we will perform some actions to balance the tree again.

Disclaimer: The illustrations given in this lesson are providing the visual representation of one case at a time. Therefore, you may notice that the tree gets unbalanced at the end of some of the illustrations. These trees have dummy values. However, in the case of an actual tree with real values, if one step ends up unbalancing the tree, then we keep moving in a bottom-up manner and applying the next possible case until the tree gets balanced again.

## Steps for Deletion
Following are the steps involved to remove any value in a Red-Black Tree:
1. Search for a node with the given value to remove. We will call it currentNode
2. Remove currentNode using standard BST deletion operation that we studied earlier

We already know that for deletion in BST, we always end up deleting either a leaf node or a node with only one child.
* In the case of leaf node deletion, it is easy to just delete the node and link the parent of the node to be deleted with null
* In the case of a node with one child, deletion is relatively easy as we just link the parent of the node to be deleted with that one child

Let’s name some nodes relative to Node C, which is the node that we want to delete:
* Node C – node to be deleted (currentNode)
* Node P – parent node of currentNode
* Node S – sibling node (once we rotate tree, Node R will have a sibling node which we name as Node S)
* Node SC – child node of Node S
* Node R – node to be replaced with currentNode and linked with Node P (Node R is the single child of Node C)

## Deletion Cases 
Now we will take a look at some of the deletion cases and see what steps should be performed in each of these cases to make the tree balanced again. Given below is the first case in which Node C or Node R is red. In this type of scenario, we make Node R black and link it to Node P.

![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/qwe1.png)
![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/qwe2.png)
![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/qwe3.png)
![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/qwe4.png)
![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/qwe5.png)

The second case is if both Node C and Node R are black, then make Node R black. Now Node R is double black, i.e. it was already black, and when both Node C and Node R are black, then we make Node R black again. Remember that null is always considered to have a black color.

Now we will convert Node R from double to single black.

![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/qwe6.png)
![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/qwe7.png)
![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/qwe8.png)
![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/qwe9.png)
![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/qwe10.png)

We need to perform the following steps while Node R is double black and not the root of the Tree. Use the specifications that Node S (sibling of Node R) is black and one or both of Node S children are red:
* Left-Left: Node S is the leftChild of Node P, and Node SC (red) is the leftChild of S, or both children of S are red.
* Right-Right: Node S is the rightChild of Node P, and Node SC (red) is the rightChild of S, or both children of S are red.
* Left-Right: Node S is the leftChild of Node P and Node SC (red) is the rightChild of S.
* Right-Left: Node S is the rightChild of Node P and Node SC (red) is the leftChild of S.

## Case 1: Left-Left 
In the case when Node S is the leftChild of Node P, and Node SC (red) is the leftChild of S or both children of S are red, we perform the following steps:
1. Rotate Node P towards the right
2. Make the right child of Node S the left child of Node P

Look at the illustration below for a better understanding.

![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/qwe11.png)
![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/qwe12.png)
![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/qwe13.png)
![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/qwe14.png)
![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/qwe15.png)
![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/qwe16.png)
![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/qwe17.png)

## Case 2: Right-Right 
In the case when Node S is the rightChild of Node P, and Node SC (red) is the rightChild of S or both children of S are red, we perform the following steps:
1. Rotate Node P towards the left
2. Make the left child of Node S the right child of Node P

Look at the illustration below for a better understanding.

![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/qwe18.png)
![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/qwe19.png)
![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/qwe20.png)
![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/qwe21.png)
![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/qwe22.png)
![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/qwe23.png)
![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/qwe24.png)
![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/qwe25.png)

## Case 3: Left-Right 
In the case when Node S is the leftChild of Node P and Node SC (red) is the rightChild of S, we perform the following steps:
1. Rotate Node S towards the left
2. Rotate Node P towards the right

Look at the illustration below for a better understanding.

![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/qwe26.png)
![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/qwe27.png)
![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/qwe28.png)
![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/qwe29.png)
![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/qwe30.png)
![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/qwe31.png)
![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/qwe32.png)
![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/qwe33.png)
![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/qwe34.png)

## Case 4: Right-Left
In the case when Node S is the rightChild of Node P and Node SC (red) is the leftChild of S, we perform the following steps:
1. Rotate Node S towards the right
2. Rotate Node P towards the left

Look at the illustration below for a better understanding.

![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/qwe35.png)
![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/qwe36.png)
![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/qwe37.png)
![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/qwe38.png)
![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/qwe39.png)
![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/qwe40.png)
![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/qwe41.png)
![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/qwe42.png)
![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/qwe43.png)
![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/qwe44.png)

Till this point, we have studied a number of trees from Binary Trees to different types of Binary Trees like BST, and then even further types of BST like AVL and Red-Black Trees. We have covered both basic deletion and insertion operations of these trees along with Java Implementation of BST. We are now left with only one important tree data structure known as 2-3 Trees. So, in the next lesson, we will cover it in detail just like we did with the rest of the tree structures.

## Overview of Trees

![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/qwe45.png)

![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/qwe46.png)

![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/qwe47.png)
![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/qwe48.png)

![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/qwe49.png)
![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/qwe50.png)

![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/qwe51.png)
![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/qwe52.png)


{% highlight java %}

{% endhighlight %}