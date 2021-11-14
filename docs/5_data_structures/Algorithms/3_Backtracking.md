---
layout: default
title: Backtracking
parent: Algorithms
grand_parent: Data Structures and Algorithms
nav_order: 3
permalink: /data_structures/algorithms/backtracking
---
<div align="center" markdown="1">
Backtracking / Java resources / Tutorial

{: .fs-8 .fw-400 }
</div>

## Backtracking Fundamentals

Combinatorial search problems#
Combinatorial search problems involve finding groupings and assignments of objects that satisfy certain conditions. Finding all permutations/subsets, solving sudoku, and 8-queens are classic combinatorial problems.

Permutations#
It’s important to review basic combinatorics to get an intuition for combinatorial problems.

Permutation means arranging things with an order. For example, permutations of [1, 2] are [1, 2] and [2, 1]. Permutations are best visualized with trees.

//back1

The number of permutations is given by n! (we looked at factorial in Recursion Review. The way to think about permutation is to imagine you have a bag of 3 letters. Initially, you have 3 letters to choose from, you pick one out of the bag. Now you are left with 2 letters. You pick again and now there’s only 1 letter. The total number of choices is 3*2*1 = 6, hence we have 6 leaf nodes in the tree above.

Complexity#
The complexity of combinatorial problems often grows rapidly with the size of the problem. For example, as we have seen, the number of permutations of 3 objects is only 6. However, the number of permutations of 10 objects is about 3 million. The number of permutations of 11 objects is about 40 million. The rapid growth of solution space with even a small increase in problem size is called combinatorial explosion.

Combinatorial search: DFS on a tree#
In combinatorial search problems, search space is in the shape of a tree. The tree that represents all the possible states is called a state-space tree.

Each node of the state-space tree represents a state we can reach in a combinatorial search (by making a particular combination). Leaf nodes are the solutions to the problem (permutations in the above example).

Combinatorial search problems boil down to DFS/backtracking on the state-space tree.

Since the search space can be quite large, we often have to “prune” the tree, i.e., discard branches.

Three steps to conquer combinatorial search problems#
We summarized a three-step system to solve combinatorial search problems:

Identify the state(s).
Draw the state-space tree.
DFS/backtrack on the state-space tree.
In step 1, we want to answer the following two questions to identify the states:

What state do we need to know whether we have reached a solution and can we use it to construct a solution if the problem asks for it? In the above permutation example, we need to keep track of the letters we have already selected when performing DFS.

What state do we need to decide which child nodes should be visited next and which ones should be pruned? In the above permutation example, we have to know what letters are left that can still be used, since each letter can only be used once.

For step 2, you want to draw the tree. A small test case that’s big enough to reach one solution (leaf node).

For step 3, apply the following backtracking template:

{% highlight java %}

def dfs(node, state):
    if state is a solution:
        report(state) # e.g. add state to final result list
        return

    for child in children:
        if child is a part of a potential solution:
            state.add(child) # make move
            dfs(child, state)
            state.remove(child) # backtrack
{% endhighlight %}

Notice how this is very similar to the ternary tree path code we’ve seen in DFS with States module. That problem has an explicit tree. For combinatorial search problems, we have to find our own tree.

All of this may sound very abstract at the moment, but it will become clear once we apply the system to a couple of real problems.

## Permutations

Given a list of unique letters, find all of its distinct permutations.

Example#
Input: ['a', 'b', 'c']

Output: [['a', 'b', 'c'], ['a', 'c', 'b'], ['b', 'a', 'c'], ['b', 'c', 'a'], ['c', 'a', 'b'], ['c', 'b', 'a']]

Explanation#
Intuition#
Classic combinatorial search problem. Let’s apply the 3-step system from the backtracking template.

1. Identify states#
What state do we need to know whether we have reached a solution and can we use it to construct a solution if the problem asks for it?

We need a state to keep track of the list of letters we have chosen for the current permutation.
What state do we need to decide which child nodes should be visited next and which ones should be pruned?

We have to know what letters are left that can still be used, since each letter can only be used once.
2. Draw the state-space tree#

//back2

3. DFS on the state-space tree#
Using the backtracking template as a basis, we add the two states we identified in step 1:

A path list to represent permutation constructed so far
A used list to record which letters are already used. used[i] == true means the ith letter in the original list has been used.
The time complexity is //back3

{% highlight java %}

class Solution {
    public static List<List<Character>> permute(char[] letters) {
        List<List<Character>> res = new ArrayList<>();
        dfs(new ArrayList<>(), new boolean[letters.length], res, letters);
        return res;
    }

    private static void dfs(List<Character> path, boolean[] used, List<List<Character>> res, char[] letters) {
        if (path.size() == used.length) {
            // make a deep copy since otherwise we'd be append the same list over and over
            res.add(new ArrayList<Character>(path));
            return;
        }

        for (int i = 0; i < used.length; i++) {
            // skip used letters
            if (used[i]) continue;
            // add letter to permutation, mark letter as used
            path.add(letters[i]);
            used[i] = true;
            dfs(path, used, res, letters);
            // remove letter from permutation, mark letter as unused
            path.remove(path.size() - 1);
            used[i] = false;
        }
    }
         // Driver code  
	public static void main(String[] args) {

        String[] inputs = {"ab","abc"};
		for (int i = 0; i<inputs.length; i++) {
			System.out.println("Permutations : " + Solution.permute(inputs[i].toCharArray()));
		}
	}
}
{% endhighlight %}

Notice how similar the solution is to Ternary Tree Paths. The only difference is that we have a new constraint: the “number of letters left” while deciding which subtree to go down to.

Note on deep copy#
In the exit logic of the above solution, we append a deep copy of the path res.append(path[:]). This creates a new list with elements being the same as current elements of path. Consider what happens if we don’t make the deep copy:

{% highlight java %}

res = []
path = []
for i in range(3):
    path.append(i)
    res.append(path)
print(res)
{% endhighlight %}

We get the same copy three times! Because append(path) actually appends a reference (memory address), we actually append the same list three times. path.append(i) mutates the list and affects all references to that list. To fix this, we create a new list before we append.

## Phone Number Letter Permutations

Given a phone number that contains digits from 2–9, find all possible letter combinations the phone number could translate to.
//back4

Explanation#
This is essentially asking for all permutations with the constraint of a number to letter mapping.

1. Identify state(s)#
To construct a letter combination we need the letters we have selected so far.

To make a choice when we visit the current node’s children, we don’t need to maintain any additional state since the next possible letters are defined by the number to letter mapping.

2. Draw the tree#

//back5

3. DFS on the tree#
We traverse the state-space tree depth-first.

The time complexity is //back6

{% highlight java %}

class Solution {
    private static final Map<Character, char[]> KEYBOARD = new HashMap<>();
    static {
        KEYBOARD.put('2', "abc".toCharArray());
        KEYBOARD.put('3', "def".toCharArray());
        KEYBOARD.put('4', "ghi".toCharArray());
        KEYBOARD.put('5', "jkl".toCharArray());
        KEYBOARD.put('6', "mno".toCharArray());
        KEYBOARD.put('7', "pqrs".toCharArray());
        KEYBOARD.put('8', "tuv".toCharArray());
        KEYBOARD.put('9', "wxyz".toCharArray());
    }
    public static List<String> letterCombinationsOfPhoneNumber(String digits) {
        List<String> res = new ArrayList<>();
        dfs(new StringBuilder(), res, digits.toCharArray());
        return res;
    }
    private static void dfs(StringBuilder path, List<String> res, char[] digits) {
        if (path.length() == digits.length) {
            res.add(path.toString());
            return;
        }
        char next_digit = digits[path.length()];
        for (char letter : KEYBOARD.get(next_digit)) {
            path.append(letter);
            dfs(path, res, digits);
            path.deleteCharAt(path.length() - 1);
        }
    }
    // Driver code  
	public static void main(String[] args) {
        String[] inputs = {"56", "23", "235"};
        for(int i = 0; i < inputs.length; i++) {
            System.out.println("Letter combinations of phone number : " + Solution.letterCombinationsOfPhoneNumber(inputs[i]));
        }
    }
}
{% endhighlight %}


