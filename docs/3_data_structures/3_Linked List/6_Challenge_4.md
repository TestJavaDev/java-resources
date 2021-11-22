---
layout: default
title: Challenge 4
parent: Linked Lists
grand_parent: Data Structures
nav_order: 6
permalink: /data_structures/linked_lists/ch4
---
<div align="center" markdown="1">
Challenge 4 / Java resources / Tutorial

{: .fs-8 .fw-400 }
</div>

## Challenge 4: Find the Length of a Linked List

Problem Statement #
In this problem, you have to implement the method int length(), which will count the number of nodes in a linked list. An illustration is also provided for your understanding.

Method Prototype #
int length()
Output #
The length of the given linked list.

Sample Input #
linkedlist = 0->1->2-3->4
Sample Output #
length = 5 
The figure below illustrates how length is calculated in a non-empty list:

![lin](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/lin/ser28.png)
![lin](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/lin/ser29.png)
![lin](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/lin/ser30.png)
![lin](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/lin/ser31.png)
![lin](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/lin/ser32.png)
![lin](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/lin/ser33.png)
![lin](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/lin/ser34.png)

## Coding Exercise

{% highlight java %}
    // This function is inside the linked list class 
    // The class does not have a data-member size
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

    // Helper Function to printList
    // public void printList() 

    public int length() {
      int count = 0;
      // Write -- Your -- Code
      return count;
    }
}
{% endhighlight %}

## Solution Review: Find the Length of a Linked List

## Solution: Linear Iteration

{% highlight java %}
public class SinglyLinkedList<T> {
    //Node inner class for SLL
    public class Node {
        public T data;
        public Node nextNode;

    }

    //head node of the linked list
    public Node headNode;

    //constructor
    public SinglyLinkedList() {
        headNode = null;
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

    public void deleteAtHead() {
        if (isEmpty())
            return;
        headNode = headNode.nextNode;
    }

    public void deleteAtEnd() {
        if (isEmpty())
            return;
        Node prevNode = this.headNode;
        Node currentNode = prevNode.nextNode;
        while (currentNode.nextNode != null) {
            prevNode = currentNode;
            currentNode = currentNode.nextNode;
        }
        prevNode.nextNode = null;
    }

    public void deleteByValue(T data) {
        //if empty then simply return
        if (isEmpty())
            return;
        //Start from head node
        Node currentNode = this.headNode;
        Node prevNode = null; //previous node starts from null

        if(currentNode.data.equals(data)) {
            //data is at head so delete from head
            deleteAtHead();
            return;
        }
        
        //traverse the list searching for the data to delete
        while (currentNode != null) {
            //node to delete is found
            if (data.equals(currentNode.data)){
                prevNode.nextNode = currentNode.nextNode;
                return;
            }
            prevNode = currentNode;
            currentNode = currentNode.nextNode;
        }
    }
    public int length() {
      //Get the refernce to headNode of the given list
      Node current = this.headNode;
      //count is zero initially
      int count = 0;
      //traverse the list until null is found
      while (current!= null){
        count++; //increment at each iteration
        current = current.nextNode;
      }

      return count;
    }
}

class CheckLength {
  public static void main( String args[] ) {
        SinglyLinkedList<String> list = new SinglyLinkedList<String>();
        list.insertAtEnd("This");
        list.insertAtEnd("list");
        list.insertAtEnd("is");
        list.insertAtEnd("Generic");
        list.printList();
        System.out.println("Length : " + list.length());
    }
}
{% endhighlight %}

Explanation #
The logic behind it is very similar to that of the search function. The trick is to iterate through the list and keep count of how many nodes you’ve visited. This count is held in a variable that is returned when the end of the list is reached.

Time Complexity #
Since this is a linear algorithm, the time complexity will be O(n).
