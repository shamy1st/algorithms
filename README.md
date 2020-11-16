# Algorithms

## Sorting

time           | best        | worst
---------------|-------------|-------
bubble sort    | O(n)        | O(n^2)
selection sort | O(n^2)      | O(n^2)
insertiin sort | O(n)        | O(n^2)
merge sort     | O(nlog n)   | O(nlog n)
quick sort     | O(nlog n)   | O(n^2)
bucket sort    | O(n + k)    | O(n^2)

--             | time | space
---------------|------|------
counting sort  | O(n) | O(k)

space          | best        | worst
---------------|-------------|----------
merge sort     | O(n)        | O(n)
quick sort     | O(log n)    | O(n)

### Bubble Sort
![](https://github.com/shamy1st/algorithms/blob/main/images/bubble-sort-complexity.png)

--          | best  | worst
------------|-------|-------
bubble sort | O(n)  | O(n^2)

* **Ascending Order**

        public void sort(T[] array) {
            for(int i=0;i<array.length;i++) {
                for (int j = 1; j < array.length - i; j++) {
                    if (array[j].compareTo(array[j - 1]) < 0) {
                        swap(array, j, j - 1);
                    }
                }
            }
        }

* **Optimized**

        public void sortOptimized(T[] array) {
            for(int i=0;i<array.length;i++) {
                boolean isSorted = true;
                for (int j = 1; j < array.length - i; j++) {
                    if (array[j].compareTo(array[j - 1]) < 0) {
                        swap(array, j, j - 1);
                        isSorted = false;
                    }
                }

                if(isSorted)
                    return;
            }
        }

### Selection Sort
![](https://github.com/shamy1st/algorithms/blob/main/images/selection-sort-complexity.png)

--             | best   | worst
---------------|--------|-------
selection sort | O(n^2) | O(n^2)

* **steps**
    * pick the minimum element and swap with the first element.
    * do that again for the (n-1) elements.

* **Ascending Order**

        public void sort(T[] array) {
            for(int i=0;i<array.length;i++) {
                swap(array, minIndex(array, i), i);
            }
        }

        private int minIndex(T[] array, int startIndex) {
            int minIndex = startIndex;
            for(int j=startIndex;j<array.length;j++) {
                if(array[j].compareTo(array[minIndex]) < 0) {
                    minIndex = j;
                }
            }
            return minIndex;
        }

### Insertion Sort
![](https://github.com/shamy1st/algorithms/blob/main/images/insertion-sort-complexity.png)

--             | best   | worst
---------------|--------|-------
insertion sort | O(n)   | O(n^2)

* **steps**
    * start with the first element and start to insert second element to it.
    * as in cards sort elment while inserting it.
    * do the same till the end of the array.

* **Ascending Order**

        public void sort(T[] array) {
            for(int i=1;i<array.length;i++) {
                T current = array[i];
                int j = i - 1;
                while(j>=0 && array[j].compareTo(current) > 0) {
                    array[j + 1] = array[j];
                    j--;
                }
                array[j + 1] = current;
            }
        }

### Merge Sort
![](https://github.com/shamy1st/algorithms/blob/main/images/merge-sort-complexity.png)

time           | best        | worst
---------------|-------------|----------
merge sort     | O(nlog n)   | O(nlog n)

space          | best        | worst
---------------|-------------|----------
merge sort     | O(n)        | O(n)

* **Ascending Order**

        public void sort(T[] array) {
            if(array.length < 2)
                return;

            int middle = array.length / 2;
            T[] left = (T[]) new Number[middle];
            T[] right = (T[]) new Number[array.length - middle];
            for(int i=0;i<array.length;i++) {
                if(i < middle)
                    left[i] = array[i];
                else
                    right[i-middle] = array[i];
            }

            sort(left);
            sort(right);

            merge(left, right, array);
        }

        private void merge(T[] left, T[] right, T[] result) {
            int i = 0, j = 0, k = 0;
            while(i < left.length && j < right.length) {
                if(left[i].compareTo(right[j]) <= 0)
                    result[k++] = left[i++];
                else
                    result[k++] = right[j++];
            }

            //remaining items
            while(i < left.length)
                result[k++] = left[i++];

            while(j<right.length)
                result[k++] = right[j++];
        }

* **In place implementation**

### Quick Sort
![](https://github.com/shamy1st/algorithms/blob/main/images/quick-sort-complexity.png)

time           | best        | worst
---------------|-------------|----------
quick sort     | O(nlog n)   | O(n^2)

* **space because of stack calls**

space          | best        | worst
---------------|-------------|----------
quick sort     | O(log n)    | O(n)

* **steps**
    * choose an element as a pivot. (last element)
    * rearrange array so all smaller elements are to the left of pivot and greater elements to the right.
    * now this pivot in the right place.
    * repeat for all elements

* **Ascending Order**

        public void sort(T[] array) {
            sort(array, 0, array.length - 1);
        }

        private void sort(T[] array, int start, int end) {
            if(start >= end)
                return;

            //index of the pivot
            int boundary = partitioning(array, start, end);

            sort(array, start, boundary - 1);
            sort(array, boundary + 1, end);
        }

        private int partitioning(T[] array, int start, int end) {
            T pivot = array[end];
            int boundary = start - 1;  //left partition ref.

            for(int i=start;i<=end;i++)
                if(array[i].compareTo(pivot) <= 0)
                    swap(array, i, ++boundary);

            return boundary;
        }

### Counting Sort
![](https://github.com/shamy1st/algorithms/blob/main/images/counting-sort.png)
![](https://github.com/shamy1st/algorithms/blob/main/images/counting-sort-complexity.png)

--             | time | space
---------------|------|------
counting sort  | O(n) | O(k)

* **steps**
    * generate array of size k to count elements.
    * loop throw counts and generate ordered array.

* **Ascending Order**

        public void sort(int[] array, int max) {
            int[] counts = new int[max + 1];
            for(int item : array) {
                counts[item]++;
            }

            int index = 0;
            for(int i=0;i<counts.length;i++) {
                for(int j=0;j<counts[i]; j++) {
                    array[index++] = i;
                }
            }
        }

### Bucket Sort
![](https://github.com/shamy1st/algorithms/blob/main/images/bucket-sort.png)
![](https://github.com/shamy1st/algorithms/blob/main/images/bucket-sort-complexity.png)
![](https://github.com/shamy1st/algorithms/blob/main/images/bucket-sort-graph.png)

--             | best     | worst
---------------|----------|-------
bucket sort    | O(n + k) | O(n^2)

* **steps**
    * distribute elements to buckets.
    * sort each bucket using any sorting technique.
    * iterate throw buckets and generate ordered array.

* **Ascending Order**

        public void sort(T[] array, int numOfBuckets) {
            List<List<T>> buckets = new ArrayList<>();
            for(int i=0;i<numOfBuckets;i++)
                buckets.add(new ArrayList<>());

            for(T item : array)
                buckets.get((Integer)item / numOfBuckets).add(item);

            int index = 0;
            for(var bucket : buckets) {
                Collections.sort(bucket);
                for(var item : bucket)
                    array[index++] = item;
            }
        }

## Searching
* Linear Search
* Binary Search (Iterative, Recursive)
* Ternary Search
* Jump Search
* Exponential Search

## Strings

### Count Vowels

Find the number of vowels in a string. Vowels in English are A, E, O, U and I.
Input: “hello”
Output: 2

* **solution**

        public static int countVowels(String str) {
            if(str == null)
                return 0;
            
            Set<Character> vowels = new HashSet<>();
            vowels.add('a'); vowels.add('e'); vowels.add('o'); vowels.add('u'); vowels.add('i');

            int count = 0;
            for(var ch : str.toLowerCase().toCharArray())
                if(vowels.contains(ch))
                    count++;

            return count;
        }

### Reverse String

Input: “hello”
Output: “olleh”

* **solution**

        public static String reverse(String str) {
            if(str == null)
                return "";

            StringBuilder reversed = new StringBuilder();
            for(int i=str.length()-1;i>=0;i--)
                reversed.append(str.charAt(i));

            return reversed.toString();
        }

### Reverse Words

Reverse the order of words in a sentence.
Input: “Trees are beautiful”
Output: “beautiful are Trees”

* **solution**

        public static String reverseWords(String str) {
            if(str == null)
                return "";

            String[] words = str.trim().split(" ");
            StringBuilder reversed = new StringBuilder();
            for(int i=words.length-1;i>=0;i--) {
                reversed.append(words[i]);
                if(i != 0)
                    reversed.append(" ");
            }
            return reversed.toString();
        }

        or

        public static String reverseWords2(String str) {
            if (str == null)
                return "";

            String[] words = str.trim().split(" ");
            Collections.reverse(Arrays.asList(words));
            return String.join(" ", words);
        }

        or using stack

### Rotation

Check if a string is a rotation of another string.
Input: “ABCD”, “DABC” (rotate one char to the right)
Output: true

* **solution**

        public static boolean areRotations(String str1, String str2) {
            if(str1 == null || str2 == null || (str1.length() != str2.length()))
                return false;
            return (str1 + str1).contains(str2);
        }



## Greedy
* Activity Selection Problem
* Kruskal’s Minimum Spanning Tree Algorithm
* Huffman Coding
* Efficient Huffman Coding for Sorted Input
* Prim’s Minimum Spanning Tree Algorithm
* Prim’s MST for Adjacency List Representation
* Dijkstra’s Shortest Path Algorithm
* Dijkstra’s Algorithm for Adjacency List Representation
* Job Sequencing Problem
* Greedy Algorithm to find Minimum number of Coins
* K Centers Problem
* Minimum Number of Platforms Required for a Railway/Bus Station

## Dynamic Programming
* Overlapping Subproblems Property
* Optimal Substructure Property
* Longest Increasing Subsequence
* Longest Common Subsequence
* Edit Distance
* Min Cost Path
* Coin Change
* Matrix Chain Multiplication
* Binomial Coefficient
* 0-1 Knapsack Problem
* Egg Dropping Puzzle
* Longest Palindromic Subsequence
* Cutting a Rod
* Maximum Sum Increasing Subsequence
* Longest Bitonic Subsequence
* Floyd Warshall Algorithm
* Palindrome Partitioning
* Partition problem
* Word Wrap Problem
* Maximum Length Chain of Pairs
* Variations of LIS
* Box Stacking Problem
* Program for Fibonacci numbers
* Minimum number of jumps to reach end
* Maximum size square sub-matrix with all 1s
* Ugly Numbers
* Largest Sum Contiguous Subarray
* Longest Palindromic Substring
* Bellman–Ford Algorithm for Shortest Paths
* Optimal Binary Search Tree
* Largest Independent Set Problem
* Subset Sum Problem
* Maximum sum rectangle in a 2D matrix
* Count number of binary strings without consecutive 1?s
* Boolean Parenthesization Problem
* Count ways to reach the n’th stair
* Minimum Cost Polygon Triangulation
* Mobile Numeric Keypad Problem
* Count of n digit numbers whose sum of digits equals to given sum
* Minimum Initial Points to Reach Destination
* Total number of non-decreasing numbers with n digits
* Find length of the longest consecutive path from a given starting character
* Tiling Problem
* Minimum number of squares whose sum equals to given number n
* Find minimum number of coins that make a given value
* Collect maximum points in a grid using two traversals
* Shortest Common Supersequence
* Compute sum of digits in all numbers from 1 to n
* Count possible ways to construct buildings
* Maximum profit by buying and selling a share at most twice
* How to print maximum number of A’s using given four keys
* Find the minimum cost to reach destination using a train
* Vertex Cover Problem | Set 2 (Dynamic Programming Solution for Tree)
* Count number of ways to reach a given score in a game
* Weighted Job Scheduling
* Longest Even Length Substring such that Sum of First and Second Half is same

## Pattern Searching
* Naive Pattern Searching
* KMP Algorithm
* Rabin-Karp Algorithm
* A Naive Pattern Searching Question
* Finite Automata
* Efficient Construction of Finite Automata
* Boyer Moore Algorithm – Bad Character Heuristic
* Suffix Array
* Anagram Substring Search (Or Search for all permutations)
* Pattern Searching using a Trie of all Suffixes
* Aho-Corasick Algorithm for Pattern Searching
* kasai’s Algorithm for Construction of LCP array from Suffix Array
* Z algorithm (Linear time pattern searching Algorithm)
* Program to wish Women’s Day

## Backtracking
* Print all permutations of a given string
* The Knight’s tour problem
* Rat in a Maze
* N Queen Problem
* Subset Sum
* m Coloring Problem
* Hamiltonian Cycle
* Sudoku
* Tug of War
* Solving Cryptarithmetic Puzzles

## Divide and Conquer
* Write your own pow(x, n) to calculate x*n
* Median of two sorted arrays
* Count Inversions
* Closest Pair of Points
* Strassen’s Matrix Multiplication
* Quick Sort vs Merge Sort 

## Geometric
* Closest Pair of Points | O(nlogn) Implementation
* How to check if two given line segments intersect?
* How to check if a given point lies inside or outside a polygon?
* Convex Hull | Set 1 (Jarvis’s Algorithm or Wrapping)
* Convex Hull | Set 2 (Graham Scan)
* Given n line segments, find if any two segments intersect
* Check whether a given point lies inside a triangle or not
* How to check if given four points form a square

## Mathematical
* Write an Efficient Method to Check if a Number is Multiple of 3
* Efficient way to multiply with 7
* Write a C program to print all permutations of a given string
* Lucky Numbers
* Write a program to add two numbers in base 14
* Babylonian method for square root
* Multiply two integers without using multiplication, division and bitwise operators, and no loops
* Print all combinations of points that can compose a given number
* Write you own Power without using multiplication(*) and division(/) operators
* Program for Fibonacci numbers
* Average of a stream of numbers
* Count numbers that don’t contain 3
* MagicSquare
* Sieve of Eratosthenes
* Number which has the maximum number of distinct prime factors in the range M to N
* Find day of the week for a given date
* DFA based division
* Generate integer from 1 to 7 with equal probability
* Given a number, find the next smallest palindrome
* Make a fair coin from a biased coin
* Check divisibility by 7
* Find the largest multiple of 3
* Lexicographic rank of a string
* Print all permutations in sorted (lexicographic) order
* Shuffle a given array
* Space and time efficient Binomial Coefficient
* Reservoir Sampling
* Pascal’s Triangle
* Select a random number from stream, with O(1) space
* Find the largest multiple of 2, 3 and 5
* Efficient program to calculate e^x
* Measure one litre using two vessels and infinite water supply
* Efficient program to print all prime factors of a given number
* Print all possible combinations of r elements in a given array of size n
* Random number generator in arbitrary probability distribution fashion
* How to check if a given number is Fibonacci number?
* Russian Peasant Multiplication
* Count all possible groups of size 2 or 3 that have sum as multiple of 3
* Tower of Hanoi
* Horner’s Method for Polynomial Evaluation
* Count trailing zeroes in factorial of a number
* Program for nth Catalan Number
* Generate one of 3 numbers according to given probabilities
* Find Excel column name from a given column number
* Find next greater number with same set of digits
* Count Possible Decodings of a given Digit Sequence
* Calculate the angle between hour hand and minute hand
* Count number of binary strings without consecutive 1?s
* Find the smallest number whose digits multiply to a given number n
* Draw a circle without floating point arithmetic
* How to check if an instance of 8 puzzle is solvable?
* Birthday Paradox
* Multiply two polynomials
* Count Distinct Non-Negative Integer Pairs (x, y) that Satisfy the Inequality x*x + y*y < n
* Count ways to reach the n’th stair
* Replace all ‘0’ with ‘5’ in an input Integer
* Program to add two polynomials
* Print first k digits of 1/n where n is a positive integer
* Given a number as a string, find the number of contiguous subsequences which recursively add up to 9
* Program for Bisection Method
* Program for Method Of False Position
* Program for Newton Raphson Method

## Bit
* Find the element that appears once
* Detect opposite signs
* Set bits in all numbers from 1 to n
* Swap bits
* Add two numbers
* Smallest of three
* A Boolean Array Puzzle
* Set bits in an (big) array
* Next higher number with same number of set bits
* Optimization Technique (Modulus)
* Add 1 to a number
* Multiply with 3.5
* Turn off the rightmost set bit
* Check for Power of 4
* Absolute value (abs) without branching
* Modulus division by a power-of-2-number
* Minimum or Maximum of two integers
* Rotate bits
* Find the two non-repeating elements in an array
* Number Occurring Odd Number of Times
* Check for Integer Overflow
* Little and Big Endian
* Reverse Bits of a Number
* Count set bits in an integer
* Number of bits to be flipped to convert A to B
* Next Power of 2
* Check if a Number is Multiple of 3
* Find parity
* Multiply with 7
* Find whether a no is power of two
* Position of rightmost set bit
* Binary representation of a given number
* Swap all odd and even bits
* Find position of the only set bit
* Karatsuba algorithm for fast multiplication
* How to swap two numbers without using a temporary variable?
* Check if a number is multiple of 9 using bitwise operators
* Swap two nibbles in a byte
* How to turn off a particular bit in a number?
* Check if binary representation of a number is palindrome

## Graph
* **Introduction, DFS and BFS**:
  * Graph and its representations
  * Breadth First Traversal for a Graph
  * Depth First Traversal for a Graph
  * Applications of Depth First Search
  * Detect Cycle in a Directed Graph
  * Detect Cycle in a an Undirected Graph
  * Detect cycle in an undirected graph
  * Longest Path in a Directed Acyclic Graph
  * Topological Sorting
  * Check whether a given graph is Bipartite or not
  * Snake and Ladder Problem
  * Biconnected Components
  * Check if a given graph is tree or not

* **Minimum Spanning Tree**:
  * Prim’s Minimum Spanning Tree (MST))
  * Applications of Minimum Spanning Tree Problem
  * Prim’s MST for Adjacency List Representation
  * Kruskal’s Minimum Spanning Tree Algorithm
  * Boruvka’s algorithm for Minimum Spanning Tree

* **Shortest Paths**:
  * Dijkstra’s shortest path algorithm
  * Dijkstra’s Algorithm for Adjacency List Representation
  * Bellman–Ford Algorithm
  * Floyd Warshall Algorithm
  * Johnson’s algorithm for All-pairs shortest paths
  * Shortest Path in Directed Acyclic Graph
  * Some interesting shortest path questions
  * Shortest path with exactly k edges in a directed and weighted graph

* **Connectivity**:
  * Find if there is a path between two vertices in a directed graph
  * Connectivity in a directed graph
  * Articulation Points (or Cut Vertices) in a Graph
  * Biconnected graph
  * Bridges in a graph
  * Eulerian path and circuit
  * Fleury’s Algorithm for printing Eulerian Path or Circuit
  * Strongly Connected Components
  * Transitive closure of a graph
  * Find the number of islands
  * Count all possible walks from a source to a destination with exactly k edges
  * Euler Circuit in a Directed Graph
  * Biconnected Components
  * Tarjan’s Algorithm to find Strongly Connected Components

* **Hard Problems**:
  * Graph Coloring (Introduction and Applications)
  * Greedy Algorithm for Graph Coloring
  * Travelling Salesman Problem (Naive and Dynamic Programming)
  * Travelling Salesman Problem (Approximate using MST)
  * Hamiltonian Cycle
  * Vertex Cover Problem (Introduction and Approximate Algorithm)
  * K Centers Problem (Greedy Approximate Algorithm)

* **Maximum Flow**:
  * Ford-Fulkerson Algorithm for Maximum Flow Problem
  * Find maximum number of edge disjoint paths between two vertices
  * Find minimum s-t cut in a flow network
  * Maximum Bipartite Matching
  * Channel Assignment Problem

* **Misc**:
  * Find if the strings can be chained to form a circle
  * Given a sorted dictionary of an alien language, find order of characters
  * Karger’s algorithm for Minimum Cut
  * Karger’s algorithm for Minimum Cut | Set 2 (Analysis and Applications)
  * Hopcroft–Karp Algorithm for Maximum Matching | Set 1 (Introduction)
  * Hopcroft–Karp Algorithm for Maximum Matching | Set 2 (Implementation)
  * Length of shortest chain to reach a target word
  * Find same contacts in a list of contacts

## Randomized
* Linearity of Expectation
* Expected Number of Trials until Success
* Randomized Algorithms | Set 0 (Mathematical Background)
* Randomized Algorithms | Set 1 (Introduction and Analysis)
* Randomized Algorithms | Set 2 (Classification and Applications)
* Randomized Algorithms | Set 3 (1/2 Approximate Median)
* Karger’s algorithm for Minimum Cut
* K’th Smallest/Largest Element in Unsorted Array | Set 2 (Expected Linear Time)
* Reservoir Sampling
* Shuffle a given array
* Select a Random Node from a Singly Linked List

## Branch and Bound
* Branch and Bound | Set 1 (Introduction with 0/1 Knapsack)
* Branch and Bound | Set 2 (Implementation of 0/1 Knapsack)
* Branch and Bound | Set 3 (8 puzzle Problem)
* Branch And Bound | Set 4 (Job Assignment Problem)
* Branch and Bound | Set 5 (N Queen Problem)
* Branch And Bound | Set 6 (Traveling Salesman Problem)

## Misc
* Commonly Asked Algorithm Interview Questions | Set 1
* Given a matrix of ‘O’ and ‘X’, find the largest subsquare surrounded by ‘X’
* Nuts & Bolts Problem (Lock & Key problem)
* Flood fill Algorithm – how to implement fill() in paint?
* Given n appointments, find all conflicting appointments
* Check a given sentence for a given set of simple grammer rules
* Find Index of 0 to be replaced with 1 to get longest continuous sequence of 1s in a binary array
* How to check if two given sets are disjoint?
* Minimum Number of Platforms Required for a Railway/Bus Station
* Length of the largest subarray with contiguous elements | Set 1
* Length of the largest subarray with contiguous elements | Set 2
* Print all increasing sequences of length k from first n natural numbers
* Given two strings, find if first string is a subsequence of second
* Snake and Ladder Problem
* Write a function that returns 2 for input 1 and returns 1 for 2
* Connect n ropes with minimum cost
* Find the number of valid parentheses expressions of given length
* Longest Monotonically Increasing Subsequence Size (N log N): Simple implementation
* Generate all binary permutations such that there are more 1’s than 0’s at every point in all permutations
* Lexicographically minimum string rotation
* Construct an array from its pair-sum array
* Program to evaluate simple expressions
* Check if characters of a given string can be rearranged to form a palindrome
* Print all pairs of anagrams in a given array of strings
