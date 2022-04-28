---
layout: default
title: Topological Sort
parent: Algorithms
nav_order: 16
permalink: /algorithms/topological_ort
---
<div align="center" markdown="1">
Topological Sort / Java resources / Tutorial

{: .fs-8 .fw-400 }
</div>

## Pattern: Topological Sort (Graph)

## Introduction
Topological Sort is used to find a linear ordering of elements that have dependencies on each other. For example, if event ‘B’ is dependent on event ‘A’, ‘A’ comes before ‘B’ in topological ordering.

This pattern defines an easy way to understand the technique for performing topological sorting of a set of elements and then solves a few problems using it.

Let’s see this pattern in action.

## Topological Sort

## Problem Statement
Topological Sort of a directed graph (a graph with unidirectional edges) is a linear ordering of its vertices such that for every directed edge (U, V) from vertex U to vertex V, U comes before V in the ordering.

Given a directed graph, find the topological ordering of its vertices.

Example 1:

![alg](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/alg/gg1.png)

![alg](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/alg/gg2.png)

![alg](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/alg/gg3.png)

![alg](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/alg/gg4.png)

![alg](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/alg/gg5.png)

![alg](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/alg/gg6.png)

## Solution
The basic idea behind the topological sort is to provide a partial ordering among the vertices of the graph such that if there is an edge from U to V then U≤V i.e., U comes before V in the ordering. Here are a few fundamental concepts related to topological sort:
1. Source: Any node that has no incoming edge and has only outgoing edges is called a source.
2. Sink: Any node that has only incoming edges and no outgoing edge is called a sink.
3. So, we can say that a topological ordering starts with one of the sources and ends at one of the sinks.
4. A topological ordering is possible only when the graph has no directed cycles, i.e. if the graph is a Directed Acyclic Graph (DAG). If the graph has a cycle, some vertices will have cyclic dependencies which makes it impossible to find a linear ordering among vertices.

To find the topological sort of a graph we can traverse the graph in a Breadth First Search (BFS) way. We will start with all the sources, and in a stepwise fashion, save all sources to a sorted list. We will then remove all sources and their edges from the graph. After the removal of the edges, we will have new sources, so we will repeat the above process until all vertices are visited.

Here is the visual representation of this algorithm for Example-3:

![alg](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/alg/gg7.png)

This is how we can implement this algorithm:

1. a. Initialization
   * We will store the graph in Adjacency Lists, which means each parent vertex will have a list containing all of its children. We will do this using a HashMap where the ‘key’ will be the parent vertex number and the value will be a List containing children vertices.
   * To find the sources, we will keep a HashMap to count the in-degrees i.e., count of incoming edges of each vertex. Any vertex with ‘0’ in-degree will be a source.
2. b. Build the graph and find in-degrees of all vertices
   * We will build the graph from the input and populate the in-degrees HashMap.
3. c. Find all sources
   * All vertices with ‘0’ in-degrees will be our sources and we will store them in a Queue.
4. d. Sort
   * For each source, do the following things:
      * Add it to the sorted list.
      * Get all of its children from the graph.
      * Decrement the in-degree of each child by 1.
      * If a child’s in-degree becomes ‘0’, add it to the sources Queue.
   * Repeat step 1, until the source Queue is empty.

## Code

{% highlight java %}
import java.util.*;

class TopologicalSort {
  public static List<Integer> sort(int vertices, int[][] edges) {
    List<Integer> sortedOrder = new ArrayList<>();
    if (vertices <= 0)
      return sortedOrder;

    // a. Initialize the graph
    HashMap<Integer, Integer> inDegree = new HashMap<>(); // count of incoming edges for every vertex
    HashMap<Integer, List<Integer>> graph = new HashMap<>(); // adjacency list graph
    for (int i = 0; i < vertices; i++) {
      inDegree.put(i, 0);
      graph.put(i, new ArrayList<Integer>());
    }

    // b. Build the graph
    for (int i = 0; i < edges.length; i++) {
      int parent = edges[i][0], child = edges[i][1];
      graph.get(parent).add(child); // put the child into it's parent's list
      inDegree.put(child, inDegree.get(child) + 1); // increment child's inDegree
    }

    // c. Find all sources i.e., all vertices with 0 in-degrees
    Queue<Integer> sources = new LinkedList<>();
    for (Map.Entry<Integer, Integer> entry : inDegree.entrySet()) {
      if (entry.getValue() == 0)
        sources.add(entry.getKey());
    }

    // d. For each source, add it to the sortedOrder and subtract one from all of its children's in-degrees
    // if a child's in-degree becomes zero, add it to the sources queue
    while (!sources.isEmpty()) {
      int vertex = sources.poll();
      sortedOrder.add(vertex);
      List<Integer> children = graph.get(vertex); // get the node's children to decrement their in-degrees
      for (int child : children) {
        inDegree.put(child, inDegree.get(child) - 1);
        if (inDegree.get(child) == 0)
          sources.add(child);
      }
    }

    if (sortedOrder.size() != vertices) // topological sort is not possible as the graph has a cycle
      return new ArrayList<>();

    return sortedOrder;
  }

  public static void main(String[] args) {
    List<Integer> result = TopologicalSort.sort(4,
        new int[][] { new int[] { 3, 2 }, new int[] { 3, 0 }, new int[] { 2, 0 }, new int[] { 2, 1 } });
    System.out.println(result);

    result = TopologicalSort.sort(5, new int[][] { new int[] { 4, 2 }, new int[] { 4, 3 }, new int[] { 2, 0 },
        new int[] { 2, 1 }, new int[] { 3, 1 } });
    System.out.println(result);

    result = TopologicalSort.sort(7, new int[][] { new int[] { 6, 4 }, new int[] { 6, 2 }, new int[] { 5, 3 },
        new int[] { 5, 4 }, new int[] { 3, 0 }, new int[] { 3, 1 }, new int[] { 3, 2 }, new int[] { 4, 1 } });
    System.out.println(result);
  }
}
{% endhighlight %}

![alg](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/alg/gg8.png)

![alg](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/alg/gg9.png)