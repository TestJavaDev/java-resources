---
layout: default
title: Challenge 1
parent: Trees
grand_parent: Data Structures
nav_order: 1
permalink: /data_structures/trees/ch1
---
<div align="center" markdown="1">
Challenge 1 / Java resources / Tutorial

{: .fs-8 .fw-400 }
</div>

## Challenge 1: Find the Minimum Value in a Binary Search Tree

Given the root to a binary search tree, write a function to find the minimum value in that tree. A solution is placed in the "solution" section to help you, but we would suggest you try to solve it on your own first.

![trie](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/tree/aa1.png)

![tree](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/tree/aa2.png)

![tree](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/tree/aa3.png)

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

    System.out.print(current.getData()+",");
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


class CheckMin 
{
	public static int findMin(Node root) 
  {
		// Write - Your - Code
		return Integer.MIN_VALUE;
	}
}
{% endhighlight %}

## Solution Review: Find the Minimum Value in a Binary Search Tree

## Solution #1: Iterative findMin()

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

class CheckMin {

    public static int findMin(Node root) {
        
        if (root == null)
            return -1;
        // In Binary Search Tree, all values in current node's left subtree are smaller 
        // than the current node's value.
        // So keep traversing (in order) towards left till you reach leaf node, and then return leaf node's value
        while (root.getLeftChild() != null) {
            root = root.getLeftChild();
        }
        return root.getData();
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
        bsT.add(10);
        bsT.add(14);

        System.out.println(findMin(bsT.getRoot()));

    }
}
{% endhighlight %}

![tree](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/tree/aa4.png)

## Solution #2 : Recursive findMin()

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

class CheckMin {

    public static int findMin(Node root) {


        // So keep traversing (in order) towards left till you reach leaf node,
        //and then return leaf node's value
        if (root == null)
            return -1;
        else if (root.getLeftChild() == null)
            return root.getData();
        else
            return findMin(root.getLeftChild());

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
        bsT.add(10);
        bsT.add(14);

        System.out.println(findMin(bsT.getRoot()));

    }
}
{% endhighlight %}

![tree](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/tree/aa5.png)
