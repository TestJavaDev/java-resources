---
layout: default
title: Operating System
parent: Coding Interview
has_children: true
nav_order: 11
permalink: /coding_interview/os
---
<div align="center" markdown="1">
Operating System / Java resources / Tutorial

{: .fs-8 .fw-400 }
</div>

## Operating System

## Project Description for Operating System

## Introduction
A modern Operating System (OS) is a complex piece of software. It must manage finite, yet complex hardware resources while efficiently providing services to user software. In terms of hardware management, the OS must handle management of processing, storage and input/output resources. Another important part of the OS is user shell, which handles user interactions.

The scenario and problems we will discuss in this chapter relate to the memory and process manager modules of operating system software.

## Statement
Suppose you are a developer on a famous OS engineering team, and the team. Your team is working on several features related to scheduling of processes as well as efficient allocation of memory to processes. Another module that you are working on deals with efficient encoding of files on disk.

## Features

To implement the above-mentioned functionalities, we will need to introduce the following features:
* Feature #1: First, we need to determine the number of possible ways one or more running processes with contiguous memory allocation can be preempted to free up memory for a new process.
* Feature #2: Second, we need to locate the nth process to resume from a list of process IDs that are currently in memory.
* Feature #3: Order the processes in such a way that whenever a process is scheduled, all of its dependencies are already met.
* Feature #4: Deploy a compression strategy to identify and isolate all concatenated words.

Understanding these feature requests and designing their solutions will help us implement the requested functionality into the operating system.

In the next few lessons, we’ll discuss the recommended implementations of these features. Before we start, think about how you would implement these features. As you do, you’ll realize some of the underlying problems that you’ll need to solve. The solutions to these basic problems are also applicable to other common coding interview questions.

## Feature #1: Allocate Space

## Description
The first feature we need to build will identify the contiguous sub-processes that can be replaced with an incoming process of size n. In this scenario, we have p running processes numbered 1 through p in our system. We allocate memory to these processes contiguously such that process 1 occupies p_1 MB, process 2 immediately occupies p_2 MB, and so on. We receive the contiguous allocations p_1, p_2, …, p_n as an array. An incoming process requires a contiguous chunk of n MB anywhere in memory. To allocate memory to this process, we can evict one process or a set of processes that occupy contiguous memory locations that once evicted free up an n MB amount of space collectively. Here, our task will be to find the total number of all possible subsets of currently running processes that together account for a contiguous allocation of n MBs of memory.

In this scenario, we will be provided with two inputs. First, we will be given an array of integers representing the size of contiguous memory chunks allocated to the running processes. Second, we’ll be given n, which is the size of the memory required for the new process (in MB).

Here is an illustration of this behavior:

![op](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/op/op1.png)

Solution#
We can intuitively solve this problem by calculating the cumulative sum at each array index. Then, to identify the subarray, we can observe whether the cumulative sum, say Sum[i], is the same up to two indices. If they are the same, the sum of the elements at those indices will be zero. Extending this observation further, if the cumulative sum up to two indices, say i and j, have a difference of n, i.e., if sum[i] - sum[j] = n, the sum of elements lying between indices i and j will also be n.

We will implement this feature like so:
1. First, we’ll use a hashmap to store the cumulative sums and the count of how many times the same sum occurs. We will treat the sum as the key and the count as its corresponding value. A single entry will be in the (cumSum[i], count of cumSum[i]) format.
2. Next, we’ll traverse over the array and compute the cumulative sum at each index. We will make an entry into the hashmap every time a new sum occurs and assign it the count value 1. If a sum repeats, increment the count value by 1.
3. In addition to the previous step, we’ll compute cumSum - n at each index; this will determine the number of times a subarray with a sum of n has occurred. We will also increment the count, the number of times n was found.
4. Finally, return the count after the array has been traversed.

The following illustration might clarify this process.

![op](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/op/op2.png)
![op](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/op/op3.png)
![op](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/op/op4.png)
![op](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/op/op5.png)
![op](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/op/op6.png)
![op](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/op/op7.png)

Let’s look at the code for the solution below:

{% highlight java %}
import java.util.*;
class Solution {

    public static int AllocateSpace(int[] processes, int new_p) {

        int count = 0, sum = 0;
        HashMap <Integer, Integer> res = new HashMap<>();
        res.put(0, 1);
        for (int i = 0; i < processes.length; i++) {
            sum += processes[i];
            if (res.containsKey(sum - new_p))
                count += res.get(sum - new_p);
            res.put(sum, res.getOrDefault(sum, 0) + 1);
        }
        return count;
    }

    public static void main(String[] args){
        // Driver code
        int[] processes = {1,2,3,4,5,6,7,1,23,21,3,1,2,1,1,1,1,1,12,2,3,2,3,2,2};
        System.out.println(AllocateSpace(processes, 1));
    }

}
{% endhighlight %}

![op](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/op/op8.png)

## Feature #2: Resume Process

## Description
Our second task is building a feature to identify which process should be resumed into memory from its preempted state. Initially, one or more contiguous memory blocks are allocated to each running process. The allocation is done in ascending order of process ID. This means that the lower-numbered process IDs get memory blocks near address 0, and higher-numbered process IDs get allocated at higher addressed portions of memory. Some processes are preempted(interrupted) and currently don’t have any memory allocated to them. The OS wants to schedule one of the preempted processes. The OS uses a strategy that the resumes preempted processes in a round-robin fashion, starting with the one that has the lowest process ID. We are currently in the nth round of process resumption. Our task is to find the nth process to resume from an array of process IDs that are currently in memory.

We’ll be provided with an array of process IDs and a number n. We’ll have to find the nth missing process id starting from the beginning of the array.

## Solution
Since we are searching for a number in a sorted array, the binary search algorithm would be most applicable to use here. Let’s assume we have an array of process IDs [5, 7, 9, 10, 13] and we want to find and resume the 3rd process that was preempted. In other words, we need to find the 3rd missing number from the sorted array.

Following the binary search algorithm, we’ll keep dividing the array from the middle to search for the required missing number in the first and second halves. The first division of our array [5,7,9,10,13] gives us [5,7,9] as our first half and [9,10,13] as our second. If there are no missing numbers in a sub-array, the size of the sub-array should be one plus the difference between the last and first numbers. For our first sub-array [5, 7, 9], the actual size is 3. However, we expected there to be 9 - 5 + 19−5+1 or 5 elements in it, so there are 5 - 35−3, or 2, elements missing from this array.

Now, we know that there are two numbers missing from this sub-array. Since we are looking for the 3rd missing number in the array, it can’t be in the current sub-array, so we won’t process it any further. The 3rd missing number should be in the right half of the original array, [9, 10, 13]. Since two numbers were missing from the left half of the array, we are looking for the first missing number in the [9, 10, 13] sub-array.

Now, we will divide the second half of the array, [9,10,13] into two halves: [9, 10] and [10, 13], and repeat the process outlined above for these two sub-arrays. Doing this, we discover that the first half [9, 10] has 0 missing elements and the second half [10, 13] gives us 13 - 10 + 1 = 4 - 2 = 213−10+1=4−2=2. As 2 > 1(New Required Number)2>1(NewRequiredNumber), our missing element is in this half and we don’t need to divide any further. Then, we will add the new required number to the leftmost element of this last half to obtain our missing number.

We’ll follow a recursive approach to implement the binary search. We will implement this feature like so:
1. If the array has an odd number of elements, we’ll split it at the center element. We can include the center element in either the right half or the left half in this case. If the array has an even size, we’ll split it into two equal-sized halves.
2. After splitting the array, we need to determine the total number of missing elements in the first half.
3. If our required number is greater than the total missing elements of a sub-array, we’ll call the function again and subtract the total missing elements from the required number.
4. If our required number is smaller than or equal to the total missing elements of a sub-array, we’ll then call the function with the exact same parameters.
5. Lastly, we need to return the missing number.

The following illustration might clarify this process.

![op](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/op/op9.png)
![op](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/op/op10.png)
![op](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/op/op11.png)
![op](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/op/op12.png)
![op](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/op/op13.png)

Let’s look at the code for the solution below:

{% highlight java %}
class Solution {
    public static int ResumeProcess(int[] arr, int n){
        
        class Local { 
            int getMissingID(int left, int right, int new_n) 
            { 
                if ((left + 1) == right)
                    return arr[left] + new_n;

                int middle = (left + right) / 2;

                int MissingNums = (arr[middle] - arr[left]) - (middle - left);
                if (new_n > MissingNums)
                    return getMissingID(middle, right, new_n - MissingNums);
                else
                    return getMissingID(left, middle, new_n);
            } 
        } 

        int pid = new Local().getMissingID(0, arr.length, n);
        return pid;
    }

    public static void main( String args[] ) {
        // Driver code
        
        int[] processes = {5, 7, 9, 10, 13};
        System.out.println(ResumeProcess(processes, 3));
    }
}
{% endhighlight %}

![op](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/op/op14.png)

## Feature #3: Schedule Processes

## Description
When a system is booted, the operating system needs to run a number of processes. Some processes have dependencies, which are specified using ordered pairs of the form (a, b); this means that process b must be run before process a. Some processes don’t have any dependencies, meaning they don’t have to wait for any processes to finish. Additionally, there cannot be any circular dependencies between the processes like (a, b)(b, a). In order to successfully start the system, the operating system needs to select an ordering to run the processes. The processes should be ordered in such a way that whenever a process is scheduled all of its dependencies are already met.

We’ll be provided with the total number of processes, n, and an array of process dependencies. Our task is to determine the order in which the processes should run. The processes in the dependency array will be represented by their ID’s.

Here is an illustration to better understand this:

![op](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/op/op15.png)

In this example, there are six processes, numbered 1 through 6. Here, arrows are used to represent dependencies. For example, process 3 depends on both processes 2 and 5.

## Solution
The vertices in the graph represent the processes, and the directed edge represents the dependency relationship. From the above example, we get the order: P6 ➔ P4 ➔ P1 ➔ P5 ➔ P2 ➔ P3. Another possible ordering of the above processes can be P6 ➔ P4 ➔ P5 ➔ P1 ➔ P2 ➔ P3. This order of graph vertices is known as a Topological Sorted Order.

The basic idea behind the topological sort is to provide a partial ordering of the graph’s vertices such that if there is an edge from U to V; then U ≤ V; this means U comes before V in the ordering. Here are a few of the fundamental concepts of topological sorting:
1. Source: Any vertex that has no incoming edge and has only outgoing edges is called a source.
2. Sink: Any vertex that has only incoming edges and no outgoing edge is called a sink.
3. So, we can say that a topological ordering starts with one of the sources and ends at one of the sinks.
4. A topological ordering is possible only when the graph has no directed cycles, i.e., if the graph is a Directed Acyclic Graph (DAG). If the graph has one or more cycles, no linear ordering among the vertices is possible.

To find the topological sort of a graph, we can traverse the graph in a Breadth First Search (BFS) manner. We will start with all the sources, and in a stepwise fashion, save all of the sources to a sorted list. We will then remove all of the sources and their edges from the graph. After removing the edges, we will have new sources, so we will repeat the above process until all vertices are visited.

Here is how we will implement this feature:
1. Initialization
   * We will store the graph in adjacency lists, in which each parent vertex will have a list containing all of its children. We will do this using a HashMap, where the key will be the parent vertex number and the value will be a list containing the children vertices.
   * To find the sources, we will keep a HashMap to count the in-degrees, which is the count of incoming vertices’ edges. Any vertex with a 0 in-degree will be a source.
2. Build the graph and find in-degrees of all vertices
   * We will build the graph from the input and populate the in-degrees HashMap.
3. Find all sources
   * Our sources will be all the vertices with 0 in-degrees, and we will store them in a queue.
4. Sort
   * For each source, we’ll do the following:
      * Add it to the sorted list.
      * Retrieve all of its children from the graph.
      * Decrement the in-degree of each child by 1.
      * If a child’s in-degree becomes 0, add it to the source queue.
   * Repeat step 1, until the source queue is empty.

The following illustration might clarify this process.

![op](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/op/op16.png)
![op](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/op/op17.png)
![op](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/op/op18.png)
![op](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/op/op19.png)
![op](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/op/op20.png)
![op](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/op/op21.png)
![op](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/op/op22.png)

Let’s look at the code for the solution:

{% highlight java %}
import java.util.*;

class Solution {

  public static List<Integer> scheduleProcess(int vertices, int[][] edges) {
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
      int parent = edges[i][1], child = edges[i][0];
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
      // Driver code

      int n = 4;
      int[][] dependencies =  {{1,0},{2,0},{3,1},{3,2}};
      List<Integer> result = scheduleProcess(4, dependencies);
      System.out.println("Topological Sort: " + result);
  }
}
{% endhighlight %}

![op](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/op/op23.png)

## Feature #4: Compress File

## Description
We have to come up with a compression strategy for text files that store our system’s information. Here is our strategy: whenever we see a word in a file composed as a concatenation of other smaller words in the same file, we will encode it with the smaller words’ IDs. For example, if we have the words n, cat, cats, dog, and catsndog in a text file. The word catsndog is the concatenation of the words n, cats, and dog, so we can assign it an ID. This way, instead of storing the entire catsndog word as is, we are storing an ID that takes much less space.

We’ll be provided an array of strings representing all the words from a text file. Our task will be to identify and isolate all the concatenated words.

## Solution
We’ll traverse the array of strings, and for each string, we’ll check every single combination. For example, some combinations of the word catsndog are (c, atsndog), (ca, tsndog), (cat, sndog), (cats, ndog), etc. For each combination, we get two words. We can call the first word as prefix and the second word as suffix. Now, for a combination to be considered a concatenated word, both the prefix and suffix should be present in our array of strings. We’ll first perform the check for prefix because there is no need to check the suffix if the prefix is not present, and we can move to the next combination.

If the prefix word is present in our array of strings, then we move to check the suffix word. If the suffix word is also present, we have found the concatenated word. Otherwise, there can be two possibilities:
1. The suffix word is a concatenation of two or more words. We will recursively call the same function on the suffix word to generate more (prefix, suffix) pairs until a suffix that is present in our array of strings is found.
2. There is no such suffix word present in our array of strings, and our current combination is not a concatenated word.

When we break down the first suffix word, it breaks that word down to the last letter to check it in our array of strings. After this, we move to the next combination. This breakdown and search process occurs in DFS fashion which helps us form a tree-like structure for all words.

Now, for a single string, we generate multiple combinations, and for each of those combinations, we might recursively generate all consecutive sequences of the words. There will likely be an overlap in which we’ll compute the validity of a word multiple times, and this will increase our time complexity. For example, for the combination (c, atsndog), at some point, we will have to check the validity of the suffix word combination (a, tsndog). Now, when we get a combination (ca, tsndog) from a different iteration, we will again check the word tsndog when it has already been checked. The easiest way to counter this extra computation time is to use a cache. This way, if we encounter the same word again, instead of calling an expensive DFS function, we can simply return its value from the cache. This technique is also known as memoization.

Let’s see how we might implement this functionality:
1. Initialize the array of strings to a set data structure for O(1)O(1) lookups. Additionally, initialize a HashMap to be used as a cache.
2. Traverse the array of strings provided as input and call the DFS on each word.
3. In the DFS function, compute the prefix and suffix words.
4. If the prefix is found in our set, then search for suffix. If the suffix word is not found, then recursively call DFS on the suffix word.
5. If a word’s result is not calculated, we compute it during the above steps and cache (or memoize) it.
6. Otherwise, we get the result from the cache directly.

Let’s look at the code for the solution:

{% highlight java %}
import java.util.*;
class Solution {
  public static List<String> identifyConcatenations(String[] words) {
    List<String> res = new ArrayList<>();
    // Set for O(1) lookups
    HashSet<String> wordSet = new HashSet<>(Arrays.asList(words));
    HashMap<String, Boolean> cache = new HashMap<>();

    // Process for each word
    for (String word : words) 
      if (dfs(word, wordSet, cache)) 
        res.add(word);
    return res;
  }
  
  public static boolean dfs(String word, HashSet<String> wordSet, HashMap<String, Boolean> cache) {
    // If result for current word already calculated then
    // return from cache
    if (cache.containsKey(word))
      return cache.get(word);

    // Traverse over the word to generate all combinations
    for (int i = 1; i < word.length(); i++) {
      // Divide the word into prefix and suffix
      String prefix = word.substring(0, i);
      String suffix = word.substring(i);

      if (wordSet.contains(prefix)) {
        if (wordSet.contains(suffix) || dfs(suffix, wordSet, cache)) {

          cache.put(word, true);
          return true;
        }
      }
    }
    cache.put(word, false);
    return false;
  }
  public static void main( String args[] ) {
    // Driver code

    String[] fileWords = {"n", "cat", "cats", "dog", "catsndog"};
    System.out.println("The following words will be compressed: " + identifyConcatenations(fileWords));
  }
}
{% endhighlight %}

![op](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/op/op24.png)

