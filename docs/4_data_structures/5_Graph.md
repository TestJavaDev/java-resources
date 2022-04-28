---
layout: default
title: Graph
parent: Data Structures
nav_order: 5
permalink: /data_structures/graph
has_children: true
---
<div align="center" markdown="1">
Graph / Java resources / Tutorial

{: .fs-8 .fw-400 }
</div>

## Introduction 
A graph is a set of vertices (nodes) that are connected to each other via edges in the form of a network.

![graph](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/graph/graph1.png)

A Graph having 6 nodes and 7 edges
## Vertex:
The structures for storing data in a graph, represented in the form of Nodes (1,3,7…), are also called Vertices

![graph](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/graph/graph2.png)

A Graph having 4 Vertices
## Edge:
A pair(x,y) is called an edge, which indicates that vertex x is connected to vertex y. An edge may contain weight/cost, showing how much cost is required to traverse from vertex x to y.

Edges are usually represented using Straight lines.

![graph](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/graph/graph3.png)

A Graph having 3 Edges
## Types of Graphs 
There are two common types of graphs:
* Undirected
* Directed

## 1. Undirected Graph 
In an undirected graph, the edges are bi-directional by default; for example, with the pair (0,1), it means there exists an edge between vertex 0 and 1 without any specific direction. You can go from vertex 0 to 1, or vice versa.

![graph](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/graph/graph4.png)

An Undirected Graph having 3 vertices and 2 edges

## 2. Directed Graph
In a directed graph, the edges are unidirectional; for example, with the pair (0,1), it means there exists an edge from vertex 0 towards vertex 1, and the only way to traverse is to go from 0 to 1.

![graph](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/graph/graph5.png)

A Directed Graph having 3 vertices and 2 edges

## Graph Terminologies
1. Degree of Vertex: Total Number of edges connected to a vertex.

Consider the figure given below:
* => Degree of 5 = 3
* => Degree of 1 = 2
* => Degree of 6 = 1

![graph](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/graph/graph6.png)

A Graph having 6 nodes and 7 edges
There are two types of degrees:
* In-Degree of Vertex: Total Number of incoming edges connected to a vertex.
* Out-Degree of Vertex: Total Number of outgoing edges connected to a vertex.

![graph](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/graph/graph7.png)

In and Out Degrees of a Directed Graph
![graph](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/graph/graph8.png)

In and Out Degrees of an Undirected Graph
2. Parallel Edges: Two or more edges that are incident to the same two vertices.

![graph](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/graph/graph9.png)

Parallel Edged Graphs
3. Self Loop: Same endpoints of an edge, e.g., pair (x,x).

![graph](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/graph/graph10.png)

A graph showing self-loop

## Ways to Represent a Graph
Here are the two most common ways to represent a graph :
* Adjacency Matrix
* Adjacency List

## Adjacency Matrix 
The adjacency matrix is a two-dimensional matrix where each cell can contain a 0 or 1. The row and column headings represent the vertices.

If a cell contains 1, there exists an edge between the corresponding vertices, e.g., Matrix[0][1]=1Matrix[0][1]=1 shows that an edge exists between vertex 0 and 1.

![graph](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/graph/graph11.png)

## Explanation: 
Initially, the whole matrix is initialized with 0’s, and as soon as we get an edge, we record the source (row) and destination (col) value inside our adjacency matrix.

## Undirected Graph:
In the figure above, there is an undirected graph. If there exists an edge from the source to the destination, then we insert 1 for both cases ([row][col] and [col][row]) as we can traverse both ways.

## Directed Graph:
In the case of a directed graph–which has an edge going from Node 0 to Node 1–, there is 1 for rowcol[0][1] in the adjacency matrix, and we similarly fill all the remaining parts of the matrix. If there is a node going from [row] to a [col], then we insert 1 for that particular [row][col]; otherwise, we put 0.

## 2. Adjacency List
An array of Linked Lists is used to store edges between two vertices. The size of the array is equal to the number of vertices. Each index in this array represents a specific vertex in the graph. The entry at the index i of the array contains a linked list containing the vertices that are adjacent to vertex i.

![graph](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/graph/graph12.png)

## Undirected Graph:
For the undirected graph shown above, each edge connected to a vertex is mentioned in the linked list of the array index (representing that vertex). Since there is an edge from vertex 0 to vertex 1, so the linked list of vertex 0 (at array index 0) has a node with value 1. Thus representing that vertex 1 is having an edge with vertex 0.

A significant point to note here is that since this is an undirected graph, a linked list of vertex 1 will also contain a node with value 0, thus representing a vertex from 1 to 0.

![graph](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/graph/graph13.png)

## Directed Graph:
For the directed graph shown above, there are two outgoing edges from vertex 0: first to vertex 1 and second to vertex 2. So the linked list at array index 0 has nodes with value 1 and value 2.

Since this is a directed graph and edges are unidirectional, hence no edge exists between vertex 1 and vertex 0 and vertex 2 and vertex 0. Therefore 0 does not exist in a linked list of vertex 1 and vertex 2.

![graph](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/graph/graph14.png)

## Structure of Graph Class
Graph class consists of two data members: a total number of vertices in the graph, and an array of the linked list to store the adjacency list of vertices. Below is a code snippet of our Graph class:

![graph](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/graph/graph15.png)

## Explanation (Describing Graph Structure)
As you can see in the code snippet above, we have a basic structure of Graph class.

## Variables 
vertices to store the total number of vertices of the graph.

adjacencyList to store an array of linked lists. Each index of the array represents a vertex of the graph, and the linked list represents the adjacent vertices.

## Methods
printGraph() method prints the graph (adjacency list). addEdge() creates a source and destination vertex and connects them with an edge.

Code Snippet:

{% highlight java %}

class HelloWorld {
    public static void main( String args[] ) {
        Graph g= new Graph(4);
        g.addEdge(0, 1);
        g.addEdge(0, 2);
        g.addEdge(1, 3);
        g.addEdge(2, 3);
        g.printGraph();
    }
}
{% endhighlight %}

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
{% endhighlight %}

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
        if(isEmpty()) {
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
        }

        Node temp = tailNode;
        System.out.print("List : null <- ");

        while (temp.prevNode != null) {
            System.out.print(temp.data.toString() + " <-> ");
            temp = temp.prevNode;
        }

        System.out.println(temp.data.toString() + " -> null");
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
{% endhighlight %}

## Explanation (Method Calls) 
Let’s break the above code down into different sections:

## 1. Graph g=new Graph (int);
In the constructor, we create an array of size equal to the total number of vertices. In this case, our graph has 4 vertices. Hence constructor takes 4 as a parameter.

## 2. addEdge (int source, int destination);
Directed Graph:

The constructor of the Graph class creates an array of linked lists, where the size of the array is equal to the number of vertices in the graph. After creating the array, we need to add nodes to linked lists. Each node of the linked list will represent the adjacent vertex of that array index. The function addEdge takes two parameters, source vertex number, and destination vertex number. First, it checks whether the value of the source and destination vertex is valid or not. If the values are valid, it goes to index of the array equal to source number received in parameter and adds a node to the corresponding list. The added node contains the destination vertex number. The node is added to the list by the following line of code:

adjacencyList[source].insertAtEnd(destination);

## 3. main(); 
The main will create a graph like the figure given above.

It first calls the constructor of the graph class: new Graph(x) where x is the number of vertices in the graph.

* g.addEdge(0,1); – Creates an edge from 0 to 1
* g.addEdge(0,2); – Creates an edge from 0 to 2
* g.addEdge(1,3); – Creates an edge from 1 to 3
* g.addEdge(2,3); – Creates an edge from 2 to 3

After that, it simply prints the graph by calling printGraph() function.

## Complexities of Graph Operations

## Time Complexities
Below, you can find the time complexities for the 4 basic graph methods.

Note that in this table, V means the total number of vertices, and E means the total number of edges in the Graph.

![graph](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/graph/war1.png)

## Adjacency List
* The addition of edge in adjacency lists take constant time, as we only need to insert at the tail in the doubly-linked list with a tail pointer of the corresponding vertex.
* The addition of a vertex is not constant in the worst case. The adjacency list is an array of linked lists. So, we would need to allocate a bigger array, copy the contents from the previous array, which takes O(n). But this operation can be considered O(1) on average because we could do it smartly as follows. We start with a small array initially. Then, when there is a need to insert a vertex, instead of allocating one size bigger array, we allocate an array that is twice as big. That way, in the long run, the cost of re-allocation is averaged out over many other operations. So, O(1) is the average or amortized cost of add vertex in the adjacency list.
* Removing an edge takes O(E) time because–in the worst case–all the edges could be at a single vertex, and hence, we would have to traverse all E edges to reach the last one.
* Removing a vertex takes O(V + E) time because we have to delete all its edges, and then reindex the rest of the list one step back in order to fill the deleted spot.

## Adjacency Matrix
* Edge operations are performed in constant time, as we only need to manipulate the value in the particular cell.
* Vertex operations are performed in O(V2) since we need to add rows and columns. We will also need to fill all the new cells.

## Comparison
Both representations are suitable for different situations. If your model frequently manipulates vertices, the adjacency list is a better choice.

If you are dealing primarily with edges, the adjacency matrix is the more efficient approach.

Keep these complexities in mind because they will give you a better idea about the time complexities of the several algorithms we’ll see in this section.

## What is a Bipartite Graph?

## Introduction 
🔍 A Bipartite Graph is a special kind of Graph, in which the vertices can be divided into two disjoint sets U and V such that no vertex of U is adjacent to any other vertex in U and no vertex of V is adjacent to any other vertex in V. Vertices in U have edges that connect it to vertices in V.

![graph](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/graph/war2.png)

connected in a closed chain, are bipartite.

## Explanation
The above graphs are Bipartite.
* Yellow-colored vertices belong to a disjoint set U.
* Green colored vertices belong to a disjoint set V.

One can observe in the above graphs that no vertex of U is adjacent to any other vertex in U, and no vertex of V is adjacent to any other vertex in V.

## Can a Cycle Graph be Bi-Partite with Even Vertices?
The illustration below shows a cycle graph with an even number of vertices.

![graph](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/graph/war3.png)

But is the above graph Bipartite? Yes!

How? You can see that the graph on the left has an even number of nodes, which means that they can be divided into two disjoint sets, shown on the right side, with non-adjacent vertices.

Note: A graph cannot be Bipartite if there are an odd number of vertices and has an odd cycle i.e., a cycle between the odd number of vertices.

## Types of bipartite graphs 
Some other types of Bipartite graphs are listed below:
* Complete Bipartite Graphs: A complete Bipartite graph connects each vertex from set V1 to each vertex from set V2.
* Star Graphs: A star graph is a complete bipartite graph if a single vertex belongs to one set, and all the remaining vertices belong to the other set.
* Acyclic Graphs: A graph with no cycles is called an acyclic graph.

![graph](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/graph/war4.png)

## Graph Traversal Algorithms

## Introduction 
There are many applications for graphs, such as the GPS navigation system, shortest path finding, peer to peer networks, crawlers in the search engine, garbage collection (java), and even social networking websites.

Depending upon the problem under, the way we traverse a graph is important, since it can affect the time in which we reach the goal.

## Types of Graph Traversals
There are two basic techniques used for graph traversal:
* Breadth First Search (BFS)
* Depth First Search (DFS)

In order to understand these algorithms, we will have to view graphs from a slightly different perspective.

Any traversal needs a starting point, but a graph does not have a linear structure like lists or stacks. So how do we give the graph traversal a better sense of direction?

This is where the concept of levels is introduced. Take any vertex as the starting point. This is the lowest level in your search. The next level consists of all the vertices adjacent to your vertex. Therefore, a level higher would consist of the vertices adjacent to these nodes.

With this is in mind, let’s begin our discussion on the two Graph Traversal algorithms.

## 1. Breadth First Search 
The BFS algorithm earns its name because it grows breadth-wise. All the nodes at a certain level are traversed before moving on to the next level.

The level-wise expansion ensures that you can reach every level of a starting vertex, one level at a time.

Now, let’s look at the BFS algorithm in action.

To build a graph based on BFS, start traversing from any vertex, call it currentVertex. If the adjacent vertices are yet already not visited, then print their values. Then, move on to children of the currentVertex.

Let’s look at BFS traversal in action!

![graph](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/graph/war5.png)
![graph](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/graph/war6.png)
![graph](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/graph/war7.png)
![graph](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/graph/war8.png)
![graph](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/graph/war9.png)
![graph](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/graph/war10.png)
![graph](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/graph/war11.png)
![graph](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/graph/war12.png)

## 2. Depth First Traversal
The DFS algorithm is the opposite of BFS in the sense that it grows depth-wise.

Starting from any node, we keep moving to an adjacent node until we reach the farthest level. Then we move back to the starting point and pick another adjacent node. Once again, we probe till the farthest level and move back. This process continues until all nodes are visited.

Let’s look at DFS traversal in action:

![graph](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/graph/war13.png)
![graph](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/graph/war14.png)
![graph](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/graph/war15.png)
![graph](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/graph/war16.png)
![graph](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/graph/war17.png)
![graph](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/graph/war18.png)
![graph](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/graph/war19.png)
![graph](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/graph/war20.png)
![graph](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/graph/war21.png)
![graph](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/graph/war22.png)

![graph](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/graph/war23.png)


{% highlight java %}

{% endhighlight %}







