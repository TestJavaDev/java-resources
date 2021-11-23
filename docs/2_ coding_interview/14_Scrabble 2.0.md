---
layout: default
title: Scrabble 2.0
parent: Coding Interview
has_children: true
nav_order: 14
permalink: /coding_interview/scrabble
---
<div align="center" markdown="1">
Scrabble 2.0 / Java resources / Tutorial

{: .fs-8 .fw-400 }
</div>

## Scrabble 2.0

## Project Description for Scrabble

## Introduction
There’s no denying the fact that we live in a digital age. Everything seems to have a digital version. A gaming company has decided to transform the traditional Scrabble game. This game will only be available through a digital medium like computers, mobile, etc. The game can either be played between two human players or a human and a computer player. The game will also provide the user an option to ask the system for help if they get stuck at any point in the game.

## Statement
Evolved Scrabble has the following rules:
* To set the game up, create different groups of words of the same size.
* To start their turn, each player will select a word group.
* They will choose an initial word and a final word from that same selected word group.
* Then, the player on the other side has to convert the initial word into the final word.
   * In one move, only one letter of the word can be converted.
   * The resulting new word should also be part of the same word group.
* The player gets full points if they figure out the minimum number of character conversions to reach the final word.
* In the end, when all the lists are exhausted by each player, the player who has converted all the words in the least time will win the game.

Imagine you are a developer on this game team. Your task is to build the computer player against which humans can play. The solution for this will also be applicable if a player needs help from the system. To do this, we have to traverse over the word group that gets chosen.

## Features
We will need to introduce the following features in order to implement the above-mentioned functionality:
* Feature #1: Find the minimum number of conversions to reach the final word from the initial word.
* Feature #2: For the minimum number of conversions from Feature #1, show all possible end results for users to choose from

In the coming lessons, we will discuss how to implement these features. Again, we’ll be able to apply these solutions to other common interview problems.

## Feature #1: Minimum Moves

## Description
The first functionality we need to build will find the minimum number of conversions needed to transform the initial word into the final word. Both of these words will be of the same length.

We’ll be provided with an initial word, a final word, and a word group in the form of an array. Our code needs to pick the shortest sequence of words of the same length from the word group, starting with the initial word and ending at the final word. This sequence should be such that each consecutive word differs from the previous one in one letter only.

Here is an illustration of this process:

![bog](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/bog/bog12.png)
![bog](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/bog/bog13.png)
![bog](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/bog/bog14.png)
![bog](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/bog/bog15.png)
![bog](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/bog/bog16.png)
![bog](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/bog/bog17.png)

![bog](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/bog/bog18.png)

BFS (Breadth-First Search) is known to optimally find the shortest path in an unweighted graph. Before we can apply BFS, we need to build the graph. Additionally, we have to find adjacent nodes in which the corresponding words only differ by one letter. This requires some preprocessing steps.

![bog](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/bog/bog19.png)

Using the above example, the word let can have three intermediary states:
1. let -> _et
2. let -> l_t
3. let -> le_

The second state can be mapped to the words lot, lit, etc., because they share the same intermediary state of l_t. Hence, let can have lot and lit as neighboring or adjacent nodes.

Here is how we will implement this feature:
1. Perform the preprocessing steps for each word in our dictionary to find all its intermediary states. Then, create a dictionary statesList. Save these intermediary states as the key and the words that correspond to each state as a list of values.
2. Create a tuple containing the initial word and 0 as (initial_word, 0). The initial word will be the root node at which the BFS will begin, and our root node will always be at level 0. We need to return the level of the final node as that would be the shortest distance from the initial word. Next, push this tuple into a queue.
3. To prevent cycles, we’ll use a dictionary to maintain visited nodes.
4. We will retrieve the latest word from the queue until it’s empty. For each word, say currentWord, check the statesList dictionary and do the following:
   * Find all the word’s intermediary states.
   * For each state found in the above step, check if it is also a state for any other word present in the initial word dictionary.
5. The list of words we obtain from the above step will be the same for the currentWord. All the words on the list will be considered adjacent nodes to the currentWord and, therefore, will be added to our queue.
6. For each new word in the nodes adjacent to the currentWord, compute the tuple (word, level + 1), where level is the level of the currentWord and incrementing this by 1 introduces a new layer on which BFS will run. Append this new tuple into our queue.
7. If the final word is found, the value of level will represent the shortest conversion sequence from the initial word to the final word.

Let’s look at the code for the solution:

{% highlight java %}
class Solution {
  public static int minimumMoves(String beginWord, String endWord, List<String> wordList) {

    // Since all words are of same length.
    int L = beginWord.length();

    // Dictionary to hold combination of words that can be formed,
    // from any given word. By changing one letter at a time.
    HashMap<String, List<String>> allComboDict = new HashMap<>();

    wordList.forEach(
        word -> {
          for (int i = 0; i < L; i++) {
            // Key is the generic word
            // Value is a list of words which have the same intermediate generic word.
            String newWord = word.substring(0, i) + '*' + word.substring(i + 1, L);
            List<String> transformations = allComboDict.getOrDefault(newWord, new ArrayList<>());
            transformations.add(word);
            allComboDict.put(newWord, transformations);
          }
        });

    // Queue for BFS
    Queue<Pair<String, Integer>> Q = new LinkedList<>();
    Q.add(new Pair(beginWord, 0));

    // Visited to make sure we don't repeat processing same word.
    HashMap<String, Boolean> visited = new HashMap<>();
    visited.put(beginWord, true);

    while (!Q.isEmpty()) {
      Pair<String, Integer> node = Q.remove();
      String word = node.getKey();
      int level = node.getValue();
      for (int i = 0; i < L; i++) {

        // Intermediate words for current word
        String newWord = word.substring(0, i) + '*' + word.substring(i + 1, L);

        // Next states are all the words which share the same intermediate state.
        for (String adjacentWord : allComboDict.getOrDefault(newWord, new ArrayList<>())) {
          // If at any point if we find what we are looking for
          // i.e. the end word - we can return with the answer.
          if (adjacentWord.equals(endWord)) {
            return level + 1;
          }
          // Otherwise, add it to the BFS Queue. Also mark it visited
          if (!visited.containsKey(adjacentWord)) {
            visited.put(adjacentWord, true);
            Q.add(new Pair(adjacentWord, level + 1));
          }
        }
      }
    }

    return 0;
  }

  public static void main(String[] args){
    // Driver code

    String initialWord = "hit";
    String finalWord = "cog";
    List<String> wordGroup = Arrays.asList("hot","dot","dog","lot","log","cog");

    System.out.print("The shortest sequece is of length: " + minimumMoves(initialWord, finalWord, wordGroup));
    
  }
}
{% endhighlight %}

![bog](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/bog/bog20.png)
![bog](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/bog/bog21.png)

## Feature #2: Possible Results

## Description
In the previous lesson, we built a feature that will calculate the minimum number of conversions from the initial to the final word. Now, we need to fetch and display each new word after each conversion until we reach our end result. We’ll traverse the array and return the complete sequence of words after each conversion from start to end.

Here is an illustration of this process:

![bog](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/bog/bog22.png)

## Solution
The previous feature involved finding the shortest path from a start node to an end node, but to solve this problem, we have to find all the possible paths from the start node to the end node.

We can use BFS to find the target word’s node from the initial node as we did for the previous feature. However, we can’t maintain the path from the start to the end node because BFS does a level order traversal. To get the paths, we can deploy a DFS (Depth First Search) algorithm, but since we are traversing a graph and not a tree, there will exist cycles. Many of the paths will not lead to the target word node, and the process will be extremely time-consuming.

In light of these observations, we can use the properties of both the BFS and DFS algorithms to build this feature. We will use BFS to construct the paths and DFS to find the shortest path.

Here is how we will implement this feature:
1. First, we’ll apply the BFS algorithm to find the correct word node by doing a level order traversal.
2. Next, we’ll replace each character in every word with one of the 26 English alphabets one at a time to check if that new word exists in our word_dict. If it exists, we can add that word to the next layer to be visited. At each level, we can ignore the non-visited nodes.
3. While implementing the BFS, we’ll create a directed subgraph on which we’ll later perform the DFS. In this subgraph, each node in layer i+1 points to the connected nodes in layer i.
4. During DFS traversal, if a node is equal to the target node, we can backtrace our steps to the initial node. This backtracking will give us the shortest path we were looking for.
5. Finally, we’ll apply DFS starting from end and using the sub-graph above. All the shortest paths will be generated.

In BFS traversal, we will not use the Queue structure like in the previous lesson. We need to collect all the connections between two layers, so the set structure will be suitable here.

![bog](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/bog/bog23.png)

Let’s look at the code for the solution:

{% highlight java %}
class Solution {
    public static ArrayList<String[]> dfs(String w, String endWord, HashMap<String, HashSet<String>>graph, ArrayList<String> path){
        ArrayList<String[]> ans = new ArrayList<>();
        if(w.equals(endWord)){
            ans.add(path.toArray(new String[path.size()]));
        }
        else{
            Iterator<String> it = graph.get(w).iterator();
            while(it.hasNext()){
                String nw = it.next();
                path.add(nw);
                ans.addAll(dfs(nw, endWord, graph, path));
                path.remove(path.size() - 1);
            }
        }
        return ans;
    }

    public static String[][] possibleResults(String beginWord, String endWord, String[] wordList){
        ArrayList<String[]> res = new ArrayList<>();
        if(beginWord == endWord){
            res.add(new String[]{beginWord});
            return res.toArray(new String[res.size()][]);
        }
        
        HashMap<String, HashSet<String>>graph = new HashMap<>();
        String helper = "qwertyuiopasdfghjklzxcvbnm";
        HashSet<String> dicSet = new HashSet<>(Arrays.asList(wordList));
        
        HashSet<String>layer = new HashSet<>();
        layer.add(beginWord);
        dicSet.remove(beginWord);
        
        boolean stop = false;
        while(layer.size() > 0 && !stop){
            HashSet<String> newLayer = new HashSet<>();
            Iterator<String> it = layer.iterator();
            while(it.hasNext()){
                String w = it.next();
                // construct next word, O(len(word) * 26)
                for(int i = 0; i < w.length() ; i++){
                    for(Character c : helper.toCharArray()){
                        String nw = w.substring(0, i) + c + w.substring(i+1);
                        
                        if(dicSet.contains(nw)){
                            newLayer.add(nw);
                            if(graph.get(w) == null){
                                graph.put(w, new HashSet<>());
                            }
                            graph.get(w).add(nw);
                        }   
                        // if we find endWord in this layer, there is no need to do next layer
                        if(nw == endWord)
                            stop = true;
                    }
                }
            }
            // removing unecessary nodes
            dicSet.removeAll(newLayer);
            layer = newLayer;
        }
            
                
        
        ArrayList<String> path = new ArrayList<>();
        path.add(beginWord);
        res = dfs(beginWord, endWord, graph, path);
        return res.toArray(new String[res.size()][]);
    }

    public static void main( String args[] ) {
        // Driver Code
        String initialWord = "hit";
        String finalWord = "cog";
        String[] wordGroup = {"hot","dot","dog","lot","log","cog","lit"};
        String[][] res = possibleResults(initialWord, finalWord, wordGroup);
        System.out.println("All minimum sequences are:\n" + Arrays.deepToString(res));
    }
}
{% endhighlight %}

![bog](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/bog/bog24.png)
![bog](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/bog/bog25.png)

