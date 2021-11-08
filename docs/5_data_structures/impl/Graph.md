---
layout: default
title: Graph
parent: Data Structures
# nav_order: 1
permalink: /data_structures/graph
---
<div align="center" markdown="1">
System Design Basics / Java resources / Tutorial

{: .fs-8 .fw-400 }
</div>

## Introduction 
A graph is a set of vertices (nodes) that are connected to each other via edges in the form of a network.

![graph](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/graph/graph1.png)
A Graph having 6 nodes and 7 edges
## Vertex:
The structures for storing data in a graph, represented in the form of Nodes (1,3,7…), are also called Vertices

![graph](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/graph/graph2.png)
A Graph having 4 Vertices
## Edge:
A pair(x,y) is called an edge, which indicates that vertex x is connected to vertex y. An edge may contain weight/cost, showing how much cost is required to traverse from vertex x to y.

Edges are usually represented using Straight lines.

![graph](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/graph/graph3.png)
A Graph having 3 Edges
## Types of Graphs 
There are two common types of graphs:

Undirected
Directed
## 1. Undirected Graph 
In an undirected graph, the edges are bi-directional by default; for example, with the pair (0,1), it means there exists an edge between vertex 0 and 1 without any specific direction. You can go from vertex 0 to 1, or vice versa.

![graph](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/graph/graph4.png)
An Undirected Graph having 3 vertices and 2 edges
## 2. Directed Graph
In a directed graph, the edges are unidirectional; for example, with the pair (0,1), it means there exists an edge from vertex 0 towards vertex 1, and the only way to traverse is to go from 0 to 1.

![graph](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/graph/graph5.png)
A Directed Graph having 3 vertices and 2 edges
## Graph Terminologies
1. Degree of Vertex: Total Number of edges connected to a vertex.

Consider the figure given below:

* => Degree of 5 = 3
* => Degree of 1 = 2
* => Degree of 6 = 1

![graph](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/graph/graph6.png)
A Graph having 6 nodes and 7 edges
There are two types of degrees:

In-Degree of Vertex: Total Number of incoming edges connected to a vertex.

Out-Degree of Vertex: Total Number of outgoing edges connected to a vertex.

![graph](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/graph/graph7.png)
In and Out Degrees of a Directed Graph
![graph](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/graph/graph8.png)
In and Out Degrees of an Undirected Graph
2. Parallel Edges: Two or more edges that are incident to the same two vertices.

![graph](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/graph/graph9.png)
Parallel Edged Graphs
3. Self Loop: Same endpoints of an edge, e.g., pair (x,x).

![graph](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/graph/graph10.png)
A graph showing self-loop

## Ways to Represent a Graph
Here are the two most common ways to represent a graph :

Adjacency Matrix
Adjacency List

## Adjacency Matrix 
The adjacency matrix is a two-dimensional matrix where each cell can contain a 0 or 1. The row and column headings represent the vertices.

If a cell contains 1, there exists an edge between the corresponding vertices, e.g., Matrix[0][1]=1Matrix[0][1]=1 shows that an edge exists between vertex 0 and 1.

![graph](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/graph/graph11.png)
## Explanation: 
Initially, the whole matrix is initialized with 0’s, and as soon as we get an edge, we record the source (row) and destination (col) value inside our adjacency matrix.

## Undirected Graph:
In the figure above, there is an undirected graph. If there exists an edge from the source to the destination, then we insert 1 for both cases ([row][col] and [col][row]) as we can traverse both ways.

## Directed Graph:
In the case of a directed graph–which has an edge going from Node 0 to Node 1–, there is 1 for rowcol[0][1] in the adjacency matrix, and we similarly fill all the remaining parts of the matrix. If there is a node going from [row] to a [col], then we insert 1 for that particular [row][col]; otherwise, we put 0.


## 2. Adjacency List
An array of Linked Lists is used to store edges between two vertices. The size of the array is equal to the number of vertices. Each index in this array represents a specific vertex in the graph. The entry at the index i of the array contains a linked list containing the vertices that are adjacent to vertex i.

![graph](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/graph/graph12.png)
## Undirected Graph:
For the undirected graph shown above, each edge connected to a vertex is mentioned in the linked list of the array index (representing that vertex). Since there is an edge from vertex 0 to vertex 1, so the linked list of vertex 0 (at array index 0) has a node with value 1. Thus representing that vertex 1 is having an edge with vertex 0.

A significant point to note here is that since this is an undirected graph, a linked list of vertex 1 will also contain a node with value 0, thus representing a vertex from 1 to 0.

![graph](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/graph/graph13.png)
## Directed Graph:
For the directed graph shown above, there are two outgoing edges from vertex 0: first to vertex 1 and second to vertex 2. So the linked list at array index 0 has nodes with value 1 and value 2.

Since this is a directed graph and edges are unidirectional, hence no edge exists between vertex 1 and vertex 0 and vertex 2 and vertex 0. Therefore 0 does not exist in a linked list of vertex 1 and vertex 2.

![graph](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/graph/graph14.png)

Structure of Graph Class #
Graph class consists of two data members: a total number of vertices in the graph, and an array of the linked list to store the adjacency list of vertices. Below is a code snippet of our Graph class:
![graph](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/graph/graph15.png)

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






