---
layout: default
title: Asynchronous to Synchronous Problem
parent: Interview Practice Problems
grand_parent: Multithreading
has_children: true
nav_order: 13
permalink: /multithreading/problems/asynch
---
<div align="center" markdown="1">
Asynchronous to Synchronous Problem / Java resources / Tutorial

{: .fs-8 .fw-400 }
</div>

## Asynchronous to Synchronous Problem

## Problem Statement

This is an actual interview question asked at Netflix.

Imagine we have an Executor class that performs some useful task asynchronously via the method asynchronousExecution(). In addition the method accepts a callback object which implements the Callback interface. the object’s done() gets invoked when the asynchronous execution is done. The definition for the involved classes is below:

## Executor Class

![inter](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/inter/inter61.png)

{% highlight java %}
class Demonstration {
    public static void main( String args[] ) throws Exception{
        Executor executor = new Executor();
        executor.asynchronousExecution(() -> {
            System.out.println("I am done");
        });

        System.out.println("main thread exiting...");
    }
}

interface Callback {

    public void done();
}


class Executor {

    public void asynchronousExecution(Callback callback) throws Exception {

        Thread t = new Thread(() -> {
            // Do some useful work
            try {
                Thread.sleep(5000);
            } catch (InterruptedException ie) {
            }
            callback.done();
        });
        t.start();
    }
}
{% endhighlight %}

ote how the main thread exits before the asynchronous execution is completed.

Your task is to make the execution synchronous without changing the original classes (imagine, you are given the binaries and not the source code) so that main thread waits till asynchronous execution is complete. In other words, the highlighted line#8 only executes once the asynchronous task is complete.

## Solution
The problem here asks us to convert asynchronous code to synchronous code without modifying the original code. The requirement that the main thread should block, till the asynchronous execution is complete hints at using some kind of notification/signalling mechanism. The main thread waits on something, which is then signaled by the asynchronous execution thread. Semaphore is the first thought that may come to your mind for solving this problem. However, I was told to use primitive Java synchronization constructs i.e. notify() and wait() methods on the Object class.

Since we can’t modify the original code, we’ll extend a new class SynchronousExecutor from the given Executor class and override the asynchronousExecution() method. The trick here is to invoke the original asynchronous implementation using super.asynchronousExecution() inside the overridden method. The overridden method would look like:

![inter](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/inter/inter62.png)

Now we need to pass the signal object to the superclass’s asynchronousExecution() method so that the asynchronous execution thread can notify() the signal variable once asynchronous execution is complete. We pass in the callback object to the super class’s method. We can wrap the original callback in another callback object and pass also in our signal variable to the super class. Let’s see how we can achieve that:

![inter](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/inter/inter63.png)

Note that the variable signal gets captured in the scope of the new callback that we define. However, the captured variable must be defined final or be effectively final. Since we are assigning the variable only once, it is effectively final. The code so far defines the basic structure of the solution and we need to add a few missing pieces for it to work.

Remember we can’t use wait() method without enclosing it inside a while loop as supurious wakeups can occur. Let’s fix that

![inter](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/inter/inter64.png)

Note that the invariant here is isDone which is set to true after the asynchronous execution is complete. The last problem here is that isDone isn’t final. We can’t declare it final because isDone gets assigned to after initialization. At this a slighly less elegant but workable solution is to use a boolean array of size 1 to represent our boolean. The array can be final because it gets assigned memory at initialization but the contents of the array can be changed later without compromising the finality of the variable.

![inter](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/inter/inter65.png)

## Complete Code
The complete code appears below:


{% highlight java %}
class Demonstration {
    public static void main( String args[] ) throws Exception {
        SynchronousExecutor executor = new SynchronousExecutor();
        executor.asynchronousExecution(() -> {
            System.out.println("I am done");
        });

        System.out.println("main thread exiting...");
    }
}

interface Callback {

    public void done();
}


class SynchronousExecutor extends Executor {

    @Override
    public void asynchronousExecution(Callback callback) throws Exception {

        Object signal = new Object();
        final boolean[] isDone = new boolean[1];

        Callback cb = new Callback() {

            @Override
            public void done() {
                callback.done();
                synchronized (signal) {
                    signal.notify();
                    isDone[0] = true;
                }
            }
        };

        // Call the asynchronous executor
        super.asynchronousExecution(cb);

        synchronized (signal) {
            while (!isDone[0]) {
                signal.wait();
            }
        }

    }
}

class Executor {

    public void asynchronousExecution(Callback callback) throws Exception {

        Thread t = new Thread(() -> {
            // Do some useful work
            try {
                Thread.sleep(5000);
            } catch (InterruptedException ie) {
            }
            callback.done();
        });
        t.start();
    }
}
{% endhighlight %}

Note the main thread has its print-statement printed after the asynchronous execution thread print its print-statement verifying that the execution is now synchronous.

Follow-up Question: Is the method asynchronousExecution() thread-safe?

The way we have constructed the logic, all the variables in the overridden method will be created on the thread-stack for each thread therefore the method is threadsafe and multiple threads can execute it in parallel.
