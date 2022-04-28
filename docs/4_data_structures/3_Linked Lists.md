---
layout: default
title: Linked Lists
parent: Data Structures
nav_order: 3
permalink: /data_structures/linked_lists
has_children: true
---
<div align="center" markdown="1">
Linked Lists / Java resources / Tutorial

{: .fs-8 .fw-400 }
</div>

## Linked List 

## What is the Singly Linked List (SLL)?

## Introduction 
Linked Lists and Arrays are quite similar in characteristics as they are both used to store a collection of the same type of data. A data type can be anywhere from a simple primitive integer to a complex object of a particular class. However, the structure of the Linked List is very different as compared to Arrays.

## Applications
Some important applications of Linked Lists include:
* Implementing HashMaps, File System and Adjacency Lists
* Dynamic memory allocation: We use linked lists of free blocks
* Performing arithmetic operations on long integers
* Maintaining a directory of names

## Structure of Linked List 
A linked list is formed by nodes that are linked together like a chain. Each node holds data, along with a pointer to the next node in the list. The Singly Linked List (SLL) is the type of linked list where each node has only one pointer that stores the reference to the next value. The following illustration shows a Singly Linked List.

![lin](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/lin/lin1.png)

In the next few lessons, we will look at how SLL is implemented and study its basic operations in detail. To implement a linked list, we need the following two classes:
* Class Node
* Class LinkedList

## Class Node
The Node class stores data in a single node. It can store primitive data such as integers and string as well as complex objects having multiple attributes. Along with data, it also stores a pointer to the next element in the list, which helps in linking the nodes together like a chain. Here’s a typical definition of a Node class:

![lin](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/lin/lin2.png)

Explanation: The code above provides a basic definition of a Node class structure with two data members: one to hold the data and the other one to store a reference to the next element. This class is a generic class made by using Java Generics. The data variable can hold any data-type value specified.

## Class Linked list 
As mentioned above, the Singly Linked list is made up of nodes that are linked together like a chain. Now to access this chain, we would need a pointer that keeps track of the first element of the list. As long as we have information about the first element, we can traverse the rest of the list without worrying about memorizing their storage locations.

The Singly Linked List contains a head node: a pointer pointing to the first element of the list. Whenever we want to traverse the list, we can do so by using this head node. Below is a basic structure of the Singly Linked List’s class:

![lin](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/lin/lin3.png)

Explanation: In the above class, we see a headNode variable of type Node. It will point to the start of the list (i.e., head of the list). In the constructor, we initialize that headNode node so that it becomes functional. If a head node points to nothing (NULL), this means that the list is empty. As you can see in the above illustration, the head points to the first element and the last pointer points to NULL to indicate the end of the list.

## Basic Linked List Operations

## Operations 
Following are the basic operations of a Singly Linked List:

![lin](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/lin/lin4.png)

If you observe the list of methods mentioned above, the last function, isEmpty() is a helper function which will prove useful in defining all the other functions.

So let’s define it first.

## isEmpty() 
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

## Explanation 
Nothing tricky going on here. The crux of the code lies in the if condition on line 20. We merely check if the head is empty.

Note: Even when a linked list is empty, the head Node must always exist.

## Time Complexity 
The time complexity of isEmpty() method is O(1).

This is just the tip of the iceberg. We’ll tackle each of the methods above in the following lessons and apply them to relevant problems.

## Insertion in a Singly Linked List

## Introduction 
In this lesson, we are going to briefly explain the basic operations which were discussed in the previous lesson and implement them using Java code. The three types of insertion strategies used in a Singly Linked List are:
* Insert at Head
* Insert at End
* Insert After

### Insertion at Head 
This type of insertion means that we want to insert a new element as the first element of the list. As the head always points to the first element of the list, insertion at head means that we are inserting the first element in the list. The following figure shows how InsertAtHead() happens in Singly Linked List:

![lin](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/lin/lin5.png)
![lin](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/lin/lin6.png)
![lin](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/lin/lin7.png)
![lin](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/lin/lin8.png)
![lin](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/lin/lin9.png)
![lin](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/lin/lin10.png)
![lin](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/lin/lin11.png)
![lin](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/lin/lin12.png)

## Insert at End 
This type of insertion means that we want to insert a new element as the last element of the list. The original tail element of the list has a nextElement pointer that points to NULL. To insert a new tail node, we have to point the nextElement pointer of the previous tail node to the new tail node, allowing the nextElement of the new tail to now point to NULL. The following figure illustrates this insertion.

![lin](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/lin/lin13.png)
![lin](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/lin/lin14.png)
![lin](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/lin/lin15.png)
![lin](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/lin/lin16.png)
![lin](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/lin/lin17.png)
![lin](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/lin/lin18.png)
![lin](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/lin/lin19.png)
![lin](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/lin/lin20.png)
![lin](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/lin/lin21.png)
![lin](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/lin/lin22.png)
![lin](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/lin/lin23.png)

## Insert After 
This insertion is a little more tricky when compared to insert at the head and insert at the end. Here, we specify the node (e.g. n), after which we want to insert the new node. To insert this node, we follow these steps:
1. We traverse the linked list to look for n.
2.  As soon as we find it, we assign n's nextElement to the new node’s nextElement.
3. Then we point n's nextElement to the new node.

The following figure illustrates how this is done.

![lin](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/lin/lin24.png)
![lin](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/lin/lin25.png)
![lin](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/lin/lin26.png)
![lin](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/lin/lin27.png)
![lin](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/lin/lin28.png)
![lin](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/lin/lin29.png)
![lin](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/lin/lin30.png)
![lin](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/lin/lin31.png)
![lin](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/lin/lin32.png)
![lin](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/lin/lin33.png)
![lin](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/lin/lin34.png)

## Implementation 
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

![lin](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/lin/lin35.png)

## Linked Lists vs. Arrays

## Array vs. Linked List

## Memory Allocation
The main difference between a linked list and an array is the way they are allocated memory. Arrays instantiate a whole block of memory, e.g., array[1000] gets space to store 1000 elements at the start even if it doesn’t contain any element yet. On the other hand, a linked list only instantiates the portion of memory it uses.

## Insertion and Deletion
For lists and arrays, many differences can be observed in the way elements are inserted and deleted. In a linked list, insertion and deletion at head happen in a constant amount of time (O(1)), while arrays take O(n) time to insert or delete a value because you have to shift the array elements left or right after that operation.

## Searching
In an array, it takes constant time to access an index. In a linked list, you have to iterate the list from the start until you find the node with the correct value.

The table given below will summarize the performance difference between linked lists and arrays.

![lin](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/lin/add12.png)

## What is a Doubly Linked List (DLL)?

## Introduction 
As we learned in the previous lesson, we need to traverse through the whole list – the most time-consuming operation in linked lists—to perform the basic operations. Although we have to traverse an array as well, an array element can be accessed in O(1) by the index because array elements are present on contiguous memory locations. In linked lists, however, the nodes are not present on contiguous memory locations. Therefore, you will need to traverse all the nodes to get to the desired node.

Another concern that must be taken into account here is that linked lists are unidirectional: they can only move forward, not backward. Also, while adding or removing elements from the list, we need to keep track of the previous node as well, which makes it complicated. That is where the Doubly Linked List (DLL) comes to the rescue!

## Doubly Linked List (DLL) 
The difference between a Doubly and a Singly Linked List is that a DLL is bi-directional; this means any particular node stores both the previous and next pointers that point to the previous and next nodes, respectively.

To implement the node class for DLL, we only need to add a new data member, a node called prevNode, in the already constructed Node class of the SLL that we created in the previous lesson.

![lin](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/lin/ser1.png)

Explanation: The data and nextNode fields are the same as in SLL. The Doubly Linked List comes with an addition of the prevNode pointer that points to the previous element of the particular node. Below is an illustration of what a Doubly Linked List looks like:

![lin](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/lin/ser2.png)
![lin](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/lin/ser3.png)
![lin](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/lin/ser4.png)
![lin](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/lin/ser5.png)
![lin](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/lin/ser6.png)
![lin](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/lin/ser7.png)
![lin](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/lin/ser8.png)

## Impact on Deletion 
This strategy considerably helps in deletion as you don’t need to keep track of the previous element while searching. To see how effective this strategy is, let’s re-write the deleteByValue() operation for Doubly Linked List. We will use the same code which we implemented in the previous lesson and make additions to it.

{% highlight java %}
public class DoublyLinkedList<T> {

    //Node inner class for DLL
    public class Node {
        public T data;
        public Node nextNode;
        public Node prevNode;
    }

    public Node headNode;
    public int size;

    public DoublyLinkedList() {
        this.headNode = null;
    }

    //checks if the list is empty
    public boolean isEmpty() {
        if (headNode == null)
            return true; //is empty
        return false;    //is not empty
    }

    public void insertAtHead(T data) {
        //create node and put in the data
        Node newNode = new Node();
        newNode.data = data;
        // Make next of new node as head and previous as NULL
        newNode.nextNode = this.headNode; 
        newNode.prevNode = null;
        //Change previous of head node to new node
        if (headNode != null)
            headNode.prevNode = newNode;
        this.headNode = newNode;
        size++;
    }

    public void printList() {
        if (isEmpty()) {
            System.out.println("List is Empty!");
            return;
        }

        Node temp = headNode;
        System.out.print("List : null <- ");

        while (temp.nextNode != null) {
            System.out.print(temp.data.toString() + " <-> ");
            temp = temp.nextNode;
        }

        System.out.println(temp.data.toString() + " -> null");
    }
    //deletes the first element
    public void deleteAtHead(){
        //if list is empty do nothing
        if(isEmpty())
            return;
        
        //if List is not empty then link head to the
        //nextElement of firstElement.
        headNode = headNode.nextNode;
        headNode.prevNode = null;
        size--;
    }
    public void deleteByValue(T data) {
        //if empty then simply return
        if (isEmpty())
            return;

        //Start from head node
        Node currentNode = this.headNode;

        if (currentNode.data.equals(data)) {
            //data is at head so delete from head
            deleteAtHead();
            return;
        }
        //traverse the list searching for the data to delete
        while (currentNode != null) {
            //node to delete is found
            if (data.equals(currentNode.data)) {
                currentNode.prevNode.nextNode = currentNode.nextNode;
                if(currentNode.nextNode != null)
                    currentNode.nextNode.prevNode = currentNode.prevNode;
                size--;
            }
            currentNode = currentNode.nextNode;
        }
    }
}

class HelloWorld {
    public static void main( String args[] ) {
        DoublyLinkedList<Integer> dll = new DoublyLinkedList<Integer>();
        for (int i = 1; i <= 10; i++) {
			dll.insertAtHead(i);
		}
        System.out.print("Original ");
        dll.printList();
        System.out.print("After deleting 10 ");
        dll.deleteByValue(10);
        dll.printList();
        System.out.print("After deleting 1 ");
        dll.deleteByValue(1);
        dll.printList();
        System.out.print("After deleting 5 ");
        dll.deleteByValue(5);
        dll.printList();
    }
}
{% endhighlight %}

Explanation: We will compare this code snippet with the one we created for SLL in the previous lessons and see which one is easier to implement. Initially, we check whether the list is empty or not; if it’s empty, we do nothing.

Next, we start traversing the elements. If the value to be deleted is present at the start, all we have to do is call deleteAtHead(), which will make the headNode point to the nextNode pointer of the headNode,i.e., it will make it point to the second element of the list. Not only that, but it will also have to update the prevNode pointer of the new headNode to point at null now.

![lin](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/lin/ser9.png)
![lin](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/lin/ser10.png)
![lin](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/lin/ser11.png)
![lin](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/lin/ser12.png)
![lin](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/lin/ser13.png)
![lin](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/lin/ser14.png)

For the other case, where the value to be deleted is not the first element of the list, we will perform the following set of operations. Let’s name the nodes again:
* currentNode: Node to be deleted
* prevCurrentNode: prevNode of currentNode
* nextCurrentNode: nextNode of currentNode

To delete the currentNode successfuly, we will follow these steps:
1. Set the nextNode of prevCurrentNode to be nextCurrentNode.
2. Set the prevNode of nextCurrentNode to be prevCurrentNode. This is expressed in the code statement below. The figure below illustrates this process:

![lin](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/lin/ser15.png)

![lin](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/lin/ser16.png)
![lin](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/lin/ser17.png)
![lin](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/lin/ser18.png)
![lin](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/lin/ser19.png)
![lin](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/lin/ser20.png)
![lin](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/lin/ser21.png)
![lin](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/lin/ser22.png)
![lin](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/lin/ser23.png)
![lin](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/lin/ser24.png)
![lin](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/lin/ser25.png)
![lin](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/lin/ser26.png)

## Linked List with Tail

## Introduction 
Another variation of a basic linked list is a Linked List with a Tail. In this type of list, in addition to the head being the starting of the list, a tail is used as the pointer to the last node of the list. Both SLL and DLL can be implemented using a tail pointer.

## Comparison between SLL with Tail and DLL with Tail 
The benefit of using a tail pointer is seen in the insertion and deletion operations at the end of the list. Let’s analyze the efficiency, in terms of time complexity, of both of these operations in SLL and DLL.

![lin](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/lin/ser27.png)

From this comparison, we can see that the real advantage of using a tail pointer comes in the deleteAtEnd scenario while dealing with Doubly Linked Lists as the tail provides a more efficient implementation of this function.

## Implementation of Doubly Linked List with Tail 
In the code below, we have used a member variable called tailNode, which will point to the last node of the list. Initially, it will be equal to null.

{% highlight java %}
public class DoublyLinkedList<T> {
    
    //Node inner class for DLL
    public class Node {
        public T data;
        public Node nextNode;
        public Node prevNode;
    }

    //member variables
    public Node headNode;
    public Node tailNode;
    public int size;

    //constructor
    public DoublyLinkedList() {
        this.headNode = null;
        this.tailNode = null; //null initially
        this.size = 0;
    }

    //returns true if list is empty
    public boolean isEmpty() {
        if (headNode == null && tailNode == null) //checking tailNode to make sure
            return true;
        return false;
    }

    //getter for headNode
    public Node getHeadNode() {
        return headNode;
    }

    //getter for tailNode
    public Node getTailNode() {
        return tailNode;
    }

    //getter for size
    public int getSize() {
        return size;
    }

    //print list function
    public void printList() {
        if (isEmpty()) {
            System.out.println("List is Empty!");
            return;
        }

        Node temp = headNode;
        System.out.print("List : null <- ");

        while (temp.nextNode != null) {
            System.out.print(temp.data.toString() + " <-> ");
            temp = temp.nextNode;
        }

        System.out.println(temp.data.toString() + " -> null");
    }
}
{% endhighlight %}

## Impact on Insertion 
1. insertAtHead() 
Insertion at head remains almost the same as in DLL without tail. The only difference is that if the element is inserted in an already empty linked list then, we have to update the tailNode as well.
2. insertAtEnd() 
Insertion at the end is a linear operation in DLL without tail. However, in DLL with tail, it becomes a constant operation. We simply insert the new node as the nextNode of the tailNode and then update the tailNode to point to the new node, after insertion.

Let us take a look at the code for the operations mentioned above.

{% highlight java %}
public class DoublyLinkedList<T> {

    //Node inner class for DLL
    public class Node {
        public T data;
        public Node nextNode;
        public Node prevNode;
    }

    //member variables
    public Node headNode;
    public Node tailNode;
    public int size;

    //constructor
    public DoublyLinkedList() {
        this.headNode = null;
        this.tailNode = null; //null initially
        this.size = 0;
    }

    //returns true if list is empty
    public boolean isEmpty() {
        if (headNode == null && tailNode == null) //checking tailNode to make sure
            return true;
        return false;
    }

    //getter for headNode
    public Node getHeadNode() {
        return headNode;
    }

    //getter for tailNode
    public Node getTailNode() {
        return tailNode;
    }

    //getter for size
    public int getSize() {
        return size;
    }
    
    //insert at start of the list
    public void insertAtHead(T data) {
        Node newNode = new Node();
        newNode.data = data;
        newNode.nextNode = this.headNode; //Linking newNode to head's nextNode
        newNode.prevNode = null; //it will be inserted at start so prevNode will be null
        if (!isEmpty())
            headNode.prevNode = newNode;
        else
            tailNode = newNode;
        this.headNode = newNode;
        size++;
    }

    //insert at end of the list
    public void insertAtEnd(T data) {
        if (isEmpty()) { //if list is empty then insert at head
            insertAtHead(data);
            return;
        }
        //make a new node and assign it the value to be inserted
        Node newNode = new Node();
        newNode.data = data;
        newNode.nextNode = null; //it will be inserted at end so nextNode will be null
        newNode.prevNode = tailNode; //newNode comes after tailNode so its prevNode will be tailNode
        tailNode.nextNode = newNode; //make newNode the nextNode of tailNode
        tailNode = newNode; //update tailNode to be the newNode
        size++;
    }
    
    //print list function
    public void printList() {
        if (isEmpty()) {
            System.out.println("List is Empty!");
            return;
        }

        Node temp = headNode;
        System.out.print("List : null <- ");

        while (temp.nextNode != null) {
            System.out.print(temp.data.toString() + " <-> ");
            temp = temp.nextNode;
        }

        System.out.println(temp.data.toString() + " -> null");
    }
}

class DLLWithTailDemo {
    public static void main( String args[] ) {
        DoublyLinkedList<Integer> list = new DoublyLinkedList<Integer> ();
        for (int i = 0; i <= 3; i++) {
            list.insertAtHead(i); //inserting 0 to 3 at start
        }
        System.out.println("After inserting 0 to 3 at start :");
        list.printList();
         for (int i = 5; i <= 10; i++) {
            list.insertAtEnd(i); //inserting 5 to 10 at end
        }
        System.out.println("\n After inserting 5 to 10 at end :");
        list.printList();
    }
}
{% endhighlight %}

## Impact on Deletion 

1. deleteAtHead() 
Deletion at head remains almost the same as in DLL without tail. The only difference is that if the element to be deleted is the only element in the linked list then, we have to update the tailNode as null after deletion.

2. deleteAtTail() 
Deletion at the tail (i.e, the end) is a linear operation in DLL without tail. However, in DLL with tail, it becomes a constant operation. We can use the same approach as in deletion at the start. Firstly, we access the last element of the list by the tailNode. Then we make the prevNode of tailNode equal to new tailNode. If the element being deleted was the only element in the list, that means we also have to assign headNode to the null value.

Let us take a look at the code for these operations.

{% highlight java %}
public class DoublyLinkedList<T> {

    //Node inner class for DLL
    public class Node {
        public T data;
        public Node nextNode;
        public Node prevNode;
    }

    //member variables
    public Node headNode;
    public Node tailNode;
    public int size;

    //constructor
    public DoublyLinkedList() {
        this.headNode = null;
        this.tailNode = null; //null initially
        this.size = 0;
    }

    //returns true if list is empty
    public boolean isEmpty() {
        if (headNode == null && tailNode == null) //checking tailNode to make sure
            return true;
        return false;
    }

    //getter for headNode
    public Node getHeadNode() {
        return headNode;
    }

    //getter for tailNode
    public Node getTailNode() {
        return tailNode;
    }

    //getter for size
    public int getSize() {
        return size;
    }
    
    //insert at start of the list
    public void insertAtHead(T data) {
        Node newNode = new Node();
        newNode.data = data;
        newNode.nextNode = this.headNode; //Linking newNode to head's nextNode
        newNode.prevNode = null; //it will be inserted at start so prevNode will be null
        if (!isEmpty())
            headNode.prevNode = newNode;
        else
            tailNode = newNode;
        this.headNode = newNode;
        size++;
    }

    //insert at end of the list
    public void insertAtEnd(T data) {
        if (isEmpty()) { //if list is empty then insert at head
            insertAtHead(data);
            return;
        }
        //make a new node and assign it the value to be inserted
        Node newNode = new Node();
        newNode.data = data;
        newNode.nextNode = null; //it will be inserted at end so nextNode will be null
        newNode.prevNode = tailNode; //newNode comes after tailNode so its prevNode will be tailNode
        tailNode.nextNode = newNode; //make newNode the nextNode of tailNode
        tailNode = newNode; //update tailNode to be the newNode
        size++;
    }
    
    public void deleteAtHead() {
        if (isEmpty())
            return;

        headNode = headNode.nextNode;
        if(headNode == null)
            tailNode = null;
        else
            headNode.prevNode = null;
        size--;
    }

    public void deleteAtTail() {
        if (isEmpty())
            return;
        tailNode = tailNode.prevNode;
        if (tailNode == null)
            headNode = null;
        else
            tailNode.nextNode = null;
        size--;
    }
    
    //print list function
    public void printList() {
        if (isEmpty()) {
            System.out.println("List is Empty!");
            return;
        }

        Node temp = headNode;
        System.out.print("List : null <- ");

        while (temp.nextNode != null) {
            System.out.print(temp.data.toString() + " <-> ");
            temp = temp.nextNode;
        }

        System.out.println(temp.data.toString() + " -> null");
    }
}

class DLLWithTailDemo {
    public static void main( String args[] ) {
        DoublyLinkedList<Integer> list = new DoublyLinkedList<Integer> ();
        for (int i = 0; i <= 3; i++) {
            list.insertAtHead(i); //inserting 0 to 3 at start
        }
         for (int i = 5; i <= 10; i++) {
            list.insertAtEnd(i); //inserting 5 to 10 at end
        }
        System.out.println("Initially :");
        list.printList();

        list.deleteAtHead();
        list.deleteAtHead();
        System.out.println("\nAfter deleting 2 elements from head :");
        list.printList();

        list.deleteAtTail();
        list.deleteAtTail();
        System.out.println("\nAfter deleting 2 elements from tail :");
        list.printList();
    }
}
{% endhighlight %}
