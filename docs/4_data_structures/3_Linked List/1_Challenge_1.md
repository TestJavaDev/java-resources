---
layout: default
title: Challenge 1
parent: Linked Lists
grand_parent: Data Structures
nav_order: 1
permalink: /data_structures/linked_lists/ch1
---
<div align="center" markdown="1">
Challenge 1 / Java resources / Tutorial

{: .fs-8 .fw-400 }
</div>

## Challenge 1: Insertion in a Singly Linked List (insert at End)

## Insertion at End 
Now, we are going to explain the second part (Insertion at End) and look at its examples, along with one coding challenge for the sake of practice. So let’s see how elements are inserted at the end of a linked list. In this type of insertion, we add an element at the end of the list. Here’s an illustration of how insertionAtEnd() works in a Singly Linked List:

![lin](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/lin/lin36.png)
![lin](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/lin/lin37.png)
![lin](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/lin/lin38.png)
![lin](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/lin/lin39.png)
![lin](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/lin/lin40.png)
![lin](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/lin/lin41.png)
![lin](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/lin/lin42.png)
![lin](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/lin/lin43.png)
![lin](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/lin/lin44.png)
![lin](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/lin/lin45.png)
![lin](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/lin/lin46.png)

## Problem Statement
Here’s a small coding exercise made for your practice. In the code snippet provided below, you will complete the void insertAtEnd(T data) method. This will take a generic type T value called data and insert that value at the end of the list. This code would be the part of the SinglyLinkedList class that we created in the previous lesson, therefore, any private members of that class can be accessed inside the function as well. After writing the code, run it and see how many tests you passed.

## Method Prototype
void insertAtEnd(T data)

## Output
The return type of the method is void. The object on which it is called will be modified only.

## Sample Input
linkedlist = 0->1->2
data = 3
## Sample Output
linkedlist = 0->1->2->3

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

    // Helper Function that checks if List is empty or not 
    // public boolean isEmpty() 

    // Inserts new data at the start of the linked list
    // public void insertAtHead(T data) 

    // Helper Function to printList
    // public void printList() 

    public void insertAtEnd(T data) {
        // Write -- Your -- Code
    }
}
{% endhighlight %}

## Solution Review: Insertion in a Singly Linked List(insert at End)

{% highlight java %}
public class SinglyLinkedList<T> {
//Node inner class for SLL
    public class Node {
        public T data;
        public Node nextNode;

    }

    public Node headNode; //head node of the linked list
    public int size;      //size of the linked list

    //Constructor - initializes headNode and size
    public SinglyLinkedList() {
        headNode = null;
        size = 0;
    }

    //Helper Function that checks if List is empty or not 
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

    // Helper Function to printList
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
}

class CheckInsertion {
    public static void main( String args[] ) {
        SinglyLinkedList<Integer> sll = new SinglyLinkedList<Integer>();
        sll.printList();
        for (int i = 1; i <= 10; i++) {
			      sll.insertAtEnd(i);
			      sll.printList();
        }
    }
}
{% endhighlight %}

![lin](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/lin/lin47.png)



