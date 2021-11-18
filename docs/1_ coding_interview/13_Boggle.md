---
layout: default
title: Boggle
parent: Coding Interview
has_children: true
nav_order: 13
permalink: /coding_interview/boggle
---
<div align="center" markdown="1">
Boggle / Java resources / Tutorial

{: .fs-8 .fw-400 }
</div>

## Boggle

## Project Description for Boggle

## Introduction
Boggle is a popular word game traditionally played using a plastic grid of lettered dice. Usually, this grid is 4x4 or bigger. During the game, the players take turns finding words that can be constructed from the letters of sequentially adjacent dice. The same letter dice cannot be used more than once. Many variations of this game also exist.

## Statement
Suppose that you are working for a startup that is creating web applications of traditional board games. They have decided to create a variation of Boggle, and you are assigned to the team responsible for this task. The game can be played in single-player mode, so your team also needs to create a computer player to play against users. Additionally, the game will have multiple modes with varying levels of difficulty.

We need to create two modules that will help the computer player. The first module will be for the easy mode, where only one word needs to be found in the Boggle grid each turn. In the second module, the computer player needs to find the maximum possible words in the Boggle grid from a given set of words. The second module will be used in the difficult mode of the game.

## Features

We will need to introduce the following features to implement the functionality discussed above:
* Feature #1: For the game’s easy mode, search for a single word in the Boggle grid.
* Feature #2: For the difficult mode, find all possible words that exist in the Boggle grid from a given list of words.

In the coming lessons, we will discuss these features and their solutions in detail, so that you’ll be able to apply the solution to this scenario to different interview problems as well.

## Feature #1: Search for a Single Word in the Boggle Grid

## Description
For this project’s first feature, you are given a grid of letters, representing the Boggle grid, and a word to search inside that grid. The input is twenty-five alphabets arranged in a 5x5 grid. In this variation of the Boggle game, there are the following rules:
* Words can be constructed from the letters in sequentially adjacent cells.
* These adjacent cells can be horizontal or vertical neighbors only. Diagonally opposite dice are not considered adjacent.
* A cell can only be part of one word.

Take a look at the following illustration to better understand how to find words in the Boggle grid

![bog](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/bog/bog1.png)

In the above-mentioned example, you can see that we have a 2D grid containing twenty-five cells. Some of the words we can find on the grid are CAT, MOON, SAILOR, and COIL. In Python code, this grid will be represented by a list of lists. For the example above, the grid will be { {'C', 'S', 'L', 'I', 'M'}, {'O', 'I', 'L', 'M', 'O'}, {'O', 'L', 'I', 'E', 'O'}, {'R', 'T', 'A', 'S', 'N'}, {'S', 'I', 'T', 'A', 'C'} }. If the word you need to find is COIL, the program should return true in this case. However, if the word to find is COCOON, it should return false.

## Solution
The intuition behind this problem’s solution is a backtracking strategy with Depth First Search (DFS) exploration. For each cell on the Boggle grid, we have four paths we can take next. If the chosen path is incorrect, we will backtrack and choose a different path until the word is found or all possibilities are exhausted. We can implement the DFS algorithm using a recursive function.

The algorithm for this program will be:
* Call DFS for each cell of the grid.
* Next, check for the base case in the DFS function. The base case occurs if the word we are searching for is empty. If the word is found, we will return true.
* If the base case returns false, we will check if the current cell is valid, meaning the position of the cell is not out of bounds. Then, we will check whether the cell contains the desired suffix for the word that we are searching for (Here, the suffix means the remaining part of the word that we are searching for.)
* If the cell is valid, we will mark the cell as visited and then call the DFS recursive function for the next four possible choices.
* When the functions return, we will unmark the visited cell.

![bog](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/bog/bog2.png)
![bog](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/bog/bog3.png)
![bog](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/bog/bog4.png)
![bog](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/bog/bog5.png)
![bog](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/bog/bog6.png)
![bog](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/bog/bog7.png)
![bog](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/bog/bog8.png)

Let’s look at the code for the solution:

{% highlight java %}
class Solution {
    public static boolean exists(char[][] grid, String word){
        for(int row = 0; row < 5; row++){
            for(int col = 0; col < 5; col++){
                if(dfs(row, col, word, grid)){
                    return true;
                }
            }
        }
        return false;
    }

    public static boolean dfs(int row, int col, String suffix, char[][] grid){
        // base case
        if (suffix.length() == 0){
            return true;
        }
        // check if this is a valid cell
        if (row < 0 || row == 5 || col < 0 || col == 5 || (grid[row][col] != suffix.charAt(0))){
            return false;
        }

        boolean ret = false;
        // mark the cell as visited
        grid[row][col] = '#';
        // explore the four neighboring directions
        int[][] offsets = { {0,1}, {1, 0}, {0, -1}, {-1, 0} };
        for (int[] offset: offsets){
            int rowOffset = offset[0];
            int colOffset = offset[1];
            ret = dfs(row + rowOffset, col + colOffset, suffix.substring(1), grid);

            // break instead of return directly to do some cleanup afterwards
            if(ret){
                break;
            }
        }

        // this will revert back the original value of the cell
        grid[row][col] = suffix.charAt(0);

        return ret;
    }
    public static void main( String args[] ) {
        char[][] grid = { {'C', 'S', 'L', 'I', 'M'}, 
                        {'O', 'I', 'L', 'M', 'O'}, 
                        {'O', 'L', 'I', 'E', 'O'}, 
                        {'R', 'T', 'A', 'S', 'N'}, 
                        {'S', 'I', 'T', 'A', 'C'} };

        String word = "COIL";
        System.out.println(exists(grid, word));

        word = "COCOON";
        System.out.println(exists(grid, word));
    }
}
{% endhighlight %}

![bog](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/bog/bog9.png)

## Feature #2: Search for Maximum Number of Words in the Boggle Grid

## Description
This feature will be used in the game’s difficult mode. For this feature, we will be given a list of words. We have to implement a module that finds the maximum number of the given words that exist in the Boggle grid. The rules we discussed in the previous lesson for finding words in the Boggle board also apply here. To review, these rules are:

Words can be constructed from the letters in sequentially adjacent cells.
These adjacent cells can be horizontal or vertical neighbors only. Diagonally opposite cells are not considered adjacent.
A cell can only be part of one word on the Boggle board.
The module will take in two inputs: the grid (in the form of a 2D list of characters) and a list of possible words. Your module should return a list containing the words from the input list that were also found in the Boggle grid. Suppose, the grid is {{'B', 'S', 'L', 'I', 'M'}, {'R', 'I', 'L', 'M', 'O'}, {'O', 'L', 'I', 'E', 'O'}, {'R', 'Y', 'I', 'L', 'N'}, {'B', 'U', 'N', 'E', 'C'}}, and the words to be searched are {"BUY", "SLICK", "SLIME", "ONLINE", "NOW"}. In this case, the feature will output: {"SLIME", "ONLINE", "BUY"}. A visual representation of this example is given below:

![bog](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/bog/bog10.png)

## Solution
To solve this problem, we will again use the backtracking strategy using the DFS exploration technique. However, we can reduce the exploration space by using the trie data structure. Let’s see how this works. The input list might contain multiple words with the same prefix. Now, if we know that there is no match for a particular prefix in the grid, we can determine that all words with that prefix cannot be found in the grid. Therefore, we do not need to explore that path in DFS further, reducing the exploration space.

The algorithm to implement this feature is as follows:
* First, we will add all the query sentence’s words into the Trie. This will be used later for matching prefixes.
* Then, we will loop over all the cells in the grid and check if there are any words in the dictionary that start with the letter in the cell.
* In the dfs() recursive function, we will explore all four possible neighboring directions.
* For each call, we will check if the traversed sequence of letters matches any word in the dictionary, with the help of the nodes of Trie that we built at the beginning.

{% highlight java %}
class TrieNode
{
    TrieNode[] children;
    boolean isWord; 
    static final int ALPHABET_SIZE = 26; 
    TrieNode(){
        this.isWord = false;
        this.children = new TrieNode[ALPHABET_SIZE]; 
    }

}

class Trie {
    TrieNode root;
    Trie() {
        root = new TrieNode();
    }

    public void insert(String key) {
        TrieNode node = this.root;
        int index = 0; 

        for (int level = 0; level < key.length(); level++) {
            index = key.charAt(level) - 'A';

            if (node.children[index] == null) {
                node.children[index] = new TrieNode();
            }
            node = node.children[index];
        }
       
        node.isWord = true;
    }

    public boolean search(String key) {

        TrieNode node = this.root;
        int index = 0;

        for (int level = 0; level < key.length(); level++) {
            index = key.charAt(level) - 'A';
            if (node.children[index] == null) return false;
            node = node.children[index];
        }
        if (node.isWord) return true;

        return false;
    }
}

class Solution {
    public static String[] searchWords(char[][] grid, String[] words){

        Trie t = new Trie();
        ArrayList<String> result = new ArrayList<>();
        // Inserting words in dictionary
        for (String word: words){
            t.insert(word);
        }
        // Calling dfs for all the cells in the grid
        for(int row = 0; row < 5; row++){
            for(int col = 0; col < 5; col++){
                dfs(t.root, grid, row, col, result, new String());
            }
        }
        return result.toArray(new String[result.size()]);
    }
    public static void dfs(TrieNode node, char[][] grid, int row, int col, ArrayList<String> result, String word){
    
        // Checking if we found the word
        if(node.isWord){
            result.add(word);
            node.isWord = false;
        }

        if(0 <= row && row < 5 && 0 <= col && col < 5){
            char c = grid[row][col];
            int index = c - 'A';
            if (c != '#' && node.children[index] != null){
                TrieNode child = node.children[index];
                word += c;
                // Marking it as visited before exploration
                grid[row][col] = '#';

                int[][] offsets = { {0,1}, {1, 0}, {0, -1}, {-1, 0} };
                for (int[] offset: offsets){
                    int rowOffset = offset[0];
                    int colOffset = offset[1];
                    dfs(child, grid, row + rowOffset, col + colOffset, result, word);

                }
                // Resotoring state after exploration
                grid[row][col] = c;
            }
        }
    }
    public static void main( String args[] ) {
        char[][] grid = { {'B', 'S', 'L', 'I', 'M'}, 
        {'R', 'I', 'L', 'M', 'O'}, 
        {'O', 'L', 'I', 'E', 'O'}, 
        {'R', 'Y', 'I', 'L', 'N'}, 
        {'B', 'U', 'N', 'E', 'C'} };

        String[] words = {"BUY", "SLICK", "SLIME", "ONLINE", "NOW"};

        System.out.println(Arrays.toString(searchWords(grid, words)));
    }
}
{% endhighlight %}

![bog](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/bog/bog11.png)
