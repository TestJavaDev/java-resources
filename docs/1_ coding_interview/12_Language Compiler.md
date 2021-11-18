---
layout: default
title: Language Compiler
parent: Coding Interview
has_children: true
nav_order: 12
permalink: /coding_interview/language
---
<div align="center" markdown="1">
Language Compiler / Java resources / Tutorial

{: .fs-8 .fw-400 }
</div>

## Language Compiler

## Project Description for Language Compiler

## Introduction
A language compiler is a software used to convert the source code of a language into machine code, which is then executed by the computer’s processor. A compiler can have various components, including a scanner, lexical analyzer, semantic analyzer, code generations, etc., which might be handled by different modules of the program. The compilers are both language-specific and specific to the underlying hardware processor.

The scenarios and problems discussed in this chapter relate to handling language compiler’s code comments and expression computation functionality in different scenarios.

## Statement
For this project, imagine that you are a developer at a company that is experimenting with the development of a new type of compiler for the C++ language. This compiler does not follow the architecture of conventional compilers.

The compiler program that your team is working on has various modules that handle different parts of the conversion. Your team is working on several optimizations to the compiler for large as well asa small program compilations.

## Features

We will need to introduce the following features to implement the functionalities we discussed above:
* Features #1: Detect comments in the source code and remove them.
* Features #2: Compute the result of a mathematical expression given to you in string format in the C++ language.
* Features #3: Unroll a loop by replacing it with repeated instructions.
* Features #4: Optimize a code by replacing slow function calls with faster ones.
* Features #5: Find the first build step that failed so we do not have to compile all the files again.
* Features #6: Find the most frequently used variable or function call in a code.

The coming lessons will discuss these features and their implementation in detail. By the end of the section, you’ll be able to apply the solution to this scenario to different interview problems.

## Feature #1: Remove Comments

## Description
The first functionality we will be building will remove comments from a piece of code prior to its compilation. There are two types of comments in the C++ language, inline comments and block comments.
* Inline comment: The string // is used for an inline comment, which means that the characters to the right of // in the same line should be ignored.
* Block comment: The block comment is enclosed between the non-overlapping occurrence of /* and */. Everything inside these delimiters is ignored. Here, occurrences happen in reading order, meaning line by line from left to right. Note that the string /*/ does not yet end the block comment because the ending would be overlapping the beginning.

Note: If two comments are nested, the first effective comment takes precedence over others. In other words, if the string // occurs in a block comment, it is ignored. Similarly, if the string /* occurs in a line or block comment, it is also ignored. For example:
* // this is an inline /* comment */
* /* this is a /* // block comment */

When implementing this feature, you have to detect the comments in the code first and then remove them. If any line of the code becomes empty after removing the comments, you should discard that line as well. Tabs and spaces are not considered empty lines. You can also assume that the // and /* will only exist in the context of comments and not part of strings or statements in the code.

Imagine that you have to remove comments from the following C++ code:

![op](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/op/op25.png)

This code will be given as input to you as a list of strings where each string represents a line of code. In the example given above, the source list will be {"/* Example code for feature */", "int main() {", " /*", " This is a", " block comment", " */", " int value = 10; // This is an inline comment", " int sum = value + /* this is // also a block */ value;", " return 0;", "}"}.

Your program should remove all the comments, making the output for the example: {'int main() {', ' ', ' int value = 10; ', ' int sum = value + value;', ' return 0;', '}'}. It can be displayed in code as:

![op](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/op/op26.png)

## Solution
The idea behind this solution is to find the comments’ starting characters by traversing the source code. Then, we use a Boolean variable to create a state that lets us know which characters to remove from the code.

The complete algorithm looks like this:
* First, declare a few variables in the removeComments function:
   * output: A list for storing the result
   * buffer: A string to store the characters that need to be added to the output
   * block: A Boolean that is set true when inside a block comment
* Then, traverse the source list line by line and character by character in a nested loop.
* Check if // is found in the loop; if found, skip the rest of the line by shifting the pointer to the end.
* If the previous condition is false, check if /* is found. If this condition is true, set block to true and keep traversing.
* When */ is found, then set block to false.
* Finally, check if block is not set. Then, append buffer to the output.

{% highlight java %}
class Solution {
    public static String[] removeComments(String[] source){
        ArrayList<String> output = new ArrayList<>();
        String buffer = "";
        boolean block = false;
        for(String line: source){
            int i = 0;
            while(i < line.length()){
                char c = line.charAt(i);
                // "//" -> inline comment.
                if(c == '/' && (i + 1) < line.length() && line.charAt(i + 1) == '/' && !block){
                    i = line.length(); // Advance pointer to end of current line.
                }
                // "/*" -> start of block comment.
                else if( c == '/' && (i + 1) < line.length() && line.charAt(i + 1) == '*' && !block){
                    block = true;
                    i++;
                }
                // "*/" -> end of block comment.
                else if( c == '*' && (i + 1) < line.length() && line.charAt(i + 1) == '/' && block){
                    block = false;
                    i++;
                }
                // normal cacter -> Append to buffer if not in block comment.
                else if(!block){
                    buffer += c;
                }
                i++;
            }
            if(buffer!= "" && !block){
                output.add(buffer);
                buffer = "";
            }
        }
        return output.toArray(new String[output.size()]); 
    }
    public static void main( String args[] ) {
        String[] source = {"/* Example code for feature */", 
            "int main() {", 
            "  /*", 
            "  This is a", 
            "  block comment", 
            "  */", 
            "  int value = 10;  // This is an inline comment", 
            "  int sum = value + /* this is // also a block */ value;", 
            "  return 0;", 
            "}"};
        String[] output = removeComments(source);
        System.out.println(Arrays.toString(output));
        
    }
}
{% endhighlight %}

![op](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/op/op27.png)

## Feature #2: Evaluate the Arithmetic Expression

## Description
For this feature, you have to create a module for evaluating mathematical expressions. The expressions are already extracted from the source code and are available as strings. Your job is to compute the result and return it. The expressions are subject to the following constraints:
* The numbers can only be integers.
* For simplicity’s sake, the expressions can only contain + and - operators.
* The expression can contain () parentheses.
* The expression has already been verified as being valid.

Let’s look at an example to understand the feature specifications. Suppose the input expression is "5-(3+4)". Your program has to evaluate it following mathematical rules. First, the expression inside parentheses is solved and then the rest. The result will be the integer value -2.

## Solution
This problem is a great candidate for a stack use case. But first, we need to keep in mind the rules of addition and subtraction, the precedence of parentheses, and that the spaces in the string do not affect the output. We can use the stack to solve for the precedence of parentheses. If an expression contains an opening bracket (, we will push the elements into the stack until a closing bracket ) is found. Then, we will pop the elements and evaluate the sub-expression inside the brackets until the opening bracket (. However, when we calculate the final answer, we process the values from right to left, whereas it should be from left to right. The following slides illustrate this issue:

![op](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/op/op28.png)
![op](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/op/op29.png)
![op](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/op/op30.png)
![op](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/op/op31.png)
![op](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/op/op32.png)
![op](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/op/op33.png)
![op](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/op/op34.png)
![op](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/op/op35.png)
![op](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/op/op36.png)

The example above shows how the string is reversed using the stack, and we will end up evaluating the expression in reverse order. Let’s look at a way to solve this problem.

We can use the - operator as the magnitude for the operand to the right of the operator. By using - as the magnitude for the operands, we will have only the addition operator left, and + is associative. This means that A - B - CA−B−C could be re-written as A + (-B) + (-C)A+(−B)+(−C). The re-written expression will follow the associativity rule. Therefore, evaluating the expression from the right or left, won’t change the result.

The complete algorithm is as follows:
* First, declare a few variables in the function:
   * number: An integer for storing the number value
   * sign: This is also an integer, but it is used to store the value of the sign. It is positive initially, represented by +1.
   * output: This is used to store the answer after evaluating the expression.
   * stack: This is the list we will use as a stack data structure.
* Iterate the expression string character by character.
* If a digit is found, we need to form the operand by multiplying the previously formed operand by 1010 and adding the digit to it.
* When we encounter the + or - operators, we evaluate the expression to the left first and save the sign for the next evaluation.
* If ( is found, we push the result calculated so far and the sign onto the stack.
* If ) is found, we calculate the expression to the left. The result of this would be the result of the expression within the set of parenthesis that just ended. This result is then multiplied by the sign (if there is a sign on top of the stack). As you know, we saved the sign on top of the stack when we had an open parenthesis. Because this sign was associated with the parenthesis that started then, thus when the expression ends or concludes, we pop the sign and multiply it with the result of the expression. It is then added to the next element on top of the stack.

Here is this solution’s implementation:

{% highlight java %}
class Solution {
    public static int evaluateExpression(String expression){
        int number = 0;
        int sign = 1;
        int output = 0;
        Stack<Integer> stack = new Stack<>();
        for(int i = 0; i < expression.length(); i++){
            char c = expression.charAt(i);
            if(Character.isDigit(c)){
                number = number * 10 + Character.getNumericValue(c); //for consecutive digits 98 => 9x10 + 8 = 98
            }
            else if(c == '-' || c == '+'){ 
                output += number * sign;
                if(c == '-')
                    sign = -1;
                else
                    sign = 1;
                number = 0;
            }
            else if(c == '('){
                stack.push(output);
                stack.push(sign);
                output = 0;
                sign = 1;
            }
            else if(c == ')'){
                output += sign * number;
                output *= stack.pop();
                output += stack.pop();
                number = 0;
            }
        }
        return output + number * sign;
    }
    public static void main( String args[] ) {
        String expression = "{4 - (10 + 52) + 99}";
        System.out.println(evaluateExpression(expression));
    }
}
{% endhighlight %}

![op](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/op/op37.png)

## Feature #3: Loop Unrolling

## Description
Loop unrolling is a technique that compilers use to optimize a program’s execution speed. It minimizes the overhead cost of a loop, including frequency of branches and loop maintenance instructions. The idea behind loop unrolling is to replicate the statements inside the loop by the number of times the loop will execute. There are other factors that go into determining how to calculate exactly how many times a loop will run to minimize the number of total instructions.

Suppose a module in your language compiler product already determines how many times a block of code will execute. This module replaces the loops in the intermediate code by adding blocks in the following format: n[statements]. For example, consider the following code snippet:

for (int i=0; i<3; i++) 
    printf("output");
This block of code will be replaced in the intermediate code by the following code snippet:

3[printf("output"); ]
These loops can also be nested. For example, this could be an intermediate code for a nested loop:

2[sum = sum + i; 2[i++; ]]
Now, your job is to translate these blocks of code and replace them with repeated instructions. The following illustration shows how to translate the above-mentioned nested loop block:

![op](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/op/op38.png)

Your module will take a string as input with the format n[statements], and you have to implement a solution that outputs a string containing the repeated instructions as explained in the example above.

## Solution
We know that the block of code begins with a number n, followed by an opening bracket [, which is then followed by a statement. After this statement, there can be two possible scenarios:
* There is a final closing bracket ].
* There is another nested encoded string pattern like n[statement n[statement]].

From the above example, we know that we have to start decoding the pattern from the innermost statement. This means that the outermost block will be processed at the end. This behavior follows the Last in First Out (LIFO) property of the stack data structure, which we’ll use to solve this problem. We will be using two stacks. The first will be used for pushing the repetition count, n, and the other stack will store the statements to be repeated.

Here is how the implementation will take place:
1. Start traversing the code character by character from the beginning.
2. If a digit is found, append it to the integer n, which will be the repetition factor.
3. If a character is found, we will append it to the currentStatement.
4. If [ is found, we will push n and currentStatemet into countStack and statementStack, respectively.
5. When the ] bracket is found, we will pop the currentN from the countStack and unroll the currentStatement.
6. The statementStack will contain the previously unrolled code (We pushed the currentStatement onto the statementStack when [ was found). Therefore, we will pop the unrolled code from statementStack and append it to the currentStatement.

Let’s look at the code for the solution:

{% highlight java %}
class Solution {
    public static String loopUnrolling(String codeBlock) {
        Stack<Integer> countStack = new Stack<>();
        Stack<StringBuilder> statementStack = new Stack<>();
        StringBuilder currentStatement = new StringBuilder();
        
        int n = 0;
        for (int i = 0; i < codeBlock.length(); i++) {
            char ch = codeBlock.charAt(i);
            if (Character.isDigit(ch) ) {
                n = n * 10 + ch - '0';
            } else if (ch == '[') {
                // push the number n to countStack
                countStack.push(n);
                statementStack.push(currentStatement);
                // reset currentStatement and n
                currentStatement = new StringBuilder();
                n = 0;
                
            } else if (ch == ']') {
                StringBuilder unrollStatement = statementStack.pop();
                // unroll currentN[currentStatement] by appending currentStatement n times
                for (int currentN = countStack.pop(); currentN > 0; currentN--) {
                    unrollStatement.append(currentStatement);
                }
                currentStatement = unrollStatement;
                
            } else {
                currentStatement.append(ch);
            }
        }
        return currentStatement.toString();
    }

    public static void main(String args[]){
        String codeBlock = "2[sum = sum + i; 2[i++; ]]";
        System.out.println(loopUnrolling(codeBlock));
    }
}
{% endhighlight %}

![op](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/op/op39.png)

## Feature #4: Optimization by Replacement

## Description
For this language compiler feature, we want to add some additional optimization to the source code. Let’s say we have identified token locations, indices, that could potentially be replaced for optimization. The token for each of those indices is also given as a list, sources. Another list, targets, holds the strings that each of the tokens in sources should be replaced with. If token sources[i] is present at location indices[i] in the input, it should be replaced with the token targets[i]. Note that sources[i] and targets[i] may not necessarily be the same length

Suppose that the line of code you are given as input is foo(input, i);. The possible replacement operations can be performed at the indices [0, 11]. Also, the sources are ["foo", "i"], and the targets array is ["foobar", "j+1"]. Considering the example inputs, you can see that both operations are valid because the source token can be found at their respective indices. After applying the replacement operations, the line of code will become foobar(input, j+1).

## Solution
Consider we are traversing the line character by character and start replacing the source strings with target strings. A notable issue we will run into is that managing the index will become a hassle as the replacements will likely change the number of characters. To tackle this issue, we can traverse the line in reverse. This way, the modifications to the line will not interfere with the index for replacement operations.

The complete algorithm for this solution is given below:
* We will start by sorting the indices for the replacement operations in descending order.
* Then, we will traverse the indices and perform replacements.
* To perform a replacement, we first check if the source substring exists at the respective index in the line.
* If it exists, we replace source with the corresponding target.
* The modified string is returned at the end.

![op](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/op/op40.png)
![op](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/op/op41.png)
![op](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/op/op42.png)
![op](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/op/op43.png)
![op](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/op/op44.png)

{% highlight java %}
class Solution {
    public static String optimizeLine(String line, int[] indices, String[] sources, String[] targets) {
        List<int[]> sorted = new ArrayList<>();
        for (int i = 0 ; i < indices.length; i++) 
            sorted.add(new int[]{indices[i], i});
        Collections.sort(sorted, Comparator.comparing(i -> -i[0]));
        for (int[] ind: sorted) {
            int i = ind[0], j = ind[1];
            String s = sources[j], t = targets[j];
            if (line.substring(i, i + s.length()).equals(s)) 
                line = line.substring(0, i) + t + line.substring(i + s.length());
        }
        return line;
    }

    public static void main(String args[]){
        String line = "foo(input, i);";
        int[] indices = {0, 11};
        String[] sources = {"foo", "i"};
        String[] targets = {"foobar", "j+1"};

        System.out.println(optimizeLine(line, indices, sources, targets));
    }
}
{% endhighlight %}

![op](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/op/op45.png)

## Feature #5: Compilation Step Failure

## Description
Large software consists of many source files and libraries. The software as a whole can only compile if all the constituent files compile successfully with the required libraries. The multi-file compilation is generally structured as a number of build steps that must be performed sequentially so that the dependencies of files and libraries are met. An individual build step can include the compilation of a source file or library.

Assume that we are working with a system that specifies the build as steps 1 through n, and the steps must be performed in ascending order. If a build step fails, repeating all the build steps is inefficient. The successful steps should not be repeated. When a build fails, you get an error message, but you don’t know which step failed. You have access to an API call, is_failed_step(i), which returns true if build step i failed. Otherwise, it will return false. If there was a total of forty steps and step 28 failed, the compilation will stop, and is_failed_step(i) will return true as long as i >= 28. You want to efficiently determine the first build step that must be repeated.

For instance, if you have n = 40 steps and the steps 28 to 40 fail. The API call is_failed_step(i) will give True for 28 to 40. Your module should then use these resources to output the first step that failed, i.e., 28.

![op](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/op/op46.png)

## Solution
To implement this feature efficiently, we will use the binary search algorithm. Our goal is to find the first failing step by making a minimum number of calls to the API. We will check if the middle step failed. If the first failing step is in the left half (including the middle) of the list, we can ignore the right half of the list. Otherwise, we can ignore the left half of the list. By successively halving the search space, we can find the first failing step in O(logn)O(logn) steps.

The complete algorithm is given below:
* As we know the number of steps, we will use two pointers that point to the IDs of the first and last steps.
* Then, we can find the middle step’s ID and call the API to check if that step fails or not.
* If the middle step fails, we know that this is either the first failing step or that the first failing step came before this step. So, we will search for the first failing step from 1 to mid.
* If the step does not fail, we need to look at the steps from mid + 1 to n for the first failing step.
* In this way, each API call helps us divide our data set in half and narrow down the search space.
* Now, we just have to keep iterating and narrowing down until the step is found.

![op](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/op/op47.png)
![op](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/op/op48.png)
![op](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/op/op49.png)
![op](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/op/op50.png)

{% highlight java %}
class Compilation{

    public static int firstFailingStep(int n){
        int first = 1;
        int last = n;
        while (first < last) {
            int mid = first + (last - first) / 2;
            if (ErrorReport.isFailingStep(mid)) { // Calling the API to determine if the step fails
                last = mid;
            } else {
                first = mid + 1;
            }
        }
        return first;
    }


    public static void main(String args[]){
        int n = 40; // Number of steps
        int v = 28; // Failing step
        ErrorReport.setFailingStep(28);
        System.out.println(firstFailingStep(40));
    }

}
{% endhighlight %}

![op](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/op/op51.png)

## Feature #6: Most Common Token

## Description
For this feature of the language compiler, the program statements are given to us as a string. We want to determine the variable or function that is most commonly referred to in a program. In this process, we want to ignore the language keywords. For example, a keyword may be used more frequently than any variable or function. The language keywords are given as an array of strings.

Let’s say you are given the following program as input:

![op](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/op/op52.png)

The list of keywords given to you is ["int", "main", "return"]. In this example, your function will return "value". Note that, your functions should ignore syntax, such as parentheses, operators, semicolons, etc.

## Solution
We can solve this problem by normalizing the code string and processing it step by step. The complete algorithm is as follows:
* First, we replace all the syntax, including parentheses, operators, semicolons, etc., with spaces. Now, the string only contains alphanumeric tokens.
* Then, we split the code obtained from the previous step into tokens.
* We iterate through the tokens to count the appearance of each unique token as keys, excluding the keywords.
* We create a HashMap count, which has tokens as keys and occurrences as values.
* In the end, we check the tokens in count to find the token with the highest frequency.

{% highlight java %}
class HelloWorld {
    public static String mostCommonToken(String code, String[] keywords){
        // Replacing the syntax with spaces
        String normalizedCode = code.replaceAll("[^a-zA-Z0-9]", " ");

        String[] tokens = normalizedCode.split("\\s+");
        HashMap<String, Integer> count = new HashMap<String, Integer>();
        Set<String> bannedWords = new HashSet<String>(Arrays.asList(keywords));

        // Count occurence of each token, excluding the keywords 
        for(String token : tokens){
            if (!bannedWords.contains(token)){
                if(!count.containsKey(token)){
                    count.put(token, 0);
                }
                count.put(token, count.get(token) + 1);
            }   
        }
        // return the maximum valued key
        return Collections.max(count.entrySet(), (entry1, entry2) -> entry1.getValue() - entry2.getValue()).getKey();
    }
    
    public static void main( String args[] ) {
        // Driver code
        String code = "int main() {\n" +
            "int value = getValue();\n" + 
            "int sum = value + getRandom();\n" +
            "int subs = value - getRandom();\n" +
            "return 0;\n" +
        "}";
        String[] keywords = {"int", "main", "return"};
        System.out.println(mostCommonToken(code, keywords));
    }
}
{% endhighlight %}

![op](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/op/op53.png)
