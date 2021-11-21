---
layout: default
title: Challenge 3
parent: Tree
grand_parent: Data Structures
nav_order: 3
permalink: /data_structures/trees/ch3
---
<div align="center" markdown="1">
Challenge 3 / Java resources / Tutorial

{: .fs-8 .fw-400 }
</div>

## Challenge 3: Find Ancestors of Given Node in Binary Search Tree

Given the root to a Binary Search Tree and a node value "k", write a function to find the ancestor of that node. A solution is placed in the "solution" section to help you, but we would suggest you try to solve it on your own first.

![trie](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/trie/aa11.png)

![trie](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/trie/aa12.png)

![trie](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/trie/aa13.png)

## Coding Exercise

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

class CheckAncestors {
  public static String findAncestors(Node root, int k) {
    return "";
  }
}
{% endhighlight %}

## Solution Review: Find Ancestors of a Given Node in a BST

## Solution

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

class IterativeAncesstors
{ 
	// Iterative Function to print all ancestors of a given key 
	public static String findAncestors(Node root, int k) { 
		
		String result = ""; 
		Node tempNode = root; 
		while(tempNode != null && tempNode.getData() != k){ 
			result = result + tempNode.getData() + ","; 
			if(k <= tempNode.getData()){ 
				tempNode = tempNode.getLeftChild(); 
			} else{ 
				tempNode = tempNode.getRightChild(); 
			} 
		} 
		if(tempNode == null){ 
			return ""; 
		} 
		return result; 
	}

	// Driver code 
	public static void main(String[] args) 
	{ 		
		binarySearchTree tree = new binarySearchTree(); 		
		/* Construct a binary tree like this
				6
			   / \
			  4   9
			 / \  |  \
			2	5 8	  12
					  / \
					 10  14 
		*/
		tree.add(6); 
		tree.add(4); 
		tree.add(9); 
		tree.add(2); 
		tree.add(5); 
		tree.add(8); 
		tree.add(8); 
		tree.add(12); 
		tree.add(10); 
		tree.add(14); 

		int key = 10; 
		System.out.print(key + " --> ");
		System.out.print(findAncestors(tree.getRoot(), key)); 

		System.out.println();
		key = 5; 
		System.out.print(key + " --> ");
		System.out.print(findAncestors(tree.getRoot(), key)); 
	} 
} 
{% endhighlight %}

![trie](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/trie/aa14.png)