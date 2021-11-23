---
layout: default
title: Challenge 2
parent: Stack_Queues
grand_parent: Data Structures
nav_order: 2
permalink: /data_structures/stack_queues/ch2
---
<div align="center" markdown="1">
Challenge 2 / Java resources / Tutorial

{: .fs-8 .fw-400 }
</div>

## Challenge 2: Implement Two Stacks using one Array

Can you implement two stacks using a single array? A solution is placed in the "solution" section to help you, but we would suggest you try to solve it on your own first

## Problem Statement 
In this problem, using a single array to store elements, you have to implement the class TwoStacks<V>, having the following methods to generate two stacks. An illustration is also provided for your understanding.

## Method Prototypes 
* void push1(V value)
* void push2(V value)
* public V pop1()
* public V pop2()

## Input/Output 
* push1(input)
   * Input: an integer
   * Output: inserts the given value in the first stack i.e. stack1
* push2(input)
   * Input: an integer
   * Output: inserts the given value in the second stack i.e stack2
* pop1()
   * Output: returns and remove the top value of stack1
* pop2()
   * Output: returns and remove the top value of stack2

![stack](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/stack/tt2.png)

## Coding Exercise

{% highlight java %}
class TwoStacks<V> {
    private int maxSize;
    private V[] array;

    @SuppressWarnings("unchecked")
    public TwoStacks(int max_size) {
        this.maxSize = max_size;
        array = (V[]) new Object[max_size];//type casting Object[] to V[]
    }

    //insert at top of first stack
    public void push1(V value) {
    
    }

    //insert at top of second stack
    public void push2(V value) {

    }

    //remove and return value from top of first stack
    public V pop1() {
        return null;
    }

    //remove and return value from top of second stack
    public V pop2() {
        return null;
    }
}
{% endhighlight %}

## Solution Review: Implement Two Stacks using one Array

## Solution: Stacks on opposite ends

{% highlight java %}
//You can either divide array in two halves or start stacks at extreme ends.
//We'll use the second technique to solve this problem.
//Top of Stack 1 start from extreme left of array i.e top1 = 0;
//Top of Stack 2 start from extreme right of array i.e top2 = size - 1
public class TwoStacks<V> {
    private int maxSize;
    private int top1, top2; //Store top value indices of Stack 1 and Stack 2
    private V[] array;

    @SuppressWarnings("unchecked")
    public TwoStacks(int max_size) {
        this.maxSize = max_size;
        this.top1 = -1;
        this.top2 = max_size;
        array = (V[]) new Object[max_size];//type casting Object[] to V[]
    }

    //insert at top of first stack
    public void push1(V value) {
        if (top1 < top2 - 1) {
            array[++top1] = value;
        }
    }

    //insert at top of second stack
    public void push2(V value) {
        if (top1 < top2 - 1) {
            array[--top2] = value;
        }
    }

    //remove and return value from top of first stack
    public V pop1() {
        if (top1 > -1) {
            return array[top1--];
        }
        return null;
    }

    //remove and return value from top of second stack
    public V pop2() {
        if (top2 < maxSize) {
            return array[top2++];
        }
        return null;
    }
}

class CheckTwoStacks {
    public static void main(String args[]) {
        TwoStacks<Integer> tS = new TwoStacks<Integer>(5);
        tS.push1(11);
        tS.push1(3);
        tS.push1(7);
        tS.push2(1);
        tS.push2(9);

        System.out.println(tS.pop1());
        System.out.println(tS.pop2());
        System.out.println(tS.pop2());
        System.out.println(tS.pop2());
        System.out.println(tS.pop1());
    }  
}
{% endhighlight %}

## Explanation 
This implementation is space-efficient as it utilizes all of the available space. It doesn’t cause an overflow if there is any space available in the array. The tops of the two stacks are the two extreme ends of the array. The first stack starts from the first element at index 0, and the second starts from the last element. The first element in stack2 is pushed at index (maxSize-1). Both stacks grow (or shrink) in the opposite direction. To check for overflow, all we need do is check for space between the top elements of both stacks, as reflected in the code.

## Time Complexity 
All the operations take constant time, i.e., O(1) because the array is being indexed and not resized.


