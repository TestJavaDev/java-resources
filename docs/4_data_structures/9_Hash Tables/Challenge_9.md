---
layout: default
title: Challenge 9
parent: Hash Tables
grand_parent: Data Structures
nav_order: 9
permalink: /data_structures/hash_tables/ch9
---
<div align="center" markdown="1">
Challenge 9 / Java resources / Tutorial

{: .fs-8 .fw-400 }
</div>

## Challenge 9: Union and Intersection of Lists using Hashing

Given two lists, find the Union & Intersection of their elements using Hashing. Solve this exercise and see if your output matches the expected output.

![has](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/has/has41.png)

## Problem Statement
In this problem you have to implement two functions:
* SinglyLinkedList<T> union(SinglyLinkedList<T> list1, SinglyLinkedList<T> list2)
* SinglyLinkedList<T> intersection(SinglyLinkedList<T> list1, SinglyLinkedList<T> list2)

You have to implement these functions using Hashing. The first function will take two linked lists as input and return the union of the two lists. A Union of two sets can be expressed as, “Union of two sets A and B is a set which contains all the elements present in A or B”. Similarly, the second function will return the Intersection of two lists. The Intersection is commonly defined as, “A set which contains all the common elements present in A and B”.

![has](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/has/has42.png)

## Output
The union and intersection of two linked lists.

Note: The order of elements in the output list does not matter!

## Sample Input
list1 = 15->22->8->null
list2 = 7->14->22->null

## Sample Output
Union = 15->22->8->7->14->null
Intersection = 22->null

![has](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/has/has43.png)

## Coding Exercise

{% highlight java %}
class SinglyLinkedList<T> {
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
            }
            prevNode = currentNode;
            currentNode = currentNode.nextNode;
        }
    }
}

class CheckUnionIntersection {
    //performs union of two lists
    public static <T> SinglyLinkedList<T> unionWithHashing(SinglyLinkedList<T> list1, SinglyLinkedList<T> list2) {
        SinglyLinkedList<T> result = new SinglyLinkedList<T>();
        // Write -- Your -- Code
        return result;
    }
    
    //performs intersection between list
    public static <T> SinglyLinkedList<T> intersectionWithHashing(SinglyLinkedList<T> list1, SinglyLinkedList<T> list2) {
        SinglyLinkedList<T> result = new SinglyLinkedList<T>();
        // Write -- Your -- Code
        return result;
    }
}
{% endhighlight %}

## Solution Review: Union and Intersection of Lists using Hashing

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
            }
            prevNode = currentNode;
            currentNode = currentNode.nextNode;
        }
    }
    public void removeDuplicatesWithHashing() {
        Node current = this.headNode;
        Node prevNode = this.headNode;
        //will store all the elements that we observe once
        HashSet<T> visitedNodes = new HashSet<T>();

        if (!isEmpty() && current.nextNode != null) {
            while (current != null) {
                //check if already visited then delete this node
                if (visitedNodes.contains(current.data)) {
                    //deleting the node by undating the pointer of previous node
                    prevNode.nextNode = current.nextNode;
                    current = current.nextNode;
                } else {
                    //if node was not already visited then add it to the visited set
                    visitedNodes.add(current.data);
                    //moving on to next element in the list
                    prevNode = current;
                    current = current.nextNode;
                }
            }
        }
    }
}

public class Stack<V> {
    private int maxSize;
    private int top;
    private V[] array;
    private int currentSize;

    /*
    Java does not allow generic type arrays. So we have used an
    array of Object type and type-casted it to the generic type V.
    This type-casting is unsafe and produces a warning.
    Un-comment the line below and execute again to see the warning.
    */
    @SuppressWarnings("unchecked")
    public Stack(int maxSize) {
        this.maxSize = maxSize;
        this.top = -1; //initially when stack is empty
        array = (V[]) new Object[maxSize];//type casting Object[] to V[]
        this.currentSize = 0;
    }

    public int getCurrentSize() {
        return currentSize;
    }

    //returns the maximum size capacity
    public int getMaxSize() {
        return maxSize;
    }

    //returns true if Stack is empty
    public boolean isEmpty() {
        return top == -1;
    }

    //returns true if Stack is full
    public boolean isFull() {
        return top == maxSize - 1;
    }

    //returns the value at top of Stack
    public V top() {
        if (isEmpty())
            return null;
        return array[top];
    }

    //inserts a value to the top of Stack
    public void push(V value) {
        if (isFull()) {
            System.err.println("Stack is Full!");
            return;
        }
        array[++top] = value; //increments the top and adds value to updated top
        currentSize++;
    }

    //removes a value from top of Stack and returns
    public V pop() {
        if (isEmpty())
            return null;
        currentSize--;
        return array[top--]; //returns value and top and decrements the top
    }

}

class UnionIntersectionChallenge {

    public static <T> SinglyLinkedList<T> unionWithHashing(SinglyLinkedList<T> list1, SinglyLinkedList<T> list2) {
        SinglyLinkedList<T> result = new SinglyLinkedList<T>();

        HashSet<T> visited = new HashSet<T>();
        
        SinglyLinkedList<T>.Node current = list1.getHeadNode(); //start from list1's head
        //Keep iterating list1
        while (current!=null) {
            //add elements of list1 into the result if they havent been visited before
            if(!visited.contains(current.data)) {
                result.insertAtHead(current.data);
                visited.add(current.data);
            }
            current = current.nextNode;
        }

        //now start from the head of list2
        current = list2.getHeadNode();

        //Keep iterating list2
        while (current!=null) {
            //add elements of list2 into the result if they havent been visited before
            if(!visited.contains(current.data)) {
                result.insertAtHead(current.data);
                visited.add(current.data);
            }
            current = current.nextNode;
        }
        
        
        return result;
    }

    public static <T> SinglyLinkedList<T> intersectionWithHashing(SinglyLinkedList<T> list1, SinglyLinkedList<T> list2) {
        SinglyLinkedList<T> result = new SinglyLinkedList<T>();

        HashSet<T> visited = new HashSet<T>();
        //start from the head of list1
        SinglyLinkedList<T>.Node current = list1.getHeadNode();
        //Keep iterating list1
        while (current != null) {
            //Add elements to visited set if they have not been visited
            if (!visited.contains(current.data)) {
                visited.add(current.data);
            }
            current = current.nextNode;
        }
        //now take head of list2
        current = list2.getHeadNode();
        //iterate list2
        while (current != null) {
            //add the elements which have been visited before into the result
            if (visited.contains(current.data)) {
                result.insertAtHead(current.data);
                visited.remove(current.data);
            }
            current = current.nextNode;
        }
        return result;
    }

    public static void main( String args[] ) {
        SinglyLinkedList<Integer> list1 = new SinglyLinkedList<Integer>();
        for(int i=7; i>3; i--){
            list1.insertAtHead(i);
        }
        System.out.print("1st ");
        list1.printList();
        SinglyLinkedList<Integer> list2 = new SinglyLinkedList<Integer>();
        for(int i=0; i<5; i++){
            list2.insertAtHead(i);
        }
        System.out.print("2nd ");
        list2.printList();
        System.out.print("After Intersection ");
        intersectionWithHashing(list1, list2).printList();
        System.out.print("After Union ");
        unionWithHashing(list1, list2).printList();
    }
}
{% endhighlight %}

## Union
In this solution, we first traverse list1 and add all elements to the visited HashSet. If the element has not been visited before, then we also add it into the result set. Then, we traverse list2 and repeat the same process. This solution is very similar to removeDuplicatedWithHashing() function that we used in the last challenge. The order of elements in output is not relevant in union operation.

## Intersection 
In this problem, we again use HashSet to keep track of duplicate elements. We first traverse list1 and add all elements into the visited set. Then, we traverse list2 and if any element from the second list is already visited, then we add that element into the result list. Same as above, the order of elements in output is not relevant.

![has](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/has/has44.png)