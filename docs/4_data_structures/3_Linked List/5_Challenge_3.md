---
layout: default
title: Challenge 3
parent: Linked Lists
grand_parent: Data Structures
nav_order: 5
permalink: /data_structures/linked_lists/ch3
---
<div align="center" markdown="1">
Challenge 3 / Java resources / Tutorial

{: .fs-8 .fw-400 }
</div>

## Challenge 3: Deletion in Singly Linked List(Delete by Value)

## Delete by Value
This operation deletes the required node, e.g., n, from any position in a Singly Linked List. This deletion follows the following steps:
1. It takes in the value that needs to be deleted from the list.
2. It traverses the list searching for that value.
3. Once the node (n) with the required value is found, it connects n's previous node to the nextNode of n.
4. It then removes n from the list.
F
Here’s an illustration of how this type of deletion works in a linked list:

![lin](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/lin/kk1.png)
![lin](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/lin/kk2.png)
![lin](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/lin/kk3.png)
![lin](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/lin/kk4.png)
![lin](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/lin/kk5.png)
![lin](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/lin/kk6.png)
![lin](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/lin/kk7.png)
![lin](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/lin/kk8.png)

## Problem Statement
In the code snippet given below, you have to implement the void deleteByValue(T data) method. In this method, we will pass a particular value that we want to delete from the list. The node containing this value could be anywhere on the list. It is also possible that such a node may not exist at all.

Therefore, we would have to traverse the whole list until we find the value which needs to be deleted. If the value doesn’t exist, we simply return control to the calling function.

Note: This function removes only the first occurrence of the value from the list.

The Node and linkedList classes implemented in the previous lessons are available to you.

You have access to:
* isEmpty()
* printList()
* deleteAtHead()

as member methods of the SinglyLinkedList class.

## Method Prototype:
void deleteByValue(T data)

## Output:
A linked list with the element removed.

## Sample Input
linkedlist = 3->2->1->0, 
data = 1

## Sample Output
linkedlist = 3->2->0


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

    // Deletes data from the head of list
    // public void deleteAtHead()

    // Helper Function to printList
    // public void printList() 
 
    public void deleteByValue(T data) {
      // Write -- Your -- Code
    }
}
{% endhighlight %}

## Solution Review: Deletion in Singly Linked List

## Explanation
While traversing through the linked list, there are three cases we can come across:
* List is empty
* One element in the list
* More than one element in the list

If the list is empty, then we have nothing to do; just return the control to calling function. For a single element in the list, we’ll call deleteAtHead(), and this will delete the value at the head.

If there is more than one element in the list, then we simply start traversing from the headNode and keep on checking until that node found and delete it. The following figure illustrates this process:

![lin](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/lin/add1.png)
![lin](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/lin/add2.png)
![lin](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/lin/add3.png)
![lin](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/lin/add4.png)
![lin](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/lin/add5.png)
![lin](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/lin/add6.png)
![lin](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/lin/add7.png)
![lin](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/lin/add8.png)
![lin](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/lin/add9.png)
![lin](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/lin/add10.png)
![lin](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/lin/add11.png)

Let’s have a look at the code for deleteByValue() which is implemented in lines 122 to 145 of the SinglyLinkedList class.

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

    //Deletes data given from the linked list
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
                size--;
                return; 
            }
            prevNode = currentNode;
            currentNode = currentNode.nextNode;
        }
    }
}

class Deletion {
	public static void main( String args[] ) {
        SinglyLinkedList<Integer> sll = new SinglyLinkedList<Integer>(); 
        for (int i = 1; i <= 10; i++) {
			sll.insertAtHead(i);
        }
        System.out.println("Originial :");
        sll.printList();
        System.out.println("After deleting 10 from List: ");
        sll.deleteByValue(10);
        sll.printList();
        System.out.println("After deleting 9 from List: ");
        sll.deleteByValue(9);
        sll.printList();
        System.out.println("After deleting 1 from List: ");
        sll.deleteByValue(1);
        sll.printList();
        System.out.println("After deleting 21 from List: ");
        sll.deleteByValue(21);
        sll.printList(); // list remains unchanged as there is no element 21 in the list
    }
}
{% endhighlight %}

## Explanation: 
To explain what we have done, let’s break the code into sections and look at each section in detail:
* main() – create the singly linked list
* deleteByValue() – takes a value as arguments. Deletes the data value if it is found or else does nothing.
Main Function: This creates a list by calling insertAtHead() method in a loop for values from 1 to 10. Initially, the list is going to look like this:

10 -> 9 -> 8 -> 7 -> 6 -> 5 -> 4 -> 3 -> 2 -> 1 -> null

It then calls the deleteByValue method for values 10, 9, 1 and 21. After deletion of valid nodes 10, 9, and 1, it prints out the list. Since node 21 does not exist in the linked list, the same list is printed again. In the end, the resulted list will look something like this:

8 -> 7 -> 6 -> 5 -> 4 -> 3 -> 2 -> null

deleteByValue(): It takes a value as a parameter. Additionally, it searches for a node in the Singly Linked List that has the given data value while keeping track of current and previous nodes. If not found, it means no such value exists in the list. If found, it performs a series of steps to delete this value. However, before jumping to those steps, look at some of the terminologies that we used in the function:
* currentNode – node we are currently standing at
* prevNode – element that comes before currentNode
* nextNode – pointer to the next node of currentNode

Executing the single line of code,

prevNode.nextNode = currentNode.nextNode 

links the prevNode to the nextNode. The current node’s link will be destroyed from the list, and the garbage collector will take care of the deletion automatically.

## Time Complexity 
In the worst case, you would have to traverse until the end of the list. This means the time complexity will be O(n).