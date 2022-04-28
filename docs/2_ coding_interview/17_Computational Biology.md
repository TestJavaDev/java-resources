---
layout: default
title: Computational Biology
parent: Coding Interview
has_children: true
nav_order: 17
permalink: /coding_interview/computational
---
<div align="center" markdown="1">
Computational Biology / Java resources / Tutorial

{: .fs-8 .fw-400 }
</div>

## Computational Biology

## Project Description for Computational Biology

## Introduction
Since the discovery of Deoxyribonucleic acid (DNA) and Ribonucleic acid (RNA), computer science found lots of applications in biology. An entire field called Computational Biology exists to apply computer science to biology problems.

The scenario and the problems discussed in this chapter also relate to the DNA and protein sequences that are dealt within Computational Biology.

## Statement
Assume you are a developer in a biology lab. You are tasked with creating simulations for DNA transformation of different species. The biology lab wants you to write a suite of programs for processing of DNA and proteins.

We’ll start by analyzing whether it is possible to convert a DNA sequence of one species to another by changing or replacing their genes. During this mutation, some virus sequences were observed which we’ll isolate. After this, we’ll explore different proteins that can provide immunity against the identified viruses.

## Features
We will need to introduce the following features to implement the functionalities we discussed above:
* Feature #1: Determine if an unknown DNA sequence differs from a known DNA sequence by only a single gene replacement.
* Feature #2: A new virus is known to infect species by inserting long sequences of k unique nucleotides. Given a chromosome, determine if it is potentially infected by finding the longest subsequence with k unique nucleotides.
* Feature #3: Locate the palindrome structure in chromosomes to identify potential proteins.
* Feature #4: Proteins are known to have palindromic sequences. Determine if a given string could be a protein.

Understanding these feature requests and designing their solutions will help us implement the requested functionality into the computational biology software suite.

In the next few lessons, we’ll discuss the recommended implementations of these features. The solutions to these will also be applicable to other common coding interview questions.

## Feature #1: Mutate DNA

## Description
Every DNA strand contains multiple chromosomes of different types. The type of genes in these chromosomes varies in different DNA samples. We can mutate a single DNA sample of one species into another by replacing the genes in the chromosomes. However, we can only replace the genes from a list of available samples. For simplicity, let’s say that the genes in chromosomes are represented by lowercase English letters, a, b, c,..., etc. The available samples will be the twenty-six letter lexicon for alphabets. In a single replacement, we can replace all occurrences of the same type of genes with any other available sample from our list. Furthermore, gene replacement must be done one by one. For example, garlano could be converted to gorlono if a is replaced with o. Then, if o is replaced with t, it becomes gtrltnt.

We’ll be provided with two chromosome samples from different DNAs in the form of strings. The genes in these chromosome samples can be of the same or different types. Our task will be to determine whether one sample can be mutated to the other under the provided constraints.

![com](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/com/com1.png)
![com](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/com/com2.png)

For instance, if we replace all occurrences of a with c, all occurrences of b with d, and all occurrences of c with e, we can transform aabcc into ccdee. However, no substitutions can transform aabaa into aadac.

## Solution
The above examples demonstrate that to convert one sample to another, both samples have to contain the same number of genes. Each character of string1 needs to be converted to a corresponding character in string2. We can map each element in string1 to what it needs to be in string2. We can model this as a graph problem by representing the mapping relationship as the edges of a graph. The graph for the above mutable example can be represented as follows:

![com](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/com/com3.png)

The condition that all occurrences of the same gene need to be replaced in one iteration. This infers that a single gene in string1 can only be mapped to a single gene in string2. This means a single node of the graph can have only one outer edge. Otherwise, the mutation will not be possible. The graph for the above mutable example can be represented as follows:

![com](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/com/com4.png)

For example, we have two strings: str1 = "abc" and str2 = "bcd". To transform str1 into str2, we get the following chain of conversions:

transform chain = a -> b -> c -> d

If we start our conversions from the beginning of the chain, we will get stuck on our second iteration because we would get two mappings of b. If we start from the end, following c -> d, b -> c, and finally a -> b, our transformation will be possible. There is also a possibility of cycles in our graph. For example, let’s say we have two strings str1 = "ac" and str2 = "ca". We get the following chain of conversions if we want to transform str1 into str2:

transform chain = a -> c -> a

We can see that in this cyclic graph, we’ll get two mappings of a in the second iteration, which is not acceptable. Here, we can break the cycle by introducing a substitute value. This substitute value will come from the list of the available samples, which in our case is the twenty-six letter English lexicon. So, instead of c -> a, we can do c -> y and y -> a to get the following:

transform chain = c -> y, a -> c, y -> a

We can tolerate cycles as long as there are characters available in our lexicon to use as substitutes. Therefore, a mutation is only possible if and only if:

Each character edge forms a linear graph with every node having one out-degree

There should be characters available in the sample(lexicon) to use as substitutes if a cycle occurs.

Note: In our case, if the strings are of size 26, we can’t break cycles and mutation will not be possible.

Here is how we will implement this feature:
1. Initialize a HashMap to store the character mapping.
2. Traverse through string1 and string2.
3. Update the HashMap with the string1[i] -> string2[i] mapping.
4. If one-or-more mapping is found, return False immediately.
5. Return size(set(string2)) < 26 at the end.

Let’s look at the code for the solution:

{% highlight java %}
import java.util.*;

class Solution {
    public static boolean mutateDNA(String s1, String s2) {
        if (s1.equals(s2)) 
            return true;
        

        // form the graph, we can represent it as a map describing the edges
        HashMap<Character, Character> edges = new HashMap<>();

        for (int i = 0; i < s1.length(); ++i) {
            
            // This clause corresponds to discovering more than one out-degree, 
            // which we concluded is not possible
            if (edges.getOrDefault(s1.charAt(i), s2.charAt(i)) != s2.charAt(i))
                return false;
            
            // This corresponds to discovering a new edge
            edges.put(s1.charAt(i), s2.charAt(i));
        }

        return new HashSet<Character>(edges.values()).size() < 26;
    }

    public static void main(String[] args){
        // Driver code

        String s1 = "aabcc";
        String s2 = "ccdee";
        
        if (mutateDNA(s1, s2) == true)
            System.out.print("Mutation Possible");
        else
            System.out.print("Mutation not Possible");
        
    }
}
{% endhighlight %}

![com](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/com/com5.png)

## Feature #2: Detect Virus

## Description
While studying different DNA samples, we observed that a certain virus consists of really long sequences of k distinct nucleotides. The virus infects a species by embedding itself into the species’s DNA. We are working on devising a test to detect the virus. The idea is to analyze the longest string that consists of, at most, k nucleotides from a species’s DNA.

We’ll be provided with a string representing a chromosome from the infected DNA and a k value supplied from a hidden function. Our task will include calculating the longest subsequence from the chromosome string that has k unique nucleotides.

Here is an illustration to better understand this process:

![com](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/com/com6.png)

## Solution
Since we want to return a substring from a specific window over the original string, we can use a sliding window approach to accomplish this efficiently. We’ll use two pointers, left and right, to denote the boundaries of our sliding window.

Initially, both our pointers will be at the beginning of the string at position 0. We’ll keep moving the right pointer to the right as long as there are k distinct characters in our window. If we get k + 1 distinct characters at any point, the left pointer will be moved to the right to prevent keeping more than k distinct characters in our window.

We can use a HashMap to control the movement of the left pointer so that we always have only k distinct characters in our window. The characters will be stored as keys in the HashMap, and those characters’ rightmost positions will be their corresponding values. Remember that the HashMap can only entertain k + 1 entries. When we get k + 1 entries, we need to move the left pointer to ensure our window contains only k distinct characters. We’ll also remove the character with the lowest position number from the HashMap.

We will maintain two dummy variables: start and end. After each iteration, we’ll update their values with the left and right pointers if the (end - start) difference is less than the (right - left) difference. In the end, the start and end pointers will contain the virus’s location.

Let’s see how we might implement this functionality:
1. Return 0 if the string is empty or if k is equal to zero.
2. Initialize the left and right pointers. Assign them the value 0. Initialize the two other start and end variables with the value 0 as well.
3. Traverse the string with the right pointer and keep adding the current value to the HashMap.
4. If the HashMap contains k + 1 distinct characters, remove the leftmost character from the HashMap and move the left pointer so that the sliding window contains only k distinct characters.
5. At the end of each iteration, assign the left value to start and the right value to end if the (end - start) difference is less than the (right - left) difference.

The following illustration might clarify this process.

![com](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/com/com7.png)
![com](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/com/com8.png)
![com](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/com/com9.png)
![com](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/com/com10.png)
![com](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/com/com11.png)
![com](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/com/com12.png)
![com](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/com/com13.png)
![com](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/com/com14.png)
![com](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/com/com15.png)
![com](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/com/com16.png)
![com](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/com/com17.png)
![com](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/com/com18.png)
![com](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/com/com19.png)

Let’s look at the code for the solution:

{% highlight java %}
import java.util.*;

class Solution {
  public static String detectVirus(String s, int k) {

    if (s.length() * k == 0) return "";

    // left and right pointers
    int left = 0;
    int right = 0;

    // dummy variables
    int start = 0;
    int end = 0;

    // character -> its rightmost position
    HashMap<Character, Integer> characterMap = new HashMap<Character, Integer>();

    while (right < s.length()) {
      // add new character and move right pointer
      characterMap.put(s.charAt(right), right++);

      // This clause checks if window contains more than k characters
      if (characterMap.size() == k + 1) {

        int min_idx = Collections.min(characterMap.values());
        characterMap.remove(s.charAt(min_idx));
        // move left pointer of the window
        left = min_idx + 1;
      }

      if ((end - start) < (right - left)){
        start = left;
        end = right;
      }
        
    }
    return s.substring(start, end);
  }

    public static void main( String args[] ) {
      // Driver code

      String infectedDNA = "ababffzzeee";
      int k = 3; // Supplied from a hidden program
      
      System.out.println(detectVirus(infectedDNA, k));
    }
}
{% endhighlight %}

![com](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/com/com20.png)

## Feature #3: Locate Protein

## Description
Experiments have shown that a certain protein provides immunity against a specific virus. Unfortunately, the presence of the protein can’t be determined based on an exact match. Instead, we only know that like any other protein, this one has really long palindromic strings of nucleotides. To detect this protein, we need to first find the longest palindromic portion in an unknown sample.

We’ll be provided with a DNA generated protein sequence in the form of a string. Our task will be to locate and isolate the portion that has the nucleotides lined up as the longest palindrome to identify the correct protein.

![com](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/com/com21.png)

## Solution
A palindrome is a string that reads the same backwards as forwards. For example, str = abba is a palindrome, but str' = abcd is not. Although there can be multiple palindromes in the input string, we have to find the longest one. There are two ways we can check if a string is a palindrome:
* Start two pointers from each end of the string. Move towards the center while checking that the element at each pointer is the same.
* Start two pointers from the center of the string. One pointer will move left and the other will move right while checking that the element at each pointer is the same.

We will use the second approach to solve our problem. We can traverse over the string, considering each position the center of a palindromic string. This way, we’ll find each palindrome within our string and return the longest one. This center position can either be a specific character in the string (if the string size is odd) or between two characters (if the string size is even). For example, if the string length is odd, say, abcba, the center exists in the middle. If the string length is even, say, abba, the center exists in between the two bb elements.

The longest palindromic substring may be odd in length. In this case, its central element would be a character in the original string. All n characters in the string must, therefore, be tried as a possible center of the longest palindromic substring. On the other hand, a palindrome could be even in length. In this case, its central element would be straddling between two characters in the original string. This means that n-1 positions must be tested for potential centers of a palindromic substring of even length. So, in total, there are 2n - 1 candidates for the center position of the longest palindromic substring in a string of size n.

Let’s see how we might implement this functionality:
1. Return an empty string if the input is null or of length 0.
2. Initialize the two start and end pointers. Assign them 0 at the start.
3. Write a function, returnPalindromeLength(s, left, right), to return the length of the palindromic string centered at that position specified as the left and right arguments. Since the center position for an even-sized substring is not an integer, instead of specifying the center index, we will pass the indices of the elements to the left and right of the center position. We will have a loop that runs n times.
4. In each iteration, we will call the returnPalindromeLength(s, left, right) function twice. In one call, we will pass the loop variable i as both the left and right indices - indicating a substring of odd length. In the other call, we will pass i for the left index and i + 1 for the right index.
5. The max of the two lengths calculated by the returnPalindromeLength(s, left, right) function would be the resultant length of the palindrome starting from the current index as its center.
6. The start and end pointers can then be updated using the index and resultant length value.
7. Return the substring from start to end+1.

Let’s look at the code for the solution:

{% highlight java %}
class Solution {

    public static String locateProtein(String s) {
        if (s == null || s.length() < 1) 
            return "";
        int start = 0, end = 0;

        for (int i = 0; i < s.length(); i++) {

            int len1 = returnPalindromeLength(s, i, i); // for odd length
            int len2 = returnPalindromeLength(s, i, i + 1); // for even length
            int len = Math.max(len1, len2);

            if (len > end - start) {
                start = i - (len - 1) / 2;
                end = i + len / 2;
            }
        }

        return s.substring(start, end + 1);
    }

    // returns size of the current/latest palindrome
    private static int returnPalindromeLength(String s, int left, int right) {

        while (left >= 0 && right < s.length() && s.charAt(left) == s.charAt(right)) {
            left--;
            right++;
        }
        
        return right - left - 1;
    }

    public static void main( String args[] ) {
        // Driver code
        String sequence = "aaccbababcbc";
        
        System.out.println(locateProtein(sequence));
    }
}
{% endhighlight %}

![com](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/com/com22.png)

## Feature #4: Identifying Proteins

## Description
We have an unknown sequence of genomes that is thought to be a new protein. To accept or reject this sequence as a new protein, one method we can use is to identify it as a palindromic sequence. A palindrome is a string that reads the same from the start as the end.

We’ll be provided with a sequence of genomes in the form of a string. Our task is to identify whether these genomes constitute a palindrome to be considered as a potential protein.

## Solution
A recursive approach can be used to solve this problem. We can keep comparing the first and last elements of the string. If these values are equal, then the updated string, with the matched entries removed, can be sent to the recursive function.

Let’s see how we might implement this functionality:
1. Define the following base case:
   * If the given sequence has a length equal to zero or one, it will return True, since a string of size 0 or 1 is, a palindrome by definition.
2. If the above-mentioned base conditions are not met, we move to the recursive case.
3. If the first and last indexes are equal, we’ll call the function recursively on the argument string minus the matched characters.
4. Next, we pass the modified string sequence to the recursive method, which will compare values from the next index to the start of the string while decrementing the last index by 1.
5. The recursive call will terminate when the above-mentioned base cases are true, or when the values do not match at their respective positions.

The sequence of function calls is illustrated below:

![com](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/com/com23.png)
![com](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/com/com24.png)
![com](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/com/com25.png)
![com](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/com/com26.png)
![com](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/com/com27.png)
![com](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/com/com28.png)

Let’s look at the code for the solution:

{% highlight java %}
class Solution {
    public static boolean isProtein(String sequence) {
        if (sequence.length() <= 1) {
            return true;
        }
        else {
            if (sequence.charAt(0) == sequence.charAt(sequence.length()-1)) {
                return isProtein(sequence.substring(1, sequence.length()-1));
            }
        }
        return false;
    }

    public static void main( String args[] ) { 
        // Driver code
        
        String protein = "acbca";
        System.out.println("Is " + protein + " a Protein? = " + isProtein(protein));
    }  
}
{% endhighlight %}

![com](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/com/com29.png)

