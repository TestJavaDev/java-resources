---
layout: default
title: Challenge 6
parent: Graph
grand_parent: Data Structures
nav_order: 6
permalink: /data_structures/graph/ch6
---
<div align="center" markdown="1">
Challenge 6 / Java resources / Tutorial

{: .fs-8 .fw-400 }
</div>

## Challenge 6: Check if a Path Exists Between Two Vertices

Given a graph and two vertices, can you write a code to check if a path exists between the two given vertices? Try it yourself!

Problem Statement #
In this problem, you have to implement checkPath() method to take a graph and two vertices as an input and find out if a path exists between them.

If there is no repeated sequence of edges and vertices between the source and the destination vertex then the path exists between these two vertices.

Note: Path will always exist if the source and destination nodes are the same.

An illustration is also provided below for your understanding:

![graph](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/graph/rr10.png)

![graph](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/graph/rr11.png)

![graph](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/graph/rr12.png)

## Coding Exercise

{% highlight java %}
public class Graph{
    int vertices;
    DoublyLinkedList<Integer> adjacencyList[];

    @SuppressWarnings("unchecked")
    public Graph(int vertices) {
        this.vertices = vertices;
        adjacencyList = new DoublyLinkedList[vertices];

        for (int i = 0; i < vertices; i++) {
            adjacencyList[i] = new DoublyLinkedList<>();
        }
    }

    public void addEdge(int source, int destination){
        this.adjacencyList[source].insertAtEnd(destination);

        //for undirected graph uncomment the line below
        //this.adjacencyList[destination].insertAtEnd(source);
    }
    public void printGraph()
    {
        System.out.println(">>Adjacency List of Directed Graph<<");
        for (int i = 0; i < vertices; i++)
        {
            if(adjacencyList[i]!=null){
                System.out.print("|" + i + "| => ");

                DoublyLinkedList<Integer>.Node temp = adjacencyList[i].getHeadNode();
                while (temp != null)
                {
                    System.out.print("[" + temp.data + "] -> ");
                    temp = temp.nextNode;
                }
                System.out.println("null");
            }
            else{

                System.out.println("|" + i + "| => "+ "null");
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
    Comment out the line below and execute again to see the warning.
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

public class Queue<V> {
    private int maxSize;
    private V[] array;
    private int front;
    private int back;
    private int currentSize;

    /*
    Java does not allow generic type arrays. So we have used an
    array of Object type and type-casted it to the generic type V.
    This type-casting is unsafe and produces a warning.
    Comment out the line below and execute again to see the warning.
    */
    @SuppressWarnings("unchecked")
    public Queue(int maxSize) {
        this.maxSize = maxSize;
        array = (V[]) new Object[maxSize];
        front = 0;
        back = -1;
        currentSize = 0;
    }

    public int getMaxSize() {
        return maxSize;
    }

    public int getCurrentSize() {
        return currentSize;
    }

    public boolean isEmpty() {
        return currentSize == 0;
    }

    public boolean isFull() {
        return currentSize == maxSize;
    }

    public void enqueue(V value) {
        if (isFull())
            return;
        back = (back + 1) % maxSize; //to keep the index in range
        array[back] = value;
        currentSize++;
    }

    public V dequeue (){
        if(isEmpty())
            return null;

        V temp = array[front];
        front = (front + 1) % maxSize; //to keep the index in range
        currentSize--;

        return temp;
    }
}

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

class CheckPaths {
    
    public static boolean checkPath(Graph g, int source, int destination) {
        // Write - Your - Code
        return 0;
    }
}
{% endhighlight %}

## Solution Review: Check if a Path Exists Between Two Vertices

## Solution: Using BFS/DFS

{% highlight java %}
public class Graph{
    int vertices; //Total number of vertices in graph
    DoublyLinkedList<Integer> adjacencyList[]; //An array of linked lists to store adjacent vertices.
    
    @SuppressWarnings("unchecked")
    public Graph(int vertices) {
        this.vertices = vertices;
        adjacencyList = new DoublyLinkedList[vertices];

        for (int i = 0; i < vertices; i++) {
            adjacencyList[i] = new DoublyLinkedList<>();
        }
    }

    public void addEdge(int source, int destination){
        if (source < vertices && destination < vertices){
        this.adjacencyList[source].insertAtEnd(destination);

        //for undirected graph uncomment the line below
        //this.adjacencyList[destination].insertAtEnd(source);
        }
    }
    public void printGraph()
    {
        System.out.println(">>Adjacency List of Directed Graph<<");
        for (int i = 0; i < vertices; i++)
        {
            if(adjacencyList[i]!=null){
                System.out.print("|" + i + "| => ");

                DoublyLinkedList<Integer>.Node temp = adjacencyList[i].getHeadNode();
                while (temp != null)
                {
                    System.out.print("[" + temp.data + "] -> ");
                    temp = temp.nextNode;
                }
                System.out.println("null");
            }
            else{

                System.out.println("|" + i + "| => "+ "null");
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
    Comment out the line below and execute again to see the warning.
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

public class Queue<V> {
    private int maxSize;
    private V[] array;
    private int front;
    private int back;
    private int currentSize;

    /*
    Java does not allow generic type arrays. So we have used an
    array of Object type and type-casted it to the generic type V.
    This type-casting is unsafe and produces a warning.
    Comment out the line below and execute again to see the warning.
    */
    @SuppressWarnings("unchecked")
    public Queue(int maxSize) {
        this.maxSize = maxSize;
        array = (V[]) new Object[maxSize];
        front = 0;
        back = -1;
        currentSize = 0;
    }

    public int getMaxSize() {
        return maxSize;
    }

    public int getCurrentSize() {
        return currentSize;
    }

    public boolean isEmpty() {
        return currentSize == 0;
    }

    public boolean isFull() {
        return currentSize == maxSize;
    }

    public void enqueue(V value) {
        if (isFull())
            return;
        back = (back + 1) % maxSize; //to keep the index in range
        array[back] = value;
        currentSize++;
    }

    public V dequeue (){
        if(isEmpty())
            return null;

        V temp = array[front];
        front = (front + 1) % maxSize; //to keep the index in range
        currentSize--;

        return temp;
    }
}

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

class CheckPaths {
    
    //Perfrom DFS Traversal starting from source and if you reach destination
    //then it means that there exist a path between source and destination
    //so return true and if you traverse the graph but can't reach destination
    //then simply return false.
    public static boolean checkPath(Graph g, int source, int destination) {
        if (source == destination){
            return true;
        }

        //Boolean Array to hold the history of visited nodes (by default-false)
        //Make a node visited whenever you push it into stack
        boolean[] visited = new boolean[g.vertices];

        //Create Stack
        Stack<Integer> stack = new Stack<>(g.vertices);

        stack.push(source);
        visited[source] = true;

        //Traverse while stack is not empty
        while (!stack.isEmpty()) {

            //Pop a vertex/node from stack
            int current_node = stack.pop();

            //Get adjacent vertices to the current_node from the array,
            //and if only push unvisited adjacent vertices into stack
            //Before pushing into stack, check if it's the destination.
            DoublyLinkedList<Integer>.Node temp = null;
            if (g.adjacencyList[current_node] != null)
                temp = g.adjacencyList[current_node].headNode;

            while (temp != null) {

                if (!visited[temp.data]) {

                    if (temp.data == destination) {
                        return true;
                    }

                    stack.push(temp.data);
                    visited[temp.data] = true;

                }

                temp = temp.nextNode;
            }

        } //end of while
        return false;
    }
    public static void main(String args[]) {
    
        Graph g1 = new Graph(9);
        g1.addEdge(0,2);
        g1.addEdge(0,5);
        g1.addEdge(2,3);
        g1.addEdge(2,4);
        g1.addEdge(5,3);
        g1.addEdge(5,6);
        g1.addEdge(3,6);
        g1.addEdge(6,7);
        g1.addEdge(6,8);
        g1.addEdge(6,4);
        g1.addEdge(7,8);
        g1.printGraph();
        System.out.println("Path exists: " + checkPath(g1, 0, 7));
        System.out.println();
        Graph g2 = new Graph(4);
        g2.addEdge(0,1);
        g2.addEdge(1,2);
        g2.addEdge(1,3);
        g2.addEdge(2,3);

        g2.printGraph();
        System.out.println("Path exists: " + checkPath(g2, 3, 0));
  }
}
{% endhighlight %}

Explanation #
This problem can be solved by both DFS and BFS. All we need is a simple traversal from source to see if we can reach destination. If the destination value is found, we return True.

Note that we only use the values in the vertices, not the vertices or the linked list objects themselves. This makes syntax easier.

Time Complexity #
It has the same time complexity as the BFS or DFS algorithm: O(V + E).

