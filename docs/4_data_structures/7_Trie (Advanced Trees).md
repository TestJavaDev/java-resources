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

## Introduction
Till now, we only studied some of the commonly used Trees like Red-Black, 2-3 Trees, etc. In this chapter, we are going to look at a tree-like data structure which proves to be really efficient while solving programming problems related to Strings. This data structure is called Trie and is also known as “Prefix Trees”; we will find out why it’s named that later.

💡## Did you know?
Trie basically comes from the word “retrieval”, as the main purpose of using this structure is that it provides fast retrieval. Tries are mostly used for searching words in the dictionary, providing auto-suggestions in search engines, and for IP routing.

![trie](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/trie/has1.png)

## Common Applications of Tries
Tries are basically used where fast retrieval is required. Let’s have a look at some real-life examples to understand how Tries are being used:

## 1. Auto-Complete Words
Today, the autocomplete feature is supported by almost all of the major applications. This feature can be very efficiently implemented with the help of Tries, as they reduce the overall cost of performance.

## 2. Spell-Checking
Tries come in handy when you need to perform spell-check on a word entered by the user, to check if that word already exists in the dictionary or if the user needs to be corrected. This feature is really helpful when the user does not know the exact spelling of a keyword he’s searching for.

## 3. Searching for a Contact in Phone
Another real-life use of Tries is the searching we do while looking for a person in the contact list. It provides auto-suggestions based on the combination of letters that we enter. This could also be performed with Hash Tables but it won’t be as efficient as Tries; we will discuss this in detail later.

## Properties of Trie
To maintain its overall efficiency, Tries have to follow the rules given below:
* Tries are similar to Graphs, as they are a combination of nodes where each node represents a unique alphabet.
* Tries are more like ordered trees where each of the children can either be Null or points to a node.
* The size of the Trie depends upon the number of letters. For example, in English there are 26 letters, so the size of a Trie node cannot exceed 26.
* The depth of a Trie depends on the longest word that it stores.
* Another important property of Tries is that they provide the same path for words that share a common prefix. For example, “there” and “their” have a common prefix “the”, so they will share the same path till “e”. After that, they will be divided into two branches. The whole working of Trie depends on this property, so we will discuss this later in detail.

## The Structure of a Trie

## Introduction
Previously, we discussed a few properties that a Trie must hold in order to improve the performance. In this lesson, we will take a look at the basic structure of Trie and then build a class in Java with the help of these concepts.

![trie](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/trie/has2.png)

## Representation of a Node
A node in a Trie represents a letter in an alphabet. For example, if we want to insert “hello” in the Trie, we will need to add 5 nodes, one for each alphabet. A typical Node in a Trie consists of two data members:
* children[]: An array which consists of the children nodes. The size of this array depends on the number of alphabets (26 for the English language). By default, all elements are set to Null.
* isEndWord: A flag to indicate the end of a word. It is set to false by default and is only updated when an end of the word is observed during insertion.

This is how we will code it in Java:

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

## Implementation of the Trie Class
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

## Inserting a word in Trie
Insertion is simple for individual characters in the trie. If the character is already present, we follow the path; if that character is not present, then we insert the corresponding nodes. While inserting the last node, we must also set the value of isEndWord() to true.

## Case 1: What if the word has no common subsequence? i.e. No Common Prefix
For example, if we want to insert a new word into the trie below, e.g. “any”, then we need to insert all of the characters for the word “any”; currently, “the” is the only word in the trie, and there are no common character subsequences between “any” and “the”.

![trie](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/trie/has3.png)
![trie](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/trie/has4.png)
![trie](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/trie/has5.png)
![trie](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/trie/has6.png)

## Case 2: If the word has a common subsequence? i.e. Common Prefix Found
For example, if we want to insert the word “there” into the trie below-- which already consists of the word “ their”–then the path to “ the” already exists. After that, we need to insert two nodes for “e” and “r” as shown below.

![trie](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/trie/has7.png)
![trie](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/trie/has8.png)
![trie](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/trie/has9.png)
![trie](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/trie/has10.png)
![trie](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/trie/has11.png)
![trie](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/trie/has12.png)
![trie](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/trie/has13.png)
![trie](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/trie/has14.png)

## Case 3: If the word is already present? i.e. Common Prefix Found
For example, if we want to insert the word “the” into the trie below-- which consists of a word “ their”–then the path for “ the” already exists. Therefore, we simply need to set the value of isEndWord() to true at “e” in order to represent the end of the word for “the” as shown below.

![trie](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/trie/has15.png)
![trie](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/trie/has16.png)
![trie](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/trie/has17.png)
![trie](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/trie/has18.png)
![trie](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/trie/has19.png)
![trie](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/trie/has20.png)

## Implementation
The following is the code snippet, so try to understand the code. If you don’t understand any point, you can read the explanation below.

If this Code had a Face

{% highlight java %}
class Trie{
    private TrieNode root; //Root Node

    //Constructor
    Trie(){
        root = new TrieNode();
    }
    //Function to get the index of a character 'x'
    public int getIndex(char x)
    {
        return x - 'a';  // the index is based on the position of character in alphabets
    }

    //Function to insert a key in the Trie
    public void insert(String key)
    {
        if(key == null) //Null keys are not allowed
        {
            System.out.println("Null Key can not be Inserted!");
            return;
        }
        key = key.toLowerCase(); //Keys are stored in lowercase
        TrieNode currentNode = this.root;
        int index = 0; //to store character index

        //Iterate the Trie with given character index,
        //If it is null, then simply create a TrieNode and go down a level
        for (int level = 0; level < key.length(); level++)
        {
            index = getIndex(key.charAt(level));
            if(currentNode.children[index] == null)
            {
                currentNode.children[index] = new TrieNode();
            }
            currentNode = currentNode.children[index];
        }
        //Mark the end character as leaf node
        currentNode.markAsLeaf();
    }
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
  public static void main(String args[]){
    // Input keys (use only 'a' through 'z' and lower case)
    String keys[] = {"the", "a", "there", "answer", "any",
                     "by", "bye", "their","abc"};
    String output[] = {"Not present in trie", "Present in trie"};
    Trie t = new Trie();
    
    System.out.println("Keys to insert: "+ Arrays.toString(keys) + "\n");
        
    // Construct trie       
    int i;
    for (i = 0; i < keys.length ; i++)
    {
      t.insert(keys[i]);
      System.out.println("\""+ keys[i]+ "\"" + "Inserted.");
    }
  }
}
{% endhighlight %}

![trie](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/trie/has21.png)
![trie](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/trie/has22.png)
![trie](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/trie/has23.png)
![trie](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/trie/has24.png)
![trie](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/trie/has25.png)
![trie](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/trie/has26.png)
![trie](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/trie/has27.png)
![trie](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/trie/has28.png)
![trie](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/trie/has29.png)
![trie](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/trie/has30.png)
![trie](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/trie/has31.png)

![trie](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/trie/has32.png)
![trie](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/trie/has33.png)

## Search in a Trie

## Searching for a word in Trie
If we want to search whether a word is present in the Trie or not, then we just need to keep tracing the path in the Trie that corresponds to the characters in the word.

## Case 1: Word is not present in Trie
If there is no path, as with the word “bedroom” in the below example, then we will only be able to trace till “bed”. Therefore, we return false because there is no character path for “r” after “bed”, indicating that this word is not present in the Trie.

![trie](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/trie/has34.png)
![trie](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/trie/has35.png)
![trie](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/trie/has36.png)
![trie](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/trie/has37.png)
![trie](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/trie/has38.png)

## Case 2: Path found but isEndWord() is not set for the last character
It returns false if the last node is not the end of the word, even if our word has been exhausted and the path is present. , For example, if we are searching for the word “be” then the path for “ being” is present. However, the value of isEndWord() for the “e” node is false, which indicates that the word does not terminate at “e”; hence "be” is not a valid word in Trie.

![trie](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/trie/has39.png)
![trie](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/trie/has40.png)
![trie](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/trie/has41.png)
![trie](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/trie/has42.png)

## Case 3: Word is found and isEndWord is set for last node of the path
The success case is when there exists a path and the last node in the path is also end-of-word.

![trie](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/trie/has43.png)
![trie](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/trie/has44.png)
![trie](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/trie/has45.png)
![trie](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/trie/has46.png)
![trie](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/trie/has47.png)

## Implementation
The following is the code snippet, so try to understand the code. If you don’t understand any point, you can read the explanation below.

{% highlight java %}
class Trie {
    private TrieNode root; //Root Node

    //Constructor
    Trie() {
        root = new TrieNode();
    }

    //Function to get the index of a character 't'
    public int getIndex(char t) {
        return t - 'a';
    }

    //Function to insert a key in the Trie
    public void insert(String key) {
        //Null keys are not allowed
        if (key == null) {
            return;
        }
        key = key.toLowerCase(); //Keys are stored in lowercase
        TrieNode currentNode = this.root;
        int index = 0; //to store character index

        //Iterate the Trie with given character index,
        //If it is null, then simply create a TrieNode and go down a level
        for (int level = 0; level < key.length(); level++) {
            index = getIndex(key.charAt(level));

            if (currentNode.children[index] == null) {
                currentNode.children[index] = new TrieNode();
            }
            currentNode = currentNode.children[index];
        }
        //Mark the end character as leaf node
        currentNode.markAsLeaf();
    }

    //Function to search given key in Trie
    public boolean search(String key) {

        if (key == null) return false; //Null Key

        key = key.toLowerCase();
        TrieNode currentNode = this.root;
        int index = 0;

        //Iterate the Trie with given character index,
        //If it is null at any point then we stop and return false
        //We will return true only if we reach leafNode and have traversed the
        //Trie based on the length of the key

        for (int level = 0; level < key.length(); level++) {
            index = getIndex(key.charAt(level));
            if (currentNode.children[index] == null) return false;
            currentNode = currentNode.children[index];
        }
        

        return currentNode.isEndWord;
    }
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
  
  public static void main(String args[]){
    // Input keys (use only 'a' through 'z' and lower case)
    String keys[] = {"the", "a", "there", "answer", "any",
                     "by", "bye", "their","abc"};
    String output[] = {"Not present in trie", "Present in trie"};
    Trie t = new Trie();
    
    System.out.println("Keys: "+ Arrays.toString(keys));
        
    // Construct trie
        
    int i;
    for (i = 0; i < keys.length ; i++)
      t.insert(keys[i]);
    
    // Search for different keys
    if(t.search("the") == true)
      System.out.println("the --- " + output[1]);
    else System.out.println("the --- " + output[0]);
         
    if(t.search("these") == true)
      System.out.println("these --- " + output[1]);
    else System.out.println("these --- " + output[0]);
         
    if(t.search("abc") == true)
      System.out.println("abc --- " + output[1]);
    else System.out.println("abc --- " + output[0]);
    }
}
{% endhighlight %}

## If this code had a face

![trie](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/trie/has48.png)
![trie](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/trie/has49.png)
![trie](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/trie/has50.png)
![trie](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/trie/has51.png)
![trie](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/trie/has52.png)
![trie](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/trie/has53.png)
![trie](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/trie/has54.png)
![trie](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/trie/has55.png)
![trie](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/trie/has56.png)
![trie](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/trie/has57.png)
![trie](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/trie/has58.png)
![trie](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/trie/has59.png)
![trie](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/trie/has60.png)
![trie](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/trie/has61.png)
![trie](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/trie/has62.png)
![trie](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/trie/has63.png)

![trie](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/trie/has64.png)
![trie](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/trie/has65.png)

## Deletion in a Trie

## Deleting a word in Trie
While deleting a word from a Trie, we make sure that the node that we are trying to delete does not have any further branches. If there are no branches, then we can easily remove the node. However, if the node contains further branches then this opens up a lot of the scenarios covered below.

## Case 1: If the word to be deleted has no common subsequence
If the word to be deleted has no common subsequence, then all the nodes of that word are deleted.
For example, in the figure given below, we have to delete all characters of “bat” in order to delete the word bat.

![trie](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/trie/der1.png)
![trie](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/trie/der2.png)
![trie](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/trie/der3.png)
![trie](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/trie/der4.png)
![trie](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/trie/der5.png)
![trie](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/trie/der6.png)
![trie](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/trie/der7.png)
![trie](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/trie/der8.png)
![trie](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/trie/der9.png)

## Case 2: If the word to be deleted is a prefix of some other word
If the word to be deleted is a prefix of some other word, then the value of isEndWord of the last node of that word is set to false, and no node is deleted.
For example, we will simply unmark e to delete the word the and show that it doesn’t exist anymore.

![trie](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/trie/der10.png)
![trie](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/trie/der11.png)
![trie](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/trie/der12.png)
![trie](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/trie/der13.png)
![trie](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/trie/der14.png)
![trie](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/trie/der15.png)

## Case 3: If the word to be deleted has a common prefix
If the word to be deleted has a common prefix and the last node of that word is also the leaf node (i.e. the last node of its branch), then this node is deleted along with all the higher-up nodes in its branch that do not have any other children and whose isEndWord is false.
For example, we’ll traverse the common path up to the and delete the characters “i” and “r” in order to delete their.

![trie](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/trie/der16.png)
![trie](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/trie/der17.png)
![trie](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/trie/der18.png)
![trie](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/trie/der19.png)
![trie](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/trie/der20.png)
![trie](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/trie/der21.png)
![trie](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/trie/der22.png)
![trie](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/trie/der23.png)
![trie](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/trie/der24.png)
![trie](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/trie/der25.png)
![trie](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/trie/der26.png)
![trie](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/trie/der27.png)
![trie](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/trie/der28.png)
![trie](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/trie/der29.png)
![trie](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/trie/der30.png)

## Implementation 
The following is the code snippet, so try to understand the code. If you don’t understand any point, you can read the explanation below

{% highlight java %}
class Trie {

    private TrieNode root; //Root Node

    //Constructor
    Trie() {
        root = new TrieNode();
    }

    //Function to get the index of a character 't'
    public int getIndex(char t) {
        return t - 'a';
    }

    //Function to insert a key in the Trie
    public void insert(String key) {
        //Null keys are not allowed
        if (key == null) {
            return;
        }
        key = key.toLowerCase(); //Keys are stored in lowercase
        TrieNode currentNode = this.root;
        int index = 0; //to store character index

        //Iterate the Trie with given character index,
        //If it is null, then simply create a TrieNode and go down a level
        for (int level = 0; level < key.length(); level++) {
            index = getIndex(key.charAt(level));

            if (currentNode.children[index] == null) {
                currentNode.children[index] = new TrieNode();
            }
            currentNode = currentNode.children[index];
        }
        //Mark the end character as leaf node
        currentNode.markAsLeaf();
    }

    //Function to search given key in Trie
    public boolean search(String key) {

        if (key == null) return false; //Null Key

        key = key.toLowerCase();
        TrieNode currentNode = this.root;
        int index = 0;

        //Iterate the Trie with given character index,
        //If it is null at any point then we stop and return false
        //We will return true only if we reach leafNode and have traversed the
        //Trie based on the length of the key

        for (int level = 0; level < key.length(); level++) {
            index = getIndex(key.charAt(level));
            if (currentNode.children[index] == null) return false;
            currentNode = currentNode.children[index];
        }
        if (currentNode.isEndWord) return true;

        return false;
    }

    //Helper Function to return true if currentNode does not have any children
    private boolean hasNoChildren(TrieNode currentNode){
        for (int i = 0; i < currentNode.children.length; i++){
            if ((currentNode.children[i]) != null)
                return false;
        }
        return true;
    }
    
    //Recursive function to delete given key
    private boolean deleteHelper(String key, TrieNode currentNode, int length, int level)
    {
        boolean deletedSelf = false;

        if (currentNode == null){
            System.out.println("Key does not exist");
            return deletedSelf;
        }

        //Base Case: If we have reached at the node which points to the alphabet at the end of the key.
        if (level == length){
            //If there are no nodes ahead of this node in this path
            //Then we can delete this node
            if (hasNoChildren(currentNode)){
                currentNode = null;
                deletedSelf = true;
            }
            //If there are nodes ahead of currentNode in this path
            //Then we cannot delete currentNode. We simply unmark this as leaf
            else
            {
                currentNode.unMarkAsLeaf();
                deletedSelf = false;
            }
        }
        else
        {
            TrieNode childNode = currentNode.children[getIndex(key.charAt(level))];
            boolean childDeleted = deleteHelper(key, childNode, length, level + 1);
            if (childDeleted)
            {
                //Making children pointer also null: since child is deleted
                currentNode.children[getIndex(key.charAt(level))] = null;
                //If currentNode is leaf node that means currntNode is part of another key
                //and hence we can not delete this node and it's parent path nodes
                if (currentNode.isEndWord){
                    deletedSelf = false;
                }
                //If childNode is deleted but if currentNode has more children then currentNode must be part of another key.
                //So, we cannot delete currenNode
                else if (!hasNoChildren(currentNode)){
                    deletedSelf = false;
                }
                //Else we can delete currentNode
                else{
                    currentNode = null;
                    deletedSelf = true;
                }
            }
            else
            {
                deletedSelf = false;
            }
        }
        return deletedSelf;
    }

    //Function to delete given key from Trie
    public void delete(String key){
        if ((root == null) || (key == null)){
            System.out.println("Null key or Empty trie error");
            return;
        }
        deleteHelper(key, root, key.length(), 0);
    }

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
  public static void main(String args[]){
    // Input keys (use only 'a' through 'z' and lower case)
    String keys[] = {"the", "a", "there", "answer", "any",
                     "by", "bye", "their","abc"};
    String output[] = {"Not present in trie", "Present in trie"};
    Trie t = new Trie();
    
    System.out.println("Keys: "+ Arrays.toString(keys));
        
    // Construct trie
        
    int i;
    for (i = 0; i < keys.length ; i++)
      t.insert(keys[i]);
    
    // Search for different keys and delete if found
    if(t.search("the") == true)
    {
      System.out.println("the --- " + output[1]);
      t.delete("the");
      System.out.println("Deleted key \"the\"");
    }
    else System.out.println("the --- " + output[0]);
         
    if(t.search("these") == true)
    {
      System.out.println("these --- " + output[1]);
      t.delete("these");
      System.out.println("Deleted key \"these\"");
    }
    else System.out.println("these --- " + output[0]);
         
    if(t.search("abc") == true)
    {
      System.out.println("abc --- " + output[1]);
       t.delete("abc");
      System.out.println("Deleted key \"abc\""); 
    }
    else System.out.println("abc --- " + output[0]);
         
    // check if the string has deleted correctly or still present
    if(t.search("abc") == true)
      System.out.println("abc --- " + output[1]);
    else System.out.println("abc --- " + output[0]);
    }
}
{% endhighlight %}

![trie](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/trie/der31.png)
![trie](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/trie/der32.png)