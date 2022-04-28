---
layout: default
title: Fizz Buzz Problem
parent: Interview Practice Problems
grand_parent: Multithreading
has_children: true
nav_order: 19
permalink: /multithreading/problems/fizzbuzz
---
<div align="center" markdown="1">
Fizz Buzz Problem / Java resources / Tutorial

{: .fs-8 .fw-400 }
</div>

## Fizz Buzz Problem

## Problem Statement
FizzBuzz is a common interview problem in which a program prints a number series from 1 to n such that for every number that is a multiple of 3 it prints "fizz", for every number that is a multiple of 5 it prints "buzz" and for every number that is a multiple of both 3 and 5 it prints "fizzbuzz". We will be creating a multi-threaded solution for this problem.

Suppose we have four threads t1, t2, t3 and t4. Thread t1 checks if the number is divisible by 3 and prints fizz. Thread t2 checks if the number is divisible by 5 and prints buzz. Thread t3 checks if the number is divisible by both 3 and 5 and prints fizzbuzz. Thread t4 prints numbers that are not divisible by 3 or 5. The workflow of the program is shown below:

![new](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/new/new31.png)

The code for the class is as follows:

![new](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/new/new32.png)

For an input integer n, the program should output a string containing the words fizz, buzz and fizzbuzz representing certain numbers. For example, for n = 15, the output should be: 1, 2, fizz, 4, buzz, fizz, 7, 8, fizz, buzz, 11, fizz, 13, 14, fizzbuzz.

## Solution
We will solve this problem using the basic Java functions; wait() and notifyAll(). The basic structure of the class is given below.

![new](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/new/new33.png)

The MultithreadedFizzBuzz class contains 2 private members: n and num.

n is the last number of the series to be printed whereas num represents the current number to be printed. It is initialized with 1.

The constructor MultithreadedFizzBuzz() initializes n with the input taken from the user.

![new](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/new/new34.png)

The second function in the class, fizz() prints "fizz" only if the current number is divisible by 3. The first loop checks if num (current number) is smaller than or equal to n(user input). Then num is checked for its divisibility by 3. We check if num is divisible by 3 and not by 5 because some multiples of 3 are also multiples of 5. If the condition is met, then "fizz" is printed and num is incremented. The waiting threads are notified via notifyAll(). If the condition is not met, the thread goes into wait().

![new](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/new/new35.png)

The next function buzz() works in the same manner as fizz(). The only difference here is the check to see if num is divisibile by 5 and not by 3. The reasoning is the same: some multiples of 5 are also multiples of 3 and those numbers should not be printed by this function. If the condition is met, then "buzz" is printed otherwise the thread will wait().

![new](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/new/new36.png)

The next function fizzbuzz() prints "fizzbuzz" if the current number in the series is divisible by both 3 and 5. A multiple of 15 is divisible by 3 and 5 both so num is checked for its divisibility by 15. After printing "fizzbuzz", num is incremented and waiting threads are notified via notifyAll(). If num is not divisible by 15 then the thread goes into wait().

![new](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/new/new37.png)

The last function number() checks if num is neither divisible by 3 nor by 5, then prints the num.

![new](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/new/new38.png)

The complete code for MultithreadedFizzBuzz is as follows

![new](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/new/new39.png)

We will be creating another class FizzBuzzThread for multithreading purpose. It takes an object of MultithreadedFizzBuzz and calls the relevant method from the string passed to it.

![new](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/new/new40.png)

To test our solution, we will be making 4 threads: t1,t2, t3 and t4. Three threads will check for divisibility by 3, 5 and 15 and print fizz, buzz, and fizzbuzz accordingly. Thread t4 prints numbers that are not divisible by 3 or 5.

{% highlight java %}
class MultithreadedFizzBuzz {
    private int n;
    private int num = 1;

    public MultithreadedFizzBuzz(int n) {
        this.n = n;
    }
    public synchronized void fizz() throws InterruptedException {
        while (num <= n) {
            if (num % 3 == 0 && num % 5 != 0) {
                System.out.println("Fizz");
                num++;
                notifyAll();
            } else {
                wait();
            }
        }
    }

    public synchronized void buzz() throws InterruptedException {
        while (num <= n) {
            if (num % 3 != 0 && num % 5 == 0) {
                System.out.println("Buzz");
                num++;
                notifyAll();
            } else {
                wait();
            }
        }
    }

    public synchronized void fizzbuzz() throws InterruptedException {
        while (num <= n) {
            if (num % 15 == 0) {
                System.out.println("FizzBuzz");
                num++;
                notifyAll();
            } else {
                wait();
            }
        }
    }

    public synchronized void number() throws InterruptedException {
        while (num <= n) {
            if (num % 3 != 0 && num % 5 != 0) {
                System.out.println(num);
                num++;
                notifyAll();
            } else {
                wait();
            }
        }
    }
}

class FizzBuzzThread extends Thread {

    MultithreadedFizzBuzz obj;
    String method;
    
    public FizzBuzzThread(MultithreadedFizzBuzz obj, String method){
        this.obj = obj;
        this.method = method;
    }
    
    public void run() {
        if ("Fizz".equals(method)) {
            try {
                obj.fizz();
            }
            catch (Exception e) {
            }
        }
        else if ("Buzz".equals(method)) {
            try {
                obj.buzz();
            }
            catch (Exception e) {
            }
        }
        else if ("FizzBuzz".equals(method)) {
            try {
                obj.fizzbuzz();
            }
            catch (Exception e) {
            }
        }
        else if ("Number".equals(method)) {
            try {
                obj.number();
            }
            catch (Exception e) {
            }
        }

    }
}

class main
{
	public static void main(String[] args) {
		MultithreadedFizzBuzz obj = new MultithreadedFizzBuzz(15);
		
		Thread t1 = new FizzBuzzThread(obj,"Fizz");
	    Thread t2 = new FizzBuzzThread(obj,"Buzz");
	    Thread t3 = new FizzBuzzThread(obj,"FizzBuzz");
	    Thread t4 = new FizzBuzzThread(obj,"Number");
	    
	    t2.start();
	    t1.start(); 
	    t4.start();
	    t3.start();
	}
}
{% endhighlight %}
