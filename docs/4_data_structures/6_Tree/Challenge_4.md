---
layout: default
title: Challenge 4
parent: Trees
grand_parent: Data Structures
nav_order: 4
permalink: /data_structures/trees/ch4
---
<div align="center" markdown="1">
Challenge 4 / Java resources / Tutorial

{: .fs-8 .fw-400 }
</div>

## Challenge 4: Find the Height of a Binary Search Tree

![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/aa15.png)

![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/aa16.png)

![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/aa17.png)

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

class CheckHeight {

  public static int findHeight(Node root) {

    // Write - Your - Code
    return Integer.MIN_VALUE;
  }
}
{% endhighlight %}

## Solution Review: Find the Height of a Binary Search Tree

## Solution: recursively finding the heights of the left and right sub-trees

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

class checkHeight {
  public static int findHeight(Node root) {
    //Base case, leaf nodes have 0 height
    if (root == null) return -1;
    else {
      return 1 + Math.max(findHeight(root.getLeftChild()),findHeight(root.getRightChild()));
      // Find Height of left subtree right subtree
      // Return greater height value of left or right subtree (plus 1)
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
    bsT.add(12);
    
    System.out.println(findHeight(bsT.getRoot()));

  }
}
{% endhighlight %}

![tree](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/tree/aa18.png)