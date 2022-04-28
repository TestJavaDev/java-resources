---
layout: default
title: Miscellaneous
parent: Coding Interview
has_children: true
nav_order: 21
permalink: /coding_interview/miscellaneous
---
<div align="center" markdown="1">
Miscellaneous / Java resources / Tutorial

{: .fs-8 .fw-400 }
</div>

## Miscellaneous

## Minimum Knight Moves

## Description
We have an infinite chessboard with coordinates starting from -infinity to infinity. Our knight starts in square (0, 0).

The knight has eight possible moves at a given time. It can move in an L-shape, meaning it can move two squares in any direction vertically and then one square horizontally or two squares in any direction horizontally and then one square vertically.

You need to find the minimum moves the knight needs to get from the origin (0,0) to the coordinates (x,y). We will assume that the provided coordinates are always reachable and the constraint | x | + | y | <= 300 holds.

For example, given the input coordinate, (5, 5) you have to find the minimum number of moves required for the knight to get from the origin to the coordinate. In this case, the program will output four because the knight needs four moves to get to the coordinate.

![wer](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/wer/wer1.png)
![wer](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/wer/wer2.png)

## Solution
Notice that the knight’s movements to both the positive and negative coordinates and the axis are symmetrical. The same number of moves are required to get to both the positive and negative coordinates. The knight can move in any of the eight directions at any given time by adding the following coordinates, [{1, 2}, {2, 1}, {-1, 2}, {1, -2}, {-1, -2}, {-2, -1}, {-2, 1}, {2, -1}] to the current coordinates.

Therefore, we can avoid the negative coordinates and create our solution around the first quadrant, keeping the coordinates positive. The origin is fixed, and we can use this to transform our input coordinates. We can take the absolute value of the coordinate and use it as our starting point. This way, we know which direction we should move in. In this case, we will only move in two directions by adding the following coordinates to the current coordinates, [{-1, -2}, {-2, -1}]. We will only explore the absolute values of the coordinates.

Here is how we will implement this solution:
1. Take the absolute values of the coordinates (x, y).
2. Manually initialize the map with the minimum moves it takes to get to the origin’s coordinates. The map contains the coordinate as the key and minimum knight it takes to get to the origin as the value.
3. Start from the input coordinates and explore all the squares in a depth-first manner back to the origin.
4. If the coordinate has already been explored, we can return that value; otherwise, we will explore the next possible coordinates the knight can move to.
5. We pick the path with the minimum moves and backtrack to the input coordinate.

![wer](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/wer/wer3.png)
![wer](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/wer/wer4.png)
![wer](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/wer/wer5.png)
![wer](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/wer/wer6.png)
![wer](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/wer/wer7.png)
![wer](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/wer/wer8.png)
![wer](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/wer/wer9.png)
![wer](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/wer/wer10.png)
![wer](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/wer/wer11.png)
![wer](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/wer/wer12.png)
![wer](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/wer/wer13.png)
![wer](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/wer/wer14.png)

Let’s review the solution:

{% highlight java %}
class Solution {
    public static HashMap<String, Integer> moves = new HashMap<>();
    public static int dfs(int x, int y){
        String key = x + ", " + y; 
        if(moves.containsKey(key)){
            return moves.get(key);
        }
        int res = Math.min(dfs(Math.abs(x-2), Math.abs(y-1)), dfs(Math.abs(x-1), Math.abs(y-2))) + 1; 
        moves.put(x + ", " + y, res);
        return res;
    }

    public static int minimumKnightMoves(int x, int y){
        
        moves.put("0, 0", 0);
        moves.put("1, 1", 2);
        moves.put("2, 0", 2);
        moves.put("0, 2", 2);
        moves.put("1, 0", 3);
        moves.put("0, 1", 3);
        
        return dfs(x, y);
    }

    public static void main( String args[] ) {
        System.out.println(minimumKnightMoves(2, 1));
        System.out.println(minimumKnightMoves(2, 0));
        System.out.println(minimumKnightMoves(3, 1));
        System.out.println(minimumKnightMoves(5, 5));
    }
}
{% endhighlight %}

![wer](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/wer/wer15.png)

## Sparse Matrix Multiplication

## Description
We have two sparse matrices, A and B.

“A sparse matrix is one in which most of the elements are zero.”

You need to multiply the two matrices and return the output matrix. You can assume that A’s column number is equal to B’s row number.

## Constraints
The following are some constraints:
* 1 <= A.length, B.length <= 100
* 1 <= A[i].length, B[i].length <= 100
* -100 <= A[i][j], B[i][j] <= 100
* Let’s review this scenario using the example below:

![wer](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/wer/wer16.png)

## Solution
We have two sparse matrices, meaning most of the matrices’ elements are zero. We can represent the input matrices as hashmaps, and only save the non-zero elements and their indexes.

Here is how we will implement this solution:
1. First, we will convert the input matrices to their corresponding hashmaps. The HashMaps contain the matrix’s pair(i, j) as the key and the non-zero element at the index as the value.
2. Next, we will define an output matrix with the dimensions rows for matrix A * column for matrix B and set all the elements to zeroes.
3. Then, we will iterate over the hashmap A and the columns of matrix B in a nested manner.
4. Check whether the pair(jth index of hashmap A, j the column) exists in the hashmap B or not.
5. If it does not exist, we will move on to the next column or the HashMap’s next element accordingly.
6. If it exists, we will multiply the value for hashmap A and the value for hashmap B and add it to the element at the (ith index of hashmap A, j) index in the output matrix.
7. Once we have iterated over all the HashMap elements, the output matrix is ready.

![wer](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/wer/wer17.png)
![wer](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/wer/wer18.png)
![wer](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/wer/wer19.png)
![wer](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/wer/wer20.png)
![wer](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/wer/wer21.png)
![wer](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/wer/wer22.png)
![wer](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/wer/wer23.png)
![wer](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/wer/wer24.png)
![wer](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/wer/wer25.png)
![wer](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/wer/wer26.png)
![wer](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/wer/wer27.png)
![wer](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/wer/wer28.png)

{% highlight java %}
class Solution {
    public static int[][] multiply(int[][] A, int[][] B){
        HashMap<Integer, Integer> mapA = new HashMap<>();
        HashMap<Integer, Integer> mapB = new HashMap<>();
        int n = A.length;
        int m = B.length;
        int p = B[0].length;

        int[][] C = new int[n][p];


        for(int i = 0; i < n; i++){
            for(int j = 0; j < m; j++){
                if(A[i][j] != 0){
                    mapA.put(i * m + j, A[i][j]);
                }
            }
        }

        for(int i = 0; i < m; i++){
            for(int j = 0; j < p; j++){
                if(B[i][j] != 0){
                    mapB.put(i * p + j, B[i][j]);
                }
            }
        }
        
        for (Map.Entry<Integer, Integer> itA : mapA.entrySet()){
            for(int j = 0; j < p; ++j){
                if(mapB.containsKey(j + p * (itA.getKey() % m))){
                    int itB = mapB.get(j + p * (itA.getKey() % m));
                    C[itA.getKey() / m][j] += itA.getValue() * itB; 
                }
            }
        }
         
        return C;
    }
    
    public static void main( String args[] ) {
        // Driver Code
        int[][] A = { {1, 0, 0}, {0, 1, 3} };
        int[][] B = { {5, 0, 0}, {0, 0, 0}, {3, 0, 2} };
        System.out.println(Arrays.deepToString(multiply(A, B)));

        int[][] D = { {1, -5} };
        int[][] E = { {12}, {-1} };
        System.out.println(Arrays.deepToString(multiply(D, E)));
        
    }
}
{% endhighlight %}

![wer](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/wer/wer29.png)

## Design In-Memory File System

## Description
You have to design an in-memory file system. The skeleton for the class FileSystem is provided to you. You have to simulate the following functions:

ls: You are given a string representing a path. If it is a file path, return a list that only contains the file’s name. If it is a directory path, return the list of file and directory names in this directory. Your function should return the output (file and directory names together) in lexicographical order.

mkdir: Given a directory path that does not exist, you need to make a new directory according to the path. The function should create all the middle directories in the path if they do not already exist. This function return type is void.

addContentToFile: You are given a file path and file content in string format. If the file doesn’t exist, you need to create that file containing the given content. If the file already exists, you need to append the given content to the original content. This function return type is void.

readContentFromFile: Given a file path, return its content in string format.

## Example
Let’s look at an example input and output chart:

![wer](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/wer/wer30.png)

## Assumptions
* You can assume all file or directory paths are absolute paths that begin with /, and do not end with / except the path that is just "/".
* You can assume that all operations will be passed using valid parameters. Users will not attempt to retrieve file content or list a non-existent directory or file or add a non-existent directory file.
* You can assume that all directory and file names only contain lower-case letters, and the file and directory names are unique.

## Solution
We need a mechanism to represent files and directories. A directory can contain other directories and files, whereas a file only contains content in the form of a string. To describe files, we will use a unified structure, File. The structure includes the following elements:
* isFile: This is a Boolean to represent whether the given entity is a file or a directory.
* files: This is a nested HashMap that contains files (represented by File Contents in the illustration below) against a string path (represented by File Names in the illustration below) if the current object is a directory.
* content: This is a string that contains the content if the object is a file. This field is empty if the object is a directory.

We store the root file in our file system. Review the directory structure below:

![wer](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/wer/wer31.png)

Next, we will look at how to implement the methods one by one:
* ls: We start by initializing a temporary file pointer and splitting the input path by "/". Once split, we traverse the files map going one level down through the directory structure during each iteration. Once we reach the subdirectory corresponding to the split path’s last element, we return the files in the current file pointer if it is a directory. Otherwise, we return the filename.
* mkdir: As in ls, we iterate the directory structure level by level. If the directory in the path does not exist, we create a new directory. We repeat this step as long as we do not reach the end level directory.
* addContentToFile: We iterate over the directory structure level by level and reach the end level directory. If the file exists, we append the content to the file. Otherwise, we create a file and initialize the contents with the input content.
* ReadContentFromFile: Similarly, we iterate over the directory structure level by level and reach the end level directory. Search the file in the files map at the current level and return its contents.

{% highlight java %}
class FileSystem {
    class File {
        boolean isFile = false;
        HashMap<String, File> files = new HashMap<>();
        String content = "";
    }
    File root;
    public FileSystem() {
        root = new File();
    }

    public List<String> ls(String path) {
        File t = root;
        List<String> files = new ArrayList<>();
        if (!path.equals("/")) {
            String[] d = path.split("/");
            for (int i = 1; i < d.length; i++) {
                t = t.files.get(d[i]);
            }
            if (t.isFile) {
                files.add(d[d.length - 1]);
                return files;
            }
        }
        List<String> resFiles = new ArrayList<>(t.files.keySet());
        Collections.sort(resFiles);
        return resFiles;
    }

    public void mkdir(String path) {
        File t = root;
        String[] d = path.split("/");
        for (int i = 1; i < d.length; i++) {
            if (!t.files.containsKey(d[i]))
                t.files.put(d[i], new File());
            t = t.files.get(d[i]);
        }
    }

    public void addContentToFile(String filePath, String content) {
        File t = root;
        String[] d = filePath.split("/");
        for (int i = 1; i < d.length - 1; i++) {
            t = t.files.get(d[i]);
        }
        if (!t.files.containsKey(d[d.length - 1]))
            t.files.put(d[d.length - 1], new File());
        t = t.files.get(d[d.length - 1]);
        t.isFile = true;
        t.content = t.content + content;
    }

    public String readContentFromFile(String filePath) {
        File t = root;
        String[] d = filePath.split("/");
        for (int i = 1; i < d.length - 1; i++) {
            t = t.files.get(d[i]);
        }
        return t.files.get(d[d.length - 1]).content;
    }
    // Driver Code
    public static void main(String args[]){
        FileSystem fs = new FileSystem();
        System.out.println(fs.ls("/"));
        fs.mkdir("/dir1/dir2/dir3");
        fs.mkdir("/dir4/dir2/dir3");
        fs.addContentToFile("/dir1/dir2/dir3/file1", "File");
        System.out.println(fs.ls("/"));
        System.out.println(fs.readContentFromFile("/dir1/dir2/dir3/file1"));
        fs.addContentToFile("/dir1/dir2/dir3/file1", " System");       
        System.out.println(fs.readContentFromFile("/dir1/dir2/dir3/file1"));
    }
}
{% endhighlight %}

![wer](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/wer/wer32.png)
![wer](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/wer/wer33.png)

## Spiral Matrix

## Description
Given an m * n matrix, you have to return all the matrix elements in spiral order. The spiral order signifies traversing the matrix in clockwise order.

Let’s review the spiral order below:

![wer](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/wer/wer34.png)
![wer](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/wer/wer35.png)
![wer](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/wer/wer36.png)
![wer](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/wer/wer37.png)
![wer](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/wer/wer38.png)
![wer](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/wer/wer39.png)
![wer](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/wer/wer40.png)
![wer](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/wer/wer41.png)
![wer](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/wer/wer42.png)
![wer](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/wer/wer43.png)
![wer](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/wer/wer44.png)

## Solution
To solve this problem, we will use a layer by layer approach. In this approach, we iterate over the outer layers’ elements in clockwise order, followed by the inner layer’s elements.

For each layer, we will start from the top left corner and iterate over the elements in that layer. We define the top-left coordinates, say (r1, c1) and bottom-right coordinates, say (r2, c2).

As we explore the layers in clockwise order, we have to:
1. Iterate the top row, (r1, c), where c ranges from c1 to c2.
2. Iterate the right side, (r, c2), where r ranges from r1 + 1 to r2.
3. Iterate the bottom row, (r2, c), where c ranges from c2 - 1 to c1 + 1.
4. Iterate the left side, (r, c1), where r ranges from r2 to r1 + 1.

We repeat these steps until either r1 > r2 or c1 > c2 or both.

Let’s start from the outermost layer. In the solution below, the top-left coordinates are (0, 0), and the bottom-right coordinates are (5, 5).

![wer](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/wer/wer45.png)
![wer](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/wer/wer46.png)
![wer](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/wer/wer47.png)
![wer](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/wer/wer48.png)
![wer](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/wer/wer49.png)
![wer](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/wer/wer50.png)
![wer](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/wer/wer51.png)
![wer](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/wer/wer52.png)
![wer](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/wer/wer53.png)

{% highlight java %}
class Solution {
    public static List<Integer> spiralOrder(int[][] matrix) {
        List<Integer> res = new ArrayList<Integer>();
        if (matrix.length == 0)
            return res;
        int r1 = 0, r2 = matrix.length - 1;
        int c1 = 0, c2 = matrix[0].length - 1;
        while (r1 <= r2 && c1 <= c2) {
            for (int c = c1; c <= c2; c++) res.add(matrix[r1][c]);
            for (int r = r1 + 1; r <= r2; r++) res.add(matrix[r][c2]);
            if (r1 < r2 && c1 < c2) {
                for (int c = c2 - 1; c > c1; c--) res.add(matrix[r2][c]);
                for (int r = r2; r > r1; r--) res.add(matrix[r][c1]);
            }
            r1++;
            r2--;
            c1++;
            c2--;
        }
        return res;
    }

    public static void main( String args[] ) {
        int[][] matrix = { {0, 1, 2}, {7, 8, 3}, {6, 5, 4} };
        System.out.println(spiralOrder(matrix));
    }
}
{% endhighlight %}

![wer](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/wer/wer54.png)
