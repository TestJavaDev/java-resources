---
layout: default
title: Challenge 4
parent: Graph
grand_parent: Data Structures
nav_order: 4
permalink: /data_structures/graph/ch4
---
<div align="center" markdown="1">
Challenge 4 / Java resources / Tutorial

{: .fs-8 .fw-400 }
</div>

## Challenge 4: Find "Mother Vertex" in a Directed Graph

Given a graph, can you find the Mother Vertex? Attempt to prove yourself!

## Problem Statement 
🔍 
## Mother Vertex? 
A mother vertex in a graph G = (v,e) is a vertex v, such that all other vertices in G can be reached by a path from v.

In this problem, you have to implement the findMotherVertex() method to take a graph as an input and find out which vertex is the mother vertex in the graph. Remember, there’s no mother vertex in a disconnected graph. An illustration is also provided below for your understanding:

![graph](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/graph/rr4.png)

![graph](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/graph/rr5.png)

![graph](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/graph/rr6.png)

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

class CheckMotherVertex {

  public static int findMotherVertex(Graph g){
    // Write - Your - Code    
    return -1;
  }
}
{% endhighlight %}

## Solution Review: Find "Mother Vertex" in a Directed Graph

## Solution: Last Finished Vertex

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

class CheckMotherVertex {
    
    public static int findMotherVertex(Graph g) {
        // visited[] is used for DFS. Initially all are
        // initialized as not visited
        boolean[] visited = new boolean[g.vertices];
        Arrays.fill(visited, false);

        // To store last finished vertex (or mother vertex)
        int lastV = 0;

        // Do a DFS traversal and find the last finished vertex
        for (int i = 0; i < g.vertices; i++) {
            if (visited[i] == false) {
                DFS(g, i, visited);
                lastV = i;
            }
        }

        // If there exist mother vertex (or vetices) in given
        // graph, then lastV must be one (or one of them)

        // Now check if lastV is actually a mother vertex (or graph
        // has a mother vertex). We basically check if every vertex
        // is reachable from lastV or not.

        // Reset all values in visited[] as false and do
        // DFS beginning from lastV to check if all vertices are
        // reachable from it or not.
        Arrays.fill(visited, false);
        DFS(g, lastV, visited);

        for (int i = 0; i < visited.length; i++){
            if(visited[i] == false){
                return -1;
            }
        }

        return lastV;
    }

    // A recursive function to print DFS starting from v
    public static void DFS(Graph g, int node, boolean[] visited) {

        visited[node] = true;
        DoublyLinkedList<Integer>.Node temp = null;
        if (g.adjacencyList[node] !=null)
            temp = g.adjacencyList[node].headNode;

        while(temp != null){
            if(visited[temp.data]){
                temp = temp.nextNode;
            }
            else{
                visited[temp.data] = true;
                DFS(g, temp.data, visited);
                temp = temp.nextNode;
            }
        }
    }
    
    public static void main(String args[]) {
        
        Graph g = new Graph(4);
        g.addEdge(0,1);
        g.addEdge(1,2);
        g.addEdge(3,0);
        g.addEdge(3,1);
        g.printGraph();
        System.out.println("Mother Vertex is: " + findMotherVertex(g));
        
    }
}
{% endhighlight %}

## Explanation 
This solution is based on Kosaraju’s Strongly Connected Component Algorithm. Initially, we run the DFS on the whole graph in a loop (line 13). The DFS ensures that all the nodes in the graph are visited. If the graph is disconnected, the visited array will still have some vertices which haven’t been set to true.

The theory is that the last vertex visited in the recursive DFS will be the mother vertex. This is because, at the last vertex, all slots in visited would be true (DFS only stops when all nodes are visited). Hence, we keep track of this last vertex using lastV.

Then, we reset the visited array and run the DFS only on lastV. If it visits all nodes, it is a mother vertex. Otherwise, a mother vertex does not exist. The only limitation in this algorithm is that it can detect one mother vertex, even if others exist.

## Time Complexity 
The DFS of the whole graph works in O(V + E). If a mother vertex exists, the second DFS takes O(V + E) as well. Therefore, the complete time complexity for this algorithm is O(V + E).