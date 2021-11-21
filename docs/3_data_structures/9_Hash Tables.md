---
layout: default
title: Hash Tables
parent: Data Structures
nav_order: 9
permalink: /data_structures/hash_tables
---
<div align="center" markdown="1">
Hash Tables / Java resources / Tutorial

{: .fs-8 .fw-400 }
</div>

## What is a Hash Table?

## Hashing
Until now, the overall time complexity accomplished in cases of insertion, deletion, and searching approach O(nLogn), or at O(Logn) at minimum in balanced Binary Trees, which is pretty good. But what to do if we want the results in constant time!?

🔍## Hashing, How and Why?
Hashing is a process used to uniquely identify objects and store each object at some pre-calculated unique index called its key. So the object is stored in the form of a key-value pair, and the collection of such items is called “Dictionary”. Each object can be searched using that key in O(1).

For a significantly large amount of data, even O(nLogn) becomes significantly large which might affect the efficiency of an algorithm. Ideally, a data structure is required that takes a constant amount of time to perform all three operations to manage a large number of records, and that is where Hashing comes in handy!

It can make searching a bit complex, but now fetching time is substantially reduced. There are different data structures based on Hashing, but the most commonly used data structure is a Hash Table.

## Hash Tables
The major target of Hash Tables is to minimize the searching time of any sort of data that needs to be fetched.

## The Working
Hash Tables are generally implemented using Arrays, as they are the only data structures that provide access to elements in constant O(1) time.

Let us explain how!

## Key-Value Pair
So the idea of data retrieval in O(1) is executed by using a key to map the data on an array (there are many ways to compute this key). In the case of arrays, you can directly use the key as an index to store data. If you pass the key to the array, the value is retrieved; alternatively (in the most naive form),

value = arr[key]

Here’s an illustration of how a Hash Table is mapped to the indices (1,2,3,…,5) in an array, with the index of this array calculated through a Hash function. (Hash function will be discussed later)

![has](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/has/has1.png)

Have a look at the following snippet, where a value is returned corresponding to the key passed to the function.

{% highlight java %}
class Hashing {
   public static String getValue(int key)  
   {    
    String [] myString = // pun intended
    { 
      "I am a programmer, I have no life.",
      "8 bytes walk into a bar, the bartenders asks \"What will it be?\
      "One of them says, \"Make us a double.\"",
      "Computers are useless. They can only give you answers.\n-Pablo Picasso"
    }; 
    if (key <= myString.length)
      return myString[key];    // value returned in constant time
    else 
      System.out.println("Key Not Found!\n");  
     return "";
  }
    public static void main( String args[] ) 
    {
        System.out.println( getValue(1) ); // Test your output for other keys
    }
}
{% endhighlight %}

## Dependency Factors
Hashing is often used in environments where we have to deal with crazy humongous datasets. So, the key to search the value might become so large that we need a function() to convert this large key into a smaller key that can fit into the range of 0 to n-1, where n is the size of the array. We can do this using a Hash Function. The performance of the Hashing data structure depends upon these three factors:
* Hash Function
* Size of the Hash Table
* Collision Handling Method

## Hash Functions

## Hash Function?
A hash function simply takes a key of an item and returns a calculated index in the array for that item.

This index calculation can be a simple or a very complicated encryption method. However, it is very important to choose an efficient Hashing function, as it directly affects the performance of the Hashing mechanism.


## What Hash Functions Do?
Have a look at the following illustration to get the analogy of a Hash function.

![has](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/has/has2.png)
![has](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/has/has3.png)
![has](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/has/has4.png)
![has](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/has/has5.png)
![has](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/has/has6.png)
![has](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/has/has7.png)
![has](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/has/has8.png)
![has](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/has/has9.png)
![has](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/has/has10.png)
![has](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/has/has11.png)
![has](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/has/has12.png)

![has](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/has/has13.png)

{% highlight java %}
class HashFunctions 
{
   public static int hashModular(int key, int size)
  {
    return key % size;
  }
  public static void main( String args[] ) 
  {
    int [] list = new int[10];// List of size 10
    int key = 35;
    int index = hashModular(key, 10); // Fit the key into the list size
    System.out.println("The index for key " + key + " is " + index);
  }
}
{% endhighlight %}

![has](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/has/has14.png)

{% highlight java %}
class HashFunctions 
{
   public static int hashTruncation(int key)
  {
    return key % 500; // we will use key upto 3 digits
  }
  public static void main( String args[] ) 
  {
    int key = 123456;
    int index = hashTruncation(key); // Fit the key into the list size
    System.out.println("The index for key " + key + " is " + index);
  }
}
{% endhighlight %}

![has](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/has/has15.png)

{% highlight java %}
class HashFunctions
{
  public static int hashFold(int key, int chunkSize) // Define the size of each divided portion
  {  
      System.out.println ("Key: "+ key);
      String strKey = Integer.toString(key); // Convert integer into string for slicing
      int hashVal = 0;
      System.out.println("Chunks:");
    
      for(int i = 0; i < strKey.length(); i+=chunkSize)
      {
        if(i + chunkSize < strKey.length())
        {
            System.out.println(strKey.substring(i,i+chunkSize));
            hashVal += Integer.parseInt(strKey.substring(i,i+chunkSize));
        }
        else
        {
          System.out.println(strKey.substring(i,strKey.length()));
          hashVal+= Integer.parseInt(strKey.substring(i,strKey.length()));
        }
      }
    return hashVal;
  }
   public static void main( String args[] ) 
   {
       int key = 3456789;
       int chunkSize = 2;
       System.out.println("Hash Key: " + hashFold(key, chunkSize));
       //try another case with different values    
   }    
}
{% endhighlight %}

## Collisions in Hash Tables

## What is Collision? 
As we know, Hash functions generate an index corresponding to every key, so it is accessed in O(1). There are times when the Hash function generates the same index of the array for two different keys; this causes the collision.

For Example:

Let’s say we are storing phone numbers as keys, but each number (e.g. 1-123-123) is too large itself to be stored as a key, or in another way, to be used in an array’s index. It is passed to the hash function, (which performs certain calculations) and the index is returned:

![has](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/has/has16.png)

![has](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/has/has17.png)

You can clearly observe that 247 is returned in either case! Since we cannot place 2 keys at the same index, this is called a collision.

The rate of collision depends on the method we’re choosing to calculate the index in the Hash Function.

![has](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/has/has18.png)

## Strategies to Handle Collisions 
When you map a big integer onto a small range of numbers from 0-N, where N is the size of the array, there is a huge possibility that two different keys may return the same index. This phenomenon is called collision. There are many methods to avoid collisions in the array, out of which these three are the most common:
* Linear Probing
* Chaining
* Re-sizing the Array

## 1. Linear Probing
Linear Probing suggests that if the index is already filled, move to the next index. It could be achieved by adding an offset value to an already computed index. If that index is also filled, add it again and so on.

Disadvantage: One drawback of using this strategy is that if you don’t pick an offset wisely, you can jump back to where you started and miss out on so many possible positions in the array.

Example: Let’s say the size of your array is 20. You pass a key to the Hash function which returns 2 (index of the array) by computing the key as key%size. If that position is already filled, then you can jump to another location by adding an offset value, let’s say 4. However, if that is filled too then you can add the offset again and jump to the next value, which will be 10 in this case. We will keep adding the offset until we find an empty spot. See the following illustration for better understanding:

![has](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/has/has19.png)

n the above example we can observe that the indices 5 and 6 remain empty.

## 2. Chaining
Chaining was initially implemented by combining multiple arrays as buckets, but we shifted to more efficient data structures later on. For example, each cell of the table holds a pointer to a linked-list on any other suitable data structure, such as a Doubly Linked-List or even a tree.

In case of a linked-list, each cell at the Hash Table points to the head of a different linked-list. Each list stores records, and all the content stored in one linked-list shares the same Hashed key. This strategy guarantees no collisions, but it gets costly in terms of space. An illustration is provided below for better understanding:

![has](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/has/has20.png)

In the above example, we can observe that due to a collision, the indices 0 and 2 both contain multiple-element linked lists. This strategy also increases the look-up time.

## 3. Resizing the Array 
Another way to reduce collisions is to resize the list. We can set a threshold and once it is crossed, we can create a new table which is double the size of the original. All we have to do then is to copy the elements from the previous table.

Resizing the list significantly reduces collisions, but the function itself is costly. Therefore, we need to be careful about the threshold we set. A typical convention is to set the threshold at 0.6, which means that when 60% of the table is filled, the resize operation needs to take place.

Another factor to keep in mind is the content of the Hash Table. The stored records might be concentrated in one region, leaving the rest of the list empty. However, this behavior will not be picked up by the resize function and you will end up resizing inappropriately.

Some other strategies to handle collisions include Quadratic Probing, Bucket Method, Random Probing or Re-hashing the key. We use the strategy that best suits our Hashing algorithm and the size of records that we plan to store.

## Building a Hash Table from Scratch

## Hash Table using Buckets
As said earlier, Hash Tables are implemented using Arrays. The implementation of a Hash Table is quite simple. In this lesson, we will use Bucket strategy to avoid collisions. In the Bucket strategy, we chain different arrays together to store elements, where each array is called Bucket.

The size of the Hash Table is set as:

n*m

Here, n is the number of keys it can hold, and m is the number of slots each bucket contains. Each slot holds a key/value pair.

![has](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/has/has21.png)

## Implementation
We will start by building a simple class. As discussed earlier, a typical Hash entry consists of three data members: a key, the data itself, and the reference to a new entry.

{% highlight java %}
class HashEntry {
	String key;
	int value;

	// Reference to next entry
	HashEntry next;

	// Constructor
	public HashEntry(String key, int value) {
		this.key = key;
		this.value = value;
	}
}
{% endhighlight %}

We want to combine all Hash entries in one table to implement this in code along with some helper functions which will be used later. So, here is what we will do:

{% highlight java %}
// Class to represent entire hash table
class HashTable {
	private ArrayList < HashEntry > bucket;
	private int slots;
	private int size;

	//Constructor
	public HashTable() {
		bucket = new ArrayList < HashEntry >();
		slots = 10;
		size = 0;
		//initialize buckets
		for (int i = 0; i < slots; i++)
		bucket.add(null);

	}
	public int size() {
		return size;
	}
	public boolean isEmpty() {
		return size() == 0;
	}
{% endhighlight %}

Now to convert the key into a Hash, which will represent an index position on the array, we need a Hash function. In this code, we will simply take modular of the key with the size of the array.

{% highlight java %}
private int getIndex(String key) {

	//hashCode is a built in function of Strings
	int hashCode = key.hashCode();
	int index = hashCode % slots;
	//Check if index is negative
	if(index<0){
		index=(index + slots) % slots;
	}
	return index;
}
{% endhighlight %}

Note: hashCode method might return a negative integer. If a string is long enough, its hashcode will be bigger than the largest integer we can store on 32 bits CPU. In this case, due to integer overflow, the value returned by hashCode can be negative. Therefore, we will get a negative index. In this case, we add slots to the current index to make it positive and then take a mod of it to get a positive index.

Since our Hash function is now ready, let’s implement the operations of search(), insert(), and delete() operations one by one in the upcoming lesson. We will also test on a driver to see if our Hash Table works fine.

## Add/Remove & Search in a Hash Table (Implementation)

## Insertion in the Table
In the previous lesson, we built a HashTable class and designed a Hash function as well. Now we will implement the main functionalities and see it if runs on the main driver perfectly. Starting with the insertion operation. The code below shows how insertion works in a HashTable. First of all, we will check if the key is already present in the table. If yes, it will insert the value into the head and point the head to next node. In order to avoid a collision, we will make sure that the array doesn’t get loaded up to a certain threshold. Whenever it crosses the threshold, we shift the elements from current table to an even bigger

{% highlight java %}
	//Inserts a key value pair into table
	public void insert(String key, int value)
{
		//Find head of the chain 
		int b_Index = getIndex(key);
		HashEntry head = bucket.get(b_Index);

		//Checks if the key is already exists 
		while(head != null)
		{
			if (head.key.equals(key))
			{
				head.value = value;
				return;
			}
			head = head.next;
		}

		// Inserts key in the chain
		size++;
		head = bucket.get(b_Index);
		HashEntry new_slot = new HashEntry(key, value);
		new_slot.next = head;
		bucket.set(b_Index, new_slot);

		
    //Checks if array >60% of the array gets filled
		if ((1.0*size)/slots >= 0.6)
		{
			ArrayList<HashEntry> temp = bucket;
			bucket = new ArrayList();
			slots = 2 * slots;
			size = 0;
			for (int i = 0; i < slots; i++)
				bucket.add(null);

			for (HashEntry head_Node : temp)
			{
				while (head_Node != null)
				{
					insert(head_Node.key, head_Node.value);
					head_Node = head_Node.next;
				}
			}
		}
}
{% endhighlight %}

## Search a Value in the Table
After insertion, let us now discuss how to search a value already present in the table. Here is how it works:

{% highlight java %}
// Return a value for a given key
public int getValue(String key)
{
	// Find the head of chain 
	int b_Index = getIndex(key);
	HashEntry head = bucket.get(b_Index);

	// Search key in the slots
	while (head != null)
	{
		if (head.key.equals(key))
			return head.value;
		head = head.next;
	}

	// If key not found
	return null;
}
{% endhighlight %}

## Deletion in the Table
Deletion in a Hash Table is quite simple. Here’s the code to delete an element from the table based on a key:

{% highlight java %}
//Remove a value based with key
public int delete(String key)
{
	//Find index 
	int b_Index = getIndex(key);

	// Get head of the chain for that index
	HashEntry head = bucket.get(b_Index);

	//Find the key in slots
	HashEntry prev = null;
	while (head != null)
	{
		//If key exists
		if (head.key.equals(key))
			break;

		// Else keep moving in chain
		prev = head;
		head = head.next;
	}

	// If key does not exist
	if (head == null)
		return null;

	// Decrease the size by one
	size--;

	// Remove key
	if (prev != null)
		prev.next = head.next;
	else
		bucket.set(b_Index, head.next);

	return head.value;
}

{% endhighlight %}

## Complete Implementation of Hash Tables

## Assembled Operations
In the previous lessons, we discussed each part in detail and went through its implementation. Now we will combine all those pieces into one executable code and run it on a given driver without any errors:

{% highlight java %}
import java.util.ArrayList;

// Class to represent entire hash table
class HashTable
{
	// to store chains of slots 
	private ArrayList<HashEntry> bucket;

	// num of slots in each bucket
	private int slots;

	// total hashed keys
	private int size;


	public HashTable()
	{
		bucket = new ArrayList <HashEntry>();
		slots = 5;
		size = 0;

		//Initialize nodes
		for (int i = 0; i < slots; i++)
			bucket.add(null);
	}

	public int size() { return size; }
	public boolean isEmpty() { return size() == 0; }

  //Look for the index based on key
  // search function
  private int getIndex(String key)
	{
		int hashCode = key.hashCode();
		int index = hashCode % slots;
		return index;
	}

  //delete a value
	public int delete(String key)
	{
    
    //Look for the index based on key		
    int b_Index = getIndex(key);

		HashEntry head = bucket.get(b_Index);

		// Search the key in slots
		HashEntry prev = null;
		while (head != null)
		{
			// If the key exists
			if (head.key.equals(key))
				break;

			//If the key not found yet
			prev = head;
			head = head.next;
		}

		// If the key does not exist
		if (head == null)
			return 0;

		size--;

	 // Delete the value by  key
		if (prev != null)
			prev.next = head.next;
		else
			bucket.set(b_Index, head.next);

		return head.value;
	}

  //to get a value for key from table
  public int get(String key)
	{
		int b_Index = getIndex(key);
		HashEntry head = bucket.get(b_Index);

		// Find the key in slots
		while (head != null)
		{
			if (head.key.equals(key))
				return head.value;
			head = head.next;
		}

		// If key does not exist
		return 0;
	}

	// Insert the key into table
	public void insert(String key, int value)
	{	
		int b_Index = getIndex(key);
		HashEntry head = bucket.get(b_Index);
		// See if the key exists
		while (head != null)
		{
			if (head.key.equals(key))
			{
				head.value = value;
				return;
			}
			head = head.next;
		}

		// Insert key into the bucket 
		size++;
		head = bucket.get(b_Index);
		HashEntry new_slot = new HashEntry(key, value);
		new_slot.next = head;
		bucket.set(b_Index, new_slot);

		//If 60% of the array gets filled, double the size
		if ((1.0*size)/slots >= 0.6)
		{
			ArrayList <HashEntry> temp = bucket;
			bucket = new ArrayList<>();
			slots = 2 * slots;
			size = 0;
			for (int i = 0; i < slots; i++)
				bucket.add(null);

			for (HashEntry head_Node : temp)
			{
				while (head_Node != null)
				{
					insert(head_Node.key, head_Node.value);
					head_Node = head_Node.next;
				}
			}
		}
	}
}

//One Entry in the Hash Table
class HashEntry
{
	String key;
	int value;

	// Reference to next node
	HashEntry next;

	// Constructor
	public HashEntry(String key, int value)
	{
		this.key = key;
		this.value = value;
	}
}

class HashTableDemo {
	public static void main(String[] args)
	{
    HashTable table = new HashTable(); //Create a HashTable
    //Before Insertion
 		System.out.println("Table Size = " + table.size());  
		table.insert("This",1 ); //Key-Value Pair
		table.insert("is",2 );
		table.insert("a",3 );
 		table.insert("Test",4 );   
		table.insert("Driver",5 );
		System.out.println("Table Size = " + table.size());
    // first search the key then delete it in the table
    // see the implementation first
		System.out.println(table.delete("is")+ 
		" : This key is deleted from table");
    System.out.println("Now Size of the table = " + table.size() );    
		if(table.isEmpty())
      System.out.println("Table is Empty");
    else
      System.out.println("Table is not Empty");  
		
	}
}

{% endhighlight %}

## Overview of Complexities
To sum up the discussion here, HashTables are ideally used when you have a large amount of data, and you need constant time for all basic operations. But you need to come up with a good Hash function to encrypt the keys to avoid collisions. Given below are the tables which show the time complexity of a Hash Table in different scenarios.

![has](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/has/has22.png)

## Trie vs Hash Table

## Comparison between Trie & HashTable
One might wonder what is the need of using Tries when we can implement dictionaries with Hash Tables as well. A simple answer to this would be, yes, you can use Hash Tables to build dictionaries, but if you need a fast lookup and have long words which share common prefixes then a Trie is the perfect data structure for you. It also makes storing words easier, as the implementation is very simple. Some of the key points which differentiate a Hash Table from Tries are given below:

## 1. Common Prefixes
In Tries, the words having common prefixes share a common path until the end of the prefix. After that, they are divided into two branches. We cannot do that in Hash Tables; no matter how similar the words are, we would still need to store them at different locations. This would result in irrelevant iterations while searching. Here is an interesting example to explain what we just said: two words “interest” and “interesting” will be stored differently in a HashTable, but in a Trie we only need to add 3 new nodes for “ing” at the end of the “t” Node. Did you notice the space efficiency?

## 2. Lookup for Exact Words
As discussed in the previous lesson, Tries can perform a spell-check, but in Hashing. We can only look up exact words, otherwise, it will not be able to identify the word.

## 3. No Re-hashing Required
The most important part of a HashTable is the Hash function. It is often very difficult to build as the performance of HashTable is entirely dependent on it. But in Tries, we do not need to perform re-hashing to generate an index. It just traverses the nodes and inserts new nodes, that’s it!

## 4. Collision Resolution
One downside of using a HashTable is that we always need to come up with good collision resolution strategies to avoid collisions if the data is huge. A collision can never occur in Trie because all words are unique and can act like a “key”. This makes the implementation of Tries so much simpler!

## 5. Memory Requirements
In worst case scenarios, a Trie will definitely perform better than a HashTable, but HashTables will be more convenient to use in average cases-- depending upon the efficiency of the Hash function. As in Trie, we need to allocate 26 pointers at every node even if most of them are Null, so a HashTable would be more of a wise choice here!

If your dictionary contains a lot of words with common prefixes or suffixes then Tries would be an efficient data structure to use as compared to Hash-Tables.

## HashMap vs HashSet

## Introduction
Before we solve any challenges regarding Hast Tables, it is necessary to look at the definitions of HashMap and HashSet and see how they are different. Both are implemented in Java using the Hash Table class, which is why it is also a common misconception that these two structures are the same, but they are very different from each other.

🔍## HashMap?
HashMap is a collection that contains all the key-value pairs; it maps the values to keys. There is a built-in class available in Java for HashMap, implemented by using Map interface. It provides the basic functionality of hashing along with some helper functions that help in the process of insertion, deletion, and search.

Some of the key features of HashMap are given below:
* A HashMap stores key-value pairs (examples given below) to map a key to the value:
   * abc->123abc−>123
   * xyz->456xyz−>456
* HashMap cannot contain duplicate keys. It can, however, have duplicate values.
* HashMap also allows multiple null values and only one null key
* This mechanism does not support synchronous operations and is not thread-safe.
🔍
 ## HashSet?
HashSet class is implemented in Java using Set interface. It is also built in the same way as HashMap, i.e., using the Hash Table class, but it is still quite different from the HashMap class. Some of the key features of HashSet are listed below:
* HashSet also stores values in an unordered way, using hashing, but this happens in the backend. On the backend, the HashSet class is implemented using the HashMap class. The value that we add to the HashSet is then added to the HashMap as a key, corresponding to a dummy value Object. The retrieval remains O(1)O(1)
* HashSet is a class which implements the Set interface and this interface only stores values, not a key-value pair.
* HashSet restricts storing multiple null values and only allows one null value in the whole table
* HashSet does not allow storing duplicate values as a set can only contain unique elements
* Just like HashMap, HashSet also does not support synchronous operations
