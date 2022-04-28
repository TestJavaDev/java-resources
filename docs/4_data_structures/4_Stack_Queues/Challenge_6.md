---
layout: default
title: Challenge 6
parent: Stack_Queues
grand_parent: Data Structures
nav_order: 6
permalink: /data_structures/stack_queues/ch6
---
<div align="center" markdown="1">
Challenge 6 / Java resources / Tutorial

{: .fs-8 .fw-400 }
</div>

## Challenge 6: Evaluate Postfix Expressions using Stacks

Let's try to compute postfix mathematical expressions using stacks!

## Infix and Postfix Expressions 
In the infix expression (the usual convention followed in mathematics), operators like + and * appear between the operands involved in the calculation:

6 + 3 * 8 - 4

Another convention is the postfix expression, where the operators appear after the operands involved in the expression. In postfix, the expression written above will become:

6 3 8 * + 4 -

The two operands preceding an operator will be used with that operator
1. From the first block of digits 6 3 8, we pick the last two, which are 3 and 8.
2. Reading the operators from left to right, the first one is *. The expression now becomes 3 * 8
3. The next number is 6 while the next operator is +, so we have 6 + 8 * 3.
4. The value of this expression is followed by 4, which is right before -. Hence we have 6 + 8 * 3 - 4.

## Problem Statement 
In this problem, you have to implement the evaluatePostFix() method that will compute a postfix expression given to it in a string.

## Input 
The input is a string containing a valid postfix mathematic expression. Each digit is considered a separate number, i.e., there are no double-digit numbers.

## Output 
An integer result of the given postfix expression.

## Sample Input 
expression = "921*-8-4+" # 9 - 2 * 1 - 8 + 4

## Sample Output 
3

## Explanation 
* 1st operation => 2 * 1 = 2,
* 2nd operation => 9 - 2 = 7,
* 3rd operation => 7 - 8 = -1,
* 4th operation => -1 + 4 = 3

![stack](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/stack/tt6.png)
![stack](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/stack/tt7.png)
![stack](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/stack/tt8.png)
![stack](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/stack/tt9.png)
![stack](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/stack/tt10.png)

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

class EvaluatePostfixChallenge {
    public static int evaluatePostFix(String expression) {
        return Integer.MIN_VALUE;
    }
}
{% endhighlight %}

## Solution Review: Evaluate Postfix Expressions using Stacks

## Solution: Numbers as Stack Elements

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

class EvaluatePostfixChallenge {
    public static int evaluatePostFix(String expression) {
        Stack<Integer> stack = new Stack<>(expression.length());
        //1.Scan expression character by character,
		//2.If character is a number push it in stack
		//3.If character is operator then pop two elements from stack
		//perform the operation and put the result back in stack
		//At the end, Stack will contain result of whole expression.
        for (int i = 0; i < expression.length(); i++) {
            char character = expression.charAt(i);

            if (!Character.isDigit(character)) {
                Integer x = stack.pop();
                Integer y = stack.pop();

                switch (character) {
                    case '+':
                        stack.push(y + x);
                        break;
                    case '-':
                        stack.push(y - x);
                        break;
                    case '*':
                        stack.push(y * x);
                        break;
                    case '/':
                        stack.push(y / x);
                        break;
                }

            } else
                stack.push(Character.getNumericValue(character));
        }
        return stack.pop();
    }
	public static void main(String args[]) {
	
		System.out.println(evaluatePostFix("921*-8-4+"));
		//Try your own examples below
		
	}
  
}
{% endhighlight %}

## Explanation
We check each character of the string from left to right. If we find a digit, it is pushed into the stack.

If we find an operator, we pop two elements from the stack (there have to be at least two present or else this postfix expression is incorrect) and solve the expression. The resulting value is pushed back into the stack.

The process continues until we reach the end of the string.

## Time Complexity
Since we traverse the string of n characters once, the time complexity for this algorithm is O(n).



