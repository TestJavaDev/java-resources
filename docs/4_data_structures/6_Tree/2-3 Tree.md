---
layout: default
title:  2-3 Tree
parent: Trees
grand_parent: Data Structures
nav_order: 6
permalink: /data_structures/trees/ch6
---
<div align="center" markdown="1">
 2-3 Tree / Java resources / Tutorial

{: .fs-8 .fw-400 }
</div>

## What is a 2-3 Tree?

## Introduction
A 2-3 Tree is another form of a search tree, but it is very different from a Binary Search Tree. Unlike BST, 2-3 Tree is a balanced and ordered search tree which provides a very efficient storage mechanism to guarantee fast operations. In this chapter, we will take a detailed look at a 2-3 Trees’s structure, the limitations it follows, and how elements are inserted and deleted from it.

One key feature of a 2-3 Tree is that it remains balanced, no matter how many insertions or deletions you perform. The leaf nodes are always present on the same level and are quite small in number. This is to make sure the height doesn’t increase up to a certain level as the time complexity of all the operations is mainly dependent upon it. Ideally, we want the height to be in logarithmic terms because the tree will require more time to perform operations as it grows larger. In 2-3 Trees, the height is logarithmic in the number of nodes present in the tree. They generally come in 2 forms:
* 2 Node Tree
* 3 Node Tree

See the figures below to get the idea of how they are different. The first figure is a 2-3 Tree with only two nodes. To keep it ordered, the left child key must be smaller than the parent node key. Similarly, the right child key must be greater than the parent key.

![tree](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/tree/xx1.png)

The next shows a 3-node tree where each node can contain a maximum of two keys and three children. Here, the parent node has 2 keys and 3 children (all at the same level). Let’s say the first key at a parent node is X and we call the second one Y. As shown in the figure, X key is greater than the left child and Y key is smaller than the right child key. The middle child has the value that is greater than X and smaller than Y.

![tree](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/tree/xx2.png)

Concluding from the explanation above, 2-3 Trees acquire a certain set of properties to keep the structure balanced and ordered. Let’s take a look at these properties.

![tree](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/tree/xx3.png)

## 2-3 Tree (Example)
See the following example of a 2-3 Tree to get a better idea. Here, 20, 70 and 120-150 are internal nodes and all leaf nodes are present at the same level.

![tree](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/tree/xx4.png)

## Operations
The basic operations of 2-3 Trees are the same as those covered in previous lessons:
* Search
* Insertion
* Deletion

The time complexity of all three operations will also be in logarithmic terms. So, they can be implemented to run in time O(logn), where n is the number of nodes.

## 2-3 Insertion

## Introduction
Insertion in 2-3 Trees is a lot different from Binary Search Trees. In 2-3 Trees, values are only inserted at leaf nodes based on certain conditions. As discussed before, the insertion algorithm takes O(Logn)O(Logn) time where n is the number of nodes in the tree. Searching for an element is done in Log(n)Log(n) and then insertion takes a constant amount of time. So, the overall time complexity of the insertion algorithm is O(Logn)O(Logn).

## Insertion Algorithm
The insertion algorithm is based on these scenarios:
* If the tree is initially empty, create a new leaf node and insert your value.
* If the tree is not empty, traverse through the tree to find the right leaf node where the value should be inserted.
* If the leaf node has only one value, insert your value into the node.
* If the leaf node has more than two values, split the node by moving the middle element to the top node.
* Keep forming new nodes wherever you get more than two elements.

## Example -1
Let’s take a look at the following example where we will build a 2-3 Tree from scratch by inserting elements one by one.

![tree](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/tree/zz1.png)
![tree](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/tree/zz2.png)
![tree](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/tree/zz3.png)
![tree](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/tree/zz4.png)
![tree](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/tree/zz5.png)
![tree](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/tree/zz6.png)
![tree](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/tree/zz7.png)
![tree](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/tree/zz8.png)
![tree](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/tree/zz9.png)
![tree](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/tree/zz10.png)
![tree](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/tree/zz11.png)
![tree](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/tree/zz12.png)
![tree](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/tree/zz13.png)
![tree](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/tree/zz14.png)
![tree](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/tree/zz15.png)
![tree](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/tree/zz16.png)
![tree](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/tree/zz17.png)
![tree](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/tree/zz18.png)
![tree](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/tree/zz19.png)
![tree](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/tree/zz20.png)
![tree](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/tree/zz21.png)
![tree](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/tree/zz22.png)

## Explanation
As we see that the tree is initially empty, we will create a new node and insert 50 in it. Then we will insert 30 in the same node as it has one space left. Next, we’ll insert 10, but since the node can only contain a max of two values we must shift the median value to the top and split the node into two children. This makes 30 the root node, with 10 and 50 as its left and right child respectively.

Now we insert 70, as 70 is greater than the root key so it will be inserted in the right child. Similarly, 60 will be inserted in the same node. However, the values have more than two again, so we will perform the same series of steps performed above–shifting 60 to the root node, and so on.

## Example - 2
This example is a little harder than the previous one. See if you can solve it on your own!

![tree](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/tree/ss1.png)
![tree](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/tree/ss2.png)
![tree](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/tree/ss3.png)
![tree](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/tree/ss4.png)
![tree](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/tree/ss5.png)
![tree](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/tree/ss6.png)
![tree](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/tree/ss7.png)
![tree](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/tree/ss8.png)
![tree](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/tree/ss9.png)
![tree](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/tree/ss10.png)
![tree](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/tree/ss11.png)
![tree](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/tree/ss12.png)
![tree](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/tree/ss13.png)
![tree](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/tree/ss14.png)
![tree](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/tree/ss15.png)
![tree](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/tree/ss16.png)
![tree](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/tree/ss17.png)
![tree](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/tree/ss18.png)
![tree](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/tree/ss19.png)
![tree](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/tree/ss10.png)
![tree](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/tree/ss21.png)
![tree](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/tree/ss22.png)
![tree](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/tree/ss23.png)
![tree](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/tree/ss24.png)
![tree](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/tree/ss25.png)
![tree](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/tree/ss26.png)
![tree](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/tree/ss27.png)
![tree](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/tree/ss28.png)
![tree](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/tree/ss29.png)

## Explanation
In this illustration, we have nodes on three levels. Initially, we insert 39 at the leaf node of 40, then insert 38 in the same node. However, as the number of nodes exceeds two, we will shift the middle element to the top and 39 will move to its parent node (30). This is how we will keep inserting the elements till the end; you just need to make sure that all leaves come at the same height.

## 2-3 Deletion (Case #1)

## Deletion Algorithm
Deletion in 2-3 Trees is implemented based on the same scenarios we discussed in the last lesson but in the reverse order. The deletion algorithm also takes O(Logn)O(Logn) time and begins from the leaf node, just like an insertion. The deletion in 2-3 Trees is performed based on these scenarios:

## Case 1: Element at Leaf
When the element which needs to be removed is present at the leaf node, we check how many keys are present in that node. The further divides the algorithm into two scenarios:

## Leaf node has more than one key
If the leaf of the element to be deleted has more than one key, then simply delete the element.

Example: See the following example where the node has more than one key.

![tree](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/tree/ss30.png)
![tree](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/tree/ss31.png)
![tree](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/tree/ss32.png)
![tree](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/tree/ss33.png)

## Leaf node only has one key
If the leaf node of the element to be removed has only one key, then we will have to adjust the keys of that sub-tree in such a way that it remains ordered and balanced. This condition is further divided into two scenarios:

## Any of the siblings has two keys
Siblings are the other adjacent leaf nodes that share the same parent. A node could have one or two siblings depending upon its position. Check how many keys are present at the left or right sibling nodes. If any of the siblings have more than one key, then your problem is solved. All you need to do is move an element from the sibling node to the parent node, and shift down a node from the parent to your node. This process is called Redistribution by Rotation and it can be performed in two ways:

Rotation from Left Sibling

In this case, we lend a key from the left sibling by shifting the key with the largest value up to the parent node; then we move the parent node key (most right) down to our node.

Rotation from Right Sibling

In this case, we lend a key from the right sibling by shifting the key with the smallest value up to the parent node; then we move the parent node key (most left) down to our node.

![tree](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/tree/ee1.png)
![tree](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/tree/ee2.png)
![tree](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/tree/ee3.png)
![tree](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/tree/ee4.png)
![tree](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/tree/ee5.png)
![tree](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/tree/ee6.png)
![tree](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/tree/ee7.png)
![tree](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/tree/ee8.png)
![tree](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/tree/ee9.png)
![tree](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/tree/ee10.png)
![tree](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/tree/ee11.png)
![tree](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/tree/ee12.png)
![tree](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/tree/ee13.png)
![tree](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/tree/ee14.png)
![tree](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/tree/ee15.png)
![tree](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/tree/ee16.png)
![tree](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/tree/ee17.png)
![tree](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/tree/ee18.png)
![tree](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/tree/ee19.png)
![tree](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/tree/ee20.png)
![tree](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/tree/ee21.png)
![tree](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/tree/ee22.png)

## No sibling has more than one key
* In the case when none of the siblings have more than one key, we have no other option but to merge the two nodes by rotation of keys. So we merge two child nodes into one node by rotating elements accordingly. This process is called Merge by Rotation.
* If there’s a case where the child nodes have more than one key, we shift an element from the child node to make it the parent node. When we are left with only one key at each child node, then we are bound to delete the node.

![tree](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/tree/ee23.png)
![tree](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/tree/ee24.png)
![tree](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/tree/ee25.png)
![tree](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/tree/ee26.png)
![tree](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/tree/ee27.png)
![tree](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/tree/ee28.png)
![tree](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/tree/ee29.png)
![tree](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/tree/ee30.png)

## 2-3 Deletion (Case #2)

## Case 2: Element at Internal Node
Deletion is always performed at the leaf. So, whenever we need to delete a key at the internal node, we swap the key with any of its in-order successors; somehow we make it shift to any leaf node, as deletion is always performed at the leaf. Shift the element at the leaf node and then delete it. The element to be deleted can be swapped by either of the following:
* an element with the largest key on the left
* an element with the smallest key on the right

This is applicable when the child node has more than one key stored at the node. If there is only one value at the child node, then you are bound to swap the parent with whatever value the child node has.

## Example
See the following illustration which covers the two scenarios that we discussed above:

![tree](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/tree/eee1.png)
![tree](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/tree/eee2.png)
![tree](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/tree/eee3.png)
![tree](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/tree/eee4.png)
![tree](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/tree/eee5.png)
![tree](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/tree/eee6.png)
![tree](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/tree/eee7.png)
![tree](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/tree/eee8.png)
![tree](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/tree/eee9.png)
![tree](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/tree/eee10.png)
![tree](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/tree/eee11.png)
![tree](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/tree/eee12.png)
![tree](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/tree/eee13.png)
![tree](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/tree/eee14.png)
![tree](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/tree/eee15.png)
![tree](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/tree/eee16.png)
![tree](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/tree/eee17.png)
![tree](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/tree/eee18.png)
![tree](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/tree/eee19.png)
![tree](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/tree/eee20.png)

## 2-3-4 Trees

![tree](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/tree/eee21.png)

![tree](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/tree/eee22.png)

## Example
Given below is an example of 2-3-4 Trees. The insertion/deletion is performed in the same way as we did in 2-3 Trees, keeping in mind the fact that nodes in 2-3-4 Trees are allowed to have three keys at a time instead of two.

![tree](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/tree/eee23.png)


