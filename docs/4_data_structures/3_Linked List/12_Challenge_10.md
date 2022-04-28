---
layout: default
title: Challenge 10
parent: Linked Lists
grand_parent: Data Structures
nav_order: 12
permalink: /data_structures/linked_lists/ch10
---
<div align="center" markdown="1">
Challenge 10 / Java resources / Tutorial

{: .fs-8 .fw-400 }
</div>

## Challenge 10: Return the Nth node from End

## Problem Statement 
In this problem, you have to implement Object nthElementFromEnd(SinglyLinkedList<T> list, int n) method, which will take a linked list as an input and returns the nth element of the list from the end. To solve this, you will have to come up with a formula by comparing multiple outputs and inputs and identifying a common pattern. An illustration is also provided for your understanding.

## Method Prototype 
public static <T> Object nthElementFromEnd(SinglyLinkedList<T> list, int n)

## Output 
It will return nth node from the end of the linked list.

## Sample Input 
linkedlist = 22->18->60->78->47->39->99 and n=3

## Sample Output 
47

Consider the following example:

![lin](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/lin/ser47.png)

## Coding Exercise

{% highlight java %}
import java.util.HashSet;

public class SinglyLinkedList<T> {
    //Node inner class for SLL
    public class Node {
        public T data;
        public Node nextNode;

    }

    //head node of the linked list
    private Node headNode;
    private int size;

    public Node getHeadNode() {
        return headNode;
    }

    public void setHeadNode(Node headNode) {
        this.headNode = headNode;
    }

    public int getSize() {
        return size;
    }

    public void setSize(int size) {
        this.size = size;
    }

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

    public void deleteAtHead() {
        if (isEmpty())
            return;
        headNode = headNode.nextNode;
        size--;
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
        size--;
    }

    public void deleteByValue(T data) {
        //if empty then simply return
        if (isEmpty())
            return;

        //Start from head node
        Node currentNode = this.headNode;
        Node prevNode = null; //previous node starts from null

        if (currentNode.data.equals(data)) {
            //data is at head so delete from head
            deleteAtHead();
            return;
        }
        //traverse the list searching for the data to delete
        while (currentNode != null) {
            //node to delete is found
            if (data.equals(currentNode.data)) {
                prevNode.nextNode = currentNode.nextNode;
                size--;
                return;
            }
            prevNode = currentNode;
            currentNode = currentNode.nextNode;
        }
    }
}

class NthElementChallenge {
    public static <T> Object nthElementFromEnd(SinglyLinkedList<T> list, int n) {
        // Write -- Your -- Code
        return -1;
    }
}
{% endhighlight %}

## Solution Review: Return the Nth node from End

{% highlight java %}
public class SinglyLinkedList<T> {
    //Node inner class for SLL
    public class Node {
        public T data;
        public Node nextNode;

    }

    //head node of the linked list
    private Node headNode;
    private int size;

    public Node getHeadNode() {
        return headNode;
    }

    public void setHeadNode(Node headNode) {
        this.headNode = headNode;
    }

    public int getSize() {
        return size;
    }

    public void setSize(int size) {
        this.size = size;
    }

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

    public void deleteAtHead() {
        if (isEmpty())
            return;
        headNode = headNode.nextNode;
        size--;
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
        size--;
    }

    public void deleteByValue(T data) {
        //if empty then simply return
        if (isEmpty())
            return;

        //Start from head node
        Node currentNode = this.headNode;
        Node prevNode = null; //previous node starts from null

        if (currentNode.data.equals(data)) {
            //data is at head so delete from head
            deleteAtHead();
            return;
        }
        //traverse the list searching for the data to delete
        while (currentNode != null) {
            //node to delete is found
            if (data.equals(currentNode.data)) {
                prevNode.nextNode = currentNode.nextNode;
                size--;
                return;
            }
            prevNode = currentNode;
            currentNode = currentNode.nextNode;
        }
    }
}

class NthElementChallenge {

   public static <T> Object nthElementFromEnd(SinglyLinkedList<T> list, int n) {
        int size = list.getSize();
        n = size - n + 1; //we can use the size variable to calculate distance from start
        if (size == 0 || n > size) {
            return null; //returns null if list is empty or n is greater than size
        }
        SinglyLinkedList.Node current = list.getHeadNode();
        int count = 1;
        //traverse until count is not equal to n
        while (current != null) {
            if (count == n)
                return current.data;
            count++;
            current = current.nextNode;
        }
        return null;
    }
    public static void main( String args[] ) {
        SinglyLinkedList<Integer> sll = new SinglyLinkedList<Integer>();
        sll.printList(); //list is empty
        System.out.println("3rd element from end : " + nthElementFromEnd(sll, 3)); //will return null
        for(int i=0; i<15; i+=2){
            sll.insertAtHead(i);
        }
        sll.printList(); // List is 14 -> 12 -> 10 -> 8 -> 6 -> 4 -> 2 -> 0 -> null
        System.out.println("3rd element from end : " + nthElementFromEnd(sll, 3)); //will return 4
        System.out.println("10th element from end : " + nthElementFromEnd(sll, 10));//will return null
    }
}
{% endhighlight %}

## Explanation 
In the above solution, we first use the getter function list.getSize() to access the length of the list. Then we find the node which is at x position from the start.

We will now calculate the value of x. Suppose that the length of our list is 7, as shown in the following example:

![lin](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/lin/ex1.png)
![lin](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/lin/ex2.png)
![lin](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/lin/ex3.png)
![lin](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/lin/ex4.png)
![lin](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/lin/ex5.png)
![lin](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/lin/ex6.png)
![lin](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/lin/ex7.png)
![lin](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/lin/ex8.png)
![lin](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/lin/ex9.png)
![lin](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/lin/ex10.png)
![lin](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/lin/ex11.png)
![lin](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/lin/ex12.png)
![lin](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/lin/ex13.png)
![lin](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/lin/ex14.png)
![lin](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/lin/ex15.png)
![lin](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/lin/ex16.png)
![lin](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/lin/ex17.png)
![lin](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/lin/ex18.png)
![lin](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/lin/ex19.png)
![lin](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/lin/ex20.png)
![lin](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/lin/ex21.png)
![lin](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/lin/ex22.png)
![lin](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/lin/ex23.png)
![lin](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/lin/ex24.png)
![lin](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/lin/ex25.png)
![lin](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/lin/ex26.png)
![lin](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/lin/ex27.png)

## Time Complexity 
In the worst-case time complexity of this algorithm is O(n). Because we might have to access the 1st element from the end.