---
layout: default
title: Challenge 2
parent: Trees
grand_parent: Data Structures
nav_order: 2
permalink: /data_structures/trees/ch2
---
<div align="center" markdown="1">
Challenge 2 / Java resources / Tutorial

{: .fs-8 .fw-400 }
</div>

## Challenge 2: Find kth Maximum Value in a Binary Search Tree

Given the root to a binary search tree--a number "k"--write a function to find the kth maximum value in that tree. A solution is placed in the "solution" section to help you, but we would suggest you try to solve it on your own first.

![tree](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/tree/aa6.png)

![tree](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/tree/aa7.png)

![tree](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/tree/aa8.png)

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

class CheckKthMax {

	public static int findKthMax(Node root, int k) {

		// Write - Your - Code
		return Integer.MAX_VALUE;
	}
}
{% endhighlight %}

## Solution Review: Find kth Maximum Value in a Binary Search Tree

## Solution #1: Sorting the tree in order

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

class CheckKthMax {

  public static int findKthMax(Node root, int k) {

    //Perform In-Order Traversal to get sorted array. (ascending order)
    //Return value at index [length - k]
    StringBuilder result = new StringBuilder(); //StringBuilder is mutable
    result = inOrderTraversal(root, result);

    String[] array = result.toString().split(","); //Spliting String into array of strings
    if ((array.length - k) >= 0) return Integer.parseInt(array[array.length - k]);

    return - 1;
  }

  //Helper recursive function to traverse tree using inorder traversal
  //and return result in StringBuilder
  public static StringBuilder inOrderTraversal(Node root, StringBuilder result) {

    if (root.getLeftChild() != null) inOrderTraversal(root.getLeftChild(), result);

    result.append(root.getData() + ",");

    if (root.getRightChild() != null) inOrderTraversal(root.getRightChild(), result);

    return result;
  }

  public static void main(String args[]) {

    binarySearchTree bsT = new binarySearchTree();

    bsT.add(6);

    bsT.add(4);
    bsT.add(9);
    bsT.add(5);
    bsT.add(2);
    bsT.add(8);

    System.out.println(findKthMax(bsT.getRoot(),3));
  }
}
{% endhighlight %}

![tree](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/tree/aa9.png)

## Solution #2: Recursive Approach

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

class CheckKthMax {

  static int  counter; //global count variable
  //used as a wrapper for the recursive algorithm
  public static int findKthMax(Node root, int k) {
    counter = 0;
    Node node = findKthMaxRecursive(root, k);
    if(node != null)
      return node.getData();
    return -1;
  }
  
  public static Node findKthMaxRecursive(Node root, int k) {
    if(root==null){
      return null;
    }
    //Recursively reach the right-most node (which has the highest value)
    Node node = findKthMaxRecursive(root.getRightChild(), k);

    if(counter != k){
      //Increment counter if kth element is not found
      counter++;
      node = root;
    }
    //Base condition reached as kth largest is found
    if(counter == k){
      return node;
    }else{
      //Traverse left child if kth element is not reached
      return findKthMaxRecursive(root.getLeftChild(), k);
    }
  }

  public static void main(String args[]) {

    binarySearchTree bsT = new binarySearchTree();

    bsT.add(6);
    bsT.add(4);
    bsT.add(9);
    bsT.add(5);
    bsT.add(2);
    bsT.add(8);

    System.out.println(findKthMax(bsT.getRoot(),3));
  }
}
{% endhighlight %}

![tree](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/tree/aa10.png)
