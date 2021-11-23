---
layout: default
title: Card Game
parent: Coding Interview
has_children: true
nav_order: 15
permalink: /coding_interview/card
---
<div align="center" markdown="1">
Card Game / Java resources / Tutorial

{: .fs-8 .fw-400 }
</div>

## Card Game

## Project Description for Card Game

## Introduction
There are countless variations of card games played all around the world, and these games are popular with people of all ages. Card games are played using a deck of playing cards, and a standard deck consists of 52 cards. All of the cards are divided into four suits:
* Spade suit ♠️
* Club suit ♣️
* Hearts suit ♥️
* Diamond suit ♦️

There are thirteen cards of each suit, including a 2, 3, 4, 5, 6, 7, 8, 9, a jack, a queen, a king, and an ace. Note that there is no 1.

## Statement
Suppose you are working for a startup that is creating a web application to play different card game variations. They are planning to design traditional card games like poker as well as introduce their own custom games. All of these games can be played in single-player mode. Therefore, your team also needs to create a computer player to play against users.

Your first task will be to implement a feature that helps the computer player play a variation of poker. We will have to determine if a hand of given cards is a hand of straights or not. For the next feature, we will create a feature for a custom card game called Fizzle. In this feature, the computer player has to find the maximum points that can be obtained by picking out cards from a set of ten revealed random cards.

## Features
We will need to introduce the following features to implement the functionality discussed above:
* Feature #1: Determine if a hand of straights is possible.
* Feature #2: Find the maximum points that can be obtained from a set of ten random cards.

In the coming lessons, we will discuss these features and their solutions in detail, so that you’ll be able to map the solution to this scenario to different interview problems as well.

## Feature #1: Hand of Straights

## Description
For the first feature, we will be working on a variation of Poker. In traditional poker, players form sets of five playing cards, called hands. This feature is concerned with a hand of Straights. Traditionally, a hand of straight is formed by five cards of sequential ranks, such as 9♣, 8♠, 7♠, 6♥, and 5♥. However, in our variation of Poker, a number kk will be determined by rolling a dice 🎲. Then, a hand of straights is only possible if kk sets of cards can be formed using all of the cards in the hand. Each group will consist of kk cards of sequential rank.

If the dice rolls a 1, we roll it again. Therefore, you can assume that kk will always be in the 2 - 6 range.

Let’s try to understand this better with an example:

![bog](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/bog/bog26.png)

In the example given above, the player was dealt a hand containing nine cards. The dice rolled a 3, so kk will be 3. Then, we rearranged the cards into groups, containing three cards in sequential order. During implementation, we will receive these cards in the form of an array, such as {10, 3, 6, 2, 13, 12, 5, 4, 7}. The jack, queen, and king cards are denoted by 11, 12, and 13, respectively. The number after rolling dice will be given as an integer, like 3. Your module should return true if a hand of straights can be formed. Otherwise, it should return false.

## Solution
The main intuition behind this solution is trying to form groups of size k starting with the lowest card. Once we identify the lowest card, a hand of straights is only possible if the lowest card is at the bottom end of a k sized group. For example, if k is 4 and the lowest card is 2, then we know that the group will be {2, 3, 4, 5}. If we cannot find such a group, our hand is not a hand of straights.

Let’s take a look at the complete algorithm:
1. First, check if the number of cards in hand is divisible by k. If not, this means we can’t create groups, so return false.
2. We want to count the occurrences of each card in the given hand, irrespective of the suit.
3. Then, we will sort the list and start traversing it from the card with the lowest ranking. We will do this in a hash map by storing card numbers as keys and occurrences as values.
4. In a nested loop that runs k times, we will check if the current card and the next k-1 cards (in increasing ranking) are in the count dictionary. If any one of them doesn’t exist, we will return false.
5. When each of the required cards is found, we will decrease its number of occurrences in the count.
6. After a complete group is found, use a while loop to find the next group’s smallest card and determine which of the next cards in count has more than zero occurrences left.
7. The function will return true if all cards are sorted into groups.

{% highlight java %}
class Solution {
    public static boolean isHandOfStraights(int[] hand, int k){

        if(hand.length % k != 0){
            return false;
        }

        Map<Integer, Integer> count = new TreeMap<>();
        for (int i : hand){
            count.put(i, count.getOrDefault(i, 0)+1);
        }
        
        Arrays.sort(hand);
        int i = 0;
        int n = hand.length;
        
        while(i < n){
            int current = hand[i];
            for(int j = 0; j < k; j++){
                if(!count.containsKey(current + j) || (count.get(current + j) == 0)){
                    return false;
                }
                count.put(current + j, count.get(current + j) - 1);
            }
            while(i < n && count.get(hand[i]) == 0){
                i +=1;
            }
        }

        return true;
    }
    public static void main( String args[] ) {
        int[] hand = {5,2,4,4,1,3,5,6,3};
        int k = 3;
        System.out.println(isHandOfStraights(hand, k));
        hand = new int[] {1,9,3,5,7,4,2,9,11};
        k = 2;
        System.out.println(isHandOfStraights(hand, k));
        
    }
}
{% endhighlight %}

![bog](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/bog/bog27.png)

## Feature #2: Maximum Points You Can Obtain from Cards

## Description
In this scenario, you will be working on a custom card game named Fizzle. In Fizzle, the dealer shuffles the deck and spreads out all the cards facing upwards in a linear fashion. Then, players take turns rolling a dice. Suppose the number rolled is kk. Players will then take turns to remove kk cards from the deck, but the players can only pick cards from either the deck’s right or left side. Each player’s goal is to pick out the cards with maximum points. Each numbered card has points corresponding to its number, and the faced cards, jack, queen, king, and ace, have 11, 12, 13, and 14 points, respectively.

Our task is to create a feature for Fizzle’s computer player. We will be given the deck’s current state and the number the player rolled. We need to determine the maximum score that the player can obtain on that turn.

Let’s take a look at the following example:

![bog](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/bog/bog28.png)

In the example above, the player picked the cards 5, 3, 6, and 3, in the given order, to obtain the maximum points possible. During implementation, we will receive this deck of cards in the form of an array, like {5, 3, 4, 4, 2, 3, 4, 6, 3}. The number after rolling dice will be given as an integer, such as 4. Your module should return the maximum number of points obtained as an integer.

## Solution
To implement this feature, we will test every possible combination in which k cards can be picked from the deck from either the left or right side. Few things to consider are that we cannot pick the n \text{th}nth card from the right unless the (n-1)\text{th}(n−1)th card from the right is picked. The same condition holds for the left side. Moreover, we know that if we pick all kk cards from the right, then 00 cards will be picked from the left. Similarly, if we pick k-1k−1 cards from the right, then 11 card will be picked from the left side, and so on. This means that we can find all possible combinations possible by assuming a sliding window with kk size that wraps from right to left. The maximum sum found by trying all combinations will be the output.

Let’s take a look at the complete algorithm:
* First, we will assume that the k cards on the right side give us the maximum points.
* Then, we will use a loop that runs k times and test all the remaining combinations.
* right and left will be two pointers that keep track of the sliding window. Initially, left will be 0 and right will be deck.length - k.
* In each iteration of the loop, we will remove the points of the card at the right side and add the points of the left side.
* Then, we will compare the total points with the current best points and keep the maximum one.

This algorithm is illustrated below:

![bog](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/bog/bog29.png)
![bog](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/bog/bog30.png)
![bog](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/bog/bog31.png)
![bog](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/bog/bog32.png)
![bog](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/bog/bog33.png)

Let’s take a look at the algorithm’s implementation:

{% highlight java %}
class Solution {
    public static int maxPoints(int[] deck, int k) {
        int left = 0;
        int right = deck.length - k;
        int total, best; 
        total = 0;
        for(int i = right; i < deck.length; i++ ){
            total += deck[i];
        }
        best = total;
        for(int i = 0; i < k; i++){
            total += deck[left] - deck[right];
            best = Math.max(best, total);
            left += 1;
            right += 1;
        }
        return best; 
    }

    public static void main( String args[] ) {
        int[] deck = {5,3,4,4,2,3,2,6,3};
        int k = 4;
        System.out.println(maxPoints(deck, k));
    }
}
{% endhighlight %}

![bog](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/bog/bog34.png)