---
layout: default
title: Challenge 7
parent: Stack_Queues
grand_parent: Data Structures
nav_order: 7
permalink: /data_structures/stack_queues/ch7
---
<div align="center" markdown="1">
Challenge 7 / Java resources / Tutorial

{: .fs-8 .fw-400 }
</div>

## Challenge 7: Next Greater Element using Stack

Can you implement a method to find the next greater element after any given element from the stack? A solution is placed in the "solution" section to help you, but we would suggest you try to solve it on your own first.

## Problem Statement 
In this problem, you have to implement int[] nextGreaterElement(int[] arr) method. For each element in an array, it finds the next greater element in that array.

Note: The next greater element is the first element towards the right, which is greater than the current element. For example, in the array [1, 3, 8, 4, 10, 5], the next greater element of 3 is 8, and the next greater element for 8 is 10. To keep it simple, the next greater element for the last or maximum value in the array is -1.

In each iteration, we only check the array elements appearing after the current element.

## Method Prototype 
int[] nextGreaterElement(int[] arr);
where arr is an Integer array

## Input 
The input is an integer array

## Output 
An array containing the next greater element of each element from the input array. For the maximum value in the array, the next greater value is -1.

## Sample Input 
arr = {4,6,3,2,8,1}

## Sample Output 
result = {6,8,8,8,-1,-1}

![stack](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/stack/tt11.png)

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

class NextGreaterChallenge {
    public static int[] nextGreaterElement(int[] arr) {
        int[] result = new int[arr.length];
        // Write -- Your -- Code
        return result;
    }
}
{% endhighlight %}

## Solution Review: Next Greater Element using Stack

## Solution: Stack Iteration

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

class NextGreaterChallenge {
    public static int[] nextGreaterElement(int[] arr) {
        int[] result = new int[arr.length];
        int resultIndex = 0;
        Stack<Integer> stack = new Stack<>(arr.length);
        // iterate for rest of the elements
        for (int i = arr.length - 1; i >= 0; i--) {
            if (!stack.isEmpty()) {
                while (!stack.isEmpty() && stack.top() <= arr[i]) {
                    stack.pop();
                }
            }
            if(stack.isEmpty()){
                result[i] = -1;
            }
            else
                result[i]  = stack.top();
            stack.push(arr[i]);
        }
        return result;
    }

	public static void main(String[] args) 
	{ 
    	int arr[] = {4,6,3,2,8,1,11}; 
		System.out.println(Arrays.toString(arr));
		int result[] = nextGreaterElement(arr); 
		System.out.println(Arrays.toString(result));
	} 
}
{% endhighlight %}

## Explanation 
Although this method can be solved by brute force using nested loops, a stack can do it much more efficiently.

Using the for-loop on line 7, we iterate the array from the last element to the first one. This is because, at every index, we will have access to the next greater element in the array, which will be present in the stack. Therefore, we just pop from the stack until we get the greater element on top of the stack on lines 8-12. After we have the next greater element on top of the stack, we simply update the value of the current index in the result array to the value of the top of the stack (line 17). In case the stack gets empty, we update the value of the current index in the result array to be -1. Finally, we return the result array from the function on line 20.

## Time Complexity 
In the above algorithm, it is observed that every element is pushed on the stack exactly once. Furthermore, since once an element is removed from the stack, it is never re-inserted, every element is removed exactly once, too. That means we perform one push and one pop operation per element, exactly. Therefore, the time complexity of this algorithm will be O(n). This is a significant improvement over the brute force method’s runtime complexity of O(n2).



