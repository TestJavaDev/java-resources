---
layout: default
title: Singly Linked List Deletion
parent: Linked Lists
grand_parent: Data Structures
nav_order: 4
permalink: /data_structures/linked_lists/deletion
---
<div align="center" markdown="1">
Singly Linked List Deletion / Java resources / Tutorial

{: .fs-8 .fw-400 }
</div>

## Singly Linked List Deletion (Implementation)

## Introduction 
The deletion operation combines principles from both insertion and search. It uses the search functionality to find the value in the list.

Deletion is one of the instances where linked lists are more efficient than arrays. In an array, you have to shift all the elements backward if one element is deleted. Even then, the end of the array is empty, and it takes up unnecessary memory.

In the case of linked lists, the node is removed at head merely in constant time.

Let’s take a look at the different types of deletion operations we can perform in singly-linked lists.

## Types of Deletion 
There are two basic delete operations for linked lists:
1. Deletion at head
2. Deletion by value

In this lesson, we will look at the implementation of the deletion at the head algorithm. The rest will be covered in the following lessons.

## Deletion at Head 
This operation simply deletes a node from the head of the list, which means that it always deletes the first element of the list. This type of deletion is used when your list is ordered, and you want to implement a priority queue–via a linked list-- to keep track of all the elements. Here’s an illustration of how this type of deletion works in a Singly Linked List:

![lin](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/lin/lin60.png)
![lin](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/lin/lin61.png)
![lin](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/lin/lin62.png)
![lin](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/lin/lin63.png)
![lin](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/lin/lin64.png)
![lin](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/lin/lin65.png)
![lin](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/lin/lin66.png)

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

    //Deletes data from the head of list
    public void deleteAtHead() {
        //if list is empty then simply return
        if (isEmpty())
            return;
        //make the nextNode of the headNode equal to new headNode
        headNode = headNode.nextNode;
        size--;
    }
}

class CheckDeletion {
  public static void main( String args[] ) {
        SinglyLinkedList<Integer> sll = new SinglyLinkedList<Integer>(); 
        for (int i = 1; i <= 10; i++) {
			    sll.insertAtEnd(i);
        }
        sll.printList();
        System.out.println("1: Calling Deletion At Head Function: ");
        sll.deleteAtHead();
        sll.printList();
        System.out.println("2: Calling Deletion At Head Function: ");
        sll.deleteAtHead();
        sll.printList();
    }
}
{% endhighlight %}

![lin](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/lin/lin67.png)