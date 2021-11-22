---
layout: default
title: Challenge 8
parent: Stack_Queues
grand_parent: Data Structures
nav_order: 8
permalink: /data_structures/stack_queues/ch8
---
<div align="center" markdown="1">
Challenge 8 / Java resources / Tutorial

{: .fs-8 .fw-400 }
</div>

## Challenge 8: Solve a Celebrity Problem using a Stack

Problem Statement #
In this problem, you have to implement findCelebrity() method to find the celebrity in a party (matrix) using a stack. A celebrity is someone that everyone knows, but he/she doesn’t know anyone at the party.

Method Prototype: #
int findCelebrity(int[][] party,int numPeople);
Where the party is a reference variable storing a 2D matrix, which has stored all the information about acquaintances, numPeople and the number of people present in the party.

In the party matrix, a particular [row][col] stores acquaintance information for row and col. In other words, if [row][col] == 1, then it means row knows col, and if it’s zero, then it means row doesn’t know col. Remember that everyone knows a celebrity, but the celebrity doesn’t know the people at the party.

An illustration is also provided for your understanding.

Output: #
It will return - 1 if there is no celebrity in the party. Otherwise, it will return the ID or number of celebrities from the party matrix.

![stack](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/stack/tt12.png)

![stack](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/stack/tt13.png)
![stack](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/stack/tt14.png)
![stack](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/stack/tt15.png)
![stack](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/stack/tt16.png)
![stack](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/stack/tt17.png)
![stack](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/stack/tt18.png)
![stack](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/stack/tt19.png)
![stack](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/stack/tt20.png)
![stack](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/stack/tt21.png)
![stack](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/stack/tt22.png)
![stack](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/stack/tt23.png)
![stack](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/stack/tt24.png)

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

class FindCelebChallenge {
    public static int findCelebrity(int[][] party, int numPeople) {
        int celebrity = -1;
        // Write -- Your -- Code
        return celebrity;
    }
}
{% endhighlight %}

## Solution Review: Solve a Celebrity Problem using a Stack

## Solution

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

class FindCelebChallenge {
   //returns true if x knows y else returns false
    private static boolean aqStatus(int[][] party, int x, int y) {
        if (party[x][y] == 1) return true;
        return false;
    }

    public static int findCelebrity(int[][] party, int numPeople) {
        Stack<Integer> stack = new Stack<>(numPeople);
        int celebrity = -1;

        //Push all people in stack
        for (int i = 0; i < numPeople; i++) {
            stack.push(i);
        }

        while (!stack.isEmpty()) {

            //Take two people out of stack and check if they know each other
            //One who doesn't know the other, push it back in stack.
            int x = stack.pop();

            if (stack.isEmpty()) {
                celebrity = x;
                break;
            }

            int y = stack.pop();

            if (aqStatus(party, x, y)) {
                //x knows y , discard x and push y in stack
                stack.push(y);
            } else stack.push(x);

        } //end of while

        //At this point we will have last element of stack as celebrity
        //Check it to make sure it's the right celebrity
        for (int j = 0; j < numPeople; j++) {

            //Celebrity knows no one while everyone knows celebrity
            if (celebrity != j && (aqStatus(party, celebrity, j) || !(aqStatus(party, j, celebrity)))) return -1;
        }
        return celebrity;
    }//end of findCelebrity()

    public static void main(String args[]) {
        
        int [][] party1 = {
          {0,1,1,0},
          {1,0,1,1},
          {0,0,0,0},
          {0,1,1,0},   
        };

        int [][] party2 = {
          {0,1,1,0},
          {1,0,1,1},
          {0,0,0,1},
          {0,1,1,0},   
        };

        int [][] party3 = {
          {0,0,0,0},
          {1,0,0,1},
          {1,0,0,1},
          {1,1,1,0},   
        };
        
        System.out.println(findCelebrity(party1,4));
        System.out.println(findCelebrity(party2,4));
        System.out.println(findCelebrity(party3,4));
    }
}
{% endhighlight %}

Explanation #
Although this method can be solved by brute force using nested loops, a stack can do it much more efficiently.

First of all, we push all the people to the stack at line number 13 - 15. Then we pop 2 people from the stack and check if they know each other or not. If someone doesn’t know, then we push back that person into the stack.

This step repeats until we have only one person in the stack. For the last person, we check if he/she is a celebrity or not at line number 39 - 43.

Time Complexity #
The time complexity of this problem is O(n)O(n).



