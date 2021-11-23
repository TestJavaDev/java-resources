---
layout: default
title: Challenge 3
parent: Stack_Queues
grand_parent: Data Structures
nav_order: 3
permalink: /data_structures/stack_queues/ch3
---
<div align="center" markdown="1">
Challenge 3 / Java resources / Tutorial

{: .fs-8 .fw-400 }
</div>

## Challenge 3: Reversing the First k Elements of a Queue

Can you reverse the first "k" elements in a given queue? A solution is placed in the "solution" section to help you, but we would suggest you try to solve it on your own first.

## Problem Statement 
In this problem, you have to implement the void reverseK(Queue<V> queue, int k) method; this will take a queue and any number (k) as input, and reverse the first k elements of the queue. An illustration is also provided for your understanding.

## Method Prototype 
void reverseK(Queue<V> queue, int k) 

## Output 
An array with the first “k” elements reversed.

## Sample Input 
Queue = {1,2,3,4,5,6,7,8,9,10}
k = 5

## Sample Output 
result = {5,4,3,2,1,6,7,8,9,10}

![stack](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/stack/tt3.png)

## Coding Exercise

{% highlight java %}
public class Queue<V> {
    private int maxSize;
    private V[] array;
    private int front;
    private int back;
    private int currentSize;

    /*
    Java does not allow generic type arrays. So we have used an
    array of Object type and type-casted it to the generic type V.
    This type-casting is unsafe and produces a warning.
    Comment out the line below and execute again to see the warning.
    */
    @SuppressWarnings("unchecked")
    public Queue(int maxSize) {
        this.maxSize = maxSize;
        array = (V[]) new Object[maxSize];
        front = 0;
        back = -1;
        currentSize = 0;
    }

    public int getMaxSize() {
        return maxSize;
    }

    public int getCurrentSize() {
        return currentSize;
    }

    public V top() {
        return array[front];
    }

    public boolean isEmpty() {
        return currentSize == 0;
    }

    public boolean isFull() {
        return currentSize == maxSize;
    }

    public void enqueue(V value) {
        if (isFull())
            return;
        back = (back + 1) % maxSize; //to keep the index in range
        array[back] = value;
        currentSize++;
    }

    public V dequeue() {
        if (isEmpty())
            return null;

        V temp = array[front];
        front = (front + 1) % maxSize; //to keep the index in range
        currentSize--;

        return temp;
    }
}

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

class ReverseKChallenge {
    public static <V> void reverseK(Queue<V> queue, int k) {
        // Write -- Your -- Code
    }
}
{% endhighlight %}

## Solution Review: Reversing the First k Elements of a Queue

## Solution: Using a queue

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

public class Queue<V> {
    private int maxSize;
    private V[] array;
    private int front;
    private int back;
    private int currentSize;

    /*
    Java does not allow generic type arrays. So we have used an
    array of Object type and type-casted it to the generic type V.
    This type-casting is unsafe and produces a warning.
    Comment out the line below and execute again to see the warning.
    */
    @SuppressWarnings("unchecked")
    public Queue(int maxSize) {
        this.maxSize = maxSize;
        array = (V[]) new Object[maxSize];
        front = 0;
        back = -1;
        currentSize = 0;
    }

    public int getMaxSize() {
        return maxSize;
    }

    public int getCurrentSize() {
        return currentSize;
    }

    public V top() {
        return array[front];
    }

    public boolean isEmpty() {
        return currentSize == 0;
    }

    public boolean isFull() {
        return currentSize == maxSize;
    }

    public void enqueue(V value) {
        if (isFull())
            return;
        back = (back + 1) % maxSize; //to keep the index in range
        array[back] = value;
        currentSize++;
    }

    public V dequeue() {
        if (isEmpty())
            return null;

        V temp = array[front];
        front = (front + 1) % maxSize; //to keep the index in range
        currentSize--;

        return temp;
    }
}

class CheckReverse {

    //1.Push first k elements in queue in a stack.
    //2.Pop Stack elements and enqueue them at the end of queue
    //3.Dequeue queue elements till "k" and append them at the end of queue   
    //4.Dequeue the remaining elements and enqueue them again to append them at end of the queue
    public static <V> void reverseK(Queue<V> queue, int k) {
        if (queue.isEmpty() || k <= 0)
            return;
        Stack<V> stack = new Stack<>(k);

        while(!stack.isFull())
            stack.push(queue.dequeue());

        while(!stack.isEmpty())
            queue.enqueue(stack.pop());

        int size = queue.getCurrentSize();
        for(int i = 0; i < size - k; i++)
            queue.enqueue(queue.dequeue());
    }
    public static void main(String args[]) {

        Queue<Integer> queue = new Queue<Integer>(10);
        queue.enqueue(1);
        queue.enqueue(2);
        queue.enqueue(3);
        queue.enqueue(4);
        queue.enqueue(5);
        queue.enqueue(6);
        queue.enqueue(7);
        queue.enqueue(8);
        queue.enqueue(9);
        queue.enqueue(10);

        reverseK(queue,5);

        System.out.print("Queue: ");
        while(!queue.isEmpty()) {
          System.out.print(queue.dequeue() + " ");
        }
    }
}

{% endhighlight %}

## Explanation 
reverseK(queue, k) takes queue as an input parameter, where k represents the number of elements we want to reverse.

Now, moving on to the actual logic of the method. First, check if the queue is empty or if k is a valid non-zero positive number. If either of them is false, then do nothing, just return.

If none of the conditions given above are true, then create a Stack. Start removing first k values from the queue and push them to the stack by using stack.push(queue.dequeue).

Once all the k values have been pushed to the stack, start popping them and enqueueing them to the back of the queue sequentially. We will do this using queue.enqueue(stack.pop()). At the end of this step, we will be left with an empty stack, and the k reversed elements will be appended to the back of the queue.

Now we need to move these reversed elements to the front of the queue. To do this, we used queue.enqueue(queue.dequeue()). Each element is first dequeued from the back.

## Time Complexity 
Overall, kk elements are dequeued, pushed to the stack, popped from it, and then enqueued. Additionally, n-kn−k elements are dequeued and enqueued to the queue. Each push, pop, enqueue, or dequeue operation takes constant time; the time complexity of this method is O(n) as all nn elements have to be processed with constant-time​ operations.



