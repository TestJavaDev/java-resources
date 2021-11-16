---
layout: default
title: Unisex Bathroom Problem
parent: Interview Practice Problems
grand_parent: Multithreading
has_children: true
nav_order: 6
permalink: /multithreading/problems/bathroom
---
<div align="center" markdown="1">
Unisex Bathroom Problem / Java resources / Tutorial

{: .fs-8 .fw-400 }
</div>

## Unisex Bathroom Problem

## Problem Statement

A bathroom is being designed for the use of both males and females in an office but requires the following constraints to be maintained:
* There cannot be men and women in the bathroom at the same time.
* There should never be more than three employees in the bathroom simultaneously.

The solution should avoid deadlocks. For now, though, don’t worry about starvation.

![inter](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/inter/inter27.png)

## Solution
First let us come up with the skeleton of our Unisex Bathroom class. We want to model the problem programmatically first. We'll need two APIs, one that is called by a male to use the bathroom and another one that is called by the woman to use the bathroom. Initially our class looks like the following

![inter](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/inter/inter28.png)

Let us try to address the first problem of allowing either men or women to use the bathroom. We'll worry about the max employees later. We need to maintain state in a variable which would tell us which gender is currently using the bathroom. Let's call this variable inUseBy. To make the code more readable we'll make the type of the variable inUseBy a string which can take on the values men, women or none.

We'll also have a method useBathroom() that'll mock a person using the bathroom. The implementation of this method will simply sleep the thread using the bathroom for some time.

Assume there's no one in the bathroom and a male thread invokes the maleUseBathroom() method, the thread has to check first whether the bathroom is being used by a female thread. If it is indeed being used by a female, then the male thread has to wait for the bathroom to be empty. If the male thread already finds the bathroom empty, which in our scenario it does, the thread simply updates the inUseBy variable to "MEN" and proceeds to use the bathroom. After using the bathroom, however, it must let any waiting female threads know that it is done and they can now use the bathroom.

The astute reader would immediately realize that we'll need to guard the variable inUseBy since it can possibly be both read and written to by different threads at the same time. Does that mean we should mark our methods as synchronized? The wary reader would know that doing so would essentially make the threads serially access the methods, i.e., if one male thread is accessing the bathroom, then another one can't access the bathroom even though the problem says that more than one male should be able to use the bathroom. This requires us to take synchronization to a finer granular level rather than implementing it at the method level. So far what we discussed looks like the below when translated into code:

![inter](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/inter/inter29.png)
![inter](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/inter/inter30.png)

The code so far allows any number of men or women to gather in the bathroom. However, it allows only one gender to do so. The methods are mirror images of each other with only gender-specific variable changes. Let's discuss the important portions of the code.
* Lines 17-26: Since java monitors are mesa monitors, we use a while loop to check for the variable inUseBy. If it is set to MEN or NONE then, we know the bathroom is either empty or already has men and therefore it is safe to proceed ahead. If the inUseBy is set to WOMEN, then the male thread, invokes wait() on line 23. Note, the thread would give up the monitor for the object on which it is synchronized thus allowing other threads to synchronize on the same object and maybe update the inUseBy variable
* Line 28 has no synchronization around it. If a male thread reaches here, we are guaranteed that either the bathroom was already in use by men or no one was using it.
* Lines 30-37: After using the bathroom, the male thread is about to leave the method so it should remember to decrement the number of occupants in the bathroom. As soon as it does that, it has to check if it were the last member of its gender to leave the bathroom and if so then it should also update the inUseBy variable to NONE. Finally, the thread notifies any other waiting threads that they are free to check the value of inUseBy in case it has updated it. Question: Why did we use notifyAll() instead of notify()?

Now we need to incorporate the logic of limiting the number of employees of a given gender that can be in the bathroom at the same time. Limiting access, intuitively leads one to use a semaphore. A semaphore would do just that - limit access to a fixed number of threads, which in our case is 3.

## Complete Code
The complete code appears below:

{% highlight java %}
import java.util.concurrent.Semaphore;

class Demonstration {
    public static void main( String args[] ) throws InterruptedException {
        UnisexBathroom.runTest();
    }
}

class UnisexBathroom {

    static String WOMEN = "women";
    static String MEN = "men";
    static String NONE = "none";

    String inUseBy = NONE;
    int empsInBathroom = 0;
    Semaphore maxEmps = new Semaphore(3);

    void useBathroom(String name) throws InterruptedException {
        System.out.println("\n" + name + " using bathroom. Current employees in bathroom = " + empsInBathroom + " " + System.currentTimeMillis());
        Thread.sleep(3000);
        System.out.println("\n" + name + " done using bathroom " + System.currentTimeMillis());
    }

    void maleUseBathroom(String name) throws InterruptedException {

        synchronized (this) {
            while (inUseBy.equals(WOMEN)) {
                this.wait();
            }
            maxEmps.acquire();
            empsInBathroom++;
            inUseBy = MEN;
        }

        useBathroom(name);
        maxEmps.release();

        synchronized (this) {
            empsInBathroom--;

            if (empsInBathroom == 0) inUseBy = NONE;
            this.notifyAll();
        }
    }

    void femaleUseBathroom(String name) throws InterruptedException {

        synchronized (this) {
            while (inUseBy.equals(MEN)) {
                this.wait();
            }
            maxEmps.acquire();
            empsInBathroom++;
            inUseBy = WOMEN;
        }

        useBathroom(name);
        maxEmps.release();

        synchronized (this) {
            empsInBathroom--;

            if (empsInBathroom == 0) inUseBy = NONE;
            this.notifyAll();
        }
    }

    public static void runTest() throws InterruptedException {

        final UnisexBathroom unisexBathroom = new UnisexBathroom();

        Thread female1 = new Thread(new Runnable() {
            public void run() {
                try {
                    unisexBathroom.femaleUseBathroom("Lisa");
                } catch (InterruptedException ie) {

                }
            }
        });

        Thread male1 = new Thread(new Runnable() {
            public void run() {
                try {
                    unisexBathroom.maleUseBathroom("John");
                } catch (InterruptedException ie) {

                }
            }
        });

        Thread male2 = new Thread(new Runnable() {
            public void run() {
                try {
                    unisexBathroom.maleUseBathroom("Bob");
                } catch (InterruptedException ie) {

                }
            }
        });

        Thread male3 = new Thread(new Runnable() {
            public void run() {
                try {
                    unisexBathroom.maleUseBathroom("Anil");
                } catch (InterruptedException ie) {

                }
            }
        });

        Thread male4 = new Thread(new Runnable() {
            public void run() {
                try {
                    unisexBathroom.maleUseBathroom("Wentao");
                } catch (InterruptedException ie) {

                }
            }
        });

        female1.start();
        male1.start();
        male2.start();
        male3.start();
        male4.start();

        female1.join();
        male1.join();
        male2.join();
        male3.join();
        male4.join();

    }
}
{% endhighlight %}