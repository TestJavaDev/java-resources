---
layout: default
title: Challenge 5
parent: Stack_Queues
grand_parent: Data Structures
nav_order: 5
permalink: /data_structures/stack_queues/ch5
---
<div align="center" markdown="1">
Challenge 5 / Java resources / Tutorial

{: .fs-8 .fw-400 }
</div>

## Challenge 5: Sort the Values in a Stack

## Problem Statement 
In this problem, you have to implement the void sortStack(Stack<Integer> stack) method, which will take an Integer type stack and sort all its elements in ascending order. An illustration is also provided for your understanding.

## Method Prototype 
void sortStack(Stack<Integer> stack)

## Output 
It returns an Integer type Stack with all its elements sorted in ascending order

## Sample Input 
stack = {23,60,12,42,4,97,2}

## Sample Output 
result = {2,4,12,23,42,60,97}

![stack](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/stack/tt5.png)

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
    public Stack(int max_size) {
        this.maxSize = max_size;
        this.top = -1; //initially when stack is empty
        array = (V[]) new Object[max_size];//type casting Object[] to V[]
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

class SortValuesChallenge {
    public static void sortStack(Stack<Integer> stack) {
        // Write -- Your -- Code
    }
}
{% endhighlight %}

## Solution Review: Sort the Values in a Stack

## Solution #1: Using a Temporary Stack

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
    public Stack(int max_size) {
        this.maxSize = max_size;
        this.top = -1; //initially when stack is empty
        array = (V[]) new Object[max_size];//type casting Object[] to V[]
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

class CheckSort {
    public static void sortStack(Stack<Integer> stack) {
        //1. Use a second tempStack.
        //2. Pop value from mainStack.
        //3. If the value is greater or equal to the top of tempStack, then push the value in tempStack
        //else pop all values from tempStack and push them in mainStack and in the end push value in tempStack and repeat from step 2.
        //till mainStack is not empty.
        //4. When mainStack will be empty, tempStack will have sorted values in descending order.
        //5. Now transfer values from tempStack to mainStack to make values sorted in ascending order.
        Stack<Integer> newStack = new Stack<>(stack.getMaxSize());
        while (!stack.isEmpty()) {
            Integer value = stack.pop();
            if (!newStack.isEmpty() && value >= newStack.top()) {
                newStack.push(value);
            } else {
                while (!newStack.isEmpty() && newStack.top() > value)
                    stack.push(newStack.pop());
                newStack.push(value);
            }
        }
        while (!newStack.isEmpty())
            stack.push(newStack.pop());
    }
    public static void main(String args[]) {

        Stack<Integer> stack = new Stack<Integer>(7);
        stack.push(2);
        stack.push(97);
        stack.push(4);
        stack.push(42);
        stack.push(12);
        stack.push(60);
        stack.push(23);
        sortStack(stack);
        while(!stack.isEmpty()){
            System.out.println(stack.pop());
        }
    }
}
{% endhighlight %}

## Explanation 
This solution takes an iterative approach towards the problem. We create a helper stack call newStack. Its job is to hold the elements of the stack in descending order.

The main functionality of the algorithm lies in the nested while loops. In the outer loop, we pop elements out of stack until it is empty. As long as the popped value is larger than the top value in tempStack, we can push it in.

The inner loop begins when stack.pop() gives us a value that is smaller than the top of newStack. All the elements (they are sorted) of newStack are shifted back to stack, and the value is pushed into newStack. This ensures that the bottom of newStack always holds the smallest value from the stack.

When stack becomes empty, all the elements are in newStack in descending order. Now we simply push them back into the stack, resulting in the whole stack being sorted in ascending fashion.

## Time Complexity 
The outer and inner loops both traverse all the n elements of the stack. Hence, the time complexity is O(n2).

## Solution #2: Recursive Sort

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
    Un-comment the line below and execute again to see the warning.
    */
    @SuppressWarnings("unchecked")
    public Stack(int max_size) {
        this.maxSize = max_size;
        this.top = -1; //initially when stack is empty
        array = (V[]) new Object[max_size];//type casting Object[] to V[]
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

class CheckSort {

  public static void insert(Stack<Integer> stack, int value) {
      if(stack.isEmpty()|| value < stack.top())
          stack.push(value);
      else{
          int temp = stack.pop();
          insert(stack,value);
          stack.push(temp);
      }
  }

  public static Stack<Integer> sortStack(Stack<Integer> stack) {
      if(!stack.isEmpty()) {
          int value = stack.pop();
          sortStack(stack);
          insert(stack,value);
      }
      return stack;
  }

    public static void main(String args[]) {

        Stack<Integer> stack = new Stack<Integer>(7);
        stack.push(2);
        stack.push(97);
        stack.push(4);
        stack.push(42);
        stack.push(12);
        stack.push(60);
        stack.push(23);
        sortStack(stack);
        while(!stack.isEmpty()){
              System.out.println(stack.pop());
          }
    }

}//end of class
{% endhighlight %}

## Explanation 
The idea is to pop out all the elements from the stack in one recursive call. Once the stack is empty, we will push back values in a sorted order using the insert function.

At each call, we receive a partially sorted stack in which we insert the value being popped out at that recursive call. If the value is smaller than the top element of the stack, we simply push it to the top.

Otherwise, we call insert again until we can find the appropriate place for the value in the stack.

As we are passing the reference of the stack in all the recursive calls, therefore; we are to pointing to the same stack throughout our recursive calls!

## Time Complexity
The sortStack function is recursively called on all n elements. In the worst case, there are n calls to insert for each element. This pushes the time complexity up to O(n2). However, unlike the first solution, we do not need to create another stack.



