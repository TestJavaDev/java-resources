---
layout: default
title: Heaps
parent: Data Structures
nav_order: 8
permalink: /data_structures/heaps
has_children: true
---
<div align="center" markdown="1">
Heaps / Java resources / Tutorial

{: .fs-8 .fw-400 }
</div>

## What is a Heap

## Introduction
Heaps are advanced data structures based on Binary Trees, which is why they are commonly known as Binary Heaps.

🔍## What is a Binary Heap?
A Binary Heap is a complete Binary Tree which satisfies the Heap ordering property.

Heaps are implemented through Arrays, where each element of the array corresponds to a node in the binary tree and the value inside the node is called a “key”. Heaps can also be implemented using trees with a node class and pointers, but it’s usually easier and more space efficient to use an array.

All the nodes are ordered according to the rules listed below:
* A Heap tree must be a Complete Binary Tree.
* The nodes must be ordered according to the Heap Property.

## Common Misconception

There is also a common misconception that the elements of a Heap are sorted. They are not at all sorted; in fact, the only key feature of a Heap is that the largest or smallest element is always placed at the top (parent node) depending on what kind of Heap we are using.

Moreover, this Data Structure Heap has nothing to do with the dynamic memory allocations on a Heap in various languages like C/C++ and Pascal.

## 1. Complete Binary Tree
As discussed in the previous chapter, a Complete Binary Tree is a tree where each node has a max. of two children and nodes at all levels are completely filled (except the leaf nodes). But the nodes at the last level must be structured in such a way that the left side is never empty. This is the only condition that differentiates Complete Binary Trees from other trees.

The new elements are inserted from left to right. When you add a new node, you must make sure that the left child of that intermediate parent node is filled. If it’s not, add a node at the left and insert the new element there.

A Heap uses Complete Binary Trees to avoid holes in the array. See the figure below to see the difference between that and an Incomplete Binary Tree:

![heap](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/heap/has1.png)

## 2. Heap Property
A heap is built, based on the Heap property, by comparing the parent node key with its child node keys. This comparison is done based on the heap property. The two heap structures that we are going to cover in this chapter are:
* Min Heap
* Max Heap

Min Heap is built on the Min Heap property, and Max Heap is implemented on the Max Heap property. Let’s see how they are different.

## 2.1 Max Heap Property:
This property states that all the parent node keys must be greater than or equal to their child node keys. So the root node, in this case, will always contain the largest element present in the Heap. If Node A has a child node B, then,

![heap](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/heap/has2.png)

## 2.2 Min Heap Property:
In Min Heap, all the parent node keys are less than or equal to their child node keys. This goes without saying that the rule will apply to all children of the node. So the root node, in this case, will always contain the smallest element present in the Heap. If Node A has a child node B, then,

![heap](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/heap/has3.png)

## Why Use Heaps?

## Where are Heaps Used?
Just like other data structures, Heaps are also used in many computing algorithms. The major uses of Heaps are elaborated below:

1. Order statistics: Heaps are primarily used for efficiently finding the smallest or largest element in an array.
2. Priority Queues: Priority queues can be efficiently implemented using Binary Heap because it supports insert(), delete(), extractmax(), and decreaseKey() operations in O(logn)O(logn) time. Binomoial Heaps and Fibonacci Heaps are variations of Binary Heaps. These variations also perform union() in O(logn)O(logn) time, which is an O(n)O(n) operation in a Binary Heap. Heap-implemented priority queues are used in Graph algorithms like Prim’s Algorithm and Dijkstra’s algorithm.

![heap](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/heap/has4.png)
![heap](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/heap/has5.png)
![heap](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/heap/has6.png)
![heap](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/heap/has7.png)
![heap](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/heap/has8.png)
![heap](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/heap/has9.png)
![heap](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/heap/has10.png)
![heap](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/heap/has11.png)

3. Sorting: HeapSort uses the Heap data structure to sort values in exactly the same way as TreeSort used a Binary Search Tree.
Each insert() and delete() operation is O(logN). At the very worst - the heap does not always have all N values in it, so the complexity is certainly no greater than O(NlogN). This is better than the worst-case for TreeSort, which–because you might build a degenerate Binary Search Tree-- is O(N*N).
HeapSort is especially useful for sorting arrays because Heaps, unlike almost all other types of trees - are usually implemented in arrays, not as linked data structures!

## Heap Representation in Arrays

Heaps can be implemented using Arrays. The contents of a heap with n nodes are stored in such a way that all the parent nodes occur in the first half of array (n/2), while the leaves are present at the last n/2 positions. So the last parent will be at the n/2th position.

The node at the kth position will have its children placed as follows:
* he Left child at 2k+1
* The Right child at 2k+2.

See the figure below to see how nodes are mapped on the array:

![heap](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/heap/has12.png)

![heap](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/heap/has13.png)

## Max Heap: Introduction

## Building a Max-Heap
As mentioned in the previous lesson, a Max Heap follows the Max Heap property, which means the key at the parent node is always greater than keys at both child nodes. The following steps illustrate how we build a Max Heap:
1. Create a new node at the end of the heap.
2. Assign a new value to the node.
3. Compare the value of this child node with its parent.
4. If the value of the parent is less than that of the child, then swap them.
5. Repeat steps 3 & 4 until the Heap property holds.

## Implementing a Max-Heap
Heaps can be implemented using arrays. Initially, elements are placed in nodes in the same order as they appear in the array. Then a function is called over the whole Heap in a bottom-up manner, which “Max Heapifies” this Heap so that the Heap property is satisfied on all nodes.

When we say bottom-up we mean the function starts from the last parent node present at the n/2th position of the array, and it checks if the values at the child nodes are greater than the parent nodes. See how we constructed a Heap in the following illustration:

![heap](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/heap/has14.png)
![heap](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/heap/has15.png)
![heap](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/heap/has16.png)
![heap](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/heap/has17.png)
![heap](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/heap/has18.png)
![heap](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/heap/has19.png)
![heap](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/heap/has20.png)
![heap](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/heap/has21.png)
![heap](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/heap/has22.png)
![heap](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/heap/has23.png)
![heap](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/heap/has24.png)
![heap](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/heap/has25.png)
![heap](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/heap/has26.png)
![heap](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/heap/has27.png)
![heap](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/heap/has28.png)
![heap](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/heap/has29.png)
![heap](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/heap/has30.png)
![heap](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/heap/has31.png)

## Insertion in Max-Heap
If you want to insert a new element in the Max Heap, you will have to follow a list of steps to make sure the Heap property still holds after adding the element. Here’s the list of steps that you will perform:
1. Create a new child node at the end of the heap.
2. Place the new key at that node.
3. Compare the value with its parent node key.
4. If the key is greater than the key at the parent node, swap values.
5. If both keys at the children nodes are greater than the parent node key, pick the larger one and see if the Heap property is satisfied.
6. Repeat until you reach the root node.

For better understanding, here’s the visual representation of what we just said:

![heap](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/heap/has32.png)
![heap](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/heap/has33.png)
![heap](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/heap/has34.png)
![heap](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/heap/has35.png)
![heap](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/heap/has36.png)
![heap](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/heap/has37.png)
![heap](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/heap/has38.png)
![heap](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/heap/has39.png)
![heap](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/heap/has40.png)
![heap](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/heap/has41.png)
![heap](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/heap/has42.png)
![heap](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/heap/has43.png)
![heap](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/heap/has44.png)
![heap](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/heap/has45.png)

## Removing an Element from a Max-Heap
Deletion in a Max-Heap is mainly performed when you want to remove the largest element. In most of the cases, the purpose of a Heap is to work as a priority queue. As an example here, we will take the case of deleting the biggest element here as we are discussing Max Heaps. Given below is the list of steps you will follow to make sure the Heap Property still holds after deleting the root element:
1. Delete the root node
2. Move the key of the last child node at the last level to the root
3. Now compare the key with its children
4. If the key is smaller than the key at any of the child nodes, swap values
5. If both keys at the children nodes are greater than the parent node key, pick the larger one and see if the heap property is satisfied
6. Repeat until you reach the last level

For better understanding, here’s the visual representation of what we just said:

![heap](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/heap/has46.png)
![heap](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/heap/has47.png)
![heap](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/heap/has48.png)
![heap](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/heap/has49.png)
![heap](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/heap/has50.png)
![heap](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/heap/has51.png)
![heap](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/heap/has52.png)
![heap](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/heap/has53.png)
![heap](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/heap/has54.png)
![heap](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/heap/has55.png)
![heap](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/heap/has56.png)
![heap](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/heap/has57.png)
![heap](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/heap/has58.png)

## Max Heap (Implementation)

## Implementation 
Now that we have discussed the important Max Heap functions, let’s move on to implementing them in Java.

{% highlight java %}
import java.util.Arrays;

class Heap {
 
	private void maxHeapify(int[] heapArray, int index, int heapSize){
		int largest = index;
		while (largest < heapSize / 2){      // check parent nodes only     
			int left = (2 * index) + 1;       //left child
			int right = (2 * index) + 2;      //right child
      
			if (left < heapSize && heapArray[left] > heapArray[index]){
				largest = left; 			
      		}
			if (right < heapSize && heapArray[right] > heapArray[largest]){
				largest = right;
			}
			if (largest != index){ // swap parent with largest child 
				int temp = heapArray[index];
				heapArray[index] = heapArray[largest];
				heapArray[largest] = temp;
				index = largest;
			}
      		else 
				break; // if heap property is satisfied 
		} //end of while
	} 
	public void buildMaxHeap(int[] heapArray, int heapSize) 
  	{
   	// swap largest child to parent node 
		for (int i = (heapSize - 1) / 2; i >= 0; i--){
			maxHeapify(heapArray, i, heapSize);
		}
	}
	
	public static void main(String[] args) {
		int[] heapArray = { 1, 4, 7, 12, 15, 14, 9, 2, 3, 16 };
		
		System.out.println("Before heapify: "+Arrays.toString(heapArray));		
		new Heap().buildMaxHeap(heapArray, heapArray.length);
		System.out.println("After heapify: "+Arrays.toString(heapArray));		
	}
}
{% endhighlight %}

![heap](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/heap/has59.png)

## If this Code had a Face

![heap](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/heap/has60.png)
![heap](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/heap/has61.png)
![heap](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/heap/has62.png)
![heap](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/heap/has63.png)
![heap](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/heap/has64.png)
![heap](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/heap/has65.png)
![heap](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/heap/has66.png)
![heap](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/heap/has67.png)
![heap](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/heap/has68.png)
![heap](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/heap/has69.png)
![heap](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/heap/has70.png)
![heap](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/heap/has71.png)
![heap](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/heap/has72.png)
![heap](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/heap/has73.png)
![heap](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/heap/has74.png)
![heap](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/heap/has75.png)
![heap](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/heap/has76.png)
![heap](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/heap/has77.png)

![heap](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/heap/has78.png)
![heap](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/heap/has79.png)

## Min Heap: An Introduction

## Building a Min-Heap
As mentioned in the previous lesson, a Min Heap follows the Min Heap property, which means the key at the parent node is always smaller than keys at both children nodes.

Heaps can be implemented using arrays. Initially, elements are placed in nodes in the same order as they appear in the array. Then a function is called over the whole Heap in a bottom-up manner, which “Min Heapifies” this Heap so that the Heap property is satisfied on all nodes.

When we say bottom-up, we mean the function starts from the last parent node present in the n/2th position of the array, and checks if the values at the children nodes are smaller than the parent node. If yes, then swap the values; if no, then move to the next parent node. See how we constructed a Heap in the following illustration:

![heap](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/heap/res1.png)
![heap](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/heap/res2.png)
![heap](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/heap/res3.png)
![heap](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/heap/res4.png)
![heap](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/heap/res5.png)
![heap](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/heap/res6.png)
![heap](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/heap/res7.png)
![heap](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/heap/res8.png)
![heap](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/heap/res9.png)
![heap](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/heap/res10.png)
![heap](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/heap/res11.png)
![heap](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/heap/res12.png)
![heap](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/heap/res13.png)
![heap](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/heap/res14.png)
![heap](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/heap/res15.png)
![heap](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/heap/res16.png)
![heap](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/heap/res17.png)
![heap](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/heap/res18.png)
![heap](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/heap/res19.png)
![heap](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/heap/res20.png)

## Insertion in Min Heap
If you want to insert a new element in a Min Heap, you will have to follow a list of steps to make sure the Heap property still holds after adding the element. Here’s the list of steps that you will perform:
1. Create a new child node at the end of the heap
2. Place the new key at that node
3. Compare the value with its parent node key
4. If the key is smaller than the key at the parent node, swap values
5. If both keys at the children nodes are smaller than the parent node key, then pick the smallest one and see if the Heap property is satisfied.
6. Repeat until you reach the root node

For better understanding, here’s the visual representation of what we just said:

![heap](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/heap/res21.png)
![heap](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/heap/res22.png)
![heap](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/heap/res23.png)
![heap](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/heap/res24.png)
![heap](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/heap/res25.png)
![heap](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/heap/res26.png)
![heap](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/heap/res27.png)
![heap](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/heap/res28.png)
![heap](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/heap/res29.png)
![heap](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/heap/res30.png)
![heap](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/heap/res31.png)

## Deletion in Min Heap
Deletion is performed in the same way as in Max Heap. We will take the case of deleting the smallest element here as we are discussing Min Heaps. Given below is the list of steps you will follow to make sure the Heap property still holds after deleting the root element:
1. Delete the root node
2. Move the key of the last child node (at the last level) to the root
3. Now compare the key with its children
4. If the key is greater than the key at any of the children nodes, swap values
5. If both keys at children nodes are smaller than the parent node key, pick the smallest one and see if the Heap property is satisfied.
6. Repeat until you reach the last level

For better understanding, here’s the visual representation of what we just said above:

![heap](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/heap/res32.png)
![heap](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/heap/res33.png)
![heap](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/heap/res34.png)
![heap](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/heap/res35.png)
![heap](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/heap/res36.png)
![heap](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/heap/res37.png)
![heap](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/heap/res38.png)

## Min Heap (Implementation)

## Implementation

{% highlight java %}
import java.util.Arrays;

class Heap {
 
  private void minHeapify(int[] heapArray, int index, int heapSize) {
		int smallest = index;

		while (smallest < heapSize / 2) { // check parent nodes only
			int left = (2 * index) + 1; //left child
			int right = (2 * index) + 2; //right child
			if (left < heapSize && heapArray[left] < heapArray[index]) {
				smallest = left;
			}

			if (right < heapSize && heapArray[right] < heapArray[smallest]) {
				smallest = right;
			}

			if (smallest != index) { // swap parent with smallest child
				int temp = heapArray[index];
				heapArray[index] = heapArray[smallest];
				heapArray[smallest] = temp;
				index = smallest;
			} else {
				break; // if heap property is satisfied
			}

		} //end of while
	}
 
	public void buildMinHeap(int[] heapArray, int heapSize) {
    
		// swap smallest child to parent node 
		for (int i = (heapSize - 1) / 2; i >= 0; i--) {
			minHeapify(heapArray, i, heapSize);
		}
	}
	
	public static void main(String[] args) {
		int[] heapArray = { 31, 11, 7, 12, 15, 14, 9, 2, 3, 16 };
		
		System.out.println("Before heapify: "+Arrays.toString(heapArray));		
		new Heap().buildMinHeap(heapArray, heapArray.length);
		System.out.println("After heapify: "+Arrays.toString(heapArray));
		
	}
}
{% endhighlight %}

## Explanation:
This code covers all the cases that we discussed in the previous chapter. Let’s look at each function one by one and see what’s going on:
* BuildHeap(): It takes the array and starts from the last child node (at the last level), then passes it to MinHeapify for comparison.
* MinHeapify(): This functions takes the node value and compares it with the key at the parent node, and swaps them if the child node < the parent node. The while loop makes sure that the nodes keep swapping until we reach the last index and Heap property is satisfied throughout the Heap!

![heap](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/heap/res39.png)
![heap](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/heap/res40.png)
![heap](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/heap/res41.png)
![heap](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/heap/res42.png)
![heap](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/heap/res43.png)
![heap](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/heap/res44.png)
![heap](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/heap/res45.png)
![heap](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/heap/res46.png)
![heap](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/heap/res47.png)
![heap](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/heap/res48.png)
![heap](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/heap/res49.png)

## Time Complexity of Min-Heap
The overall time complexity of building the Heap in a Min Heap is the same in as a Max Heap: O(n). You can refer to this lesson for the complete calculation.
