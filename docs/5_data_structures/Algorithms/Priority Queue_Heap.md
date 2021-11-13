---
layout: default
title: DFS
parent: Data Structures
# nav_order: 1
permalink: /data_structures/bfs
---
<div align="center" markdown="1">
Priority Queue and Heap / Java resources / Tutorial

{: .fs-8 .fw-400 }
</div>

## Priority Queue/Heap
What is the relationship between a priority queue and heap?#
A priority queue is an abstract data type while a heap is the concrete data structure we use to implement a priority queue.

Priority queue#
A priority queue is a data structure that consists of a collection of items and supports the following operations:

insert: insert an item with a key
delete_min/delete_max: remove the item with the smallest/largest key and return it
Note that we only allow getting and deleting the element with min/max key and NOT with any arbitrary key.

Use cases#
The hospital triage process is a quintessential priority queue. Patients are sorted based on the severity of their condition. For example, a person with a cold comes in and he is placed near the end of the queue. Then a person who had a car accident comes in. He is placed before the person with the cold even though he came in later because his condition is more severe. Severity is the key in this case.

Consider a problem like Merge K sorted lists. We need to keep track of the min value among k elements (smallest element in each sorted list), remove the min value, and insert new values at will while still having access to the min value at any point in time. Here are some other problems where the priority queue comes in handy:

K closest pointers to origin
Kth largest element
Kth largest element in a stream
Median of a data stream
Implement priority queue using an array#
To do this, we could try using:

an unsorted array. Insert would be O(1)O(1) as we just have to put it at the end, but finding and deleting the min value would be O(N)O(N) since we would have to loop through the entire array to find it.
a sorted array. Finding min value would be easy O(1)O(1), but it would be O(N)O(N) to insert since we would have to loop through to find the correct position of the value and move elements after the position to make space and insert into the space.
Heap#
There are two kinds of heaps: min heap and max heap. A min heap is a tree that has two properties:

Almost complete, i.e. every level is filled except possibly the last(deepest) level. The filled items in the last level are left-justified.
For any node, its key (priority) is greater than its parent’s key (Min Heap).
A max heap has the same property #1 and opposite property #2, i.e., for any node, its key is less than its parent’s key.

Let’s play “is it a heap?” game:
![heap](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/heap/heap1.png)
Note that:

The number in each node is the key, not value (remember a tree node has a value). Keys are used to sort the nodes/construct the tree, and values are the data we want heap to store.
Unlike a binary search tree, there is no comparable relationship between children. For example, the third example in the first row, 17 and 8 are both larger than 2 but they are NOT sorted left to right. In fact, there is no comparable relationship across a level of a heap at all.
Why are heaps useful?#
At first look, the heap is an odd data structure –– it’s required to be a complete tree but unlike the binary search tree, it’s not sorted across a level.

What makes it so useful is that:

Because a heap is a complete tree, the height of a heap is guaranteed to be O(log(N))O(log(N)). This makes operations that go from root to leaf guaranteed to be O(log(N))O(log(N)).
Because only nodes in a root-to-leaf path are sorted (nodes in the same level are not sorted), when we add/remove a node, we only have to fix the order in the vertical path the node is in. This makes inserting and deleting O(log(N))O(log(N)) too.
Being complete also makes an array a good choice to store a heap since data is continuous. As we will see later in this module, we can find the parent and children of a node simply by doing index arithmetic.
Operations#
Insert#
To insert a key into a heap

Place the new key at the first free leaf.
If property #2 is violated, perform a bubble-up.
![heap](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/heap/heap2.png)
![heap](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/heap/heap3.png)
![heap](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/heap/heap4.png)
![heap](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/heap/heap5.png)
![heap](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/heap/heap6.png)
![heap](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/heap/heap7.png)
As the name of the algorithm suggests, it “bubbles up” the new node by swapping it with its parent until the order is correct

Since the height of a heap is O(log(N))O(log(N))`, the complexity of bubble-up is O(log(N))O(log(N)).

delete_min#
This operation

Deletes a node with the min key and returns it.
Reorganizes the heap so the two properties still hold.
To do that, we

Remove and return the root since the node with the minimum key is always at the root.
Replace the root with the last node (the rightmost node at the bottom) of the heap.
If property #2 is violated, perform a bubble-down.
![heap](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/heap/heap8.png)
![heap](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/heap/heap9.png)
![heap](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/heap/heap10.png)
![heap](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/heap/heap11.png)
![heap](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/heap/heap12.png)
![heap](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/heap/heap13.png)
What this says is we keep swapping between the current node and its smallest child until we get to the leaf, hence a “bubble down”. Again, the time complexity is O(log(N))O(log(N))` since the height of a heap is O(log(N))O(log(N)).
## Implementing Heap
Being a complete tree makes an array a natural choice to implement a heap since it can be stored compactly and wastes no space. Pointers are not needed. The parent and children of each node can be calculated with index arithmetic.
![heap](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/heap/heap14.png)
For node i, its children are stored at 2i+1 and 2i+2, and its parent is at floor((i-1)/2). So, instead of node.left, we’d do 2*i+1.

This is exactly how the Python language implements heaps.

tldr#
A heap

Is a complete tree.
Allows O(log(N)) to insert and remove an element with priority.
is implemented with arrays.
Each node of a min heap is less than all of its children.

Heap in Python#
Python comes with a built-in heapq that we can and it is a min heap, i.e. the element at the top is the smallest.

heapq.heappush akes two arguments: the first is the heap (an array/list) we want to push the element into and the second argument can be anything as long as it can be used for comparison. Typically, we push a tuple since in Python tuples are compared in an item-by-item order. For example, (1, 10) is smaller than (2, 0) because the first element is smaller. (1, 10) is smaller than (1, 20) because when the first item is the same, we compare the next one and in this case 10 is smaller than 20. Typically, we set the first element of the tuple to be the key used for comparison and the last element to the value we want the heap to store.

heapq.heappop takes a single argument, a heap, and returns the smallest element in that heap.
{% highlight java %}

import heapq
h = []
heapq.heappush(h, (5, 'write code'))
heapq.heappush(h, (7, 'release product'))
heapq.heappush(h, (1, 'write spec'))
heapq.heappush(h, (3, 'create tests'))
print(heapq.heappop(h))
print(h[0])
{% endhighlight %}
If the list is known beforehand, we can create a heap out of it by simply using heapify, which is actually an O(N)O(N) operation.
{% highlight java %}

import heapq
arr = [3, 1, 2]
heapq.heapify(arr)
print(arr)
{% endhighlight %}

Heap in Java#
By default, the Java class java.util.PriorityQueue is a min heap. The elements are mostly sorted using their natural comparison methods, but when there isn’t one (for example, sorting points by distance), it can be provided by passing in a Comparator at construction time. A Comparator is required if the elements don’t implement the Comparable interface.

To create a PriorityQueue of non-comparable objects, we can use lambda expressions or method reference introduced in Java 8 and provide an inline comparator to the constructor.
{% highlight java %}

class Task {
    private int priority;
    private String description;

    public Task(int priority, String description) {
        this.priority = priority;
        this.description = description;
    }
    public static void main(String[] args) {
        // initialize a min heap sorted by the priority of tasks with an initial capacity of 5
        PriorityQueue<Task> tasks = new PriorityQueue<>(5, Comparator.comparingInt(t -> t.priority));
        tasks.add(new Task(5, "write code"));
        tasks.add(new Task(7, "release product"));
        tasks.add(new Task(1, "write spec"));
        tasks.add(new Task(3, "create tests"));
        Task head = tasks.poll();  // return the task with min priority
        System.out.println("Task : "+head.description);  // print out "write spec"
    }
}
{% endhighlight %}

Heap in JavaScript#
JavaScript does not support the heap data structure natively, so you might have to implement your own heap during an interview. Here is a common implementation of min-heap in JavaScript:
{% highlight java %}
class HeapItem {
    constructor(item, priority = item) {
        this.item = item;
        this.priority = priority;
    }
}

class MinHeap {
    constructor() {
        this.heap = [];
    }

    push(node) {
        // insert the new node at the end of the heap array
        this.heap.push(node);
        // find the correct position for the new node
        this.bubble_up();
    }

    bubble_up() {
        let index = this.heap.length - 1;

        while (index > 0) {
            const element = this.heap[index];
            const parentIndex = Math.floor((index - 1) / 2);
            const parent = this.heap[parentIndex];

            if (parent.priority <= element.priority) break;
            // if the parent is bigger than the child then swap the parent and child
            this.heap[index] = parent;
            this.heap[parentIndex] = element;
            index = parentIndex;
        }
    }

    pop() {
        const min = this.heap[0];
        this.heap[0] = this.heap[this.size() - 1];
        this.heap.pop();
        this.bubble_down();
        return min;
    }

    bubble_down() {
        let index = 0;
        let min = index;
        const n = this.heap.length;

        while (index < n) {
            const left = 2 * index + 1;
            const right = left + 1;
            // check if left or right child is smaller than parent
            if ((left < n && this.heap[left].priority < this.heap[min].priority) || 
            (right < n && this.heap[right].priority < this.heap[min].priority)) {
                // pick the smaller child if both child is present
                if (right < n) {
                    min = this.heap[left].priority < this.heap[right].priority ? left : right;
                } else {
                    min = left;
                }
            }

            if (min === index) break;
            [this.heap[min], this.heap[index]] = [this.heap[index], this.heap[min]];
            index = min;
        }
    }

    peek() {
        return this.heap[0];
    }

    size() {
        return this.heap.length;
    }
}

 const heap = new MinHeap();
 heap.push(new HeapItem("First item"));
 heap.push(new HeapItem("Second item"));
 console.log(heap.pop().item)
 console.log(heap.pop().item)
{% endhighlight %}

## Merge K Sorted Lists
Problem statement#
Given k sorted lists of numbers, merge them into one sorted list.

Example:#
Input: [[1, 3, 5], [2, 4, 6], [7, 10]]

Output: [1, 2, 3, 4, 5, 6, 7, 10]
Explanation#
Intuition#
The first thing that comes to mind is that we can concatenate all the lists into one and then sort the list. This is O(N log(N))) because sorting is O(N log(N)) where N is the total length of all the lists.

Next, we ask the question: “are there any conditions that we haven’t used?” We know that all the lists are sorted and we haven’t used that condition. For each list, the smallest number is the first number. We can take the first number of each list and put them into a “pool of top k smallest numbers”, where k is the number of lists. The smallest number in the pool is the smallest number of all the lists and should be added to the final merged list. We then take the next smallest number from the list and add it to the pool. Repeat until we have exhausted all the lists.

Now the question is, “how do we compare a stream of k numbers?”, which is a perfect use case for a min heap.
![heap](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/heap/heap15.png)
![heap](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/heap/heap16.png)
![heap](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/heap/heap17.png)
![heap](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/heap/heap18.png)
![heap](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/heap/heap19.png)
![heap](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/heap/heap20.png)
![heap](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/heap/heap21.png)
![heap](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/heap/heap22.png)
![heap](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/heap/heap23.png)
![heap](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/heap/heap24.png)
![heap](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/heap/heap25.png)
![heap](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/heap/heap26.png)
![heap](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/heap/heap27.png)
![heap](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/heap/heap28.png)
![heap](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/heap/heap29.png)
![heap](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/heap/heap30.png)
![heap](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/heap/heap31.png)
Note that we push a tuple (val, current_list, head_index) into the heap. val is used to compare in the heap. We need current_list and head_index because we want to know the next number to push.
{% highlight java %}
class Solution {

    public static List<Integer> mergeKSortedLists(List<List<Integer>> lists) {
      List<Integer> res = new ArrayList<>();
      PriorityQueue<Element> heap = new PriorityQueue<>(lists.size(), Comparator.comparingInt(e -> e.val));
      // push first number of each list into the heap
      for (List<Integer> list : lists) {
          heap.add(new Element(list.get(0), list, 0));  // 1
      }
      while (!heap.isEmpty()) {
          Element e = heap.poll();
          res.add(e.val);
          int headIndex = e.headIndex + 1;
          // if there are more numbers in the list, push into the heap
          if (headIndex < e.currentList.size()) {
              heap.add(new Element(e.currentList.get(headIndex), e.currentList, headIndex));
          }
      }
      return res;
    }
    private static class Element {
        private int val;
        private List<Integer> currentList;
        private int headIndex;

        public Element(int val, List<Integer> currentList, int headIndex) {
            this.val = val;
            this.currentList = currentList;
            this.headIndex = headIndex;
        }
    }
    //Driver code
    public static void main(String[] arg){
      String[] inputs = {"3","1"};
	    String[][] inputs1 = {{"1 3 5", "2 4 6", "7 10"}, {"1 2 3"}};
      for(int i = 0; i < inputs.length; i++) {
        int n = Integer.parseInt(inputs[i]);
        List<List<Integer>> lists = new ArrayList<>(n);
        for (int j = 0; j < n; j++) {
            List<Integer> list = Arrays.stream(inputs1[i][j].split(" ")).map(Integer::parseInt).collect(Collectors.toList());
            lists.add(list);
        }
        System.out.println("Merge k sorted list : "+Solution.mergeKSortedLists(lists).stream().map(num -> Integer.toString(num)).collect(Collectors.joining(" ")));
      }
    }
}
{% endhighlight %}
The time complexity is O(Nlog(K))O(Nlog(K)) where KK is the number of lists.

## Median of Data Stream
Problem statement#
Given a stream of numbers, find the median number at any given time (accurate to 1 decimal place). Do this in O(1) time complexity.

Example:#
![heap](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/heap/heap32.png)
Explanation#
Intuition#
The brute force way is to sort the entire list every time we get a new number. This would be O(Nlog(N)) for each add_number operation.

One step up is to notice that the list is sorted before we add any new number to it. So, every time we add a new number to the existing list we just have to find the spot to add it to. We can find the insert position using binary search in O(log(N)). Since inserting into a position also means shifting after the insert position by 1, the overall run time is O(N).

Upon re-examining the conditions and unknowns of the problem, we notice we only need to find the median and don’t need the rest of the list to be sorted. But how will we find the median without having a sorted list?

It’s useful to use the first principle and go back to the definition of median:

Half the numbers are smaller than the median and the other half are larger than the median.

Let’s assume the total number of elements is even and we can divide the numbers into two piles of equal size based on their values: a smaller half small pile and the bigger half big pile. The median of both piles is the average of the largest number in the small pile and the smallest number of the big pile. When we add a new number, two things could happen:

The new number is smaller than the largest of the small pile. In this case, we put it into the small pile, and the size of the small pile is now 1 greater than big pile. The median of both piles is the largest number of the small pile.
The new number is bigger than the largest of the small pile. In this case, the number belongs to the big pile. And the median of both piles is the smallest number of the big pile.
Now the problem boils down to how to keep a small pile where we can find max value easily and a big pile where we can find min value easily. min heap and max heap fit these requirements perfectly.
![heap](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/heap/heap33.png)
![heap](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/heap/heap34.png)
![heap](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/heap/heap35.png)
![heap](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/heap/heap36.png)
![heap](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/heap/heap37.png)
![heap](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/heap/heap38.png)
![heap](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/heap/heap40.png)
![heap](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/heap/heap41.png)
![heap](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/heap/heap42.png)
![heap](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/heap/heap43.png)
![heap](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/heap/heap44.png)
![heap](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/heap/heap45.png)
![heap](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/heap/heap46.png)
{% highlight java %}
class MedianOfStream {
    private Queue<Double> minHeap = new PriorityQueue<>(),
                        maxHeap = new PriorityQueue<>();
    public void addNum(int num) {
        // push into max heap if
        if (minHeap.size() == 0 || num < minHeap.peek()) {
            maxHeap.add((double) -num); // Note the - sign since it's max heap
        } else {
            minHeap.add((double) num);
        }
        _balance();
    }

    public double getMedian() {
        if (maxHeap.size() == minHeap.size()) {
            return (-maxHeap.peek() + minHeap.peek()) / 2.0;
        } else {
            return -maxHeap.peek();
        }
    }
    private void _balance() {
        if (maxHeap.size() < minHeap.size()) {
            maxHeap.add(-minHeap.poll());
        }
        if (maxHeap.size() > minHeap.size() + 1) {
            minHeap.add(-maxHeap.poll());
        }
    }
    //Driver code
    public static void main(String[] arg){
        String[] inputs = {"6"};
        String[][] inputs1 ={{"1", "2", "3" ,"get","4","get"}};
        for(int i = 0; i < inputs.length; i++) {
            int numInputs = Integer.parseInt(inputs[i]);
            MedianOfStream medianOfStream = new MedianOfStream();
            List<Double> res  = new ArrayList<Double>();
            for (int j = 0; j < numInputs; ++j) {
                String input = inputs1[i][j];
                if (input.equals("get")) {
                    res.add(medianOfStream.getMedian());
                } else {
                    medianOfStream.addNum(Integer.parseInt(input));
                }
            }
            System.out.println("Median of data stream :"+res.toString());
        }
    }
}
{% endhighlight %}
The time complexity to add an element is O(log(N))O(log(N)) since the heap push operation is O(log(N))O(log(N)). The time complexity to find the median is O(1)O(1) since inspecting the top of each heap is O(1)O(1).



