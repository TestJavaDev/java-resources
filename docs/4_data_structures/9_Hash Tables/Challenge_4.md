---
layout: default
title: Challenge 4
parent: Hash Tables
grand_parent: Data Structures
nav_order: 4
permalink: /data_structures/hash_tables/ch4
---
<div align="center" markdown="1">
Challenge 4 / Java resources / Tutorial

{: .fs-8 .fw-400 }
</div>

## Challenge 4: Trace the complete path of a journey

Given a HashMap with all the points, can you find the starting point and print out the complete path from start to end? A solution is placed in the "solution" section to help you, but we would suggest you try to solve it on your own first.

## Problem Statement
In this problem, you have to implement the tracePath() function to find the starting point of a journey and print out the complete path from start to end. An illustration is also provided for your understanding.

## Function Prototype:
String tracePath(HashMap<String,String> map);
Here, map is a HashMap containing strings as keys and values corresponding to the cities, where the key is the departure city and the value is the arrival city

## Output:
It returns the String containing the complete path from the start until the end of the journey.

![has](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/has/has29.png)

## Explanation
The starting point of the path is “Boston”, so we find it first to help us traverse the whole path; we get to Texas through Boston, to Missouri through Texas, and so on.

![has](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/has/has30.png)

## Coding Exercise

{% highlight java %}
//Hash Set  =>  HashSet<Integer> hSet = new HashSet<>();
//HashMap   =>  HashMap<Integer,String> hMap = new HashMap<>();  
//HashTable =>  Hashtable<Integer,String> hTable = new Hashtable<>();  
//Hash Set Functions => {add(), remove(), contains()}
//Hash Map and Table Functions => {put(key,value), get(key), remove(key), containsKey(key), containsValue(value)}
class CheckPath {

  public static String tracePath(Map<String,String> map) {

    String result = "";

    // Write - Your - Code        
    return result; 
  }
}
{% endhighlight %}

## Solution Review: Trace the complete path of a journey

## Solution: A Hash Table to Deduce The Starting Point

{% highlight java %}
//Hash Set  =>  HashSet<Integer> hSet = new HashSet<>();
//HashMap   =>  HashMap<Integer,String> hMap = new HashMap<>();  
//HashTable =>  Hashtable<Integer,String> hTable = new Hashtable<>();  
//Hash Set Functions => {add(), remove(), contains()}
//Hash Map and Table Functions => {put(key,value), get(key), remove(key), containsKey(key), containsValue(value)}
class CheckPath {

  public static String tracePath(Map < String, String > map) {

    String result = "";

    //Create a reverse Map of given map i.e if given map has (N,C) then reverse map will have (C,N) as key value pair
    //Traverse original map and see if corresponding key exist in reverse Map
    //If it doesn't exist then we found our starting point.
    //After starting point is found, simply trace the complete path from original map.

    HashMap < String,String > reverseMap = new HashMap < >();

    //To fill reverse map, iterate through the given map
    for (Map.Entry < String, String > entry : map.entrySet())		
      reverseMap.put(entry.getValue(), entry.getKey());

    //Find the starting point of itinerary
    String from = "";

    //Check if graph is disconnected
    int count = 0;

    for (Map.Entry < String, String > entry: map.entrySet()) {
      if (!reverseMap.containsKey(entry.getKey())) {
        count++;
        from = entry.getKey();
        //break;
      }
    }

    if(count > 1){
      return "null"; // Disconnected graph
    }

    //Trace complete path
    String to = map.get(from);

    while (to != null) {
      result += from + "->" + to + ", ";
      from = to;
      to = map.get(to);
    }
    //System.out.println(result);

    return result;
  }

  public static void main(String[] args) {
    HashMap<String,String> hMap = new HashMap<>();  

    hMap.put("NewYork","Chicago");
    hMap.put("Boston","Texas");
    hMap.put("Missouri","NewYork");
    hMap.put("Texas","Missouri");

    String actual_output = CheckPath.tracePath(hMap);

    System.out.println(actual_output);
  }
}
{% endhighlight %}

![has](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/has/has31.png)