---
layout: default
title: Challenge 10
parent: Stack_Queues
grand_parent: Data Structures
nav_order: 10
permalink: /data_structures/stack_queues/ch10
---
<div align="center" markdown="1">
Challenge 10 / Java resources / Tutorial

{: .fs-8 .fw-400 }
</div>

## Challenge 10: Create Stack where min() gives minimum in O(1)

## Problem Statement 
In this problem, you have to implement a new kind of stack called MinStack, which can get the minimum value in O(1) time. An illustration is also provided for your understanding.

Note: MinStack only deals with integer type values.

## Method Prototype: 
int min()

## Output: 
It returns the minimum number in O(1) time

![stack](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/stack/tt28.png)

## Coding Exercise

{% highlight java %}
 public class Stack<V> {
    private int maxSize;
    private int top;
    private V[] array;
    private int currentSize;

    /*
    Java does not allow generic type arrays. So we have used an
    array of Object type and type-casted it to the generic type V.
    This type-casting is unsafe and produces a warning.
    Comment out the line below and execute again to see the warning.
    */
    @SuppressWarnings("unchecked")
    public Stack(int maxSize) {
        this.maxSize = maxSize;
        this.top = -1; //initially when stack is empty
        array = (V[]) new Object[maxSize];//type casting Object[] to V[]
        this.currentSize = 0;
    }

    public int getCurrentSize() {
        return currentSize;
    }

    //returns the maximum size capacity
    public int getMaxSize() {
        return maxSize;
    }

    //returns true if Stack is empty
    public boolean isEmpty() {
        return top == -1;
    }

    //returns true if Stack is full
    public boolean isFull() {
        return top == maxSize - 1;
    }

    //returns the value at top of Stack
    public V top() {
        if (isEmpty())
            return null;
        return array[top];
    }

    //inserts a value to the top of Stack
    public void push(V value) {
        if (isFull()) {
            System.err.println("Stack is Full!");
            return;
        }
        array[++top] = value; //increments the top and adds value to updated top
        currentSize++;
    }

    //removes a value from top of Stack and returns
    public V pop() {
        if (isEmpty())
            return null;
        currentSize--;
        return array[top--]; //returns value and top and decrements the top
    }

}

public class MinStack {
    int maxSize;
    
    //constructor
    public MinStack(int maxSize) {
        // Write -- Your -- Code
        this.maxSize = maxSize;
    }
    //removes and returns value from stack
    public Integer pop(){
        // Write -- Your -- Code
        return Integer.MIN_VALUE;
    }
    //pushes value into the stack
    public void push(Integer value){
        // Write -- Your -- Code
    }
    //returns minimum value in O(1)
    public int min(){
		// Write -- Your -- Code
        return Integer.MIN_VALUE;
    }
}
{% endhighlight %}

## Solution Review: Create Stack where min() gives minimum in O(1)

## Solution: A Two Stack Class

{% highlight java %}
 public class Stack<V> {
    private int maxSize;
    private int top;
    private V[] array;
    private int currentSize;

    /*
    Java does not allow generic type arrays. So we have used an
    array of Object type and type-casted it to the generic type V.
    This type-casting is unsafe and produces a warning.
    Comment out the line below and execute again to see the warning.
    */
    @SuppressWarnings("unchecked")
    public Stack(int maxSize) {
        this.maxSize = maxSize;
        this.top = -1; //initially when stack is empty
        array = (V[]) new Object[maxSize];//type casting Object[] to V[]
        this.currentSize = 0;
    }

    public int getCurrentSize() {
        return currentSize;
    }

    //returns the maximum size capacity
    public int getMaxSize() {
        return maxSize;
    }

    //returns true if Stack is empty
    public boolean isEmpty() {
        return top == -1;
    }

    //returns true if Stack is full
    public boolean isFull() {
        return top == maxSize - 1;
    }

    //returns the value at top of Stack
    public V top() {
        if (isEmpty())
            return null;
        return array[top];
    }

    //inserts a value to the top of Stack
    public void push(V value) {
        if (isFull()) {
            System.err.println("Stack is Full!");
            return;
        }
        array[++top] = value; //increments the top and adds value to updated top
        currentSize++;
    }

    //removes a value from top of Stack and returns
    public V pop() {
        if (isEmpty())
            return null;
        currentSize--;
        return array[top--]; //returns value and top and decrements the top
    }
}

public class MinStack {
    int maxSize;
    Stack<Integer> mainStack;
    Stack<Integer> minStack;
    //constructor
    public MinStack(int maxSize) {
        //We will use two stacks mainStack to hold original values
        //and minStack to hold minimum values. Top of minStack will always
        //be the minimum value from mainStack
        this.maxSize = maxSize;
        mainStack = new Stack<>(maxSize);
        minStack = new Stack<>(maxSize);
    }
    //removes and returns value from stack
    public int pop(){
        //1. Pop element from minStack to make it sync with mainStack,
        //2. Pop element from mainStack and return that value
        minStack.pop();
        return mainStack.pop();
    }
    //pushes value into the stack
    public void push(Integer value){
        //1. Push value in mainStack and check value with the top value of minStack
        //2. If value is greater than top, then push top in minStack
        //else push value in minStack
        mainStack.push(value);
        if(!minStack.isEmpty() && minStack.top() < value)
            minStack.push(minStack.top());
        else
            minStack.push(value);
    }
    //returns minimum value in O(1)
    public int min(){
        return minStack.top();
    }
}

class CheckMinStack {
  public static void main(String args[]) {

    MinStack stack = new MinStack(6);
    stack.push(5);
    stack.push(2);
    stack.push(4);
    stack.push(1);
    stack.push(3);
    stack.push(9);

    System.out.println(stack.min());

    stack.pop();
    stack.pop();
    stack.pop();

    System.out.println(stack.min()); 

  }

}
{% endhighlight %}

This is a smart solution for obtaining the minimum value in a stack, yet, it isn’t a very tricky one.

The whole implementation relies on the existence of two stacks, minStack, and mainStack.

mainStack holds the actual stack with all the elements, whereas minStack is a stack whose top always contains the current minimum value in the stack.

How does it do this? The answer is in the push function. Whenever push is called, mainStack simply inserts the new value at the top. However, minStack checks the value being pushed. If minStack is empty, this value is pushed into it and becomes the current minimum. If minStack already has elements in it, the value is compared with the top element. If the value is lower than the top of minStack, it is pushed in and hence, becomes the new minimum. Otherwise, the top remains the same.

Due to all these safeguards we’ve put in place, the min function only needs to return the value at the top of minStack.

## Time Complexity 
Our goal was to create a stack that returns the minimum value in constant time. As we can see in the algorithm above, the min function truly works in O(1).




