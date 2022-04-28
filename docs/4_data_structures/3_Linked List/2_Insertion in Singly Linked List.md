---
layout: default
title: Insertion in Singly Linked List
parent: Linked Lists
grand_parent: Data Structures
nav_order: 2
permalink: /data_structures/linked_lists/insertion
---
<div align="center" markdown="1">
Insertion in Singly Linked List / Java resources / Tutorial

{: .fs-8 .fw-400 }
</div>

## Insertion in Singly Linked List (Insert After)

## Insert After 
As discussed earlier, the insertAfter function takes the data of the new node and the node after, which we want to insert this new node. The illustration below will help jog your memory.

![lin](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/lin/lin48.png)
![lin](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/lin/lin49.png)
![lin](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/lin/lin50.png)
![lin](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/lin/lin51.png)
![lin](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/lin/lin52.png)
![lin](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/lin/lin53.png)
![lin](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/lin/lin54.png)
![lin](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/lin/lin55.png)
![lin](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/lin/lin56.png)
![lin](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/lin/lin57.png)
![lin](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/lin/lin58.png)

## Implementation 
Now that we’ve revised the concept let’s implement it using Java code. The insertAfter method will take a value called data and the value of the node, after which we want to insert the new node called previous as parameters.

## Method Prototype 
void insertAfter(T data, T previous)

## Output 
The updated linked list in which new element will be inserted after previous.

## Sample Input 
linkedlist = 0->1->2->3->4
data = 8
previous = 2

## Sample Output 
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