---
layout: default
title: Challenge 11
parent: Linked Lists
grand_parent: Data Structures
nav_order: 13
permalink: /data_structures/linked_lists/ch11
---
<div align="center" markdown="1">
Challenge 11 / Java resources / Tutorial

{: .fs-8 .fw-400 }
</div>

## Challenge 11: Find if Doubly Linked-list is a Palindrome

Problem Statement#
This challenge is easier to perform on a doubly linked-list with a tail pointer than on a singly linked-list. Let’s first see what a palindrome is. A palindrome is any string or sequence that reads the same from both ends. The following snippet shows examples of some palindromes.

RACECAR
MADAM
WOW
2002
You can extend this example to a linked-list as well. For example, the following linked-lists are palindromes:

List = 2<->0<->0<->2
List = 1<->2<->3<->2<->1
List = 1
The following ones are not palindrome:

List = 1<->2<->3
List = 2<->3
Method Prototype#
public static boolean isPalindrome(DoublyLinkedList<T> list)
Output#
Your function will return a boolean variable; true when linked-list is a palindrome, false when it is not.

Sample Input#
A doubly linked list with tail pointer

linkedlist = 1<->2<->3<->2<->1
Sample Output#
true

![lin](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/lin/ex28.png)

## Coding Exercise

{% highlight java %}
public class DoublyLinkedList<T> {

    //Node inner class for DLL
    public class Node {
        public T data;
        public Node nextNode;
        public Node prevNode;
    }

    public Node headNode;
    public Node tailNode;
    public int size;

    public DoublyLinkedList() {
        this.headNode = null;
        this.tailNode = null;
    }

    public boolean isEmpty() {
        if (headNode == null && tailNode == null)
            return true;
        return false;
    }

    public Node getHeadNode() {
        return headNode;
    }

    public Node getTailNode() {
        return tailNode;
    }

    public int getSize() {
        return size;
    }

    public void insertAtHead(T data) {
        Node newNode = new Node();
        newNode.data = data;
        newNode.nextNode = this.headNode; //Linking newNode to head's nextNode
        newNode.prevNode = null;
        if (headNode != null)
            headNode.prevNode = newNode;
        else
            tailNode = newNode;
        this.headNode = newNode;
        size++;
    }

    public void insertAtEnd(T data) {
        if (isEmpty()) {
            insertAtHead(data);
            return;
        }
        Node newNode = new Node();
        newNode.data = data;
        newNode.nextNode = null;
        newNode.prevNode = tailNode;
        tailNode.nextNode = newNode;
        tailNode = newNode;
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

    public void printListReverse() {
        if (isEmpty()) {
            System.out.println("List is Empty!");
            return;
        }

        Node temp = tailNode;
        System.out.print("List : null <- ");

        while (temp.prevNode != null) {
            System.out.print(temp.data.toString() + " <-> ");
            temp = temp.prevNode;
        }

        System.out.println(temp.data.toString() + " -> null");
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
                if (currentNode.nextNode != null)
                    currentNode.nextNode.prevNode = currentNode.prevNode;
                size--;
            }
            currentNode = currentNode.nextNode;
        }
    }

    public void deleteAtHead() {
        if (isEmpty())
            return;

        headNode = headNode.nextNode;
        if (headNode == null)
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

}

class PalindromeChallenge {
    public static <T> boolean isPalindrome(DoublyLinkedList<T> list) {
        //Write Your Code Here
        return false;
    }
}
{% endhighlight %}

## Solution: Find if a Doubly Linked-list is a Palindrome

{% highlight java %}
public class DoublyLinkedList<T> {

    //Node inner class for DLL
    public class Node {
        public T data;
        public Node nextNode;
        public Node prevNode;
    }

    public Node headNode;
    public Node tailNode;
    public int size;

    public DoublyLinkedList() {
        this.headNode = null;
        this.tailNode = null;
    }

    public boolean isEmpty() {
        if (headNode == null && tailNode == null)
            return true;
        return false;
    }

    public Node getHeadNode() {
        return headNode;
    }

    public Node getTailNode() {
        return tailNode;
    }

    public int getSize() {
        return size;
    }

    public void insertAtHead(T data) {
        Node newNode = new Node();
        newNode.data = data;
        newNode.nextNode = this.headNode; //Linking newNode to head's nextNode
        newNode.prevNode = null;
        if (headNode != null)
            headNode.prevNode = newNode;
        else
            tailNode = newNode;
        this.headNode = newNode;
        size++;
    }

    public void insertAtEnd(T data) {
        if (isEmpty()) {
            insertAtHead(data);
            return;
        }
        Node newNode = new Node();
        newNode.data = data;
        newNode.nextNode = null;
        newNode.prevNode = tailNode;
        tailNode.nextNode = newNode;
        tailNode = newNode;
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

    public void printListReverse() {
        if (isEmpty()) {
            System.out.println("List is Empty!");
            return;
        }

        Node temp = tailNode;
        System.out.print("List : null <- ");

        while (temp.prevNode != null) {
            System.out.print(temp.data.toString() + " <-> ");
            temp = temp.prevNode;
        }

        System.out.println(temp.data.toString() + " -> null");
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
                if (currentNode.nextNode != null)
                    currentNode.nextNode.prevNode = currentNode.prevNode;
                size--;
            }
            currentNode = currentNode.nextNode;
        }
    }

    public void deleteAtHead() {
        if (isEmpty())
            return;

        headNode = headNode.nextNode;
        if (headNode == null)
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

}

class PalindromeChallenge {
    public static <T> boolean isPalindrome(DoublyLinkedList<T> list) {
        DoublyLinkedList<T>.Node start = list.getHeadNode(); // get the head pointer
        DoublyLinkedList<T>.Node end = list.getTailNode(); // get the tail
        if (start == null){ // if list is empty, it is a palindrome
            return true;
        }
        while(start != null){ //otherwise traverse list from both sides
            if (start.data != end.data){ // if data mismatches at any point list is not a palindrome
            return false;
            }
            start = start.nextNode;
            end = end.prevNode;
        }
        return true; // if data didn't mismatch at any point, list is a palindrome.
    }
    public static void main( String args[] ) {
        DoublyLinkedList<Integer> list1 = new DoublyLinkedList<Integer>();
        list1.insertAtEnd(1);
        list1.insertAtEnd(2);
        list1.insertAtEnd(2);
        list1.insertAtEnd(1);
        System.out.print("1st ");
        list1.printList();
        DoublyLinkedList<Integer> list2 = new DoublyLinkedList<Integer>();
        list2.insertAtEnd(6);
        list2.insertAtEnd(8);
        list2.insertAtEnd(6);
        list2.insertAtEnd(6);
        System.out.print("2nd ");
        list2.printList();
        System.out.println("Is 1st list a palindrome?  " + isPalindrome(list1));
        System.out.println("Is 2nd list a palindrome?  " + isPalindrome(list2));

    }
    
}

{% endhighlight %}

Explanation#
We start by taking pointers to headNode and tailNode (lines 3-4). Next, we check for a corner-case, when linked-list is empty, an empty linked-list is a palindrome so we return true (lines 5-7). Then, we simply traverse the linked-list from both ends simultaneously and see if the traversals result in the same sequence of values (lines 8-14). If that is not the case, the linked-list is not a palindrome (line 9-11), otherwise, it is.

Time Complexity#
It is an O(n)O(n) solution since we traverse the whole linked list