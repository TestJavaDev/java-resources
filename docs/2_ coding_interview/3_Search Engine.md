---
layout: default
title: Search Engine
parent: Coding Interview
has_children: true
nav_order: 3
permalink: /coding_interview/search
---
<div align="center" markdown="1">
Search Engine / Java resources / Tutorial

{: .fs-8 .fw-400 }
</div>

## Search Engine

## Project Description for Search Engine

## Introduction
A search engine is a software that lets users search on the web. Search engines use a database of web pages that they collect using bots. The user’s query is run on the database, and the results are fetched. Some of the most commonly used search engines are Google, Bing, Baidu, Yahoo!, Duckduckgo, etc. All of these search engines contain complex, underlying algorithms for optimized searching and web page ranking for search results.

The scenarios and problems discussed in this chapter also relate to any search engine’s word searching, storage handling, and document fetching functionalities.

## Statement
For this project, imagine you are developing a search engine at a new startup. This startup is experimenting with new and improved algorithms to carry out word searches in documents.

The first order of business is designing and implementing a system for efficient storage and retrieval of words from the index. The UI team is requesting an auto-complete functionality. Your users are familiar with the auto-complete functionality offered by currently popular search engines. This functionality suggests keywords as the user types the search string. It makes it faster and more convenient for a user to search the web. Moreover, your system should contain a module that checks if the query can be broken into multiple valid words, which is helpful in case the original query does not get any search results. In addition, we will also implement some features related to search ranking, result organization and optimization.

## Features

We will need to introduce the following features to implement the functionalities we mentioned above:
* Feature #1: Design a system that can store and fetch words efficiently. This can be used to store web pages to make searching easier.
* Feature #2: Implement the auto-complete functionality to apply when the user is entering a query. For this feature, you will be recommending auto-completion using a set of popular, already-available queries.
* Feature #3: Check if white-spaces can be added to a query to create valid words in case the original query does not get any hits on the web.
* Feature #4: As an extension of the previous feature, find all the possible queries that can be created by adding white spaces to the original query.
* Feature #5: Calculate a search ranking factor based on the ranking score of pages that refer to it.
* Feature #6: Rearrange the search results such that results from the same website do not show up together.
* Feature #7: Search engine has many services that are chained or recursive. For optimization efforts, calculate the individual time taken by each service to run.

Understanding these feature requests and designing their solutions will help us implement the requested functionality into the search engine’s system. The coming lessons will discuss these features and their implementations in detail so that you will be able to apply these solutions to different interview problems as well.

## Feature #1: Store and Fetch Words

## Description
For the first feature, your company wants you to design a module for the search engine that can be used to store and fetch words efficiently. This module will act as a dictionary with insert and search functionalities. Moreover, this dictionary should also have a feature for searching whether a given prefix exists in the dictionary or not. This feature can be represented by the startsWith function because a prefix comes at the beginning of the word.

Let’s say we insert the following words in the dictionary: the, a, there, answer, any, by, bye, their, and abc by calling the insertWord() function. Then, by calling the searchWord() function with input, there should return True. Similarly, calling the startsWith() function with the prefix by should also return True.

## Solution
To implement this dictionary with efficient lookup times, we will use a trie data structure. Maybe you had already come to this conclusion, or maybe you were considering using a hash table instead. However, we will not use a hash table for this particular scenario is because it would be very inefficient for the prefix searching. Additionally, scaling hashtables for large datasets also increases collisions and space complexity. On the contrary, a trie is efficient in both time and space.

Briefly, a trie is a tree of characters. The tree takes a word as a parameter and creates a new node for each character of that word. The node registered for the last character of the word is marked as the end of the word, using a Boolean variable.

To implement the WordDictionary class, we will do the following:
* Constructor: We will initialize the root node of the tree in the constructor. This node will be of type Node. The Node class contains a dictionary of nodes and the Boolean isWord, which determines if the character is at the end of a word or not.
* insertWord() function: In this function, we will take in a word as input. Starting from the root node, we will add the word’s characters to the children dictionary of each character as nested dictionaries. We will check if the child node with the character is present or not at each step. If it’s not present, a new node is initialized. For the last character of the word, we also set the isWord to True for the corresponding node.

![sear](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/sear/sear1.png)
![sear](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/sear/sear2.png)
![sear](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/sear/sear3.png)
![sear](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/sear/sear4.png)
![sear](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/sear/sear5.png)
![sear](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/sear/sear6.png)
![sear](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/sear/sear7.png)

* searchWord() function: In this function, we begin checking from the root node to see if the first character exists in children. If it exists, we move on to that node and check its children for the next character. If at any point the node corresponding to a character is not found, we return False. If the whole word is found but isWord is not set to True for the last node, we return False as well. True is only returned if all the characters match and the word also ends at that point.

![sear](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/sear/sear8.png)
![sear](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/sear/sear9.png)
![sear](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/sear/sear10.png)
![sear](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/sear/sear11.png)
![sear](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/sear/sear12.png)
![sear](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/sear/sear13.png)
![sear](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/sear/sear14.png)

* startsWith() function: This function is mostly the same as the searchWord function. The only exception is that we do not check if isWord is also set to True in the last-found node because we are not looking for a complete word, a prefix is enough. In the above trie, for instance, startsWith("th") should return true.

Let’s look at the code for the solution below:

{% highlight java %}
class Node {
    public HashMap<Character, Node> children;
    public boolean isWord;

    public Node(){
        this.children = new HashMap<Character, Node>();
        this.isWord = false;
    }
}

class WordDictionary {
    private Node root;
    public WordDictionary(){
        this.root = new Node();
    }
    
    public void insertWord(String word){
        Node node = this.root;
        for (Character c:  word.toCharArray()){
            if (!node.children.containsKey(c))
                node.children.put(c, new Node());
            node = node.children.get(c);
        }
        node.isWord = true;
    }

    public boolean searchWord(String word){
        Node node = this.root;
        for (Character c:  word.toCharArray()){
            if (!node.children.containsKey(c))
                return false;
            node = node.children.get(c);
        }
        return node.isWord;
    }
}
class Solution {
    public static void main( String args[] ) {
        System.out.println( "Hello World!" );
        String[] keys = {"the", "a", "there", "answer", "any",
        "by", "bye", "their", "abc"};
        System.out.println("Keys to insert: ");
        System.out.println(Arrays.toString(keys));

        WordDictionary d = new WordDictionary();

        for(int i=0; i < keys.length; i++)
            d.insertWord(keys[i]);
        
        System.out.println("Searching 'there' in the dictionary results: " + d.searchWord("there"));
    }
}
{% endhighlight %}

![sear](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/sear/sear15.png)

## Feature #2: Design Search Autocomplete System

## Description
The second feature we want to implement is the auto-complete query. This is the feature that prompts the search engine to give you some suggestions to complete your query when you start typing something in the search bar. These suggestions are given based on common queries that users have searched already that match the prefix you have typed. Moreover, these suggestions are ranked based on how popular each query is.

Assume the search engine has the following history of queries: {"beautiful", "best quotes", "best friend", "best birthday wishes", "instagram", "internet"}. Additionally, you have access to the number of times each query was searched. The following list shows the number each query string occurred, respectively: {30, 14, 21, 10, 10, 15}. Given these parameters, we want to implement an autoComplete() function that takes in an incomplete query a user is typing and recommends the top three queries that match the prefix and are most popular.

The system should consider the inputs of the autoComplete() function as a continuous stream. For example, if the autoComplete("be") is called, and then the autoComplete("st") is called, the complete input at that moment will be "best". The input stream will end when a specific delimiter is passed. In our case, the delimiter is "#", and, autoComplete("#") will be called. This marks the end of the query string. At this point, your system should store this input string in the record, or if it already exists, it should increase its number of instances.

Suppose, the current user has typed "be" in the search bar; this will be the input for the autoComplete() function, meaning autoComplete("be") will be called. It will return {'beautiful', 'best friend', 'best quotes'} because these queries match the prefix and are the most popular. The order of queries in the output list is determined by popularity. Then, the user adds "st" to the query, making the string "best", and the autoComplete("st") will be called. Now, the output should be {'best friend', 'best quotes', 'best birthday wishes'}. Lastly, the user finishes the query, so the autoComplete("#") will be called. It will output [] and "best" will be added in the record to be used in future suggestions.

![sear](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/sear/sear16.png)
![sear](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/sear/sear17.png)
![sear](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/sear/sear18.png)
![sear](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/sear/sear19.png)
![sear](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/sear/sear20.png)
![sear](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/sear/sear21.png)

## Solution
To design this system, we will again use the trie data structure. Instead of simply storing the words in the prefix tree, as we did in the WordDictionary, we will now store the query strings. The AutocompleteSystem class will act as a trie that keeps a record of the previous queries and assigns them a rank based on their number of occurrences.

We will implement the AutocompleteSystem class as follows:
* Constructor: In the constructor, we will feed the historical data into the system and create a trie out of it. We will initialize the root node of trie and call the addRecord() function to add all the records.
* addRecord() function: This function inserts records in the trie by creating new nodes. Its functionality is similar to the insertWord() function that we discussed in Feature #1: Store and Fetch Words. Each node of the trie will have:
   * A children dictionary
   * A Boolean called isEnd to set the end of the query sentence
   * A new variable called data that is optional, but we can use it to store the whole query sentence in the last character of the sentence. This will increase space complexity but can make computation easier.
   * A rank variable to store the number of occurrences

* In the code below, you will notice that we are storing the rank as a negative value. There is a valid reason for doing this unintuitive step. Later, you will see that we will be using the sorted() method to obtain the top three results, and this negative rank will play a significant role. This will be explained in more detail in the explanation for the autoComplete() function.
* search() function: This function checks to see if the first character exists in its children beginning with the root node. If it exists, we move on to the node with the first character and check its children for the next character. If the node corresponding to a character is not found, we return []. If the search string is found, the dfs() helper function is called on the node with the last character of the input query.
* dfs() function: This function is the helper function that returns all the possible queries in the record that match the input. First, it will check if the node has isEnd set to True; if it does, the node’s rank and data will be appended as a tuple in an output list ret. Then, DFS exploration will be performed on all children nodes. All the possible queries will be added in ret and returned at the end.
* autoComplete() function: This function checks if the input string is not the end of string delimiter "#". If it is not the end of the input string, we append the value to the keyword member variable. Then, we call the search() function, which returns the list of tuples as discussed above. On the other hand, if the input string is the end of the input, we add the value present in keyword to the trie by calling addRecord(). Next, the value of the keyword variable is reset to an empty string. Before returning, you can see that we do some computation on the result list. The list that we received from the search() function was a list of tuples with rank and sentence as elements. We will sort the array in ascending order using the sorted() function and fetch the first three elements of the sorted list. From this list of three tuples, we will create a list containing only the second element of each tuple, meaning only the sentences. Finally, we return it. If we had used the actual positive value for rank, we would have needed to sort ascending for sentence and descending for rank. So, by making rank negative, we can easily sort the array in ascending using the default configuration in the sorted() function.

{% highlight java %}
class Node implements Comparable<Node>{
    public HashMap<Character, Node> children;
    public boolean isEnd;
    public String data;
    int rank;
    public List<Node> hot;

    public Node(){
        this.children = new HashMap<Character, Node>();
        this.isEnd = false;
        this.rank = 0;
        hot = new ArrayList<>();
    }

    public int compareTo(Node n){
        if(this.rank == n.rank)
            return this.data.compareTo(n.data);
        return n.rank - this.rank;
    }

    public void update(Node n){
        if(!this.hot.contains(n)){
            this.hot.add(n);
        }
        Collections.sort(hot);
        if (hot.size() > 3) {
            hot.remove(hot.size() - 1);
        }
    }
}

class AutocompleteSystem{

    private Node root;
    private Node current;
    private String keyword;


    public AutocompleteSystem(String[] sentences, int[] times){
        this.root = new Node();
        this.current = root;
        this.keyword = "";

        for (int i = 0; i < sentences.length; i++){
            this.addRecord(sentences[i], times[i]);
        }
    }
    
    public void addRecord(String sentence, int t){
        Node node = this.root;
        List<Node> visited = new ArrayList<>();
        for (Character c:  sentence.toCharArray()){
            if (!node.children.containsKey(c))
                node.children.put(c, new Node());
            node = node.children.get(c);
            visited.add(node);
        }
        node.isEnd = true;
        node.data = sentence;
        node.rank += t;

        for (Node i: visited){
            i.update(node);
        }
    }

    public String[] autoComplete(char c){
        List<String> res = new ArrayList<>();
        if (c == '#') {
            addRecord(keyword, 1);
            keyword = "";
            current = root;
            return new String[]{};
        }
        
        this.keyword += c;
        if (current != null) {
            if (!current.children.containsKey(c))
                return new String[]{};
            else
                current = current.children.get(c);
        }
        else
            return new String[]{};

        for (Node node : current.hot) {
            res.add(node.data);
        }
        return res.toArray(new String[res.size()]);
    }
}
class Solution {
    public static void main( String args[] ) {
        String[] sentences = {"beautiful", "best quotes", "best friend", "best birthday wishes", "instagram", "internet"};
        int[] times = {30, 14, 21, 10, 10, 15};
        AutocompleteSystem auto = new AutocompleteSystem(sentences, times);
        System.out.println(Arrays.toString(auto.autoComplete('b')));
        System.out.println(Arrays.toString(auto.autoComplete('e')));
        System.out.println(Arrays.toString(auto.autoComplete('s')));
        System.out.println(Arrays.toString(auto.autoComplete('t')));
        System.out.println(Arrays.toString(auto.autoComplete('#')));
    }
}
{% endhighlight %}

![sear](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/sear/sear22.png)

## Feature #3: Add White Spaces to Create Words

## Description
While searching on the web, we know that users make many spelling errors. One error is combining multiple words. To tackle this issue, your team has decided to create a module that adds white spaces in the query to see if valid words can be created by breaking the original query. This module will be triggered if the original query gives very few results or no results at all. You are not concerned with implementing the triggering function; you only have to implement the breakQuery functionality, which receives the current query and a list of all possible valid words.

Let’s consider a case where you are given the query "vegancookbook". This query didn’t get any web hits, so now it is sent to the break_query function to check if it’s possible to add white spaces to this query to create valid words. You are also given a dictionary containing all possible words. For this problem, we will assume that the only possible words are {"i", "cream", "cook", "scream", "ice", "cat", "book", "icecream", "vegan"}. Your function should use this list of strings to determine if the original query can be broken down into words provided in the dictionary. Then, the break_query function should return a Boolean value depending on whether it is possible to break down the query or not. In the example we just discussed, the function will return True because we can add spaces in the "vegancookbook" to produce "vegan cook book", which contains words from the dictionary.

## Solution
This problem can be solved using the dynamic programming technique. The idea behind this approach is that the given problem pp can be divided into subproblems p1p1 and p2p2. If these subproblems satisfy the required conditions individually, the complete problem also satisfies the conditions. This means that the string "vegancookbook" can be split into the substrings: "vegan" and "cookbook". The substring "vegan" is a word found in the dictionary, meaning the condition is satisfied. Now, let’s consider the other substring, "cookbook", this can be divided further into "cook" and "book". These strings can also be found as words in the dictionary, meaning this part of the problem also satisfies the given condition. Hence, we can say that the input string "vegancookbook", as a whole, satisfies the condition.

The complete algorithm is given below:

![sear](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/sear/sear23.png)

{% highlight java %}
class Solution {
    public static boolean breakQuery(String query, String[] dict){
        Set<String> dictSet = new HashSet<>(Arrays.asList(dict));
        boolean[] dp = new boolean[query.length() + 1];
        dp[0] = true;
        for (int i = 1; i <= query.length(); i++) {
            for (int j = 0; j < i; j++) {
                if (dp[j] && dictSet.contains(query.substring(j, i))) {
                    dp[i] = true;
                }
            }
        }
        return dp[query.length()];
    }
    public static void main( String args[] ) {
        String query = "vegancookbook";
        String[] dict = {"i", "cream", "cook", "scream", "ice", "cat", "book", "icecream", "vegan"};
        System.out.println(breakQuery(query, dict));

        query = "veganicetea";
        System.out.println(breakQuery(query, dict));
    }
}
{% endhighlight %}

![sear](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/sear/sear24.png)

## Feature #4: Suggest Possible Queries After Adding White Spaces

## Description
This feature is an extension of the one we programmed in the previous lesson. Like the last feature, we are given a user query that doesn’t provide a significant number of web hits. Therefore, we have decided to break down the query by adding white spaces to see if valid words can be created by breaking the original query. However, this time the difference is that you are tasked with finding a list of all the possible valid queries created by adding white spaces in the original query.

Let’s suppose the user searches "vegancookbook". This query didn’t get any web hits, so it is sent to the break_query function to check if it’s possible to add white spaces to create valid words. You are also given a dictionary containing all the possible words. In this problem, we will assume that the only possible words are {"an", "book", "car", "cat", "cook", "cookbook", "crash", "cream", "high", "highway", "i", "ice", "icecream", "low", "scream", "veg", "vegan", "way"}. Your function should use this list of strings to determine if the original query can be broken down into words provided in the dictionary. Then, the break_query function should return a list of strings that can be created by breaking down the query into the words present in the dictionary. In the example we just discussed, the function will return {'vegan cook book', 'vegan cookbook', 'veg an cook book', 'veg an cookbook'}. Similarly, for the query string "highwaycarcrash" and the same word dictionary, the function should return {"high way car crash", "highway car crash"}

## Solution
This problem can also be solved using a dynamic programming (DP) technique. We will be using top-down dynamic programming, which is more efficient, even though other variations of DP can also be used. Let’s take a look at the intuition behind this solution.

![sear](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/sear/sear25.png)

![sear](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/sear/sear26.png)

Here is the complete algorithm for the implementation:
* The breakQuery() function takes in the query string and the list of words called dict. This function then calls a recursive helper function.
* The recursive function takes in the query string. The dict is converted into a set before sending to the function (lookup in sets is linear), and an empty hashmap is also sent. Later, we will use this hashmap to store results for each substring.
* The helper function’s base case is when the query is empty; this returns an empty list. Note that it is actually an empty list of lists because that is the return type of this function.
* In the recursive function, we run an iteration over all the prefixes of the query. If the corresponding prefix happens to match a word in the set, we recursively invoke the function on the postfix.
* At the end of the iteration, we store the results in the list called res with each valid postfix string as the key and the list of words that compose the prefix as the value. For instance, for the postfix cookbook, the corresponding set entry would be [“cook”, “book”].
* At last, we return the value from result that corresponds to the query string as the key.

{% highlight java %}
class Solution {
    public static String[]breakQuery(String query, String[] dict) {
        Set<String> dictSet = new HashSet<>(Arrays.asList(dict));
        List<String> res = helper(query, dictSet, new HashMap<String, LinkedList<String>>());
        return res.toArray(new String[res.size()]);
    }       

    // helper function returns an array including all substrings derived from s.
    public static List<String> helper(String s, Set<String> dictSet, HashMap<String, LinkedList<String>>map) {
        if (map.containsKey(s)) 
            return map.get(s);
            
        LinkedList<String>res = new LinkedList<String>();     
        if (s.length() == 0) {
            res.add("");
            return res;
        }               
        for (String word : dictSet) {
            if (s.startsWith(word)) {
                List<String>sublist = helper(s.substring(word.length()), dictSet, map);
                for (String sub : sublist) 
                    res.add(word + (sub.isEmpty() ? "" : " ") + sub);               
            }
        }       
        map.put(s, res);
        return res;
    }
    public static void main( String args[] ) {
        String query = "vegancookbook";
        String[] dict = {"an", "book", "car", "cat", "cook", "cookbook", "crash", 
                "cream", "high", "highway", "i", "ice", "icecream", "low", 
                "scream", "veg", "vegan", "way"};
        
        System.out.println(Arrays.toString(breakQuery(query, dict)));
        query = "highwaycarcrash";
        System.out.println(Arrays.toString(breakQuery(query, dict)));
    }
}
{% endhighlight %}

![sear](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/sear/sear27.png)

## Feature #5: Calculate the Search Ranking Factor

## Description
Consider that your company has decided to experiment with a different search ranking algorithm. This algorithm favors search results that reference each other and create a closed graph. All the web pages in the search result have already been assigned scores based on their content quality and relevance. Now, we want to determine the ranking factor of each page, which will be used in tandem with other criteria to determine the final page rank. To find this ranking factor, the team has decided to take the product of the scores of all pages that are referenced by the current page. This means that in the set of web pages where each one references the other, the ranking factor of each page will be determined by multiplying the scores of all the other pages in the set except itself.

To implement this feature, you will be provided with an array containing the page scores of web pages that reference each other. A page’s rank is calculated as the product of the scores of all the pages that link to it. For example, you are given the following scores of five web pages that link to each other: {1, 4, 6, 9}. The ranking factor found by the algorithm mentioned above will be: {216, 54, 36, 24}.

![sear](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/sear/sear28.png)

## Solution
The optimal approach for solving this problem is that for every index, i, we will evaluate the product of all the numbers to the left and all the numbers to the right of i. Then, we will multiply those two individual products. This will give us the product of all the numbers except the one at the index, i.

The complete algorithm is given below:
* First, let’s start by calculating the product of all the elements to the left for each index.
* We will use a ranking array and start populating it with the product of the elements to the left. The product of the elements to the left for index 0 will be 1 because there are no elements to the left.
* Then, we will traverse the page scores from index 1. For each ranking[i], we will find the product of elements to the left by multiplying pageScores[i - 1] and ranking[i - 1].
* We have the product of elements to the left for each index stored in ranking. Now, we need to do the same for the right side and multiply both. We can use another array to do this. However, we will prioritize saving space and use a constant variable, right, to store the product.
* Initialize this variable with 1, and start traversing the list from the end.
* We will multiply right with ranking[i] to find the final ranking for the page at i. The right variable will also get updated at each iteration by multiplying it with pageScores[i].
* Finally, we can find the required page ranking factors in the resultant ranking list.

![sear](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/sear/sear29.png)
![sear](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/sear/sear30.png)
![sear](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/sear/sear31.png)
![sear](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/sear/sear32.png)
![sear](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/sear/sear33.png)
![sear](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/sear/sear34.png)
![sear](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/sear/sear35.png)
![sear](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/sear/sear36.png)
![sear](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/sear/sear37.png)
![sear](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/sear/sear38.png)
![sear](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/sear/sear39.png)
![sear](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/sear/sear40.png)
![sear](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/sear/sear41.png)
![sear](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/sear/sear42.png)

{% highlight java %}
class Solution {
    public static int[] searchRanking(int[] pageScores) {
        int length = pageScores.length;
        int[] ranking = new int[pageScores.length];
        ranking[0] = 1;
        for(int i = 1; i < length; i++){
            ranking[i] = pageScores[i - 1] * ranking[i - 1];
        }
        
        int right = 1;
        for(int i = length - 1; i >= 0; i--){
            ranking[i] = ranking[i] * right;
            right *= pageScores[i];
        }
        return ranking;
    }

    public static void main( String args[] ){
        int[] pageScores = {3, 5, 1, 1, 6, 7, 2, 3, 4, 1, 2};
        System.out.println(Arrays.toString(searchRanking(pageScores)));
    }
}
{% endhighlight %}

![sear](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/sear/sear43.png)

## Feature #6: Reorganizing Search Results

## Description
For this search engine feature, we are given all the search results to display on one page. Each page shows a maximum of twenty-five search results at a time. Multiple pages in the search results can belong to the same domain. However, the team has decided that we do not want adjacent results to be from the same domain because they are likely to be similar and might favor only one site. To give our users a wide range of results, we want to rearrange the results such that two results from the same domain are not consecutive.

![sear](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/sear/sear44.png)

Suppose, we denote each domain with a character. There can only be twenty-five results on a page, so the maximum number of simultaneous domains in the search results will also be 25. Thus, denoting them with a character will be simple. Now, you are given a string that represents the initial order of the search results. Your job is to reorganize this string so adjacent characters are not identical. For example, if the input string is bbnnc then the output should be bnbnc or any other reordering of characters such that it fulfills the conditions. If this is not possible, we will just show the original order of results.

## Solution
The optimal way to solve this question to use the greedy technique using the heap data structure. If we build the resultant order from the most common letter followed by the second most common letter and keep following this trend, we are likely to get the needed result. If this fails, it means that it was not possible to rearrange the string. The condition for failing occurs when the frequency of a character exceeds (n+1) / 2.

The complete algorithm is given below:
* First, we will find the frequency of the most frequent character in the input string.
* If the most frequent character in the string has the frequency max_freq, for a valid rearrangement of the string, the remaining characters should be at least max_freq - 1. We will verify this case. We can use the HashMap class in Java. We will simply return the initial string if this test fails.
* Now, we will use a StringBuilder called result to store the rearrangement of the characters.
* We will be using a max heap to store the frequencies of the characters. We can use the PriorityQueue data structure in Java to simulate a max heap. We will add (char, freq) tuples to a heap.
* Next, we will remove the most frequent element. If that element is not the last element in the result, we add it to the result.
* If it is the last element of the result, we pick the second most frequent element and add that to the result. We also add the most frequent element back to the heap.
* When we pop from the heap and append it to the result, we need to add it back to the heap if the frequency is not 0.
* In the end, we will convert the result into a string and return it.

{% highlight java %}
class Solution {
    public static String reorganizeResults(String initialOrder) {
        
        Map<Character, Integer> map = new HashMap<>();
        for (char c : initialOrder.toCharArray()) {
            int freq = map.getOrDefault(c, 0) + 1;
            if (freq > (initialOrder.length() + 1) / 2) 
                return initialOrder;
            map.put(c, freq);
        }
        
        PriorityQueue<int[]> pq = new PriorityQueue<>((a, b) -> b[1] - a[1]);
        for (char c : map.keySet()) {
            pq.add(new int[] {c, map.get(c)});
        }
       
        StringBuilder result = new StringBuilder();
        while (!pq.isEmpty()) {
            int[] first = pq.poll();
            if (result.length() == 0 || first[0] != result.charAt(result.length() - 1)) {
                result.append((char) first[0]);
                if (--first[1] > 0) {
                    pq.add(first);
                }
            } else {
                int[] second = pq.poll();
                result.append((char) second[0]);
                if (--second[1] > 0) {
                    pq.add(second);
                }
                pq.add(first);
            }
        }
        return result.toString();
    }

    public static void main(String args[]){
        String initialOrder = "bbbnnc";
        System.out.println(reorganizeResults(initialOrder));
    }
}
{% endhighlight %}

![sear](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/sear/sear45.png)

## Feature #7: Find Searching Time

## Description
A typical search engine consists of many services, such as crawling, indexing, word stemming, synonym fetching, etc. When a user’s search query arrives at a web front end, it is dispatched to the above-mentioned search-related services. A single search query turns into a large number of calls to these services. Some of these calls are recursive, too. For instance, the stemming service may stem one or more words from the search query before invoking itself recursively on the rest of the search string.

Optimization is an ongoing effort and search engines keep trying to reduce the time it takes for the search results to be displayed on the user’s screen. To better guide this optimization activity, we instrumented code to achieve some statistics. Using these statistics, we want to figure out the time spent in each of the search-related services over a specific time window.

To find the time spent by each service, we will use log messages. Each service is identified in the logs by a service_id, and the logs contain the start and end timestamps of each invocation of the service. The logs will be stored in a list of strings, where each string will have the following format: "{service_id}:{"start" | "end"}:{timestamp}".

Below is an illustration of this format:

![sear](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/sear/sear46.png)

## Solution
Once we encounter a particular function’s start message, we will calculate the time spent in all the subsequent nested calls until we encounter the end message for the first function. This can be done using the stack data structure. We can also subtract the difference of the end time and the nested function execution time from the start time to determine the running time of the first function.

Here is how the implementation will take place:
1. Initialize the servTimes list with 0’s.
2. Start traversing over the list of strings. Retrieve the ID of the first service, push it on the stack, and store its time in the time variable.
3. If the next service in line has a start state, add its time to servTimes[i] and subtract the time variable.
4. If the service next in line has an end state, add its time to servTimes[i], subtract the time variable, and add 1 because the service will run until the end of its specified time.
5. Repeat steps 2 and 3 until all the services in the list have been executed.
6. Return the sum of the servTimes list.

![sear](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/sear/sear47.png)
![sear](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/sear/sear48.png)
![sear](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/sear/sear49.png)
![sear](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/sear/sear50.png)
![sear](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/sear/sear51.png)
![sear](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/sear/sear52.png)
![sear](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/sear/sear53.png)
![sear](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/sear/sear54.png)

Let’s look at the code for the solution below:

{% highlight java %}
class Solution {
    public static int[] serviceTime(int n, String[] logs){
        Stack<Integer> stack = new Stack<Integer>();
        int[] servTimes = new int[n];
        String[] func = logs[0].split(":");
        stack.push(Integer.parseInt(func[0]));
        int time = Integer.parseInt(func[2]);
        for (int i = 0; i < logs.length; i++){
            func = logs[i].split(":");
            if(func[1].indexOf("start") != -1){
                if(stack != null)
                    servTimes[stack.peek()] += Integer.parseInt(func[2]) - time;
                stack.push(Integer.parseInt(func[0]));
                time = Integer.parseInt(func[2]);
            }
                
            else{
                servTimes[stack.peek()] += Integer.parseInt(func[2]) - time + 1;
                stack.pop();
                time = Integer.parseInt(func[2]) + 1;
            }
                
        } 
        
        return servTimes;
    }
    public static void main( String args[] ) {

        // Driver code
        String[] logs = {"0:start:0","0:start:2","0:end:5","1:start:6","1:end:6","0:end:7"};
        System.out.println(Arrays.toString(serviceTime(2, logs)));
    }
}
{% endhighlight %}

![sear](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/sear/sear55.png)

