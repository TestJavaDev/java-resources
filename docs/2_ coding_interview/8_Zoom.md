---
layout: default
title: Zoom
parent: Coding Interview
has_children: true
nav_order: 8
permalink: /coding_interview/zoom
---
<div align="center" markdown="1">
Zoom / Java resources / Tutorial

{: .fs-8 .fw-400 }
</div>

## Zoom

## Project Description for Zoom

## Introduction
Zoom is a widely popular video-conferencing application. In addition to personal use by individuals, it is also used by businesses around the world to manage remote work meetings, host virtual events, and more. Zoom allows meetings to be conducted using video-only, audio-only, or both, all while conducting live chats. Moreover, it lets you record sessions to view later.

The scenario and problems we will discuss in this chapter relate to Zoom’s participant management functionality and how to implement it.

## Statement
Imagine you are working as a developer for Zoom. The team you are working for handles participant management.

First, you have to implement pagination for the meeting lobby’s “Gallery Mode,” which will display the participant names in alphabetical order. Next, you need to develop a serializer/deserializer that will serialize data before transmission through the network and deserialize it when it reaches the destination.

As teams navigate the unprecedented challenges of working from home, they regularly engage in remote fun team-building activities. At Zoom, you want to help out by integrating mini games into the application. As a pilot, you will start with one game.

## Features

We will need to introduce the following features to implement the functionalities discussed above:
* Feature #1: Implement pagination for the display showing the names of participants present in a meeting.
* Feature #2: Participant data needs to be serialized from the server to the network and de-serialized at the client.
* Feature #3: Implement an algorithm to find the correct answer of minigame that prompts the user to find the minimum number of steps taken to reach from one point to another.

The coming lessons will discuss these features and their implementation in detail. The solutions to these basic problems are also applicable to many other common coding interview questions.

## Feature #1: Display Meeting Lobby

## Description
For the first feature of the Zoom application, we need to develop a display structure for the list of participants attending a Zoom meeting. As you know, the names of attendees in a Zoom meeting are displayed in alphabetical order. However, attendees can join or leave a meeting at random, so the order has to be updated continuously. To tackle this issue, Zoom has decided to store the names of attendees in a binary search tree (BST). Additionally, we are specifically working on a meeting’s “Gallery Mode” display., where the participants’ names/videos are paginated (divided into pages that can be scrolled). In this scenario, we will assume that only ten participants can be shown on one page.

Our task is to use the binary search tree containing the names of participants and implement the pagination. Whenever our function is called, the names of the next ten participants should be returned in alphabetical order. Consider the following binary search tree, which contains the names of meeting attendees:

![zon](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/zon/zon32.png)

Assume that the above-mentioned binary search tree is provided as our feature’s input. The first time the function is called, it should return the following list: ["Albert", "Antoinette", "Anya", "Caryl", "Cassie", "Charity", "Cherlyn", "Elia", "Elvira", "Iliana"]. After the second call, it should return [ "Jeanette", "Kandice", "Lala", "Latasha", "Lyn"]. All calls after that should return [].

## Solution
We can implement this feature with the help of the in-order traversal algorithm. We will simulate an in-order traversal using a custom stack and an iterative, rather than recursive, approach. In the solution below, some helper functions are also implemented to make it modular and reusable. Let’s take a close look at the implementation of each function in the DisplayLobby class.
* constructor: This function will take the root of the BST as input and create a stack. The values of the tree will populate the stack by calling the helper function push_all() with the root of BST as a parameter.
* push_all(): This function will take a node as input. We will start traversing the tree from the node provided. The value of the current node will be pushed inside the stack, and we will jump to the left child of the current node and continue the process until the current node becomes None. This way, we will be adding the leftmost branch of the tree (rooted at the input node) into the stack. For the input node, the next smallest element in the tree will always be the leftmost element in the tree. So, for a given root node, we will follow the leftmost branch until we reach a node that doesn’t have a left child. This node will be the next smallest element.
* next_name(): This function returns the next element in stack at any moment. The stack is popped to find the next smallest element. Then, it is populated again by calling the push_all() function on the popped element’s right child, and the popped element is returned. We do this because the function returns the smallest element of the BST. Finally, it simulates recursion by moving one step forward towards the next smallest element, which is inside the right subtree of the smallest element.
* has_next(): This function lets us know if the next element exists in the stack. This is done by checking if the stack is empty or not. We use this helper function to avoid exceptions.
* next_page(): This is the function that implements pagination by returning a maximum of ten participants at a time. Inside this function, we will call the next_name() function ten times and populate the resulting array. Before calling the next_name() function, we will call the has_next() function to check if the stack is empty. If the stack is empty, we will break the loop and return the result.

The following illustration demonstrates all the algorithm’s steps:

![zon](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/zon/zon33.png)
![zon](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/zon/zon34.png)
![zon](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/zon/zon35.png)
![zon](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/zon/zon36.png)
![zon](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/zon/zon37.png)
![zon](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/zon/zon38.png)
![zon](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/zon/zon39.png)
![zon](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/zon/zon40.png)
![zon](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/zon/zon41.png)
![zon](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/zon/zon42.png)

The implementation of this algorithm is given below:

{% highlight java %}
class BinarySearchTree{
    public Node root;

    public BinarySearchTree(){
        this.root = null;
    }

    public void insert(String val){
        if(root == null)
            root = new Node(val);
        else
            this.root.insert(val);
    }
}

class Node{
    public String val;
    public Node leftChild;
    public Node rightChild;

    public Node(String val){
        this.val = val;
        this.leftChild = null;
        this.rightChild = null;
    }

    public void insert(String val){
        Node current = this;
        Node parent = null;
        while(current!= null){
            parent = current;
            if(val.compareTo(current.val) < 0)
                current = current.leftChild;
            else
                current = current.rightChild;
        }
        if(val.compareTo(parent.val) < 0)
            parent.leftChild = new Node(val);
        else
            parent.rightChild = new Node(val);
    }
}

class DisplayLobby{
    Stack<Node> stack;
    public DisplayLobby(Node root){
        this.stack = new Stack<Node>();
        this.push_all(root);
    }

    public void push_all(Node node){
        while(node != null){
            this.stack.push(node);
            node = node.leftChild;
        }
    }

    public boolean has_next(){
        return !stack.isEmpty();
    }

    public String next_name(){
        Node tmpNode = this.stack.pop();
        this.push_all(tmpNode.rightChild);
        return tmpNode.val;
    }

    public String[] next_page(){
        ArrayList<String> res = new ArrayList<>();
        for(int i = 0; i < 10; i++){
            if(this.has_next())
                res.add(this.next_name());
            else
                break;
        }
        return res.toArray(new String[res.size()]); 
    }
}
class Solution {
    public static void main( String args[] ) {
        BinarySearchTree bst = new BinarySearchTree();
        String[] names = {"Jeanette", "Latasha", "Elvira", "Caryl", "Antoinette", "Cassie", "Charity", "Lyn", "Elia", "Anya", "Albert", "Cherlyn", "Lala", "Kandice", "Iliana"};
        for(String name: names)
            bst.insert(name);

        DisplayLobby display = new DisplayLobby(bst.root);
        System.out.println(Arrays.toString(display.next_page()));
        System.out.println(Arrays.toString(display.next_page()));
        System.out.println(Arrays.toString(display.next_page()));
    }
}
{% endhighlight %}

![zon](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/zon/zon43.png)
![zon](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/zon/zon44.png)

## Feature #2: Serialize and Deserialize Participant Data

## Description
Like in the previous feature, the participant data of a Zoom session is maintained using a binary search tree. This is beneficial because the sorted order of names on the display does not change even when participants join or leave the meeting. We’ll assume that this binary search tree is maintained on both the server and client sides. However, while transmitting this information back and forth, we also want to serialize the data, send it from the server to the client, and then deserialize the data received by the client into a BST. Therefore, we need to create two modules: a serializer that deserializes the data before sending it through the network and a deserializer that translates the serialized data into its original form.

There are many ways to represent a serialized representation of a binary search tree. All that matters is that it is optimized.

Let’s look at an example of serializing a binary search tree. Suppose we are given the followin

![zon](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/zon/zon45.png)

The serializer will take the root of this BST as an input and return a string, which is the serialized form. This string can be (but is not limited to): Jeanette, Elia, Albert, Elvira, Latasha, Kandice, Maggie. Then, the deserializer will take this string as input and return the root as a BST containing all the values identical to the original BST.

## Solution
We can perform a tree traversal to efficiently serialize a BST into a string. We will be using pre-order to implement the tree traversal because it will be slightly easier and more efficient to deserialize it later. However, any other traversal can be used. Let’s take a look at the algorithm in detail:

## serialize:
* The serialize() function takes the root of the BST as input.
* An inner function called preOrder() is called on the root, which populates a list by first appending the root value. Then, it recursively calls preOrder() on the left subtree. After that, we will make a recursive call to preOrder() on the right subtree.
* A comma is appended to the list entry as a delimiter; this will be helpful later for deserializing.
* The resultant list is converted into a string using join(), and the string is returned.

## deserialize:
* The deserialize() function takes the data string as input, which represents the serialized BST.
* Using the split() function with , as the delimiter, the string is converted into a list.
* Then, we will traverse this list and create a BST by inserting data in the root node.
* Finally, the root node is returned when the traversal ends.

{% highlight java %}
class BinarySearchTree{ .. }

class Node{ ... }

class Translator{
    public String serialize(Node root){
        ArrayList<String> res = new ArrayList<>();
        preOrder(root, res);
        return String.join(",", res);
    }

    public void preOrder(Node root, ArrayList<String> res){
        if(root != null){
            res.add(root.val);
            preOrder(root.leftChild, res);
            preOrder(root.rightChild, res);
        }
    }

    public Node deserialize(String data){
        String[] lst = data.split(",");
        Stack<Node> stack = new Stack<>();
        Node root = null;
        for(String name: lst){
            if(root == null){
                root = new Node(name);
                stack.push(root);
            }
            else{
                root.insert(name);
            }
        }
        return root;
    }
}
class Solution {
    public static void main( String args[] ) {
        BinarySearchTree bst = new BinarySearchTree();
        String[] names = {"Jeanette", "Elia", "Albert", "Latasha", "Elvira", "Kandice", "Maggie"};
        for(String name: names)
            bst.insert(name);
        System.out.println("Original BST:");
        Display.printTree(bst.root);

        Translator trans = new Translator();
        String string = trans.serialize(bst.root);
        System.out.println("\nSerialized: " + string);

        Node deserialized = trans.deserialize(string);
        System.out.println("\nDeserialized:");
        Display.printTree(deserialized);
        
    }
}
{% endhighlight %}

![zon](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/zon/zon46.png)

## Feature #3: Meeting Activity

## Description
A large number of employees across the globe had to switch to working from home during the pandemic as their companies shut offices down. In this situation, Zoom is a popular collaboration tool, and the number of people using Zoom to work from home is increasing daily. Working from home has caused a lot of stress for employees and has made team building challenging for the employer. Employers have introduced several remote activities that help people relax and get to know each other. Zoom wants to play its part in this by providing fun team activities for online meetings. Zoom has decided to introduce mini games that can be played during meetings. One game they are making is a guessing game that is played on a timer. In this game, the user will be shown an image of stairs with n steps numbered from 0 to n - 1. Each step on the stair also has a number written on it. The player’s answer will be the minimum number of steps that a sprite at the bottom of the stairs needs to take to get to the top.

Your task is to implement a function that can find the correct answer given an array, k, containing the values written on the steps of the stairs. The rules of the game are the following:
* The sprite can jump from step i to step i + 1, where i + 1 < n.
* The sprite can jump from step i to step i - 1, where i - 1 >= 0.
* The sprite can jump from step i to step j, where k[i] == k[j] and i != j.

For example, consider the following mini-game and its solution:

![zon](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/zon/zon47.png)
![zon](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/zon/zon48.png)

In the example given above, four jumps are needed to reach the end. The k array for this example will be [2, 5, 7, 5, 3, 4], and your function should return 4 as output.

## Solution
This problem can be mapped as a graph problem in which we need to find the shortest path between two vertices. So, to solve this problem, we will use a breadth-first search.
* First, we will build a graph. This will be an unweighted, undirected graph, and the indices of k will represent nodes.
* There will be an edge between the nodes corresponding to the surrounding indices and also to the other indices that have the same value. We will store nodes with the same value together in a graph hash table.
* Now, we will do a breadth-first search and find all paths from the first index to the last.
* However, if we already checked one index, we do not need to check it again. We can mark the index as visited by storing it in a visited set.
* While searching, we do not need to iterate the whole list to find the nodes with the same value as the next steps, we need to consult the precomputed graph hash table. However, to prevent retracing our own steps, we need to clear the corresponding hash table entry once we reach a specific node.

{% highlight java %}
import java.util.*;
class Solution {
    public static int minSteps(int[] k) {
        int n = k.length;
        if (n <= 1) {
            return 0;
        }

        Map<Integer, List<Integer>> graph = new HashMap<>();
        for (int i = 0; i < n; i++) {
            graph.computeIfAbsent(k[i], v -> new LinkedList<>()).add(i);
        }

        List<Integer> current = new LinkedList<>(); // store current layer
        current.add(0);
        Set<Integer> visited = new HashSet<>();
        int step = 0;

        // when current layer exists
        while (!current.isEmpty()) {
            List<Integer> nextNode = new LinkedList<>();

            // iterate the layer
            for (int node : current) {
                // check if reached end
                if (node == n - 1) {
                    return step;
                }

                // check same value
                for (int child : graph.get(k[node])) {
                    if (!visited.contains(child)) {
                        visited.add(child);
                        nextNode.add(child);
                    }
                }

                // clear the list to prevent redundant search
                graph.get(k[node]).clear();

                // check neighbors
                if (node + 1 < n && !visited.contains(node + 1)) {
                    visited.add(node + 1);
                    nextNode.add(node + 1);
                }
                if (node - 1 >= 0 && !visited.contains(node - 1)) {
                    visited.add(node - 1);
                    nextNode.add(node - 1);
                }
            }

            current = nextNode;
            step++;
        }

        return -1;
    }
    public static void main( String args[] ) {
        // Driver code
        
        int[] k = {1, 2, 3, 4, 1, 3, 5, 3, 5};
        System.out.println(minSteps(k));
    }
}
{% endhighlight %}

![zon](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/zon/zon49.png)
