---
layout: default
title: Plagiarism Checker
parent: Coding Interview
has_children: true
nav_order: 9
permalink: /coding_interview/plagiarism
---
<div align="center" markdown="1">
Plagiarism Checker / Java resources / Tutorial

{: .fs-8 .fw-400 }
</div>

## Plagiarism Checker

## Project Description for Plagiarism Checker

## Introduction
Plagiarism means presenting someone else’s work as your own. With the advent of the Internet, it has become very easy to plagiarize. A plagiarism checker application locates instances of similar content within someone’s work or documents. This application is widely used in the academic industry to catch plagiarism cases within student’s work.

The scenario and problems we will discuss in this chapter relate to the identifying similar content functionality and how we can improve it.

## Statement
Assume you are a developer hired by an educational institute to improve their current plagiarism checker application. The institute wants you to add the ability to catch plagiarism between multiple students’ code snippets.

We will follow a new strategy where we convert code snippets into specific alphabetic tokens. These tokens can then be matched against each other to filter out what content and how much content is the same. Students can add dummy statements or comments between copied content to throw off the application. So, we need our application to be robust to this sort of modification. We also need to return the number of sources a given document may have been copied from and highlight the similar portions in two documents.

## Features
We will need to introduce the following features to implement the functionalities discussed above:
* Feature #1: Match a student’s code with the rest of the class’s code samples to identify the number of possible matches.
* Feature #2: Match code samples of two students to identify which part has been copied and altered to avoid plagiarism detection.

Understanding these feature requests and designing their solutions will help us implement the requested functionality into the plagiarism application. In the next few lessons, we’ll discuss the recommended implementations of these features. Before we start, we suggest that you think about how you would implement these features. As you do, you’ll realize some of the underlying problems that you’ll need to solve. The solutions to these basic problems are also applicable to other common coding interview questions.

## Feature #1: Possible Matches

## Description
We are given a set of documents. Each document is submitted by a different individual. However, we suspect that some individuals may have copied from others. Given a plagiarised submitted document, we want to identify the number of documents with which there is a potential match. We have converted each document into a set of tokens based on their content. As mentioned previously, the students could have added dummy statements between the copied content to avoid identification. We’ll have to match the tokens of two students while taking into account that there can be dummy tokens that might not match. A potential match can occur if one token results in the subsequence of the other token. It is not a guarantee that every match is plagiarized content. In this scenario, we’ll discard the matched tokens that have a length less than two.

We’ll be provided with a string, plagiarised, and an array, students. The plagiarised will contain the tokens against which we’ll match the code samples present in the students array. We have to return the number of possible students in a class the plagiarised content may have been copied from.

## Solution
The size of the plagiarised variable can be very large considering the amount of code converted to tokens. We’ll try to traverse this string only once to efficiently identify plagiarism. We can create a dictionary, called waitingList, for code tokens in students. students is an array containing tokenized submitted documents by different students. For example, four students submitted different documents that have been tokenized to a, bb, acd, and ace, respectively. In this scenario, ace may have been copied from a, with an addition of ce to try to deceive the plagiarism detector.

Initially, we’ll group the tokens in students with their starting character. For example, if we have students = ['a', 'bb', 'acd', 'ace'], we can group them as 'a' : ('a', 'acd', 'ace'), 'b' : ('bb'). The words are grouped by what letter they are currently waiting for to appear in plagiarised as we traverse through it. While traversing over plagiarised, we’ll keep modifying our waitingList depending upon the next waiting letter. For example, consider a string like plagiarised = 'abcde':

waitingList = 'a' : ('a', 'acd', 'ace'), 'b' : ('bb') at beginning;

waitingList = 'c' : ('cd', 'ce'), 'b' : ('bb'), None : ('a') after plagiarised[i] = 'a';

waitingList = 'c' : ('cd', 'ce'), 'b' : ('b'), None : ('a') after plagiarised[i] = 'b';

waitingList = 'd' : ('d'), 'e' : ('e'), 'b' : ('b'), None : ('a') after plagiarised[i] = 'c';

waitingList = 'e' : ('e'), 'b' : ('b'), None : ('a', 'acd') after plagiarised[i] = 'd';

waitingList = 'b' : ('b'), None : ('a', 'acd', 'ace') after plagiarised[i] = 'e';

We will keep track of all the code tokens in the students array simultaneously. The dictionary structure tracks the progress of how much each word in students matches with plagiarised. We update the progress of each word in students whose letter occurs in plagiarised and store the modified arrays. If we use the last letter of a word, we add it as a value against the None key. Finally, comparing the length of the array against the None key will give us the number of possible matches.

The following illustration will clarify this process further.

![zon](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/zon/zon50.png)
![zon](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/zon/zon51.png)
![zon](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/zon/zon52.png)
![zon](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/zon/zon53.png)
![zon](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/zon/zon54.png)
![zon](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/zon/zon55.png)
![zon](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/zon/zon56.png)

{% highlight java %}
import java.util.*;
import java.text.StringCharacterIterator;

class Solution {

  public static int possibleMatches(String S, String[] words) {
    List<StringCharacterIterator>[] waitingList = new List[128];
    for (int c = 0; c <= 'z'; c++)
        waitingList[c] = new ArrayList();
    for (String w : words)
        waitingList[w.charAt(0)].add(new StringCharacterIterator(w));
    for (char c : S.toCharArray()) {
        List<StringCharacterIterator> advance = waitingList[c];
        waitingList[c] = new ArrayList();
        for (StringCharacterIterator it : advance)
            waitingList[it.next() % it.DONE].add(it);
    }
    return waitingList[0].size();
  }

  public static void main( String args[] ) {
    // Driver code

    String plagiarised = "abcde";
    String students[] = {"a","bb","acd","ace"}; 

    System.out.print("The content was copied from " + possibleMatches(plagiarised, students) + " students");
  }
}
{% endhighlight %}

![zon](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/zon/zon57.png)

## Feature #2: Return Match

## Description
Now, we need to identify the plagiarized code snippets from two sets of code sample tokens. We will use the same rules from the previous feature to match the tokens. For a cheating student, we need to locate all the instances of copied content, keeping in mind that some text may have been inserted to make a copied submission look different than the original. Like before, we have to avoid dummy statements or comments. We will do this by returning the copied tokens as a subsequence match for the second student’s code tokens. In the cheater string, there could be many subsequences of different sizes that can match with student. We will have to fetch the smallest of them.

We’ll be provided with two strings: cheater and student. We have to return the smallest subsequence of student that occurs in the cheater (if it exists).

## Solution
Initially, we can search for the first occurrence of the subsequence. Then, we can find the subsequence in the opposite direction to find the smaller one. For example, if we have student = ab and cheater = acab, the first occurrence would result in acab, and we’ll start searching in the opposite direction. When b is matched, we’ll look for the most recent a in cheater, which will give us ab as our final result. We can then apply this method to bigger strings as well.

The following illustration might clarify this process.

![zon](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/zon/zon58.png)
![zon](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/zon/zon59.png)
![zon](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/zon/zon60.png)
![zon](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/zon/zon61.png)
![zon](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/zon/zon62.png)
![zon](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/zon/zon63.png)
![zon](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/zon/zon64.png)
![zon](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/zon/zon65.png)
![zon](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/zon/zon66.png)

Let’s see how we might implement this functionality:
1. Traverse the cheater string, and for each letter, check if it’s equal to the current letter in student.
2. If the letters are equal, move to the next letter in both the strings.
3. When the last letter of student is matched with a letter of cheater, mark that letter position of cheater as a possible window.
4. Now, go backward from the end of student and match the letters with cheater from the marked position. Do this until the student string is exhausted.
5. Check if your current window is smaller than the previous one. If yes, mark it as the minimum window.
6. Repeat from step 2 until you reach the end of cheater.

Let’s look at the code for the solution below:

{% highlight java %}
class Solution {
  public static String match(String cheater, String student) {
    String window = "";
    int j = 0, min = cheater.length() + 1;
    for (int i = 0; i < cheater.length(); i++) {
      if (cheater.charAt(i) == student.charAt(j)) {
        j++;
        if (j == student.length()) {
          int end = i + 1;
          j--;
          while (j >= 0) {
            if (cheater.charAt(i) == student.charAt(j)) j--;
            i--;
          }
          j++;
          i++;
          if (end - i < min) {
            min = end - i;
            window = cheater.substring(i, end);
          }
        }
      }
    }
    return window;
  }

  public static void main(String[] args){
    // Driver code

    String cheater = "quiqutit";
    String student = "quit";

    System.out.print("Copied Content: " + match(cheater, student));

    
  }
}
{% endhighlight %}

![zon](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/zon/zon67.png)
