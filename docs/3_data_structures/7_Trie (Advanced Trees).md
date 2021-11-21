---
layout: default
title: Trie (Advanced Trees)
parent: Data Structures
nav_order: 7
permalink: /data_structures/trie_advanced_trees
has_children: true
---
<div align="center" markdown="1">
Trie (Advanced Trees) / Java resources / Tutorial

{: .fs-8 .fw-400 }
</div>

## What is a Trie?

ntroduction#
Till now, we only studied some of the commonly used Trees like Red-Black, 2-3 Trees, etc. In this chapter, we are going to look at a tree-like data structure which proves to be really efficient while solving programming problems related to Strings. This data structure is called Trie and is also known as “Prefix Trees”; we will find out why it’s named that later.

💡 Did you know?#
Trie basically comes from the word “retrieval”, as the main purpose of using this structure is that it provides fast retrieval. Tries are mostly used for searching words in the dictionary, providing auto-suggestions in search engines, and for IP routing.

![trie](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/trie/has1.png)

Common Applications of Tries#
Tries are basically used where fast retrieval is required. Let’s have a look at some real-life examples to understand how Tries are being used:

1. Auto-Complete Words#
Today, the autocomplete feature is supported by almost all of the major applications. This feature can be very efficiently implemented with the help of Tries, as they reduce the overall cost of performance.

2. Spell-Checking#
Tries come in handy when you need to perform spell-check on a word entered by the user, to check if that word already exists in the dictionary or if the user needs to be corrected. This feature is really helpful when the user does not know the exact spelling of a keyword he’s searching for.

3. Searching for a Contact in Phone#
Another real-life use of Tries is the searching we do while looking for a person in the contact list. It provides auto-suggestions based on the combination of letters that we enter. This could also be performed with Hash Tables but it won’t be as efficient as Tries; we will discuss this in detail later.

Properties of Trie#
To maintain its overall efficiency, Tries have to follow the rules given below:

Tries are similar to Graphs, as they are a combination of nodes where each node represents a unique alphabet.

Tries are more like ordered trees where each of the children can either be Null or points to a node.

The size of the Trie depends upon the number of letters. For example, in English there are 26 letters, so the size of a Trie node cannot exceed 26.

The depth of a Trie depends on the longest word that it stores.

Another important property of Tries is that they provide the same path for words that share a common prefix. For example, “there” and “their” have a common prefix “the”, so they will share the same path till “e”. After that, they will be divided into two branches. The whole working of Trie depends on this property, so we will discuss this later in detail.

## The Structure of a Trie

Introduction#
Previously, we discussed a few properties that a Trie must hold in order to improve the performance. In this lesson, we will take a look at the basic structure of Trie and then build a class in Java with the help of these concepts.

![trie](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/trie/has2.png)

{% highlight java %}
class TrieNode
{
    TrieNode[] children;
    boolean isEndWord; //will be true if the node represents the end of word
    static final int ALPHABET_SIZE = 26; //Total # of English Alphabets = 26
    TrieNode(){
        this.isEndWord = false;
        this.children = new TrieNode[ALPHABET_SIZE]; 
    }

    //Function to mark the currentNode as Leaf
    public void markAsLeaf(){
        this.isEndWord = true;
    }

    //Function to unMark the currentNode as Leaf
    public void unMarkAsLeaf(){
        this.isEndWord = false;
    }
}

class TrieNodeDemo
{
 
  public static void main(String args[])
  {
    TrieNode t = new TrieNode();
    System.out.println("Children: " + t.children[0]); // will be null by default
    System.out.println("isEndWord: " + t.isEndWord);  // will be false by default
   
  }
}
{% endhighlight %}

Implementation of the Trie Class#
A Trie will be implemented using the TrieNode class. As discussed above, a TrieNode in Trie represents one letter which keeps its pointers on the children nodes. Each Node can have a max. of 26 children if we are storing English words.

A root TrieNode is placed at the top, which is Null, and contains 26 links (one per letter). These links are either Null or point to another TrieNode. The index of children pointers is decided based on the sequence of the letters (starting from 0). For instance, TrieNode A (if it exists) will be stored at the 0th index, B at the index 1, and TrieNode Z will come at the 25th index. For the next TrieNode, again, there could be 26 possibilities so we’ll initialize an array of 26 pointers.

All the words are stored in a top-bottom manner. While storing the last character, you should always set the isEndWord flag as true to indicate the end of a word, and store the particular value for the key(word). This technique helps us in searching for a word to see if it even exists. The size of a Trie depends on the number of letters each node can store and the number of words. A typical class of Trie looks like this in Java:

{% highlight java %}
class Trie{  
  private TrieNode root; //Root Node
  
  //Constructor
  Trie(){
    root = new TrieNode();
  }
  //Function to get the index of a character 't'
  public int getIndex(char t){
    return t - 'a';
  }
  
  //Function to insert a key,value pair in the Trie
  public void insert(String key,int value){}
  
  //Function to search given key in Trie
  public boolean search(String key){ return false;}
  
  //Function to delete given key from Trie
  public boolean delete(String key){ return false;}
}

class TrieNode
{
    TrieNode[] children;
    boolean isEndWord; //will be true if the node represents the end of word
    static final int ALPHABET_SIZE = 26; //Total # of English Alphabets = 26
    TrieNode(){
        this.isEndWord = false;
        this.children = new TrieNode[ALPHABET_SIZE]; 
    }

    //Function to mark the currentNode as Leaf
    public void markAsLeaf(){
        this.isEndWord = true;
    }

    //Function to unMark the currentNode as Leaf
    public void unMarkAsLeaf(){
        this.isEndWord = false;
    }
}

class TrieDemo{  
  public static void main(String args[])
  {
    Trie t = new Trie();
    System.out.println("Index to insert a = " + t.getIndex('a'));
    System.out.println("Index to insert t = " + t.getIndex('t'));
  }
}
{% endhighlight %}

## Insertion in a Trie

Inserting a word in Trie#
Insertion is simple for individual characters in the trie. If the character is already present, we follow the path; if that character is not present, then we insert the corresponding nodes. While inserting the last node, we must also set the value of isEndWord() to true.

Case 1: What if the word has no common subsequence? i.e. No Common Prefix#
For example, if we want to insert a new word into the trie below, e.g. “any”, then we need to insert all of the characters for the word “any”; currently, “the” is the only word in the trie, and there are no common character subsequences between “any” and “the”.

![trie](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/trie/has3.png)
![trie](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/trie/has4.png)
![trie](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/trie/has5.png)
![trie](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/trie/has6.png)





{% highlight java %}

{% endhighlight %}