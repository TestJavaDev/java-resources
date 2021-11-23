---
layout: default
title: Challenge 4
parent: Stack_Queues
grand_parent: Data Structures
nav_order: 4
permalink: /data_structures/stack_queues/ch4
---
<div align="center" markdown="1">
Challenge 4 / Java resources / Tutorial

{: .fs-8 .fw-400 }
</div>

## Challenge 4: Implement Queue using Stack

Can you implement a queue using a built-in stack? A solution is placed in the "solution" section to help you, but we would suggest you try to solve it on your own first.

## Problem Statement 
In this problem, you have to implement enqueue() and dequeue(), and use a built-in Stack to insert or remove value to and from the queue. An illustration is also provided for your understanding.

## Method Prototype 
void enqueue(int value)
int dequeue() 

## Input/Output 
* enqueue()
   * Input: an integer
   * Output: returns true after inserting value in the queue
* dequeue()
   * Input: an integer
   * Output: returns true after removing value from the queue

![stack](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/stack/tt4.png)

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

class QueueWithStack <V> {

    public QueueWithStack(int maxSize){
        // Write -- Your -- Code
    }
  
    public void enqueue(V value){
      	// Write -- Your -- Code 
    }
    public V dequeue(){
		// Write -- Your -- Code
        return null;
    }
    public boolean isEmpty(){
        //Write -- Your -- Code
        return false;
    }
}
{% endhighlight %}

## Solution Review: Implement Queue using Stack

## Solution 1: Optimized dequeue() operation

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
        array = (V[]) new Object[maxSize];//type casting Object[] to V[]
        this.currentSize = 0;
		this.top = -1;
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

class QueueWithStack <V> {
	//We can use 2 stacks for this purpose, stack1 to store original values
	//and stack2 which will help in dequeue operation.
    Stack<V> stack1;
    Stack<V> stack2;

    public QueueWithStack(int maxSize){
        stack1 = new Stack<>(maxSize);
        stack2 = new Stack<>(maxSize);
    }
    public boolean isEmpty(){
      return stack1.isEmpty();
    }
    public void enqueue(V value){
        stack1.push(value);
    }
    public V dequeue(){
        //Traverse stack1 and pop all elements in stack2
        while (!stack1.isEmpty()){
            stack2.push(stack1.pop());
        }
        //pop from stack2 (which was at the end of stack1)
        V result = stack2.pop();
        //put all elements back in stack1
        while (!stack2.isEmpty()){
            stack1.push(stack2.pop());
        }
        return result;
    }

}

class CheckQueueWithStack {

  public static void main(String args[]) {
    
    QueueWithStack<Integer> queue = new QueueWithStack<Integer>(5);
    
    queue.enqueue(1);
    queue.enqueue(2);
    queue.enqueue(3);
    queue.enqueue(4);
    queue.enqueue(5);
  
    System.out.println(queue.dequeue());
    System.out.println(queue.dequeue());
    System.out.println(queue.dequeue());
    System.out.println(queue.dequeue());
    System.out.println(queue.dequeue());
    System.out.println(queue.dequeue()); //this will output null because queue will be empty
  }
  
}
{% endhighlight %}

## Explanation 
In this approach, we use two stacks. The stack1 stores the queue elements while the stack2 acts as a temporary buffer to provide queue functionality.

The enqueue operation simply pushes the element at the top of stack1. This is the first element in the stack.

We make sure that whenever a dequeue operation takes place, we first put all the values of stack1 into stack2 by using stack2.push(stack1.pop()). Doing this inverts the stack1. Now, the last element lies at the top of stack2. Then, we simply pop() the first element from stack2 and save it in a variable called result to be returned later. Before method returns, stack2 is emptied back into stack1.

We can observe that the meat of the implementation lies in dequeue, making it the costlier operation.

## Time Complexity 
Whenever a value is dequeued, all the elements are transferred to stack2 and then back to stack1. Hence, for n elements in our queue, the runtime complexity of the dequeue operation is O(n)O(n).

The enqueue operation takes constant time, i.e, O(1).

Note: This solution is optimized for enqueue() but not for dequeue(). Therefore, we will improve upon it in the next solution.

## Solution 2: Optimizing both enqueue() and dequeue()


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
    public Stack(int maxSize) {
        this.maxSize = maxSize;
        array = (V[]) new Object[maxSize];//type casting Object[] to V[]
        this.currentSize = 0;
		this.top = -1;
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

class QueueWithStack <V> {
	//We can use 2 stacks for this purpose, stack1 to store original values
	//and stack2 which will help in dequeue operation.
    Stack<V> stack1;
    Stack<V> stack2;

    public QueueWithStack(int maxSize){
        stack1 = new Stack<>(maxSize);
        stack2 = new Stack<>(maxSize);
    }
    public boolean isEmpty(){
      return (stack1.isEmpty() && stack2.isEmpty());
    }
    public void enqueue(V value){
        stack1.push(value);
    }
    public V dequeue(){
        //return null if both the stacks are empty 
        if (isEmpty()){
          return null;
        }
        else if (stack2.isEmpty()){ 
          //if stack2 is empty, we pop all the elements
			    //from stack1 and push them to the stack2
          while(!stack1.isEmpty()){
            stack2.push(stack1.pop());
          }
          //finally, we return the top of stack2
          return stack2.pop();
        }
        else{ 
          //if none of the above conditions are true
          //we will simply return the top of stack2
          return stack2.pop();
        }
    }

}

class CheckQueueWithStack {

  public static void main(String args[]) {
    
    QueueWithStack<Integer> queue = new QueueWithStack<Integer>(5);
    
    queue.enqueue(1);
    queue.enqueue(2);
    queue.enqueue(3);
    queue.enqueue(4);
    queue.enqueue(5);
  
    System.out.println(queue.dequeue());
    System.out.println(queue.dequeue());
    System.out.println(queue.dequeue());
    System.out.println(queue.dequeue());
    System.out.println(queue.dequeue());
    System.out.println(queue.dequeue()); //this will output null because queue will be empty
  }
  
}
{% endhighlight %}

## Explanation 
The solution above follows a simple algorithm. We make use of two stacks, i.e., stack1 and stack2.

For the enqueue operation, value is pushed on to the stack1 on line 15. Hence, the enqueue operation takes a constant amount of time to execute.

On the other hand, in the dequeue operation, we check if both the stacks are empty on line 19. If they are empty, null is returned on line 20. On line 22, we check if stack2 is empty using the isEmpty() method from the Stack class. If the method returns true, execution jumps to the while loop on line 25. All the elements are popped from the stack1 and pushed to stack2. On line 29, the top is popped from stack2 and returned from the dequeue operation.

If the conditions on line 19 and line 22 evaluate to false, the top value is popped from the stack2 and returned.

## Time Complexity 
This solution is more optimized than the previous one, as the transfer of elements between stacks takes place only if stack2 is empty. Most of the time, we will be doing stack2.pop() from the else clause, which is O(1). Occasionally, we will find stack2 empty and pop elements over from stack1 onto stack2. But once we’ve done that, stack2 is no longer empty, and we’d be going to the else clause again with the O(1)O(1) time complexity. Therefore, the amortized complexity of the dequeue operation becomes O(1). While the time complexity for the enqueue operation is O(1) as well.

Note: We use amortized complexity analysis with data structures that have a state which persists between operations. So, a costly operation will change the state such that it will take a long time for the worst-case to happen again, which amortizes its cost.



