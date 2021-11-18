---
layout: default
title: Amazon
parent: Coding Interview
has_children: true
nav_order: 7
permalink: /coding_interview/amazon
---
<div align="center" markdown="1">
Amazon / Java resources / Tutorial

{: .fs-8 .fw-400 }
</div>

## Amazon

## Project Description for Amazon

## Introduction
Amazon is the most widely used online store around the world. After their success in e-commerce, the company has now branched out into other technologies such as cloud computing, digital streaming, artificial intelligence, etc. However, most people still know Amazon for its online store because it connects customers to vendors across the globe. Through Amazon, customers can get better deals and a bigger variety of items as compared to buying from a brick and mortar store.

The scenario and the problems discussed in this chapter relate to Amazon’s online store and the exclusive deals that it offers its customers.

## Statement
Consider you are a developer in Amazon’s online store team. Your team is working on several features related to product recommendations, promoting special deals and up-selling of items. In addition to these customer-facing features, you are also working on optimizations of delivery fleet management as well as integration with other e-commerce companies that Amazon acquired.

## Features

We will need to introduce the following features to implement the functionalities we discussed above:
* Feature #1: All orders above a certain total amount are eligible for free delivery. If a customer’s total bill is near the free-shipping threshold, recommend items to add to cart to avail free delivery.
* Feature #2: Some customers have won a coupon worth $200 to buy up to three items. Suggest a bundle of three items to these lucky users.
* Feature #3: Up-sell a random product from a set of related products by recommending it to users at checkout.
* Feature #4: We are integrating data from a recently acquired e-commerce website. Create a deep copy of a list of products from the acquired company’s website so that it may be imported to Amazon.
* Feature #5: We want to showcase order-processing milestones on a dashboard. We need to mine daily stats to populate this dashboard.
* Feature #6: Show product recommendations with items that are frequently viewed together.
* Feature #7: Help the logistic division of the company to optimally utilize contractor delivery trucks.
* Feature #8: Merge product recommendations using the data from an acquired company.
* Feature #9: Allow a user to set a minimum and maximum price range filter to the list of products.

In the next few lessons, we’ll discuss the recommended implementations of these features. Before we start, we suggest that you think about how you would implement these features. As you do, you’ll realize some of the underlying problems that you’ll need to solve. The solutions to these basic problems are also applicable to other common coding interview questions.

## Feature #1: Suggest Items for Free Delivery

## Description
For the first feature, we want to suggest products customers can buy to make their orders eligible for free delivery. The minimum order amount to qualify for free shipping varies by customer location. When a customer views their cart and the current total does not qualify for free shipping, we want to show them a pair of products that can be bought together to make the total amount equal to the amount required to be eligible for free delivery. You can assume that it was a corporate decision to show a pair of products instead of a single product. Historical data collected by your team shows that customers are more willing to buy multiple products as it gives the illusion of a better deal. Also, the UX team says that only two items should be displayed given the screen space for this feature.

To implement this feature, we will have access to a list of products that the customer is likely to buy. These products will include the items from their wishlist and other items based on previous purchases. We will also be given the amount, nn, that the customer needs to spend in addition to the current total: n = [\text{free shipping price} - \text{current total}]n=[free shipping price−current total].

Let’s say you are given a list of numbers containing the prices of products that a customer is likely to buy, {2, 30, 56, 34, 55, 10, 11, 20, 15, 60, 45, 39, 51}. In addition, the amount that needs to be spent to claim the free delivery offer is 61 dollars. Then, we can see that the sum of 10 and 51 is 61. Therefore, we will suggest the customer buys these products. Our program should return the indices of these products in an array such as: {5, 12}.

You can assume that the list contains at least one pair of products to suggest. If there is more than one pair, you can suggest any of them.

The following illustration shows how products are mapped to prices for the example we are discussing. The prices have been rounded off for simplicity.

![zon](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/zon/zon1.png)

The illustration given below shows how we obtained the result from the list of prices.

![zon](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/zon/zon2.png)

## Solution
This feature can be easily implemented using hashing, meaning dictionaries in python. For every item price, p_i, we will look for p_i - n in the hashmap. Then, we will check whether each product’s complement exists in the hashmap or not. This will continue until a product’s complement is found, and the indices of these products will be returned.

The algorithm’s complete steps are given below:
* Create a hashmap called buffer, which will be used to store the products’ prices.
* Then, iterate over the itemPrices list and calculate the remaining amount for each product by subtracting its price from the given amount.
* Check if the remaining amount is present in the buffer; if it’s not present, add this amount in the hashmap as a key and set the index i as the value.
* On the other hand, if the remaining amount is present in the buffer, return a list containing the value (index) of the product from the hashmap with the key equal to the remaining amount and the index of the current product, i.

The illustration below shows this process step by step:

![zon](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/zon/zon3.png)
![zon](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/zon/zon4.png)
![zon](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/zon/zon5.png)
![zon](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/zon/zon6.png)
![zon](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/zon/zon7.png)
![zon](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/zon/zon8.png)

The implementation of this algorithm is given below:

{% highlight java %}
class Solution {
    static public int[] suggestTwoProducts(int[] itemPrices, int amount){
        HashMap<Integer, Integer> buffer = new HashMap<>();
        for(int i = 0; i < itemPrices.length; i++){
            int price = itemPrices[i];
            int remaining = amount - price;
            if (buffer.containsKey(remaining)){
                return new int[]{buffer.get(remaining), i};
            }
            else{
                buffer.put(price, i);
            }
        }  
        return null;  
    }
    public static void main( String args[] ) {
        int[] itemPrices = {2, 30, 56, 34, 55, 10, 11, 20, 15, 60, 45, 39, 51};
        int amount = 61;
        System.out.println(Arrays.toString(suggestTwoProducts(itemPrices, amount)));
    }
}
{% endhighlight %}

![zon](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/zon/zon9.png)

## Feature #2: Suggest Items for Special Offer

## Description
In this scenario, Amazon held a lucky draw contest and the customers who won, have been given a $200 shopping credit. The restriction placed by Amazon is that the customers can only buy up to three products. Now, we want to help the customer by suggesting a list of triplets that contain products worth $200. In other words, a triplet will be a package deal containing three products that sum up to $200, and we want to suggest as many triplets as possible. To implement this feature, you will have access to a list of products that the customer is likely to buy. These products will include products from the person’s wishlist and other products based on previous purchases.

Let’s say we are given a list of numbers containing the prices of products that the customer is likely to buy: {100, 75, 150, 200, 50, 65, 40, 30, 15, 25, 60}. In this example, the following triplets sum up to 200: {25, 100, 75}, {40, 100, 60}, {60, 75, 65}. Therefore, these are the products we will suggest to the customer. Notice that a product can be part of multiple package deals. Your program should return the prices of these products in a list, such as: { {25, 100, 75}, {40, 100, 60}, {60, 75, 65} }. The order of product prices in the final output does not matte

![zon](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/zon/zon10.png)
![zon](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/zon/zon11.png)
![zon](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/zon/zon12.png)
![zon](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/zon/zon13.png)
![zon](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/zon/zon14.png)

## Solution
This feature can also be implemented by using a dictionary. For every item with price, p_i, we need to find a pair of elements at list indices i + 1 to n that add up to 200 - p_i. To find the pair, we use the hashing technique mentioned in the previous lesson.

The following steps show the complete algorithm:
* First, we iterate the list and check if the price of the item at the current index is greater than 200. If so, the item can’t be part of a triplet in the result. Therefore, we will break from the loop.
* Next, check if the current value and previous value are the same. If this is true, then we will skip the current element.
* Now, call the twoProducts helper function with the itemPrices list and the current element’s index, i.
* In the twoProducts helper function, start iterating the list using the index j that starts from i + 1.
* Then, compute the complement by subtracting the prices of items at i and j from 200.
* For each complement, check if it already exists in the set called seen (you can also use a dictionary here). If it does not, store the current complement in the set.
* If the complement already exists in the set, this means that we have found the triplet. We will add the list of these three elements to the output list.
* Also, add itemPrices[j] into the seen set.

{% highlight java %}
class Solution {
    static public int[][] suggestThreeProducts(int[] itemPrices){
        ArrayList<int[]> res = new ArrayList<>();
        Arrays.sort(itemPrices);
        for(int i = 0; i < itemPrices.length; i++){
            if(itemPrices[i] > 200){
                break;
            }
            if(i == 0 || itemPrices[i - 1] != itemPrices[i]){
                twoProducts(itemPrices, i, res);
            }
        }
        return res.toArray(new int[res.size()][]); 
    }
    public static void twoProducts(int[] itemPrices, int i, ArrayList<int[]> res){
        HashSet<Integer> seen = new HashSet<>();
        int j = i + 1; 
        while(j < itemPrices.length){
            int complement = 200 - itemPrices[i] - itemPrices[j];
            if(seen.contains(complement)){
                res.add(new int[]{itemPrices[i], itemPrices[j], complement});
                while(j + 1 < itemPrices.length && itemPrices[j] == itemPrices[j + 1]){
                    j++;
                }
            }
            seen.add(itemPrices[j]);
            j++;
        }
    }
    public static void main( String args[] ) {
        int[] itemPrices = {100, 75, 150, 200, 50, 65, 40, 30, 15, 25, 60};
        System.out.println(Arrays.deepToString(suggestThreeProducts(itemPrices)));
    }
}
{% endhighlight %}

![zon](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/zon/zon15.png)

## Feature #3: Upselling Products

## Description
Amazon wants to upsell related products to the customer during checkout. Amazon wants to do this by recommending a single product picked randomly from a collection of several related products. You must implement three related features to recommend. First, you want to enable adding an item to the list of related products. Second, you want to enable removing an item from the list once it is deprecated. Lastly, you want to enable picking a random item from the list such that any item is equally likely to be picked. You must implement all of these features so that they run in O(1) time.

For this feature, we will keep track of the products by only using their IDs. The insertion, deletion, and retrieval will use the ID of the product. The following illustration shows how products are mapped to IDs:

![zon](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/zon/zon16.png)

## Solution
This data structure’s most important feature is recommending products at random in O(1) time. So, let’s consider the data structures with constant time lookup, including arrays and Hashtables.

If we consider storing all the products in the array, given the index of the element, accessing that element will take O(1)O(1) time. To implement the random functionality, we need to choose a random index first and then retrieve the array element. The problem with arrays is that deleting a value at an arbitrary index takes linear time.

Now, let’s consider HashMaps. In HashMaps, insertion, and deletion occur in constant time. However, we cannot fetch a random product with the identifier because HashMaps do not have identifiers. If we want to get a truly random product, we will have to first convert all the keys in the HashMap into a list and then choose randomly. This will be a linear-time operation.

Both of these data structures have their own advantages. To benefit from both, we will create a hybrid data structure to store the products.
* Insertion: For the insertion in our data, we will store the product in a list. The index at which this product is stored will be inserted into the HashMap as a value, and the key will be the product. Both of these operations will take O(1)O(1) time.
* Deletion: Using the HashMap, find the index at which the product exists. Swap the last product in the list, with the one to be removed. Then, change the key-value pair in the HashMap accordingly. Lastly, pop out the last element from the list.
* Get random: For this operation, we can choose a random index using the Random object in Java. Then, the product at this index will be returned using the list.

![zon](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/zon/zon17.png)

{% highlight java %}
class UpsellProducts{
    Map<Integer, Integer> productDict;
    List<Integer> productList;
    Random rand = new Random();

    /** Initialize your data structure here. */
    public UpsellProducts() {
        productDict = new HashMap<>();
        productList = new ArrayList<>();
    }

    /** Inserts a product to the dataset. Returns true if the dataset did not already contain the specified product. */
    public boolean insertProduct(int prod) {
        if (productDict.containsKey(prod)) 
            return false;
        productDict.put(prod, productList.size());
        productList.add(productList.size(), prod);
        return true;
    }

    /** Removes a product from the dataset. Returns true if the dataset contained the specified product. */
    public boolean removeProduct(int prod) {
        if (! productDict.containsKey(prod)) 
            return false;
        int last = productList.get(productList.size() - 1);
        int index = productDict.get(prod);
        productList.set(index, last);
        productDict.put(last, index);
        productList.remove(productList.size() - 1);
        productDict.remove(prod);
        return true;
    }

    /** Get a random product from the dataset. */
    public int getRandomProduct() {
        return productList.get(rand.nextInt(productList.size()));
    }
}

class Solution{
    public static void main (String args[]){
        UpsellProducts dataset = new UpsellProducts();
        dataset.insertProduct(1212);
        dataset.insertProduct(190);
        dataset.insertProduct(655);
        dataset.insertProduct(327);
        System.out.println(dataset.getRandomProduct());
        dataset.removeProduct(190);
        dataset.removeProduct(1212);
        System.out.println(dataset.getRandomProduct());
    }
}
{% endhighlight %}

![zon](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/zon/zon18.png)

## Feature #4: Copy Product Data

## Description
Amazon has acquired a grocery shopping website and is now integrating grocery shopping into their own website. In order to bootstrap their own site’s grocery section, they want to derive item relationships from the sales data of the company they acquired. The items in the affiliate’s store are stored as a linked list. For each product, we also have a pointer to the item that is most frequently bought with it. For example, the item most frequently bought with bread is eggs. In this example, the node for bread has a pointer to the node for eggs, in addition to whatever element is next in the list.

Now, you have been assigned the task of taking this linked list and making a deep copy of it for the new online store. The list’s Node will contain the following attributes:
* prod: The ID of the product
* next: Points to the next product in the list.
* related: Points to the product most frequently bought with the current product; this could also be empty if enough sales data about the product is not available.

The following illustration shows how products are mapped to IDs for the example we will be discussing below:

![zon](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/zon/zon19.png)

The following illustration shows an example of the list of products:

![zon](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/zon/zon20.png)

## Solution
To make a deep copy of the list, we will iterate over the original list and create new nodes via the related pointer or the next pointer. We can also use a Hashtable/dictionary to track whether the copy of a particular node is already present or not.

The complete algorithm is as follows:
* We will traverse the linked list starting at the head.
* We will use a dictionary/Hashtable to keep track of visited nodes.
* We will make a copy of the current node and store the old node as the key and the new node as the value in visited.
* If the related pointer of the current node, ii, points to the node jj and a clone of jj already exists in visited, we will use the cloned node as a reference.
* Otherwise, if the related pointer of the current node, ii, points to the node jj, which has not been created yet, we will create a new node that corresponds to jj and add it to visited.
* If the next pointer of the current node, ii, points to the node jj and a clone of jj already exists in visited, we will use the cloned node as a reference.
* Else, if the next pointer of the current node, ii, points to the node jj, which has not been created yet, we will create a new node corresponding to jj and add it to the visited dictionary.

The implementation of this algorithm is given below:

{% highlight java %}
class Node {
    public int prod;
    public Node next;
    public Node related;
    public Node(int prod){
        this.prod = prod;
    }
    public Node(int prod, Node next, Node related) {
        this.prod = prod;
        this.next = next;
        this.related = related;
    }
};

class Solution {

    // Visited hashmap 
    public static HashMap<Node, Node> visited = new HashMap<Node, Node>();

    public static Node copyProductRelations(Node head){

        if (head == null) {
          return null;
        }

        Node oldNode = head;

        // Creating the new head node.
        Node newNode = new Node(oldNode.prod);
        visited.put(oldNode, newNode);

        // Iterate on the linked list until all nodes are cloned.
        while (oldNode != null) {
          // Get the clones of the nodes referenced by related and next pointers.
          newNode.related = getClonedNode(oldNode.related);
          newNode.next = getClonedNode(oldNode.next);

          
          oldNode = oldNode.next;
          newNode = newNode.next;
        }
        return visited.get(head);
    }

    public static Node getClonedNode(Node node) {
       
        if (node != null) {
            
            if (visited.containsKey(node)) {
                // If its in the visited hashmap then return the new node reference from the hashmap
                return visited.get(node);
            } else {
                // Otherwise create a new node, add to the hashmap and return it
                visited.put(node, new Node(node.prod, null, null));
                return visited.get(node);
            }
        }
        return null;
    }
    
    public static void main(String args[]) {
        Node products = Utility.createList(new int[]{3, 1, 5, 4}, new int[]{2, 0, -1, 1});
        // The createList(values, pointer) is a utility function with parameters as: 
        // 1. values: an array of values to be stored in linked list, i.e., product IDs.
        // 2. pointer: an array containing indices of values that the "related" pointer
        // of the corresponding product will point to. 
        // This function creates the list and returns the head. 

        System.out.println("Original list:");
        System.out.println(Utility.listToString(products));
        // The listToString(head) function is also a utility function that returns 
        // string representation of the list.

        Node copied_list = copyProductRelations(products);
        System.out.println("Deep copy of list:");
        System.out.println(Utility.listToString(copied_list));
    }
}
{% endhighlight %}

![zon](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/zon/zon21.png)

## Feature #5: Order Processing Milestones

## Description
Let’s assume the Amazon team wants to collect stats of the number of orders processed. These stats will be presented in a quarterly report using a histogram. To collect data for this presentation, the devs have stored the number of orders for each day rounded down to the nearest significant milestone. For example, when we meet or exceed one million orders, we display “1M+ orders processed.” We continue to display the same message until another milestone is reached. For instance, when nine million orders or more are processed, we display “9M+ orders processed.” Every day, the rounded cumulative number of orders processed is appended to an array.

Now, your task is to find out how many days we spent jumping from one milestone to the next. You will be given the array containing the daily milestones. Assume that this array resets each quarter, so we start from 0 million. Let’s say the array is: {0, 1, 1, 2, 2, 2, 3, 4, 4, 4, 5, 5, 6, 7}. This array shows the stats for fourteen days. Now, you will also be given a value representing a certain milestone; suppose it is 4. This means that you need to find in which days the “4M+ orders processed” milestone occurred.

Your feature should return {7, 9}, which means that we remained at the 4M+ milestone from the 7th day to the 9th day. (The first day of the quarter is considered the 0th day. )

## Solution

To implement this feature, we can use a modified binary search approach. Let’s take a look at the step by step algorithm:
* First, we will implement a search() function that returns the first index at which we can insert a number, n, into milestones to keep it sorted.
* In the search() function, we will use two pointers, first and last, that point to either side of the array. Then, we calculate the mid of the array.
* If the milestone at mid is equal to or greater than target, the first day of the milestone will be in the left half (including the middle) of the list, and the right half of the list can be ignored. Otherwise, the left half of the list can be ignored, and we will focus on the right half.
* Now that we have the search(), we will use it to find the first occurrence of the target milestone. However, target might not be present in the milestone. This could happen if we jump two or more milestones in a day. Therefore, we will first check if the target is present in milestones. If it isn’t present, we will return [-1, -1].
* When the target is in the array, we need to find the last day of the milestone. To do this, we can search for target+1 in the milestones array using the search() function. After finding the first occurrence of target+1, we can subtract 1 to find the last day of the milestone.

The implementation of this solution is given below:

{% highlight java %}
class Solution {
    public static int search(int[] milestones, int n){
        int first = 0;
        int last = milestones.length;
        while (first < last){
            int mid = (first + last) / 2;
            if (milestones[mid] >= n)
                last = mid;
            else
                first = mid + 1;
        }
        return first;
    }
    public static int[] milestoneDays(int[] milestones, int target){
        int first_day = search(milestones, target);
        if (target == milestones[first_day]){
            int last_day = search(milestones, target+1)-1;
            return new int[]{first_day, last_day};
        }
        else
            return new int[]{-1, -1};
        
    }
    public static void main(String args[]) {
        int[] milestones = {0, 1, 1, 2, 2, 2, 3, 4, 4, 4, 5, 5, 6, 7};
        int target = 4;
        System.out.println(Arrays.toString(milestoneDays(milestones, target)));
    }
}
{% endhighlight %}

![zon](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/zon/zon22.png)

## Feature #6: Products Frequently Viewed Together

## Description
We want to improve the recommendation system of products at Amazon. For this purpose, the management has decided that if a group of products is searched or viewed back to back by users, these products are similar or related. So, if another user is browsing one of these products, we can recommend the other ones to them. To determine these similar products, we will look at the previous activities of all users and check if particular products are viewed back to back.

Your task is to create a module that is given a dataset of product IDs in the order they were viewed by the user. You will also be given a list of products that are likely similar. Your job is to find how many times these products occur together in the dataset. The order of their occurrence does not matter unless they are back to back without any other products in between.

For example, let’s say the dataset of product IDs you are given is:{3, 2, 1, 5, 2, 1, 2, 1, 3, 4}. The candidates for similar products are {1, 2, 3}. We can see that these products occur together twice in the dataset, first at indices 0 to 2 and then at 6 to 8. The function’s output should be the list of the occurrences’ starting indices, which in this example is {0, 6]}.

The following illustration shows how products are mapped to IDs:

![zon](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/zon/zon23.png)

The illustration given below represents the example discussed above.

![zon](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/zon/zon24.png)

## Solution

The basic idea behind this solution is to use a sliding window on the products dataset and keep a hashtable referring to the occurrences of the products in the sliding window. Another HashMap will be kept for the candidates. At each step, the HashMaps will be compared to check if a permutation of candidate products exists.
* We will first create a HashMap from the candidates list, called the candCount. This HashMap will have product IDs as keys and their frequency of occurrence as values.
* Then, we will use a sliding window with the capacity of candidates's size.
* We will also create a HashMap reference called prodCount for the products inside the sliding window.
* As the sliding window moves, we will recompute prodCount in constant time by adding one product to the right and removing one product from the left.
* While moving the sliding window, we will compare the HashMaps. If they are equal at any point, this means that the window is a permutation of the candidates list. So, we will update the result.
* The result will be returned at the end when the products list is completely traversed.

The implementation of this algorithm is given below:

{% highlight java %}
class HelloWorld {
    public static List<Integer> findSimilarity(int[] products, int[] candidates) {
        int prodN = products.length, candN = candidates.length;
        if (prodN < candN) return new ArrayList<Integer>();

        Map<Integer, Integer> candCount = new HashMap<>();
        Map<Integer, Integer> prodCount = new HashMap<>();
      
        for (int i : candidates) {
            if (candCount.containsKey(i)) {
                candCount.put(i, candCount.get(i) + 1);
            }
            else {
                candCount.put(i, 1);
            }
        }

        List<Integer> output = new ArrayList<>();
        for (int i = 0; i < prodN; ++i) {
            int k = products[i];
            if (prodCount.containsKey(k)) {
                prodCount.put(k, prodCount.get(k) + 1);
            }
            else {
                prodCount.put(k, 1);
            }
            
            if (i >= candN) {
                k = products[i - candN];
                if (prodCount.get(k) == 1) {
                    prodCount.remove(k);
                }
                else {
                    prodCount.put(k, prodCount.get(k) - 1);
                }
            }
            
            if (candCount.equals(prodCount)) {
                output.add(i - candN + 1);
            }
        }
        return output;
    }
    public static void main( String args[] ) {
        int[] products = {3, 2, 1, 5, 2, 1, 2, 1, 3, 4};
        int[] candidates = {1, 2, 3};
        System.out.println(findSimilarity(products, candidates));
    }
}
{% endhighlight %}

![zon](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/zon/zon25.png)

## Feature #7: Optimize Delivery Cost

## Description
In addition to other important tasks, Amazon’s logistic division is responsible for delivering packages. They have partnered with many delivery services so that the orders can reach customers quickly. One of the carrier companies has pricing criteria; we want to use that criteria to our advantage so that we can deliver maximum packages at minimum cost. This carrier is willing to send one or more trucks for deliveries as needed, but they charge in increments of kk lbs. The vendor has different size truck (in increments of kk lbs) available. Anything below kk lbs costs $10. Whereas, anything between kk and 2k2k lbs costs $20 and so on. If we ship anything less than n∗k lbs, where nn is a natural number, we are not fully utilizing the money we’re spending. So, we want to fully utilize the cost.

Your task is to write a program looks at the current lineup of the packages and determines if we can fully utilize the cost by delivering n number of packages from the lineup; n is greater than or equal to 2. One thing to note is that the packages are arranged so that adjacent packages are to be delivered to near locations. So, we always want adjacent packages to be delivered together. Therefore, the chosen n packages should appear back to back in the lineup.

Consider an example where the weights of the packages are given to you in the form of an array, {11, 42, 54, 44, 49, 26}, and the value of k is 10. Now, we need to check if we can efficiently load and utilize the delivery contractor given the packages in the delivery dock. The example should return True because the mentioned condition is satisfied.

## Solution
To solve this problem, we will calculate the cumulative sum of the products in the array and use the remainder theorem to determine if n products containing the sum of weights equal to n * k exist or not. Let’s take a look at the complete algorithm.

* First, we will find the cumulative sums up to the i^{th} index and find the remainder after the division of the sum by k.
* Then, these remainders will be stored in a hash table structure, and the cumulative sum will be equal to the remainder. However, before storing the reminder in the hash table, we will check if the value of remainder already exists for any other index, jj. If the value does not exist, we will add another entry in the hash table.
* If the remainder already exists, this is the case we are looking for. To understand this, let’s take a look at the remainder theorem:
   * (a+(n * k))\%k = (a\%k)(a+(n∗k))%k=(a%k)

* In case of the [11, 42, 54, 44, 49, 26] array and k = 10, the current sums are [11, 43, 57, 51, 50, 26] and the remainders are [1, 3, 7, 1, 0, 6]. We have remainder 1 at index 0 and at index 3. This means that in between these two indexes, including the right bound, we must have added a number that is a multiple of k. If indexes i and j give the same remainder, the values at i + 1 to j will satisfy the condition. So, for this example, [42, 54, 44] sum up to a multiple of k.
* If the same remainder value is encountered again during the traversal, we return True directly.

{% highlight java %}
class Solution {
    public static boolean checkDelivery(int[] packages, int k) {
        int currSum = 0;
        HashMap < Integer, Integer > map = new HashMap < > ();
        map.put(0, -1);
        for (int i = 0; i < packages.length; i++) {
            currSum += packages[i];
            if (k != 0)
                currSum = currSum % k;
            if (map.containsKey(currSum)) {
                if (i - map.get(currSum) > 1)
                    return true;
            } else
                map.put(currSum, i);
        }
        return false;
    }

    public static void main(String args[]){
        int[] packages = {58, 42, 46, 49, 331, 26, 6, 37, 3};
        int k = 10;
        System.out.println(checkDelivery(packages, k));
    }
}
{% endhighlight %}

![zon](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/zon/zon26.png)

## Feature #8: Merge Recommendations

## Description
Amazon has acquired a new company that already has a database of user-profiles and their corresponding product recommendation data. Now, Amazon wants to check if any of their current users have an account on the acquired website, so they can use the recommendation data. To accomplish this, Amazon has decided to merge the users’ accounts. We will be using the name of the user and the emails associated with their account to determine if multiple accounts belong to the same person. A person may have provided primary, secondary, tertiary emails, etc when setting up an account on either of the websites

You will be given a 2D array of accounts. Each element, accounts[i], is an array of strings, such that accounts[i][0] is a name while the remaining elements are emails associated with that account. You have to determine if two accounts belong to the same person by checking if both accounts have at least one email in common. Remember that if two accounts have the same name, they might belong to different people, as people can have the same name. However, all accounts that belong to one person will have the same name. Moreover, there can be more than two accounts made by one person.

The output should be the merged accounts in which the first element of each account is the name and the rest of the elements are emails in sorted order.

![zon](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/zon/zon27.png)

## Solution
This feature can be mapped to a graph problem. We draw an edge between two emails, in case they occur in the same account. From here, the problem comes down to finding the connected components of this graph.

The complete algorithm is as follows:
* First, we will build an undirected graph by creating an edge from the first email to all the other emails in the same account. Each email is treated as a node and an adjacency graph will be made.
* Additionally, we’ll remember a map from emails to names on the side.
* Now, we will use a depth-first search starting with the first email.
* We will find all the nodes/emails that can be reached from the current email and denote it as a connected component. Then, we will add the respective name and this component, in sorted order, to the final answer.
* We will keep track of the visited nodes. If a visited node is found, this means that it was already a part of a previous component, so we can skip it.

{% highlight java %}
class Solution {
    public static List<List<String>> accountsMerge(String[][] accounts){
        HashMap<String, String> emailToName = new HashMap<String, String>();
        HashMap<String, Set<String>>graph = new HashMap<String, Set<String>>();

        for(String[] acc : accounts){
            String name = acc[0];
            for(int i = 1; i < acc.length; i++){
                String email = acc[i];
                if(!graph.containsKey(acc[1])){
                    graph.put(acc[1], new HashSet<String>());
                }
                graph.get(acc[1]).add(email);
                if(!graph.containsKey(email)){
                    graph.put(email, new HashSet<String>());
                }
                graph.get(email).add(acc[1]);
                emailToName.put(email, name);
            }
                
        }
            

        Set<String> seen = new HashSet<String>();
        List<List<String>> ans = new ArrayList<List<String>>();
        for (String email: graph.keySet()) {
            if (!seen.contains(email)) {
                seen.add(email);
                Stack<String> stack = new Stack<String>();
                stack.push(email);
                List<String> component = new ArrayList<String>();
                while (!stack.empty()) {
                    String node = stack.pop();
                    component.add(node);
                    for (String nei: graph.get(node)) {
                        if (!seen.contains(nei)) {
                            seen.add(nei);
                            stack.push(nei);
                        }
                    }
                }
                Collections.sort(component);
                component.add(0, emailToName.get(email));
                ans.add(component);
            }
        }
        return ans;
    }
    

    public static void main( String args[] ) {
        // Driver Code
        String[][] accounts = { {"Sarah", "sarah22@email.com", "sarah@gmail.com", "sarahhoward@email.com"},
            {"Alice", "alicexoxo@email.com", "alicia@email.com", "alicelee@gmail.com"},
            {"Sarah", "sarah@gmail.com", "sarah10101@gmail.com"},
            {"Sarah", "sarah10101@gmail.com", "misshoward@gmail.com"} };
        System.out.println(accountsMerge(accounts));
    }
}
{% endhighlight %}

![zon](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/zon/zon28.png)

## Feature #9: Products in Price Range

## Description
In this feature of the Amazon website, we want to implement a search filter that searches for products in a given price range. The product data is given to us in the form of a binary search tree, where the values are the prices. You will be given the parameters low and high; these represent the price range the user selected. This range is inclusive.

For example, let’s consider the following list of products that are mapped to their prices. The prices have been rounded off for simplicity.

![zon](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/zon/zon29.png)

These products have been stored in the binary search tree based on their prices as such:

![zon](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/zon/zon30.png)

Now, let’s assume that the price range selected by the user is low = 7 and high = 20. In this case, your function should return {9, 8, 14, 20, 17}. The order of products in the output does not matter.

## Solution

We can implement this feature by using a variation of the preorder traversal on the binary tree. Other binary tree traversals can also be used. The complete algorithm is given below:
* We will use a recursive helper function for the preorder traversal.
* In this function, we will first check if the value at the current node is in the given range or not. If the value is in range, we will add it to the output array.
* Then, we will recursively call the preorder function on the left child of the node, but only if the value of the current node is greater than or equal to low. This way we will minimize the traversal.
* Similarly, if the value of the current node is less than or equal to high, we will also recursively traverse the right child of the node.
* The output will be returned when the traversal is done.

{% highlight java %}
public class BinarySearchTree{
    public Node root;
    public BinarySearchTree(){
        this.root = null;
    }

    public void insert(int val){
        if (this.root == null)
            this.root = new Node(val);
        else
            this.root.insert(val);
    }
}

class Node{
    public int val;
    public Node leftChild;
    public Node rightChild;

    public Node(int val){
        this.val = val;
        this.leftChild = null;
        this.rightChild = null;
    }

    public void insert(int val){
        Node current = this;
        Node parent = current;
        while (current != null){
            parent = current;
            if (val < current.val)
                current = current.leftChild;
            else
                current = current.rightChild;
        }
        if(val < parent.val)
            parent.leftChild = new Node(val);
        else
            parent.rightChild = new Node(val);
    }
}

class Solution {
    public static void preOrder(Node node, int low, int high, List<Integer> output){
        if (node != null) {
            if (node.val <= high && low <= node.val)
                output.add(node.val);
            if (low <= node.val)
                preOrder(node.leftChild, low, high, output);
            if (node.val <= high)
                preOrder(node.rightChild, low, high, output);
        }
    }
    public static List<Integer> productsInRange(Node root, int low, int high){
        List<Integer> output = new ArrayList<Integer>();
        preOrder(root, low, high, output);
        return output;
    }
    public static void main( String args[] ) {
        // Driver code
        BinarySearchTree bst = new BinarySearchTree();
        bst.insert(9);
        bst.insert(6);
        bst.insert(14);
        bst.insert(20);
        bst.insert(1);
        bst.insert(30);
        bst.insert(8);
        bst.insert(17);
        bst.insert(5);

        System.out.println(productsInRange(bst.root, 7, 20));
    }
}
{% endhighlight %}

![zon](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/zon/zon31.png)

