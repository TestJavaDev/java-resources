---
layout: default
title: Challenge 5
parent: Trees
grand_parent: Data Structures
nav_order: 5
permalink: /data_structures/trees/ch5
---
<div align="center" markdown="1">
Challenge 5 / Java resources / Tutorial

{: .fs-8 .fw-400 }
</div>

## Challenge 5: Find Nodes at "k" Distance from the Root

Given the root to a Binary Search Tree and a value "k", write a function to find the nodes at "k" distance from the root. A solution is placed in the "solution" section to help you, but we would suggest you try to solve it on your own first.

![tree](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/tree/aa19.png)

![tree](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/tree/aa20.png)

![tree](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/tree/aa21.png)

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

class CheckKNodes {

	public static String findKNodes(Node root, int k) {

		//Write Your Code Here
		return "ready-set-go";
	}
}
{% endhighlight %}

## Solution Review: Find Nodes at "k" Distance from the Root

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

class CheckKNodes {

  public static String findKNodes(Node root, int k) {

    StringBuilder result = new StringBuilder(); //StringBuilder is immutable
    result = findK(root, k, result);

    return result.toString();
  }

  //Helper recursive function to traverse tree and append all the nodes 
  // at k distance into result StringBuilder
  public static StringBuilder findK(Node root, int k, StringBuilder result) {

    if (root == null) return null;

    if (k == 0) {
      result.append(root.getData() + ",");
    }
    else {
      //Decrement k at each step till you reach at the leaf node 
      // or when k == 0 then append the Node's data into result string
      findK(root.getLeftChild(), k - 1, result);
      findK(root.getRightChild(), k - 1, result);
    }
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
    bsT.add(12);
 
    System.out.println(findKNodes(bsT.getRoot(), 2));

  }

}
{% endhighlight %}

![tree](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/tree/aa22.png)