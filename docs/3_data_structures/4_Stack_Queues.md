---
layout: default
title: Stack_Queues
parent: Data Structures
nav_order: 4
permalink: /data_structures/stack_queues
has_children: true
---
<div align="center" markdown="1">
Stack_Queues / Java resources / Tutorial

{: .fs-8 .fw-400 }
</div>

## What is a Stack?

Introduction #
We are all familiar with the famous Undo option, which is present in almost every application. Have you ever wondered how it works? The idea is that you store the previous states of your work (which are limited to a specific number), in the memory in such an order that the last one appears first. This can’t be done just by using arrays, which is why the Stack comes in handy.

You can think of the Stack as a container, in which we can add items and remove them. Only the top of this container is open, so the item we put in first will be taken out last, and the items we put in last will be taken out first. This is called the last in first out (LIFO) ordering.

A real-life example of a Stack can be a pile of books placed in a vertical order. So, to get the book that’s somewhere in the middle, you need to remove all the books placed on top of it. That is how the LIFO method works. The following figure illustrates a Stack:

![stack](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/stack/st1.png)

What are Stacks Used for? #
A stack is one of the most fundamental data structures. Its implementation is very simple, yet it can be used to solve complex problems!

There are many computer algorithms like Depth First Search and Expression Evaluation Algorithm, etc., which are dependent on stacks to run perfectly. Stacks are used for the below actions:

To backtrack to the previous task/state, e.g., in a recursive code

To store a partially completed task, e.g., when you are exploring two different paths on a Graph from a point while calculating the smallest path to the target.

How do stacks work? #
A Stack can be implemented in many ways, but a typical Stack must offer the following functionalities:

![stack](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/stack/st2.png)

The entire functionality of a stack depends on the push and pop methods listed in the table. The following animation shows how to push elements in the given stack and then pop them off.

![stack](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/stack/st3.png)
![stack](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/stack/st4.png)
![stack](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/stack/st5.png)
![stack](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/stack/st6.png)
![stack](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/stack/st7.png)
![stack](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/stack/st8.png)
![stack](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/stack/st9.png)
![stack](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/stack/st10.png)
![stack](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/stack/st11.png)
![stack](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/stack/st12.png)

Explanation #
When you insert an element into the stack, the variable that stores the position of the top element would be pointing to the number below it. So, you will have to update its value every time you insert a new element into the stack. Similarly, the value of the top variable will also change when you delete an element from the stack. It’s a good practice to update the top variable first, and then perform the operation; otherwise, the variable would be pointing to nothing or a wrong value in case of insertion.

## Stack (Implementation)

Introduction #
Every programming language comes with the basic functionality of Stack. In Java, you can use the pre-built class of Stack by importing it to your program. However, you can manually implement a stack and extend its functionality for your use.

Stacks can either be implemented using arrays or linked lists. It has yet to be concluded which implementation is more efficient, as both data structures offer different variations of Stack. However, stacks are generally implemented using arrays because it takes less space; we don’t need to store an additional pointer like in a linked list.

Implementation #
As we discussed in the previous lesson, a typical Stack must contain the following standard methods:

push (datatype V)
datatype pop()
boolean isEmpty()
datatype top()
Before we take a look at these methods one by one, let’s construct a class of Stack, and create an instance. This class has the following three data members:

the array that will hold all the elements
the size of this array
a variable for the top element of Stack.
The following code shows how to construct the Stack class:

{% highlight java %}
public class Stack <V> {
    private int maxSize;
    private int top;
    private V arr[];

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
        arr = (V[]) new Object[max_size];//type casting Object[] to V[]
    }
    public int getCapacity() {
        return maxSize;
    }

}

class StackDemo {
    public static void main( String args[] ) {
        Stack<Integer> stack = new Stack<Integer>(10);
        System.out.print("You have successfully created a Stack!");
    }
}
{% endhighlight %}

Now before adding the push and pop methods into this code, we need to implement some helper methods to keep the code simple and reusable. Here’s a list of the helper methods that we will implement in the code below:

isEmpty()
isFull()
top()
Here is the code for stacks with the new helper methods. Try experimenting with them!

{% highlight java %}
public class Stack <V> {
    private int maxSize;
    private int top;
    private V array[];

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
    }

    //returns the maximum size capacity
    public int getMaxSize() {
        return maxSize;
    }

    //returns true if Stack is empty
    public boolean isEmpty(){
        return top == -1;
    }

    //returns true if Stack is full
    public boolean isFull(){
        return top == maxSize -1;
    }

    //returns the value at top of Stack
    public V top(){
        if(isEmpty())
            return null;
        return array[top];
    }
}

class HelloWorld {
    public static void main( String args[] ) {
        Stack<Integer> stack = new Stack<Integer>(10);
				
        //output if stack is empty or not
        if(stack.isEmpty())
        System.out.print("Stack is empty");
        else
        System.out.print("Stack is not empty");
        
        System.out.printf("%n");
        
        //output if stack is full or not
        if(stack.isFull())
        System.out.print("Stack is full");
        else
        System.out.print("Stack is not full");
    }
}
{% endhighlight %}

If your output returns true for isEmpty() and false for isFull(), it means that these helper functions are working properly! Now, take a look at this extended code with push and pop functions added to the definition of Stack class. We will try to add and remove some elements from this stack by using these two functions. Let’s get to it!

{% highlight java %}
public class Stack <V> {
    private int maxSize;
    private int top;
    private V array[];

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
    }

    //returns the maximum size capacity
    public int getMaxSize() {
        return maxSize;
    }

    //returns true if Stack is empty
    public boolean isEmpty(){
        return top == -1;
    }

    //returns true if Stack is full
    public boolean isFull(){
        return top == maxSize -1;
    }

    //returns the value at top of Stack
    public V top(){
        if(isEmpty())
            return null;
        return array[top];
    }

    //inserts a value to the top of Stack
    public void push(V value){
        if(isFull()) {
            System.err.println("Stack is Full!");
            return;
        }
        array[++top] = value; //increments the top and adds value to updated top
    }

    //removes a value from top of Stack and returns
    public V pop(){
        if(isEmpty())
            return null;
        return array[top--]; //returns value and top and decrements the top
    }

}

class StackDemo {
	public static void main(String[] args) {
    
		Stack<Integer> stack = new Stack<Integer>(5); 
        System.out.print("Elements pushed in the Stack: ");
        for (int i = 0; i < 5; i++) {
            stack.push(i); //pushes 5 elements (0-4 inclusive) to the stack
            System.out.print(i + " ");
        }
        System.out.println("\nIs Stack full? \n" + stack.isFull());
        System.out.print("Elements popped from the Stack: ");
        for (int i = 0; i < 5; i++) {
            System.out.print(stack.pop()+" "); //pops all 5 elements from the stack and prints them
        }
        System.out.println("\nIs Stack empty? \n" + stack.isEmpty());

	}//end of main 
}
{% endhighlight %}

If you look at the output of the code, you can see that the elements popped out of the stack in the exact reverse order as they were pushed in. That means our Stack works perfectly.

Complexities of Stack Operations #
Let’s look at the time complexity of each stack operation.

![stack](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/stack/st13.png)

## What is a Queue?

Introduction #
Similar to Stack, Queue is another linear data structure that stores the elements in a sequential manner. The only significant difference between Stack and Queue is that instead of using the LIFO principle, Queue implements the FIFO method, which is short for First in First Out.

According to FIFO, the first element inserted is the one that comes out first. You can think of a queue as a pipe with both ends open. Elements enter from one end (back) and leave from the other (front). The following animation illustrates the structure of a queue.

![stack](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/stack/st14.png)
![stack](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/stack/st15.png)
![stack](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/stack/st16.png)
![stack](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/stack/st17.png)
![stack](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/stack/st18.png)
![stack](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/stack/st19.png)
![stack](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/stack/st20.png)
![stack](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/stack/st21.png)
![stack](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/stack/st22.png)
![stack](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/stack/st23.png)
![stack](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/stack/st24.png)
![stack](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/stack/st25.png)
![stack](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/stack/st26.png)
![stack](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/stack/st27.png)
![stack](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/stack/st28.png)
![stack](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/stack/st29.png)
![stack](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/stack/st30.png)
![stack](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/stack/st31.png)

Queues are slightly trickier to implement compared to stacks, as we have to keep track of both ends of the array. The elements are inserted from the back and removed from the front.

A perfect real-life example of Queue is a line of people waiting to get a ticket from the booth. If a new person comes, he will join the line from the end; meanwhile, the person standing at the front will be the first to get the ticket and leave the line.

What are Queues used for? #
Most operating systems also perform operations based on a Priority Queue—a kind of queue that allows operating systems to switch between appropriate processes. They are also used to store packets on routers in a certain order when a network is congested. Implementing a cache also heavily relies on queues. We generally use queues in the following situations:

We want to prioritize something over another
A resource is shared between multiple devices (e.g., Web Servers and Control Units)
How does a Queue work? #
A typical queue contains the following set of methods to work perfectly:

![stack](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/stack/st32.png)

The entire functionality of Queue depends on the enqueue and dequeue methods; the rest are just helper methods to produce simple, understandable code.

Example #
Take a look at the animation below to understand the working of a Queue. The variables that store the positions of front and back of the array will have to be updated accordingly whenever you will enqueue or dequeue an element from the queue.

![stack](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/stack/t1.png)
![stack](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/stack/t2.png)
![stack](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/stack/t3.png)
![stack](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/stack/t4.png)
![stack](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/stack/t5.png)
![stack](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/stack/t6.png)
![stack](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/stack/t7.png)
![stack](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/stack/t8.png)
![stack](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/stack/t9.png)
![stack](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/stack/t10.png)
![stack](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/stack/t11.png)
![stack](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/stack/t12.png)
![stack](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/stack/t13.png)
![stack](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/stack/t14.png)
![stack](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/stack/t15.png)
![stack](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/stack/t16.png)
![stack](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/stack/t17.png)
![stack](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/stack/t18.png)
![stack](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/stack/t19.png)

Types of Queues #
There are three common types of queues which cover a wide range of problems:

Linear Queue
Circular Queue
Priority Queue
The queue that we have discussed so far was Linear Queue. Let’s look at the last two types and see how they are different from the Linear Queue.

Circular Queue: #
Circular Queues are almost similar to Linear Queues with only one exception. As the name itself suggests, circular queues are circular in the structure; this means that both ends are connected to form a circle. Initially, the front and rear parts of the queue point to the same location and eventually move apart as more elements are inserted into the queue. Circular queues are generally used in the following ways:

Simulation of objects
Event handling (do something when a particular event occurs)
The following illustration shows how circular queues work.

![stack](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/stack/t20.png)
![stack](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/stack/t21.png)
![stack](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/stack/t22.png)
![stack](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/stack/t23.png)
![stack](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/stack/t24.png)
![stack](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/stack/t25.png)
![stack](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/stack/t26.png)
![stack](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/stack/t27.png)
![stack](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/stack/t28.png)

Priority Queue #
In Priority Queues, elements are sorted in a specific order. Based on that order, the most prioritized object appears at the front of the queue, the least prioritized object appears at the end, and so on. These queues are widely used in an operating system to determine which programs should be given more priority.

## Queue (Implementation)

Implementation of Queues #
Queues are implemented in many ways. They can be represented by using an array, a linked list, or even a stack. That being said, an array is most commonly used because it’s the easiest way to implement Queues. As discussed in the previous lesson, a typical Queue must contain the following standard methods:

enqueue (datatype V)
datatype dequeue()
boolean isEmpty()
boolean isFull()
datatype top()
Before we take a look at these methods one by one, let’s construct a Queue class with an integer data type and create an instance. We will make a class with 5 data members to hold the following information:

The array that will contain all the elements
The maxSize is the size of this array
The front element of the Queue
The back element of the Queue
The currentSize of elements in the Queue
The code given below shows how to construct the Queue class:

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

}

class QueueDemo {
 
	public static void main(String[] args) {
		Queue<Integer> queue = new Queue<Integer>(5);
        System.out.print("You have successfully created a Queue!");
	}
}
{% endhighlight %}

Adding Helper Functions #
Now before adding the enqueue and dequeue methods into this class, we need to implement some helper methods to keep the code simple and understandable. Here’s the list of helper functions that we will implement in the code below:

isEmpty()
isFull()
top()
Now run the following code and see if the helper function outputs correctly.

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

    public boolean isEmpty() {
        return currentSize == 0;
    }

    public boolean isFull() {
        return currentSize == maxSize;
    }

    public V top() {
        return array[front];
    }

}

class QueueDemo {
	public static void main(String[] args) {
		Queue<Integer> queue = new Queue<Integer>(5); //create the queue
    
        if(queue.isEmpty())
        System.out.print("Queue is empty.");
        else
        System.out.print("Queue is not empty.");
        
        System.out.printf("%n");
        
        if(queue.isFull())
        System.out.print("Queue is full.");
        else
        System.out.print("Queue is not full.");
	}
}
{% endhighlight %}

For the above code, isEmpty() should return true and isFull() should return false. Now, we will extend this code with the enqueue and dequeue methods to add and remove elements, respectively.

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

    public boolean isEmpty() {
        return currentSize == 0;
    }

    public boolean isFull() {
        return currentSize == maxSize;
    }

    public V top() {
        return array[front];
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

class QueueDemo {
	public static void main(String[] args) {
		Queue<Integer> queue = new Queue<Integer>(5);
		//equeue 2 4 6 8 10 at the end
        queue.enqueue(2);
		queue.enqueue(4);
		queue.enqueue(6);
		queue.enqueue(8);
		queue.enqueue(10);
        //dequeue 2 elements from the start
		queue.dequeue();
		queue.dequeue();
		//enqueue 12 and 14 at the end
        queue.enqueue(12);
        queue.enqueue(14);

        System.out.println("Queue:");
        while(!queue.isEmpty()){
                System.out.print(queue.dequeue()+" ");
            }
	}
}
{% endhighlight %}

If you look at the output of the code, you can see that the elements are enqueued in the back and dequeued from the front. This means that our queue works perfectly.

In the last few chapters, we discussed some fundamental data structures and went through their implementations. Soon, we will take a look at some advanced data structures which are mainly derived using the basic data structures that we have studied so far.
