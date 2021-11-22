---
layout: default
title: Challenge 9
parent: Stack_Queues
grand_parent: Data Structures
nav_order: 9
permalink: /data_structures/stack_queues/ch9
---
<div align="center" markdown="1">
Challenge 9 / Java resources / Tutorial

{: .fs-8 .fw-400 }
</div>

## Challenge 9: Check for Balanced Parentheses using a Stack

![stack](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/stack/tt25.png)

![stack](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/stack/tt26.png)

![stack](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/stack/tt27.png)

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

class CheckBalancedChallenge {
    public static boolean isBalanced(String exp) {
        // Write -- Your -- Code
        return false;
    }
}
{% endhighlight %}

## Solution Review: Check for Balanced Parentheses using a Stack

## Solution: A Stack of Characters

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

class CheckBalancedChallenge {
    public static boolean isBalanced(String exp) {

        //Iterate through the string exp.
        //For each opening parentheses, push it into stack
        //For every closing parenthesis check for its opening parentheses in stack
        //If you can't find the opening parentheses for any closing one then returns false.
        //and after complete traversal of string exp, if there's any opening parentheses left
        //in stack then also return false.
        //At the end return true if you haven't encountered any of the above false conditions.
        Stack<Character> stack = new Stack<>(exp.length());

        for (int i = 0; i < exp.length(); i++) {

            char character = exp.charAt(i);

            if (character == '}' || character == ')' || character == ']') {

                if (stack.isEmpty()) return false;

                if ((character == '}' && stack.pop() != '{') || (character == ')' && stack.pop() != '(') || (character == ']' && stack.pop() != '[')) return false;

            }
            else stack.push(character);

        } //end of for
        if (!stack.isEmpty()) return false;

        return true;
    }

    public static void main(String args[]) {

        System.out.println(isBalanced("{[()]}"));
        System.out.println(isBalanced("[{(}]"));

    }
}
{% endhighlight %}

## Explanation 
This is a simple algorithm. We iterate over the string, one character at a time. Whenever we find a closing parenthesis, we can deduce that the string is unbalance based on two conditions:

The stack is empty.
The top element in the stack is not an opening parenthesis of the same type.
If any of these conditions are true, we return false.

If the parenthesis in the string is an opening parenthesis, it is simply pushed into the stack. If all the parentheses are balanced, the stack should be empty by the end because we pop() every opening parenthesis once its closing parenthesis is found.

If it is not empty, we return false.

## Time Complexity 
We traverse the string exp once. So, the time complexity is O(n), where n is the length of the string. Similarly, the space complexity of this algorithm is also O(n) because we have initialized the stack with the size equal to the length of string exp.




