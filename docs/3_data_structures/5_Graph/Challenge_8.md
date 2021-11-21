---
layout: default
title: Challenge 8
parent: Graph
grand_parent: Data Structures
nav_order: 8
permalink: /data_structures/graph/ch8
---
<div align="center" markdown="1">
Challenge 8 / Java resources / Tutorial

{: .fs-8 .fw-400 }
</div>

## Challenge 8: Find Length of Shortest Path between Two Vertices

Given a graph, find the shortest path between two vertices. A solution is placed in the "solution" section to help you, but we would suggest trying to solve it on your own first.

Problem Statement#
In this problem, you have to implement the findShortestPathLength() method to take an undirected graph and two vertices (A and B) as inputs, and return the length of the shortest path between those vertices in Graph. Remember, the shortest path will contain the minimum number of edges. An illustration is provided below for your understanding:

![graph](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/graph/rr16.png)

![graph](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/graph/rr17.png)

![graph](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/graph/rr18.png)

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
        this.adjacencyList[destination].insertAtEnd(source);
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

class CheckMin {
    public static int findShortestPathLength(Graph g, int source, int destination) {
        //Write -- Your -- Code
       return -1;
    }
}
{% endhighlight %}

## Solution Review: Find the Shortest Path between Two Vertices

## Solution: BFS Queue

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

class CheckMin {
    public static int findMin(Graph g, int source, int destination) {
        if (source == destination){
            return 0;
        }

        int result = 0;
        int num_of_vertices = g.vertices;

        //Boolean Array to hold the history of visited nodes (by default-false)
        //Make a node visited whenever you enqueue it into queue
        boolean[] visited = new boolean[num_of_vertices];

        //For keeping track of distance of current_node from source
        int[] distance = new int[num_of_vertices];

        //Create Queue for Breadth First Traversal and enqueue source in it
        Queue<Integer> queue = new Queue<Integer>(num_of_vertices);

        queue.enqueue(source);
        visited[source] = true;

        //Traverse while queue is not empty
        while (!queue.isEmpty()) {

            //Dequeue a vertex/node from queue and add it to result
            int current_node = queue.dequeue();

            //Get adjacent vertices to the current_node from the array,
            //and if they are not already visited then enqueue them in the Queue
            //and also update their distance from source by adding 1 in current_nodes's distance
            DoublyLinkedList<Integer>.Node temp = null;
            if (g.adjacencyList[current_node] != null)
                temp = g.adjacencyList[current_node].headNode;

            while (temp != null) {

                if (!visited[temp.data]) {
                    queue.enqueue(temp.data);
                    visited[temp.data] = true;
                    distance[temp.data] = distance[current_node] + 1;
                }
                if (temp.data == destination) {
                    return distance[destination];
                }
                temp = temp.nextNode;
            }
        }//end of while
        return -1;
    }
    public static void main(String args[]) {
        Graph g=new Graph(5);
        g.addEdge(0,1);
        g.addEdge(0,2);
        g.addEdge(1,3); 
        g.addEdge(3,4); 
        g.addEdge(1,4);
        System.out.println(findMin(g, 0, 4));
    }
}
{% endhighlight %}

Explanation #
Once again, Breadth First Search comes to the rescue. The visited list must be familiar to you by now. The crux of this algorithm, however, lies in the distance list. For each node, the indexed value in the distance shows the node’s distance from the source in terms of the number of edges.

The rest is a simple BFS traversal, where the distance is incremented by 1 each time.

We are guaranteed to find the shortest distance to destination, once it has already been visited through the longer path and consequently marked because it won’t be visited the same way again.

Time Complexity #
The algorithm will have the same time complexity as BFS:

O(V + E)O(V+E)


