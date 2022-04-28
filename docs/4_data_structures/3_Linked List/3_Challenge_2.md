---
layout: default
title: Challenge 2
parent: Linked Lists
grand_parent: Data Structures
nav_order: 3
permalink: /data_structures/linked_lists/ch2
---
<div align="center" markdown="1">
Challenge 2 / Java resources / Tutorial

{: .fs-8 .fw-400 }
</div>

## Challenge 2: Search in Singly Linked List

## Introduction 
Now, we will take a look at the second most important operation, i.e. searching for an element in a linked list. This exercise of finding a value in a Singly Linked List is relatively more straightforward than the other three operations of insertion.

## Searching For A Node
The steps to search for a node in a Singly Linked List are as follows:
1. Start from the headNode.
2. Traverse the list till you either find a node with the given value, or you reach the end showing that the node being searched doesn’t exist.

## Problem Statement
If you know how to insert an element in a list, then searching for an item will not be that difficult for you. Now, based on the steps mentioned above, we have designed a simple coding exercise for your practice. There is a solution placed in the solution section for your help, but try to solve it on your own first.

## Method Prototype 
boolean searchNode(T data)

## Output 
It returns true or false to show if a certain value does or does not exists in the list.

## Sample Input 
linkedlist = 5->90->10->4   and  value = 4

## Sample Output 
true

## Coding Exercise

{% highlight java %}
    // This function is inside the linked list class 
    // You can access all private members of the class
    // Here is how the class looks like
    // Node inner class for SLL
    // public class Node {
    //    public T data;
    //    public Node nextNode;
    // } 

    // public Node headNode; // head node of the linked list
    // public int size;      // size of the linked list

    // Access HeadNode => this.headNode;

    // Helper Function that checks if List is empty or not 
    // public boolean isEmpty() 

    // Helper Function to printList
    // public void printList() 

    public boolean searchNode(T data) {
        // Write -- Your -- Code
        return false; //value not found
    }
}
{% endhighlight %}

## Solution Review: Search in a Singly Linked List

{% highlight java %}
public class SinglyLinkedList<T> {
    //Node inner class for SLL
    public class Node {
        public T data;
        public Node nextNode;

    }

    //head node of the linked list
    public Node headNode;
    public int size;

    //constructor
    public SinglyLinkedList() {
        headNode = null;
        size = 0;
    }

    public boolean isEmpty() {

        if (headNode == null) return true;
        return false;
    }

    //Inserts new data at the start of the linked list
    public void insertAtHead(T data) {
        //Creating a new node and assigning it the new data value
        Node newNode = new Node();
        newNode.data = data;
        //Linking head to the newNode's nextNode
        newNode.nextNode = headNode;
        headNode = newNode;
        size++;
    }

    //Inserts new data at the end of the linked list
    public void insertAtEnd(T data) {
        //if the list is empty then call insertATHead()
        if (isEmpty()) {
            insertAtHead(data);
            return;
        }
        //Creating a new Node with value data
        Node newNode = new Node();
        newNode.data = data;
        newNode.nextNode = null;

        Node last = headNode;
        //iterate to the last element
        while (last.nextNode != null) {
            last = last.nextNode;
        }
        //make newNode the next element of the last node
        last.nextNode = newNode;
        size++;
    }

    //inserts data after the given prev data node
    public void insertAfter(T data, T previous) {

        //Creating a new Node with value data
        Node newNode = new Node();
        newNode.data = data;
        //Start from head node
        Node currentNode = this.headNode;
        //traverse the list until node having data equal to previous is found
        while (currentNode != null && currentNode.data != previous) {
            currentNode = currentNode.nextNode;
        }
        //if such a node was found
        //then point our newNode to currentNode's nextElement
        if (currentNode != null) {
            newNode.nextNode = currentNode.nextNode;
            currentNode.nextNode = newNode;
            size++;
        }
    }

    public void printList() {
        if (isEmpty()) {
            System.out.println("List is Empty!");
            return;
        }

        Node temp = headNode;
        System.out.print("List : ");

        while (temp.nextNode != null) {
            System.out.print(temp.data.toString() + " -> ");
            temp = temp.nextNode;
        }

        System.out.println(temp.data.toString() + " -> null");
    }

    //Searches a value in the given list.
    public boolean searchNode(T data) {
        //Start from first element
        Node currentNode = this.headNode;

        //Traverse the list till you reach end
        while (currentNode != null) {
            if (currentNode.data.equals(data))
                return true; //value found

            currentNode = currentNode.nextNode;
        }
        return false; //value not found
    }
}

class CheckSearch {  
    public static void main(String args[]) {
        SinglyLinkedList<Integer> sll = new SinglyLinkedList<Integer>(); 
        for (int i = 1; i <= 10; i++) {
            sll.insertAtEnd(i);
        }

        if(sll.searchNode(3)) {   // Calling search function
            System.out.println("Value: 3 is Found");
        }
        else {
            System.out.println("Value: 3 is not Found");
        }

        if(sll.searchNode(15)) {   // Calling search function
            System.out.println("Value: 15 is Found");
        }
        else {
            System.out.println("Value: 15 is not Found");
        }
    }
}
{% endhighlight %}

![lin](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/lin/lin59.png)