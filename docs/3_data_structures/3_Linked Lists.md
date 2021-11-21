---
layout: default
title: Linked Lists
parent: Data Structures
nav_order: 3
permalink: /data_structures/linked_lists
---
<div align="center" markdown="1">
Linked Lists / Java resources / Tutorial

{: .fs-8 .fw-400 }
</div>

## Linked List 

## What is the Singly Linked List (SLL)?

Introduction #
Linked Lists and Arrays are quite similar in characteristics as they are both used to store a collection of the same type of data. A data type can be anywhere from a simple primitive integer to a complex object of a particular class. However, the structure of the Linked List is very different as compared to Arrays.

Applications #
Some important applications of Linked Lists include:

Implementing HashMaps, File System and Adjacency Lists
Dynamic memory allocation: We use linked lists of free blocks
Performing arithmetic operations on long integers
Maintaining a directory of names
Structure of Linked List #
A linked list is formed by nodes that are linked together like a chain. Each node holds data, along with a pointer to the next node in the list. The Singly Linked List (SLL) is the type of linked list where each node has only one pointer that stores the reference to the next value. The following illustration shows a Singly Linked List.

![lin](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/lin/lin1.png)

In the next few lessons, we will look at how SLL is implemented and study its basic operations in detail. To implement a linked list, we need the following two classes:

Class Node
Class LinkedList
Class Node #
The Node class stores data in a single node. It can store primitive data such as integers and string as well as complex objects having multiple attributes. Along with data, it also stores a pointer to the next element in the list, which helps in linking the nodes together like a chain. Here’s a typical definition of a Node class:

![lin](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/lin/lin2.png)

Explanation: The code above provides a basic definition of a Node class structure with two data members: one to hold the data and the other one to store a reference to the next element. This class is a generic class made by using Java Generics. The data variable can hold any data-type value specified.

Class Linked list #
As mentioned above, the Singly Linked list is made up of nodes that are linked together like a chain. Now to access this chain, we would need a pointer that keeps track of the first element of the list. As long as we have information about the first element, we can traverse the rest of the list without worrying about memorizing their storage locations.

The Singly Linked List contains a head node: a pointer pointing to the first element of the list. Whenever we want to traverse the list, we can do so by using this head node. Below is a basic structure of the Singly Linked List’s class:

![lin](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/lin/lin3.png)

Explanation: In the above class, we see a headNode variable of type Node. It will point to the start of the list (i.e., head of the list). In the constructor, we initialize that headNode node so that it becomes functional. If a head node points to nothing (NULL), this means that the list is empty. As you can see in the above illustration, the head points to the first element and the last pointer points to NULL to indicate the end of the list.

## Basic Linked List Operations

Operations #
Following are the basic operations of a Singly Linked List:

![lin](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/lin/lin4.png)

If you observe the list of methods mentioned above, the last function, isEmpty() is a helper function which will prove useful in defining all the other functions.

So let’s define it first.

isEmpty() #
The basic condition for our list to be considered empty is that the head should be the only pointer in the list. This implies that the head points to NULL.

With that in mind, let’s write down the simple implementation for isEmpty():

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
}
{% endhighlight %}

Explanation #
Nothing tricky going on here. The crux of the code lies in the if condition on line 20. We merely check if the head is empty.

Note: Even when a linked list is empty, the head Node must always exist.

Time Complexity #
The time complexity of isEmpty() method is O(1)O(1).

This is just the tip of the iceberg. We’ll tackle each of the methods above in the following lessons and apply them to relevant problems.

## Insertion in a Singly Linked List

Introduction #
In this lesson, we are going to briefly explain the basic operations which were discussed in the previous lesson and implement them using Java code. The three types of insertion strategies used in a Singly Linked List are:

Insert at Head
Insert at End
Insert After
Insertion at Head #
This type of insertion means that we want to insert a new element as the first element of the list. As the head always points to the first element of the list, insertion at head means that we are inserting the first element in the list. The following figure shows how InsertAtHead() happens in Singly Linked List:

![lin](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/lin/lin5.png)
![lin](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/lin/lin6.png)
![lin](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/lin/lin7.png)
![lin](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/lin/lin8.png)
![lin](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/lin/lin9.png)
![lin](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/lin/lin10.png)
![lin](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/lin/lin11.png)
![lin](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/lin/lin12.png)

Insert at End #
This type of insertion means that we want to insert a new element as the last element of the list. The original tail element of the list has a nextElement pointer that points to NULL. To insert a new tail node, we have to point the nextElement pointer of the previous tail node to the new tail node, allowing the nextElement of the new tail to now point to NULL. The following figure illustrates this insertion.

![lin](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/lin/lin13.png)
![lin](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/lin/lin14.png)
![lin](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/lin/lin15.png)
![lin](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/lin/lin16.png)
![lin](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/lin/lin17.png)
![lin](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/lin/lin18.png)
![lin](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/lin/lin19.png)
![lin](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/lin/lin20.png)
![lin](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/lin/lin21.png)
![lin](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/lin/lin22.png)
![lin](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/lin/lin23.png)

Insert After #
This insertion is a little more tricky when compared to insert at the head and insert at the end. Here, we specify the node (e.g. n), after which we want to insert the new node. To insert this node, we follow these steps:

We traverse the linked list to look for n.
As soon as we find it, we assign n's nextElement to the new node’s nextElement.
Then we point n's nextElement to the new node.
The following figure illustrates how this is done.

![lin](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/lin/lin24.png)
![lin](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/lin/lin25.png)
![lin](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/lin/lin26.png)
![lin](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/lin/lin27.png)
![lin](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/lin/lin28.png)
![lin](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/lin/lin29.png)
![lin](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/lin/lin30.png)
![lin](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/lin/lin31.png)
![lin](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/lin/lin32.png)
![lin](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/lin/lin33.png)
![lin](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/lin/lin34.png)

Implementation #
For this lesson, we are only looking at the first strategy, insert at the head; the other two will be covered later. The implementation of this operation is simple and straightforward. Take a look at the following code that shows how to implement this method in Java:

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
}
{% endhighlight %}

![lin](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/lin/lin35.png)

## Challenge 1: Insertion in a Singly Linked List (insert at End)

Insertion at End #
Now, we are going to explain the second part (Insertion at End) and look at its examples, along with one coding challenge for the sake of practice. So let’s see how elements are inserted at the end of a linked list. In this type of insertion, we add an element at the end of the list. Here’s an illustration of how insertionAtEnd() works in a Singly Linked List:

![lin](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/lin/lin36.png)
![lin](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/lin/lin37.png)
![lin](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/lin/lin38.png)
![lin](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/lin/lin39.png)
![lin](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/lin/lin40.png)
![lin](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/lin/lin41.png)
![lin](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/lin/lin42.png)
![lin](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/lin/lin43.png)
![lin](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/lin/lin44.png)
![lin](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/lin/lin45.png)
![lin](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/lin/lin46.png)

Problem Statement#
Here’s a small coding exercise made for your practice. In the code snippet provided below, you will complete the void insertAtEnd(T data) method. This will take a generic type T value called data and insert that value at the end of the list. This code would be the part of the SinglyLinkedList class that we created in the previous lesson, therefore, any private members of that class can be accessed inside the function as well. After writing the code, run it and see how many tests you passed.

Method Prototype#
void insertAtEnd(T data)
Output#
The return type of the method is void. The object on which it is called will be modified only.

Sample Input#
linkedlist = 0->1->2
data = 3
Sample Output#
linkedlist = 0->1->2->3

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

![lin](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/lin/lin47.png)

## Insertion in Singly Linked List (Insert After)

Insert After #
As discussed earlier, the insertAfter function takes the data of the new node and the node after, which we want to insert this new node. The illustration below will help jog your memory.

![lin](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/lin/lin48.png)
![lin](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/lin/lin49.png)
![lin](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/lin/lin50.png)
![lin](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/lin/lin51.png)
![lin](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/lin/lin52.png)
![lin](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/lin/lin53.png)
![lin](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/lin/lin54.png)
![lin](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/lin/lin55.png)
![lin](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/lin/lin56.png)
![lin](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/lin/lin57.png)
![lin](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/lin/lin58.png)

Implementation #
Now that we’ve revised the concept let’s implement it using Java code. The insertAfter method will take a value called data and the value of the node, after which we want to insert the new node called previous as parameters.

Method Prototype #
void insertAfter(T data, T previous)
Output #
The updated linked list in which new element will be inserted after previous.

Sample Input #
linkedlist = 0->1->2->3->4
data = 8
previous = 2
Sample Output #
linkedlist = 0->1->2->8->3->4

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

    //inserts data after the given prev data node
    public void insertAfter(T data, T previous) {

        //Creating a new Node with value data 
        Node newNode = new Node();
        newNode.data = data;
        //Start from head node
        Node currentNode = this.headNode;
        //traverse the list until node having data equal to previous is found
        while (currentNode != null && !currentNode.data.equals(previous)) {
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
}

class CheckInsertion {
    public static void main( String args[] ) {
        SinglyLinkedList<Integer> sll = new SinglyLinkedList<Integer>();
        for (int i = 1; i <= 6; i++) {
			    sll.insertAtEnd(i); // inserting value at the tail of the list
        }
        sll.printList();

        System.out.println ("\nInserting 8 after 2");
        sll.insertAfter(8, 2);
        sll.printList();   // calling insert after
        System.out.println ("\nInserting 10 after 3");
        sll.insertAfter (10, 3);   // calling insert after
        sll.printList();
    }
}
{% endhighlight %}

## Challenge 2: Search in Singly Linked List

Introduction #
Now, we will take a look at the second most important operation, i.e. searching for an element in a linked list. This exercise of finding a value in a Singly Linked List is relatively more straightforward than the other three operations of insertion.

Searching For A Node #
The steps to search for a node in a Singly Linked List are as follows:

Start from the headNode.
Traverse the list till you either find a node with the given value, or you reach the end showing that the node being searched doesn’t exist.
Problem Statement #
If you know how to insert an element in a list, then searching for an item will not be that difficult for you. Now, based on the steps mentioned above, we have designed a simple coding exercise for your practice. There is a solution placed in the solution section for your help, but try to solve it on your own first.

Method Prototype #
boolean searchNode(T data)
Output #
It returns true or false to show if a certain value does or does not exists in the list.

Sample Input #
linkedlist = 5->90->10->4   and  value = 4
Sample Output #
true

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

![lin](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/lin/lin59.png)

## Singly Linked List Deletion (Implementation)

Introduction #
The deletion operation combines principles from both insertion and search. It uses the search functionality to find the value in the list.

Deletion is one of the instances where linked lists are more efficient than arrays. In an array, you have to shift all the elements backward if one element is deleted. Even then, the end of the array is empty, and it takes up unnecessary memory.

In the case of linked lists, the node is removed at head merely in constant time.

Let’s take a look at the different types of deletion operations we can perform in singly-linked lists.

Types of Deletion #
There are two basic delete operations for linked lists:

Deletion at head
Deletion by value
In this lesson, we will look at the implementation of the deletion at the head algorithm. The rest will be covered in the following lessons.

Deletion at Head #
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





{% highlight java %}

{% endhighlight %}