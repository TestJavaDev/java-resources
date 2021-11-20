---
layout: default
title: Arrays
parent: Data Structures
grand_parent: Data Structures and Algorithms
nav_order: 2
permalink: /data_structures/structures/arrays
---
<div align="center" markdown="1">
Arrays / Java resources / Tutorial

{: .fs-8 .fw-400 }
</div>

## Arrays

## What is an Array?

In this lesson, we will revise the basic concepts of Arrays and go through some practical examples to get a grip over this simple yet powerful data structure.

## Introduction 
An array also referred to as a collection of elements, is the simplest and most widely used Data Structure. Most of the Data Structures (e.g.Stack and Queue) were derived using the Array structure, which is why it is known as one of the central building blocks of Data Structures. These Data Structures will be discussed later in the coming chapters. The purpose of an Array is to group similar kinds of data for fast access.

Look at the figure below; we have made a simple array with four elements. Each item in the collection is called a Data Element, and the number of data elements stored in an Array is known as its size. You can see that each data element has a maximum of two neighbors, except the first and last one.

![arr](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/arr/arr1.png)

## Array Indexing
Each data element is assigned a numerical value called the index, which corresponds to the position of that item in the array. It is important to note that the value of the index is non-negative and always starts from zero. So the first element of an array will be stored at index 0 and the last one at index size-1.

An index makes it possible to access the contents of the array directly. Otherwise, we would have to traverse through the whole array to access a single element. That is the key feature that differentiates Arrays from Linked lists (we will cover them in the next chapter).

## Types of Arrays
Arrays can store primitive data-type values (e.g., int, char, floats, boolean, byte, short, long, etc.), non-primitive data-type values (e.g., Java Objects, etc.) or it can even hold references of other arrays. That divides the arrays into two categories:
* One Dimensional Array
* Multi-Dimensional Array

In primitive array, values are stored in a contiguous memory location. Whereas, in the non-primitive array, objects are stored in the heap segment.

## One-Dimensional Array
The basic syntax for declaring and initializing the one-dimensional array is given below:

## Array Declaration
In the array declaration, reference of an array is created. To declare an array, you have to specify the data type and name of the array.

![arr](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/arr/arr2.png)

![arr](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/arr/arr3.png)

## Two Dimensional Arrays

## Introduction
As discussed earlier, arrays can also store references as values. These references can point to anything. They can be a reference to an object or any other data structure. Before we move forward, let’s briefly discuss what pointers are:
* References are used to explicitly store memory locations that hold a value or an object.
* Any time you build an object in Java, you basically create a reference to that object.

## Two Dimensional Arrays
A Two Dimensional Array is an array of references that holds references to other arrays. These arrays are preferably used if you want to put together data items in a table or matrix-like structure. Matrices are widely used in the field of Game Development, where you are required to store and update the location of the player at each second.

Take a look at the figure below to get a good understanding of what a Two Dimensional Array looks like:

![arr](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/arr/arr4.png)

Explanation: If we take a look at the structure of the Two Dimensional Array, we get the idea that a Two Dimensional Array is basically an array of One Dimensional Array; in other words, every element points to the first element of a different One Dimensional Array.

It is important to note that in 2D arrays, all values must have the same data type. This means that you can’t store an array of integers next to an array of strings and vice versa. For example, if one array is declared of type int, then its pointer can’t point to the string type array. Each element must be of the same data type.

## Example 1: Student’s Records

Let’s say there’s a class of 30 students, and we want to store their grades for each of their courses (six courses in total). Is there a way we can map all this information using the knowledge we have covered so far? Yes, we can!

All we need to do is to keep the first column(i.e., Column 0), fixed for students, and the rest of the columns to store grades. We will have to follow a specific order to make sure the scores and students don’t get mixed up. Each element of the first column will hold a reference to an array containing marks of the student. So, there will be 30 rows and 6 columns. Now we can calculate the student’s percentage, class average, and the student’s position.

![arr](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/arr/arr5.png)

## Three Dimensional Arrays
Just like Two Dimensional Arrays, we can also design Three Dimensional Arrays. These arrays are an extension to 2D Arrays but are slightly more complex as they have one additional feature. Now the values in the cell will also hold a reference to some object, any primitive type value, or any other data structure.

You can use 3D Arrays if you want to assemble your data in a “cube-like” structure. These arrays are indexed by three variables, one for each dimension.
