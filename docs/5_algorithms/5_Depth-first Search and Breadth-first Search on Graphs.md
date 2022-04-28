---
layout: default
title: Depth-first Search and Breadth-first Search on Graphs
parent: Algorithms
nav_order: 5
permalink: /algorithms/search_on_graphs
---
<div align="center" markdown="1">
Depth-first Search and Breadth-first Search on Graphs / Java resources / Tutorial

{: .fs-8 .fw-400 }
</div>

## Depth-first Search and Breadth-first Search on Graphs

## Tree with 0+ cycle
At this point, you should be pretty familiar with trees. A tree is a special graph: a connected acyclic (cycle-less) graph. A graph may contain cycle(s) and nodes could be disconnected.
![dsbs](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/dsbs/dsbs1.png)

## Graph Terminologies
A graph consists of vertices (“nodes” in trees) and edges. Vertices are connected by edges. Two vertices connected by an edge are called neighbors and are adjacent (“children” and “parents” in trees).
![dsbs](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/dsbs/dsbs2.png)
Edges can be undirected or directed. For most interview problems, we will deal with undirected graphs. A tree is also an undirected graph. We’ll discuss directed graphs in the course schedule module.
![dsbs](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/dsbs/dsbs3.png)
A path is a sequence of vertices. A cycle is a path that starts and ends at the same vertex.
![dsbs](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/dsbs/dsbs4.png)
An undirected graph is connected if every vertex is joined by a path to another vertex. Otherwise, it’s disconnected.
![dsbs](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/dsbs/dsbs5.png)
A graph is most commonly stored as a map of adjacency lists: for each vertex, store a list of its neighbors.
![dsbs](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/dsbs/dsbs6.png)
Note that even though a graph is represented as an adjacency list, we don’t actually have to create it upfront. What we really need is a function to get a vertex’s neighbors. We’ll see that in the next module.

## BFS on Graphs

## Tree vs Graph traversal
A tree is a connected, acyclic undirected graph. Statistically, most interview graph problems are about connected and undirected graphs.So, for simplicity, we will define a tree as a graph without any cycles. The search algorithms we have learned in tree modules are applicable to graphs as well.

Hopefully, by this point, you are very familiar with DFS on trees and BFS on trees. We must be cognizant of the fact that the difference between a tree and a graph is the potential of having a cycle. We use an extra visited variable to keep track of vertices we have already visited to prevent re-visiting and getting into infinite loops. visited can be any data structure that can answer existence queries quickly. For example, both a hash set and an array, where each element maps to a vertex in the graph, can do this in constant time.

## BFS on graphs

Let’s visualize BFS:
![dsbs](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/dsbs/dsbs7.png)
![dsbs](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/dsbs/dsbs8.png)
![dsbs](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/dsbs/dsbs9.png)
![dsbs](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/dsbs/dsbs10.png)
![dsbs](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/dsbs/dsbs11.png)
![dsbs](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/dsbs/dsbs12.png)
![dsbs](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/dsbs/dsbs13.png)
![dsbs](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/dsbs/dsbs14.png)
![dsbs](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/dsbs/dsbs15.png)
![dsbs](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/dsbs/dsbs16.png)

## Time complexity
During a BFS, we visit each node and each vertex at most once. The time complexity for BFS on a graph is O(E + V)O(E+V) where EE is the number of edges of the graph, and VV is the number of vertices of the graph.

But in the BFS on trees section, we stated that the time complexity of BFS is O(N). This is because a tree is a special graph where the number of edges is one less than the number of nodes.

## BFS on graph template
The BFS template consists of two core functions:
1. bfs: uses a queue to keep track of the nodes to be visited.
2. get_neighbors: returns a node’s neighbors. In an adjacency list representation, this would be returning the list of neighbors for the node. If the problem is about a matrix, this would be the surrounding valid cells as we will see in the number of islands and knight shortest path. If the graph is implicit, we have to generate the neighbors as we traverse. We will see this in the word ladder.

{% highlight java %}

public void bfs(Node root) {
    ArrayDeque<Node> queue = new ArrayDeque<>();
    queue.add(root);
    Set<Node> visited = new HashSet<>();
    while (queue.size() > 0) {
        Node node = queue.pop();
        for (Node neighbor : getNeighbors(node)) {
            if (visited.contains(neighbor)) {
                continue;
            }
            queue.add(neighbor);
            visited.add(neighbor);
        }
    }
}
{% endhighlight %}

## Tracking levels/finding distance
BFS is by-level traversal. Sometimes we need to track how many levels we have traversed (much like level order traversal problem in BFS on Tree module).

Similar to binary tree level order traversal, we can get the number of nodes of a level from the queue size.

{% highlight java %}

public void bfs(Node root) {
    ArrayDeque<Node> queue = new ArrayDeque<>();
    queue.add(root);
    Set<Node> visited = new Hashset<>();
    int level = 0;
    while (queue.size() > 0) {
        int n = queue.size();  // get # of nodes in the current level
        for (int i = 0; i < n; i++) {
            Node node = queue.pop();
            for (Node neighbor : getNeighbors(node)) {
                if (visited.contains(neighbor)) {
                    continue;
                }
                queue.add(neighbor);
                visited.add(neighbor);
            }
        }
        // increment level after we have processed all nodes of the level
        level++;
    }
}
{% endhighlight %}

## DFS on Graphs
![dsbs](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/dsbs/dsbs17.png)
![dsbs](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/dsbs/dsbs18.png)
![dsbs](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/dsbs/dsbs19.png)
![dsbs](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/dsbs/dsbs20.png)
![dsbs](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/dsbs/dsbs21.png)
![dsbs](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/dsbs/dsbs22.png)
![dsbs](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/dsbs/dsbs33.png)
![dsbs](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/dsbs/dsbs34.png)
![dsbs](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/dsbs/dsbs25.png)
![dsbs](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/dsbs/dsbs26.png)

Similar to BFS, we just have to add the visited variable to keep track of the visited nodes and use get_neighbors to get the next nodes to visit.

{% highlight java %}

public void dfs(Node root, Set<Node> visited) {

    if (visited.contains(root)) {
        continue;
    }

    for (Node child : node.children) {
        dfs(child);
        visited.add(child);
    }
}
{% endhighlight %}

## Complexity
We only visit each vertex once in both BFS and DFS with visited. Since technically a graph is made of vertices and edges, the time complexity of BFS/DFS on graphs is normally expressed as O(|V| + |E|) where |V| stands for the number of vertices and |E| stands for the number of edges. V is a set of vertices and in maths |V| means the size of a set.

## BFS or DFS

## When should you use one over the other?
If you just have to visit each node once without memory constraints (e.g. number of islands problem), then it doesn’t really matter which one you use. It comes down to your personal preference for recursion/stack vs queue.

BFS is better at:
* Finding the shortest distance between two vertices
* Graph of unknown size, e.g. word ladder, or even infinite size, e.g. knight shortest path

DFS is better at:
* Using less memory than BFS for wide graphs since BFS has to keep all the nodes in the queue because this can be quite large for wide graphs;
* Finding nodes far away from the root, e.g. looking for an exit in a maze.

## Matrix as Graph

## Problem statement#

Very often, graph problems are represented as matrices. For example:
* Number of Islands
* Knight Shortest Path

A matrix translates to a graph (adjacency list):
![dsbs](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/dsbs/dsbs27.png)
When we code the problem, we have to build the graph as we go. Nodes/vertices are represented by coordinates of matrix entries.
![dsbs](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/dsbs/dsbs28.png)

## Getting neighboring node’s coordinates
The core of BFS/DFS is to add neighbors of the current vertex to a queue/stack. The get_neighbors function returns all 4 coordinates of neighboring nodes (or 8 if you are allowed to go diagonal).
![dsbs](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/dsbs/dsbs29.png)
One way to get each neighbor’s coordinates is to keep each neighbor’s horizontal and vertical offsets in a list and adding them to the each vertex’s coordinates.
![dsbs](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/dsbs/dsbs30.png)
{% highlight java %}

public List<Coordinate> getNeighbors(Coordinate coord) {
    int row = coord.row;
    int col = coord.col;
    int[] deltaRow = {-1, 0, 1, 0};
    int[] deltaCol = {0, 1, 0, -1};
    List<Coordinate> res = new ArrayList<>();
    for (int i = 0; i < deltaRow.length; i++) {
        int neighborRow = row + deltaRow[i];
        int neighborCol = col + deltaCol[i];
        if (0 <= neighborRow && neighborRow < numRows && 
            0 <= neighborCol && neighborCol < numCols) {
                res.add(new Coordinate(neighborRow, neighborCol));
            }
    }
    return res;
}
{% endhighlight %}

## BFS template
Here’s the complete template for BFS on the matrix:
{% highlight java %}

public int numRows = grid.length;
public int numCols = grid[0].length;

public List<Coordinate> getNeighbors(Coordinate coord) {
    int row = coord.row;
    int col = coord.col;
    int[] deltaRow = {-1, 0, 1, 0};
    int[] deltaCol = {0, 1, 0, -1};
    List<Coordinate> res = new ArrayList<>();
    for (int i = 0; i < deltaRow.length; i++) {
        int neighborRow = row + deltaRow[i];
        int neighborCol = col + deltaCol[i];
        if (0 <= neighborRow && neighborRow < numRows && 
            0 <= neighborCol && neighborCol < numCols) {
                res.add(new Coordinate(neighborRow, neighborCol));
            }
    }
    return res;
}

public void bfs(Coordinate startingNode) {
    Deque<Coordinate> queue = new ArrayDeque<>();
    queue.add(startingNode);
    Set<Coordinate> visited = new HashSet<>();
    visited.add(startingNode)

    while (queue.size() > 0) {
        Coordinate node = queue.pop();
        for (Coordinate neighbor : getNeighbors(node)) {
            if (visited.contains(neighbor)) {
            continue;
            queue.add(neighbor);
            visited.add(neighbor);
            }
        }
    }
}
{% endhighlight %}

## Shortest Path [BFS]
Given an (unweighted) graph, return the length of the shortest path between two nodes A and B in terms of the number of edges.
![dsbs](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/dsbs/dsbs31.png)

## Explanation
BFS is the best for finding distance between two nodes since it traverses level by level. Apply the template from the BFS template. Since the graph is already built for us, get_neighbors retrieves the adjacency list.

A quick note on “unweighted”; sometimes, a graph’s edges can have weight. For example, a graph that represents city connections and the weights of the edges represent the distance between cities.

BFS can find the shortest path for unweighted graphs. For weighted graphs, we need algorithms like Dijkstra’s algorithm. Dijkstra’s algorithm rarely comes up in coding interviews, so we won’t get into its details here.

The time complexity is O(E + V), where EE is the number of edges of the graph, and VV is the number of vertices of the graph.

{% highlight java %}

class Solution {

    public static int getLengthOfShortestPath(Map<Node, List<Node>> graph, Node A, Node B) {
        return bfs(graph, A, B);
    }

    private static List<Node> getNeighbors(Map<Node, List<Node>> graph, Node node) {
        return graph.get(node);
    }

    private static int bfs(Map<Node, List<Node>> graph, Node root, Node target) {
        ArrayDeque<Node> queue = new ArrayDeque<>();
        queue.add(root);
        Set<Node> visited = new HashSet<>();
        int level = 0;
        while (queue.size() > 0) {
            int n = queue.size();  // get # of nodes in the current level
            for (int i = 0; i < n; i++) {
                Node node = queue.pop();
                if (node.equals(target)) return level;
                for (Node neighbour : getNeighbors(graph, node)) {
                    if (visited.contains(neighbour)) continue;
                    queue.add(neighbour);
                    visited.add(neighbour);
                }
            }
            level++;
        }
        return level;
    }

    // Driver code
    public static void main(String[] args) {
        String[] inputs =  {"4"};
        String[][] inputs1 = [{"1", "2"},{"0", "2", "3"},{"0", "1"},{"1"}];
        String[] inputs2 = {"0"};
        String[] inputs3 = {"3"};

        for(int i = 0; i < inputs.length; i++) {

            int n = Integer.parseInt(inputs[i]);
            Node[] nodes = new Node[n];
            for (int j = 0; j < n; j++) {
                nodes[j] = new Node(j);
            }
            Map<Node, List<Node>> graph = new HashMap<>(n);
            for (int j = 0; j < n; j++) {
                List<Node> neighbors = Arrays.stream(inputs1[j]).map(node -> nodes[Integer.parseInt(node)]).collect(Collectors.toList());
                graph.put(nodes[j], neighbors);
            }
            Node A = nodes[Integer.parseInt(inputs2[i])];
            Node B = nodes[Integer.parseInt(inputs3[i])];

            System.out.println("Length of shortest path : " + String.valueOf(Solution.getLengthOfShortestPath(graph, A, B)));
        }
    }
}
class Node {
    int val;

    public Node(int val) {
        this.val = val;
    }
}
{% endhighlight %}

## Word Ladder

## Problem statement
Word Ladder is “a puzzle that begins with two words, and to solve the puzzle one must find a chain of other words to link the two, in which two adjacent words (that is, words in successive steps) differ by one letter.”

For example: COLD → CORD → CARD → WARD → WARM

![dsbs](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/dsbs/dsbs42.png)

iven a start word, an end word, and a list of dictionary words, determine the minimum number of steps to go from the start word to the end word using only words from the dictionary.

## Example

Input:
start = "COLD"
end = "WARM"
word_list = ["COLD", "GOLD", "CORD", "SOLD", "CARD", "WARD", "WARM", "TARD"]
Output:
4

Explanation: We can go from COLD to WARM by going through COLD → CORD → CARD → WARD → WARM

## Intuition

We start from a word. In each step, we can only go from one word in the list to another, and we want to end up on some word. This suggests that we can represent each word with a node in a graph and each step that transforms a word to another as an edge between the corresponding nodes:
![dsbs](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/dsbs/dsbs43.png)

Now the problem becomes “find the minimum distance from one node in a graph to the other”, which is a problem that BFS handles very easily.

Conceptually, we now have an algorithm that is a 2-step process:
1. Build a graph that represents the words and transformations
2. Use BFS on the graph to find the minimum distance

In the actual algorithm, we do not need to build up the graph before using BFS. We can build the graph as we go. Instead of storing the edges, we calculate the set of neighbors for the current node only when we need to visit them.

Our get_neighbors function looks like this:
{% highlight java %}
for (char c : ALPHABETS) {
    StringBuilder wordBuilder = new StringBuilder(word.length());
    wordBuilder.append(word.substring(0, j));
    wordBuilder.append(c);
    wordBuilder.append(word.substring(j + 1));
    String nextWord = wordBuilder.toString();
    if (words.contains(nextWord)) {
      process(nextWord)
    }
}

class Solution {
    public static final char[] ALPHABETS = new char[26];
    static {
        // ascii representation of english alphabets a - z are 
        numbers 97 - 122
        for (int i = 0; i < 26; i++) {
            ALPHABETS[i] = (char) (i + 'a');
        }
    }

    public static int wordLadder(String begin, String end, 
    String[] wordList) {
        // make a set because existence query is O(1) vs O(N) for list
        Set<String> words = new HashSet<>(Arrays.asList(wordList));
        ArrayDeque<String> queue = new ArrayDeque<>();
        queue.add(begin);
        int distance = 0;
        while (queue.size() > 0) {
            int n = queue.size();
            distance++;
            for (int i = 0; i < n; i++) {
                String word = queue.pop();
                for (int j = 0; j < word.length(); j++) {
                    for (char c : ALPHABETS) {
                        StringBuilder wordBuilder = new StringBuilder(
                        word.length());
                        wordBuilder.append(word.substring(0, j));
                        wordBuilder.append(c);
                        wordBuilder.append(word.substring(j + 1));
                        String nextWord = wordBuilder.toString();
                        if (!words.contains(nextWord)) continue;
                        if (nextWord.equals(end)) return distance;
                        queue.add(nextWord);
                        // removing from the set is equivalent as 
                        marking the word visited
                        words.remove(nextWord);
                    }
                }
            }
        }
        return 0;
    }

    // Driver code
    public static void main(String[] args) {
        String[] inputs = {"cold", "fool"};
        String[] inputs1 = {"warm", "sage"};
        String[] inputs2 = {"cold  gold  cord  card  ward  warm
          tard  sold","fool pool poll pole pale sale sage"};

         for(int i = 0; i < inputs.length; i++) {
             System.out.println("Word ladder : " + Solution.
             wordLadder(inputs[i], inputs1[i], inputs2[i].split(" ")));
         }
    }
}
{% endhighlight %}
![dsbs](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/dsbs/dsbs44.png)

## Flood Fill

## Problem statement
In computer graphics, an uncompressed raster image is presented as a matrix of numbers. Each entry of the matrix represents the color of a pixel. A flood fill algorithm takes a coordinate, r, c, and replaces all pixels connected to r, c that have the same color as r, c with the replacement color. An example of this is MS-Paint’s paint bucket tool.
![dsbs](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/dsbs/dsbs45.png)

## Explanation
The goal is to replace every neighboring cell of the same color with a different color. We can easily do this with a BFS or DFS.

Using BFS template and get_neighbor template, there’s very little we have to do except updating color with replacement_color.

The time complexity is O(MN) where MM and NN are the length and width of the matrix.
{% highlight java %}
class Coordinate {
    int r;
    int c;

    public Coordinate(int r, int c) {
        this.r = r;
        this.c = c;
    }
}
class Solution {

    public static void floodFill(List<List<Integer>> image, Coordinate start, 
    int replacementColor) {
        int numRows = image.size();
        int numCols = image.get(0).size();
        bfs(image, start, replacementColor, numRows, numCols);
    }

    private static List<Coordinate> getNeighbors(List<List<Integer>> image,
     Coordinate node, int rootColor, int numRows, int numCols) {
        List<Coordinate> neighbors = new ArrayList<>();
        int[] deltaRow = {-1, 0, 1, 0};
        int[] deltaCol = {0, 1, 0, -1};
        for (int i = 0; i < deltaRow.length; i++) {
            int neighborRow = node.r + deltaRow[i];
            int neighborCol = node.c + deltaCol[i];
            if (0 <= neighborRow && neighborRow < numRows && 0 <= neighborCol
             && neighborCol < numCols) {
                if (image.get(neighborRow).get(neighborCol) == rootColor) {
                    neighbors.add(new Coordinate(neighborRow, neighborCol));
                }
            }
        }
        return neighbors;
    }

    private static void bfs(List<List<Integer>> image, Coordinate root, 
    int replacementColor, int numRows, int numCols) {
        ArrayDeque<Coordinate> queue = new ArrayDeque<>();
        queue.add(root);
        boolean[][] visited = new boolean[numRows][numCols];
        int rootColor = image.get(root.r).get(root.c);
        image.get(root.r).set(root.c, replacementColor);  // replace root color
        visited[root.r][root.c] = true;
        while (queue.size() > 0) {
            Coordinate node = queue.pop();
            List<Coordinate> neighbors = getNeighbors(image, node, 
            rootColor, numRows, numCols);
            for (Coordinate neighbor : neighbors) {
                if (visited[neighbor.r][neighbor.c]) continue;
                image.get(neighbor.r).set(neighbor.c, 
                replacementColor);  // replace color
                queue.add(neighbor);
                visited[neighbor.r][neighbor.c] = true;
            }
        }
    }
    public static void main(String[] args) throws IOException {
        String[] inputs = {"2 2","1 1"};
        String[] inputs1 = {"9", "9"};
        String[] inputs2 = {"5", "4"};
        String[][] inputs3 = [{"0 1 3 4 1","3 8 8 3 3","6 7 8 8 3",
        "12 2 8 9 1","12 3 1 3 2"},
                {"0 1 6 4","2 3 3 5","3 3 3 3","6 4 3 4"}];

        for(int i = 0; i < inputs.length; i++) {
            String[] coord = inputs[i].split(" ");
            Coordinate start = new Coordinate(Integer
            .parseInt(coord[0]), Integer.parseInt(coord[1]));
            int color = Integer.parseInt(inputs1[i]);
            int rows = Integer.parseInt(inputs2[i]);
            List<List<Integer>> image = new ArrayList<>();
            for (int j = 0; j < rows; j++) {
                image.add(
                        Arrays.stream(inputs3[i][j].split(" "))
                        .map(Integer::parseInt).collect(Collectors.toList())
                );
            }


            Solution.floodFill(image, start, color);
                    
            List<String> actual_output = image.stream()
            .map(row -> row.stream().map(pixel -> Integer.toString(pixel))
            .collect(Collectors.joining(" "))).collect(Collectors.toList());
            
            System.out.println("output : " + Arrays.toString(
            actual_output.toArray())); 
        }
    }
}
{% endhighlight %}

## Number of Islands

A map is represented as a 2D grid of 1s and 0s where 1 represents land and 0 represents water. An island is a horizontally and vertically (but not diagonally) continuous block of land surrounded by water. Find the number of islands on the map. Assume cells beyond grid boundaries are water.
![dsbs](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/dsbs/dsbs32.png)

## Explanation

## Intuition
The 2D grid (matrix) is a graph as discussed in the Matrix as Graph module. To find an island, we can do BFS/DFS on a node and expand our search if the neighboring cell is 1. This is similar to how we find cells with the same color in Flood Fill.

Since there might be multiple islands, we have to do flood fill on every cell. Wouldn’t that blow up the time complexity, though? Remember, we record the visited cells and we can skip cells that have been visited already. So overall, every cell is visited only once.

Applying the BFS for matrix graph template:
{% highlight java %}

class Solution {
    
    public static int countNumberOfIslands(List<List<Integer>> grid) {
        int numRows = grid.size();
        int numCols = grid.get(0).size();
        int count = 0;
        // note that all bfs share the same visited set
        boolean[][] visited = new boolean[numRows][numCols];
        // bfs starting from each unvisited land cell
        for (int r = 0; r < numRows; r++) {
            for (int c = 0; c < numCols; c++) {
                if (grid.get(r).get(c) == 0 || visited[r][c]) continue;
                bfs(grid, visited, new Coordinate(r, c), numRows, numCols);
                // bfs would find 1 connected island, increment count
                count++;
            }
        }
        return count;
    }

    private static List<Coordinate> getNeighbors(Coordinate cell, int numRows, int numCols) {
        List<Coordinate> neighbors = new ArrayList<>();
        int[] deltaRow = {-1, 0, 1, 0};
        int[] deltaCol = {0, 1, 0, -1};
        for (int i = 0; i < deltaRow.length; i++) {
            int neighborRow = cell.r + deltaRow[i];
            int neighborCol = cell.c + deltaCol[i];
            if (0 <= neighborRow && neighborRow < numRows && 0 <= neighborCol && neighborCol < numCols) {
                neighbors.add(new Coordinate(neighborRow, neighborCol));
            }
        }
        return neighbors;
    }

    private static void bfs(List<List<Integer>> grid, boolean[][] visited, Coordinate root, int numRows, int numCols) {
        ArrayDeque<Coordinate> queue = new ArrayDeque<>();
        queue.add(root);
        visited[root.r][root.c] = true;
        while (queue.size() > 0) {
            Coordinate node = queue.pop();
            List<Coordinate> neighbors = getNeighbors(node, numRows, numCols);
            for (Coordinate neighbor : neighbors) {
                if (grid.get(neighbor.r).get(neighbor.c) == 0 || visited[neighbor.r][neighbor.c]) continue;
                queue.add(neighbor);
                visited[neighbor.r][neighbor.c] = true;
            }
        }
    }
    // Driver code  
	public static void main(String[] args) {

         String[] inputs = {
            "6", "2", "3"
        };
        String[][] inputsMatrix = {
            {
                "1 1 1 0 0 0", "1 1 1 1 0 0", "1 1 1 0 0 0", "0 1 0 0 0 0", "0 0 0 0 1 0", "0 0 0 0 0 0"
            }, {
                "1 0 1", "0 1 0"
            }, {
                "0 0 0", "0 0 0", "0 0 0"
            }
        };
		for (int i = 0; i<inputs.length; i++) {
			int rows = Integer.parseInt(inputs[i]);
            List<List<Integer>> grid = new ArrayList<>();
            for (int j = 0; j < rows; j++) {
                grid.add(
                    Arrays.stream(inputsMatrix[i][j].split(" ")).map(Integer::parseInt).collect(Collectors.toList())
                );
            }
            int actual_output = Solution.countNumberOfIslands(grid);
			System.out.println("Count number of islands : " + actual_output);
		}
	}
}
class Coordinate {
    int r;
    int c;

    public Coordinate(int r, int c) {
        this.r = r;
        this.c = c;
    }
}
{% endhighlight %}

## Using a matrix to store the visited nodes
You may have noticed the matrix itself is a good place to store the information of whether a cell has been visited. We can update the cell that has already been visited to another number —– like 2 –— to denote that it has been visited. Since the island has been recorded, we can even simply update it to 0, and can consider the visited cells simply as water.

Note that although this is a common solution in coding problems, in the real world you most likely do NOT want to mutate the function arguments.

The time complexity is O(MN) where MM and NN are the length and width of the matrix.

## Knight Minimum Moves

On an infinitely large chessboard, a knight is located on [0, 0].

A knight can move in eight directions.
![dsbs](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/dsbs/dsbs33.png)

Given a destination coordinate [x, y], determine the minimum number of moves from [0, 0] to [x, y].

## Explanation

## Intuition
The problem asks for the minimum moves so BFS is our choice here. The chessboard being infinite is totally fine with BFS since we build the graph as we go.

The get_neighbors function now returns cells in 8 directions.
![dsbs](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/dsbs/dsbs34.png)
The chessboard is infinite so we no longer have to worry about bound checking.

## Solution
{% highlight java %}

class Solution {

    public static int getKnightShortestPath(int x, int y) {
        return bfs(new Coordinate(0, 0), x, y);
    }
    private static int bfs(Coordinate start, int x, int y) {
        Set<Coordinate> visited = new HashSet<>();
        visited.add(start);
        int steps = 0;
        ArrayDeque<Coordinate> queue = new ArrayDeque<>();
        queue.add(start);
        while (queue.size() > 0) {
            int n = queue.size();
            for (int i = 0; i < n; i++) {
                Coordinate node = queue.pop();
                if (node.c == x && node.r == y) {
                    return steps;
                }
                List<Coordinate> neighbors = getNeighbors(node);
                for (Coordinate neighbor : neighbors) {
                    if (visited.contains(neighbor)) continue;
                    queue.add(neighbor);
                    visited.add(neighbor);
                }
            }
            steps++;
        }
        return steps;
    }

    private static List<Coordinate> getNeighbors(Coordinate coord) {
        List<Coordinate> res = new ArrayList<>();
        int[] deltaRow = {-2, -2, -1, 1, 2, 2, 1, -1};
        int[] deltaCol = {-1, 1, 2, 2, 1, -1, -2, -2};
        for (int i = 0; i < deltaRow.length; i++) {
            int r = coord.r + deltaRow[i];
            int c = coord.c + deltaCol[i];
            res.add(new Coordinate(r, c));
        }
        return res;
    }
    // Driver code  
	public static void main(String[] args) {

        String[] inputs = {"2 1", "5 5"};
		for (int i = 0; i<inputs.length; i++) {
			String[] target = inputs[i].split(" ");
            int x = Integer.parseInt(target[0]);
            int y = Integer.parseInt(target[1]);
			System.out.println("Get knight shortest path : " + Solution.getKnightShortestPath(x, y));
		}
	}
}

class Coordinate {
    int r;
    int c;

    public Coordinate(int r, int c) {
        this.r = r;
        this.c = c;
    }

    @Override
    public int hashCode() {
        return Objects.hash(r, c);
    }

    @Override
    public boolean equals(Object obj) {
        if (obj == null) return false;
        if (this == obj) return true;
        if ((obj instanceof Coordinate) && ((Coordinate) obj).r == r && ((Coordinate) obj).c == c) {
            return true;
        }
        return false;
    }
}
{% endhighlight %}

## Course Schedule

There are a total of n courses a student has to take, numbered from 0 to n-1. A course may have prerequisites. The “depends on” relationship is expressed as a pair of numbers. For example, [0, 1] means you need to take course 1 before taking course 0. Given n and the list of prerequisites, decide if it is possible to take all the courses.

## Example 1:
Input: n = 2, prerequisites = [[0, 1]]

Output: true

Explanation: we can take 1 first and then 0.

## Example 2:
Input: n = 2, prerequisites = [[0, 1], [1, 0]]

Output: false

Explanation: the two courses depend on each other, there is no way to take them

## Explanation

## Intuition
Naturally, the dependency relationship can be modelled as a directed graph.

Notice that a course is “not takeable” if any of its dependencies are “not takeable”. This only happens when there is a circular dependency, e.g., A depends on B and B depends on A. In graph terms, this is called a cycle. This problem then comes down to determining if the graph contains a cycle. Note that this is a directed graph, and a path is only a cycle if one of the nodes points back to one of the nodes in the current path.
![dsbs](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/dsbs/dsbs35.png)

## Cycle detection
One way to detect cycles is to use DFS. For normal graph DFS a node has two states: to be visited and visited. We traverse the graph and visit each node and mark it as visited.

In cycle detection, we need a third state visiting. We perform DFS on each node by:
* marking a node as visiting
* visiting each of its neighbors

When we reach the end of the path, i.e. no more out edges from the last node in the path, we mark the node in the path as visited. If during the DFS we happen to come back to a node that is in the visiting state, we have a cycle.

Draw a figure
![dsbs](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/dsbs/dsbs36.png)
![dsbs](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/dsbs/dsbs37.png)
![dsbs](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/dsbs/dsbs38.png)
![dsbs](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/dsbs/dsbs39.png)
![dsbs](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/dsbs/dsbs40.png)
![dsbs](https://raw.githubusercontent.com/TestJavaDev/java-resources/master/resources/dsbs/dsbs41.png)

## Solution
One question you may ask is why we have to introduce an additional state visiting. Couldn’t we have solved it with only visited and to be visited as in normal DFS?

Consider the following case:
* If we use the normal DFS logic and reject when a node in the visited state is revisited, we would have determined the above graph to have a cycle. Even though node 3 is visited twice, the graph does not contain a cycle.
* In a directed graph, a path is only a cycle if a node on the path points to an existing node on the same path. If we only have two states, we wouldn’t be able to distinguish this. The visiting state gives us a way to represent the “current path”.

{% highlight java %}
enum State {
    TO_VISIT, VISITING, VISITED
}

class Solution {

    public static boolean isValidCourseSchedule(int n, int[][] prerequisites) {
        Map<Integer, List<Integer>> graph = buildGraph(prerequisites);
        State[] states = new State[n];
        Arrays.fill(states, State.TO_VISIT);
        // dfs on each node
        for (int i = 0; i < n; i++) {
            if (!dfs(i, states, graph)) return false;
        }
        return true;
    }

    private static boolean dfs(int start, State[] states, Map<Integer, List<Integer>> graph) {
        // mark self as visiting
        states[start] = State.VISITING;

        if (graph.get(start) != null) {
            for (Integer nextVertex : graph.get(start)) {
                // ignore visited nodes
                if (states[nextVertex] == State.VISITED) continue;
                // revisiting a visiting node, CYCLE!
                if (states[nextVertex] == State.VISITING) return false;
                // recursively visit neighbours
                // if a neighbour found a cycle, we return false right away
                if (!dfs(nextVertex, states, graph)) return false;
            }
        }

        // mark self as visited
        states[start] = State.VISITED;
        // if we have gotten this far, our neighbours haven't found any cycle, return true
        return true;
    }

    private static Map<Integer, List<Integer>> buildGraph(int[][] prerequisites) {
        Map<Integer, List<Integer>> graph = new HashMap<>(prerequisites.length);
        for (int[] dependency : prerequisites) {
            if (graph.get(dependency[0]) == null) {
                List<Integer> list = new ArrayList<>();
                graph.put(dependency[0], list);
            }
            graph.get(dependency[0]).add(dependency[1]);
        }
        return graph;
    }
    // Driver code  
	public static void main(String[] args) {

        String[] inputs = {"2","2", "4"};
        String[] inputs1 = {"1", "2", "4"};
        String[][] inputs2 = [{"0 1"},{"0 1","1 0"},{"0 1","1 2","2 3","3 1"}];
		for (int i = 0; i<inputs.length; i++) {
			int n = Integer.parseInt(inputs[i]);
            int numDependencies = Integer.parseInt(inputs1[i]);
            int[][] relationships = new int[numDependencies][];
            for (int j = 0; j < numDependencies; j++) {
                String[] courses = inputs2[i][j].split(" ");
                int[] dependency = new int[2];
                dependency[0] = Integer.parseInt(courses[0]);
                dependency[1] = Integer.parseInt(courses[1]);
                relationships[j] = dependency;
            }
			System.out.println("Course Schedule : " +Solution.isValidCourseSchedule(n, relationships));
		}
	}
}
{% endhighlight %}










