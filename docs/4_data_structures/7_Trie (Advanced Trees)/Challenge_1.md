---
layout: default
title: Challenge 1
parent: Trie (Advanced Trees)
grand_parent: Data Structures
nav_order: 1
permalink: /data_structures/trie_advanced_trees/ch1
---
<div align="center" markdown="1">
Challenge 1 / Java resources / Tutorial

{: .fs-8 .fw-400 }
</div>

## Challenge 1: Total Number of Words in a Trie

## Problem Statement
Implement the totalWords(TrieNode root) function to find the total number of words in a Trie.

## Function Prototype
int totalWords(TrieNode root);
Here, root is the root node of the Trie.

## Output
It returns the total number of words in the Trie

## Sample Input
String keys[] = {"the", "a", "there", "answer", "any",
                     "by", "bye", "their","abc"};
## Sample Output
9

## Explanation
There are 9 words total in the given keys array.

Here’s an illustration of the given challenge:

![trie](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/trie/der33.png)

## Coding Exercise

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

    //Function to get root
    public TrieNode getRoot() {
        return root;
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
    private boolean hasNoChildren(TrieNode currentNode) {
        for (int i = 0; i < currentNode.children.length; i++) {
            if ((currentNode.children[i]) != null)
                return false;
        }
        return true;
    }

    //Recursive function to delete given key
    private boolean deleteHelper(String key, TrieNode currentNode, int length, int level) {
        boolean deletedSelf = false;

        if (currentNode == null) {
            System.out.println("Key does not exist");
            return deletedSelf;
        }

        //Base Case: If we have reached at the node which points to the alphabet at the end of the key.
        if (level == length) {
            //If there are no nodes ahead of this node in this path
            //Then we can delete this node
            if (hasNoChildren(currentNode)) {
                currentNode = null;
                deletedSelf = true;
            }
            //If there are nodes ahead of currentNode in this path
            //Then we cannot delete currentNode. We simply unmark this as leaf
            else {
                currentNode.unMarkAsLeaf();
                deletedSelf = false;
            }
        } else {
            TrieNode childNode = currentNode.children[getIndex(key.charAt(level))];
            boolean childDeleted = deleteHelper(key, childNode, length, level + 1);
            if (childDeleted) {
                //Making children pointer also null: since child is deleted
                currentNode.children[getIndex(key.charAt(level))] = null;
                //If currentNode is leaf node that means currntNode is part of another key
                //and hence we can not delete this node and it's parent path nodes
                if (currentNode.isEndWord) {
                    deletedSelf = false;
                }
                //If childNode is deleted but if currentNode has more children then currentNode must be part of another key.
                //So, we cannot delete currenNode
                else if (!hasNoChildren(currentNode)) {
                    deletedSelf = false;
                }
                //Else we can delete currentNode
                else {
                    currentNode = null;
                    deletedSelf = true;
                }
            } else {
                deletedSelf = false;
            }
        }
        return deletedSelf;
    }

    //Function to delete given key from Trie
    public void delete(String key) {
        if ((root == null) || (key == null)) {
            System.out.println("Null key or Empty trie error");
            return;
        }
        deleteHelper(key, root, key.length(), 0);
    }

}

//TrieNode => {TrieNode[] children, boolean isEndWord, int value, 
//access root => getRoot()
//markAsLeaf(int val), unMarkAsLeaf()}
class NumWords {
  public static int totalWords(TrieNode root){
    // Write - Your - Code
    return 0;
  }
}
{% endhighlight %}

## Solution Review: Total Number of Words in a Trie

## Solution: Increment Recursively

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

    //Function to get root
    public TrieNode getRoot() {
        return root;
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
    private boolean hasNoChildren(TrieNode currentNode) {
        for (int i = 0; i < currentNode.children.length; i++) {
            if ((currentNode.children[i]) != null)
                return false;
        }
        return true;
    }

    //Recursive function to delete given key
    private boolean deleteHelper(String key, TrieNode currentNode, int length, int level) {
        boolean deletedSelf = false;

        if (currentNode == null) {
            System.out.println("Key does not exist");
            return deletedSelf;
        }

        //Base Case: If we have reached at the node which points to the alphabet at the end of the key.
        if (level == length) {
            //If there are no nodes ahead of this node in this path
            //Then we can delete this node
            if (hasNoChildren(currentNode)) {
                currentNode = null;
                deletedSelf = true;
            }
            //If there are nodes ahead of currentNode in this path
            //Then we cannot delete currentNode. We simply unmark this as leaf
            else {
                currentNode.unMarkAsLeaf();
                deletedSelf = false;
            }
        } else {
            TrieNode childNode = currentNode.children[getIndex(key.charAt(level))];
            boolean childDeleted = deleteHelper(key, childNode, length, level + 1);
            if (childDeleted) {
                //Making children pointer also null: since child is deleted
                currentNode.children[getIndex(key.charAt(level))] = null;
                //If currentNode is leaf node that means currntNode is part of another key
                //and hence we can not delete this node and it's parent path nodes
                if (currentNode.isEndWord) {
                    deletedSelf = false;
                }
                //If childNode is deleted but if currentNode has more children then currentNode must be part of another key.
                //So, we cannot delete currenNode
                else if (!hasNoChildren(currentNode)) {
                    deletedSelf = false;
                }
                //Else we can delete currentNode
                else {
                    currentNode = null;
                    deletedSelf = true;
                }
            } else {
                deletedSelf = false;
            }
        }
        return deletedSelf;
    }

    //Function to delete given key from Trie
    public void delete(String key) {
        if ((root == null) || (key == null)) {
            System.out.println("Null key or Empty trie error");
            return;
        }
        deleteHelper(key, root, key.length(), 0);
    }

}

class numWords{
  public static int totalWords(TrieNode root){
    int result = 0;

    // Leaf denotes end of a word
    if (root.isEndWord)
      result++;

    for (int i = 0; i < 26; i++)
      if (root.children[i] != null)
        result += totalWords(root.children[i]);
    return result;
  }


  public static void main(String args[]){
    // Input keys (use only 'a' through 'z' and lower case)
    String keys[] = {"the", "a", "there", "answer", "any",
                     "by", "bye", "their","abc"};

    System.out.println("Keys: "+ Arrays.toString(keys));

    // Construct trie
    Trie t = new Trie();

    for (int i = 0; i < keys.length ; i++)
      t.insert(keys[i]);

    System.out.println(totalWords(t.getRoot()));
  }
}
{% endhighlight %}

![trie](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/trie/der34.png)