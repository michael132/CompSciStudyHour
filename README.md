## Overview
The point of this repository is to outline and store common data structures and sorting algorithms.
Of course these are readily available for anyone to use, though these are very basic implementations
written in python. These are solely for educational purposes. 

## Datastructures

#### Average Scenario
| Data Structure | Access | Search | Insertion | Deletion | 
| ---: | :---: | :---: | :---: | :---: |
| [Array](#array) | `O(1)` | `O(n)` | `O(n)` | `O(n)` | 
| [Linked List](#llist) | `O(n)` | `O(n)` | `O(1)` | `O(1)` |
| [BST](#bst) | `O(log(n))` | `O(log(n))` | `O(log(n))` | `O(log(n))` |
| [Heap](#heap) | `O(log n)` | `O(n)` | `O(1)` | `O(log n)` |
| [Hash Table](#hash) | `N/A` | `O(1)` | `O(1)` | `O(1)` |
| [Stack](#stack) | `O(1)` | `O(n)` | `O(1)` | `O(1)` |
| [Queue](#queue) | `O(n)` | `O(n)` | `O(1)` | `O(1)` |
| [Trie](#trie) | `O(m)` | `O(m)` | `O(m)` | `O(n+m)` |

#### Worst Case Scenario
| Data Structure | Access | Search | Insertion | Deletion | Space |
| ---: | :---: | :---: | :---: | :---: | :---: |
| [Array](#array) | `O(1)` | `O(n)` | `O(n)` | `O(n)` | `O(n)` |
| [Linked List](#llist) | `O(n)` | `O(n)` | `O(1)` | `O(1)` | `O(n)` |
| [BST](#bst) | `O(n)` | `O(n)` | `O(n)` | `O(n)` | `O(n)` |
| [Heap](#heap) | `O(log n)` | `O(n)` | `O(1)` | `O(log n)` | `O(n)` |
| [Hash Table](#hash) | `N/A` | `O(n)` | `O(n)` | `O(n)` | `O(n)` |
| [Stack](#stack) | `O(1)` | `O(n)` | `O(1)` | `O(1)` | `O(n)` |
| [Queue](#queue) | `O(n)` | `O(n)` | `O(1)` | `O(1)` | `O(n)` |
| [Trie](#trie) | `O(m)` | `O(m)` | `O(n*m)` | `O(m)` | `O(n+m)` |

**[Graph](#graph)**

___from [wikipedia](https://en.wikipedia.org/wiki/Graph_(abstract_data_type))___

|    | Adjacency List | Adjency Matrix | Incidence Matrix |
|:---|    :---:       |    :---:       |     :---:        |
| Store Graph  | `O(V + E)` | O(V<sup>2</sup>) | `O(V * E)` |
| Add Vertex  | `O(1)` | O(V<sup>2</sup>) | `O(V * E)` |
| Add Edge  | `O(1)` | `O(1)` | `O(V * E)` |
| Remove Vertex | `O(E)` | O(V<sup>2</sup>) | `O(V * E)` |
| Remove Vertex | `O(E)` | `O(1)` | `O(V * E)` |
| Query neighbors | `O(V)` | `O(1)` | `O(E)` |
| Remarks | Slow to remove vertices and edges, because it needs to find all vertices or edges | slow to add or remove vertices, because matrix must be resized/copied | slow to add or remove vertices and edges, because matrix must be resized/copied |


**<a name="array"></a>Array**

An array is a contiguous block of memory that has been allocated to store a specific type of data. Arrays
are allocated statically in languages like C/C++; however, resizing an array can be costly as a temporary
array must be constructed to hold the values while the initial array is resized and reassigned.  

**<a name="list"></a>Linked Lists**

Similar to arrays LinkedLists store data in a contiguous manner; however, the memory is not allocated contiguously
and the LinkedList stores a pointer to the next node.  The benefit is the reduced cost of resizing (as you 
no longer have to do this); however, lookups are `O(n)` and no longer in constant time. Insertions to the end
of a linked list are `O(n)` unless bookkeeping is done to keep track of the tail.  Otherwise insertions must
be done at the root or head of the list to keep time constant. 

DoublyLinked lists are similar to a Linked List as described above; however, each  node contains a pointer to
the previous node.  This makes insertion at either end of the list a constant time of `O(1)`

**<a name="bst"></a>Binary Tree / BST**

A BST is a type of Binary Tree in which the nodes are arranged in a specific order to enable searching of the tree. 
Each node/subnode on the left of the tree is less than the nodes of the right branch of the sub stree.  
 
similar to a heap that is Min-Down. 

A Binary tree is a tree structure in which each node may contain only two leafs, or 0 and 1 respectively.
Binary Trees can be utilized to create huffman coding tables to greatly reduce the amount of space required
to store arbitrary amounts of text.

**<a name="heap"></a>Heap**

A heap is a specialized tree-based data structure that satisfies the heap constraint which states. 

> If A is a parent node of B then A is ordered with respect to B

In terms of heaps we typically have MinHeaps and MaxHeaps, wherein the data is ordered with respect to whether
or not the parent node is a smaller or larger. 

To `heapify` a list such as [3, 2, 1, 5, 7, 9] into a max heap we would have `log n` number of operations
utilizing a sift up strategy.  

Quickly, sifting up vs. sifting down, sifting up places a newly inserted node at the bottom level of the tree
then comparing the node to its parents node, determines if the node should be "sifted up." average time is `O(1)` 
meaning that hte node does not require to be sifted.  Worst case is `O(log n)` in which we must check each branch 
as we work our way up the tree, sifting the node up one level. 

Sifting down is a slightly more costly endeavor having to a complexity of `O(n log n)` in the worst case, being that 
there are more nodes to possibly check as we sift down a tree.  


The operations to build our heap:

```
11, 2, 1, 5,10, 7, 9
pop()

11, 2, 1, 5,10, 7

                      9
                      
pop()
11, 2, 1, 5,10,

                      9
                     /
                    7
pop()
11, 2, 1, 5,
                     9
                    / \
                   7   10 - sift up
                 
                 
                     10
                    /  \
                   7    9
pop()
11, 2, 1,                   

                     10
                    /  \
                   7    9
                  /
                 5
pop()
11, 2,                   

                      10
                    /    \
                   7      9
                  / \
                 5   1
pop()
11,

                      10
                    /    \
                   7      9
                  / \    /
                 5   1  2
                 
pop()

                      10
                    /    \
                   7      9
                  / \    / \
                 5   1  2   11 -- sift up
                  
                      10
                    /    \
                   7      11 -- sift up
                  / \    / \
                 5   1  2   9

                      11 -- New root
                    /    \
                   7      10 
                  / \    / \
                 5   1  2   9 
```

**<a name="hash"></a>Hash Table**

Hash table, as the name implies, is a table of hashes that uniquely identify a value.  Given a key a particular
hash is stored into the pre-allocated table at a provided index.  

Hash tables provide constant time lookups and storage in the average case `O(1)`. With a worst case complexity 
of `O(n)` when multiple keys collide and linear probing must be performed. 

```
'a' -> hash('a') -> 2 ---          [0]
                        |          [1]
                        ----->     [2] -> stores the value for the provided key 'a'
                                   [3]
                                   [n]... 
```

When there is a collision, as was stated earlier, linear probing must be performed.  Linear probing proceeds 
through the allocated table checking for the next empty cell, this is where the worst case scenario of `O(n)`
comes into play.  Due to the fact that the table is pre-allocated, it is especially costly when the number of elements
stored into the table exceeds the table size, as the table must be re-sized and all keys re-hashed into the table. 

```
'c' -> hash('c') -> 2 ---          [0]
                    |   |          [1]
      collision-----    |          [2] -> stores the value for the provided key 'a'
                        |----->    [3] -> linear probing stores the key/value into the third slot instead
                                   [n]... 
```

**<a name="stack"></a>Stack**

A stack, as the name implies, is a "stack" of data with a Last In First Out policy.  Stacks are the backbone of DFS
algorithms.  Values are placed onto the top of the stack and removed from the bottom as the data is processed.

**<a name="queue"></a>Queue**

Analogous to a stack, data is placed into a queue and removed single file; however, queues use the First In First Out `FIFO`
methodology.  Queues work great with a BFS strategy given the nature of how they store and retrieve data. 

**<a name="trie"></a>Trie**

A trie is a tree like data structure, in which the leafs for a given node fan out wide. 
This creates short trees that are very wide. Tries are great data structures for performance
driven applications wherein you need to lookup data from a given set, this is due to the fact
that the complexity for searching is related directly to the number of characters in the word
being looked up. The worst case for insertion is n*m*c or `nodes * keySize * characterSetSize`  

A depth-first strategy is implemented to locate lookup suffixes or entire keys. 

Consider the following keys 

```['a', 'abc', 'abd', 'x', 'xy', 'xyz', 'bag',]```

In a Trie data structure we would have the following structure

```
'*' denotes a key

                   _
                /  |  \
               a*  b   x*
              /    |    \
             b     a     y*
            /  \   |      \
           c*   d* g*       z*
```

A DFS strategy would locate the given search term 'abd' in 3 recursions `A* -> B* -> D*`.

Where as a BFS strategy would find key 'abd' in 8 recursions `A* -> B -> X -> B* -> A -> Y -> C -> D*`

**<a name="graph"></a>Graph**

A graph data structure is similar to a tree or cluster of tress, a graph is represented by edges connected vertices, though 
not all vertices are connected by edges. 

A `directed` graph is simply a graph whose vertices may only be traversed in a single direction or bi-directionally, whereas an undirected graph
does not make this distinction and edges may be traversed in any direction.  

One use for a graph is to represent a site navigation layout.  With each node representing a page and the edge representing the flow
of traffic between each page.  In terms of a single-page application a directed graph can help identify workflows on the site in which
backwards navigation may not be possible (e.g. a workflow which includes actions which cannot be reversed until the entire workflow has
taken place).  

A simple data structure to represent a graph is called an adjacency list it is represented as such

```
A -> B
A -> C
B -> D
E -> G
```

This would generate the following adjacency list
```
A -> {B, C}
B -> {A, D}
C -> {B}
E -> {G}
```

This translates to the following graph

```
     A ---- B---- D
     |     /
     |   /
     | / 
     C     E ---- G
```

A DFS search can be utilized to search the graph to determine the shortest paths between any two nodes. 
Additionally the diameter of a graph is determined the distance of the two furthest nodes of the graph. 

## Sorting
These are just a few of many sorting algorithms - below you will find the algo and the space
and time complexity as well as the average case and worst case scenario run complexities

| Algo             | Time Complexity | Time Complexity | Space Complexity |
| ---: | :---:           | :---:           | :---:            |
|                  | **Average**     | **Worst**       | **Worst**        |
| [Radix](#radix)  | `O(nk)`       |`O(nk)`          |`O(n+k)`|
| [Bucket](#bucket) | `O(nk)`       |`O(nk)`          |`O(n+k)`|
| [Quick](#quick)  | `O(n log(n))` |`O(n^2)`         |`O(log(n))`|
| [Bubble](#bubble) | `O(n^2)`      |`O(n^2)`         |`O(1)`|
| [Merge](#merge)  | `O(n log(n))` |`O(n log(n))`    |`O(n)`|


**<a name="radix"></a>Radix Sort**

As the name implies, the Radix sort is a sorting algorithm that works with integers of a given base. 
Given that the sort only works against integer values it is incredibly fast at sorting numbers with 
an upper and lower bounds complexity time of `O(nk)` where `n` is the number of items to sort and `k`
is passes required for the most significant digit. 

Similar to how a bucket sort works, the radix sort uses buckets (queues) to process each individual 
digit from 0..n where `n` is the base of the number being processed.  Each pass enqueus the numbers 
into their respective bucket, with `k` number of passes required to completely sort the set.

**<a name="bucket"></a>Bucket Sort**

Similar to the radix sort a bucket sort uses "buckets" to divide the data into smaller and smaller
groupings of data that can be sorted.  The partition, or pivot, is determined by the data and used
to place all values greater than or less than the pivot into individualized buckets.  Each bucket
may then be sorted by calling whatever sort routine is desired, or even calling the bucket sort again.
This behavior would be considered analgous to calling a quick sort; however, the pivot point may not
be desirable given the data causing a worst case sorting of `O(n^2)` time. 

**<a name="quick"></a>Quick Sort**

A powerful sorting algorithm that pivots the data based on a random pivot point or median, placing all
values greater than the pivot point into one bucket, and those that are less than or equal to the pivot
into another (though for values equal this distinction does not matter). 

Quick sort works considerably slower against data sets with many duplicate values, as the pivot point
does not account for duplicates.  Duplicate values may found themselves sorted against repeatedly (`O(n^2)`).
To compensate for this one may use a "fat" or "wide" partition/pivot in which all values of a given pivot
are stored and only those of lesser or greater stored into separate buckets. This solves the 'Dutch Flag Problem'

**<a name="bubble"></a>Bubble Sort**

The bubble sort is the simplest of all sorting mechanisms on the list.  Checking each value with its neighbor, large
values are quickly bubbled to the top of the list while smaller values are shifted to the rear of the list. However, 
using this means to sort in the worst case carries an n<sup>2</sup> time complexity. For a list is completely reversed 
it will take a factor of two to the number of elements in passes to completely sort.  It is a simple algo though... 

**<a name="merge"></a>Merge Sort**

Utilizing the divide and conquer methodology, the Merge Sort divides the list in half and continuousely breaks the list
down bit by bit until the items are split into individual buckets. While the list is being split, each sublist is being 
sorted via a merge function. maintaining a `O(n log n)` time.  Merge sorts are considered a great general purpose sorting
algorithm, working especially well with linked lists. 

## Searching

**Depth-First-Search DFS**

Depth first searches are a means for searching graphs / matrices / trees by means of searching all 
connected vertices downwards and traversing back up before moving to a neighbor node. Typically
starting at the root; however, it can be done from any particular node (search node). 

```
     A
   B   C
 D    E  F
 
A DFS Search would return A, B, D, C, E, F
```

Particularly a DFS does its work with a `stack`, as you would grab the root A, and push the child
nodes onto the stack. then recursively call the work on B (LIFO - last in first out) and traverse 
down the tree until all nodes had traversed before returning to C and continuing so and so forth. 



**Breadth-First-Search BFS**

Conversely the Breadth first searches all neighbor nodes (starting from the root node or a provided
search node) across a tree before traversing down a level.
  
```
     A
   B   C
 D    E  F
 
A DFS Search would return A, B, C, D, E, F
```

A BFS performs its work with a `queue` wherein the data is processed FIFO (first in first out). 
Wherein we push the children nodes of A into the queue and process them before continuing to 
any subsequent children found. 

**DFS vs. BFS**

Using one vs the other depends greatly on the structure of the data stored in the tree or graph. 


Typically DFS is favored against shorter wider trees, where BFS is favored against taller narrower
trees.  Additionally if memory is a concern the DFS search does not require a separate data structure
to store the visited nodes when written recursively. 

Consider a family tree, where we want to search for relatives - living relatives would be located
near the bottom of the tree and located by a DFS much faster.  Whereas relatives long since passed
would be located much higher in the tree and found with a BFS much faster.

The point being, that it depends on the structure of the data and what you are searching for and 
its place to be found within the tree. 


## Algorithms in General

**Divide and Conquer**

Divide and conquer is the idea of splitting a problem into two or more sub problems via recursion and continuing to  do
so until the problem is simple enough to solve.  The sub-solutions are then recombined to create a solution that answers
the entire question.  

For example, the Merge Sort algorithm utilized the divide and conquer methodology, of continuously breaking down the subset
of data until it has been completely reduced to 1 or two elements being compared.  Each sub set is then sorted and merged together
and via the magic of recursion each walk up the stack handles merging a slightly smaller and smaller set of the data until
everything is sorted and merged at the end.  

It is notable that most Divide & Conquer algorithms are written recursively, which may raise concern for memory or stack
allocation causing stack overflows. 

**Tortoise and Hare**

Imagine you have a linked list, you are unaware of whether or not it is a circularly linked list or a 
singly linked list with a null pointer at the end. 

```a -> b -> c -> NULL```

vs.

```
    a -> b -> c --
    ^            |
     \___________|
     
    a -> b -> c --
         ^       |
          \______|
     
```

In the above example we could simply traverse the list and determine if the first one is acyclic; 
however either of the last two examples we would never find the end as it is cyclic (or circular)

One option is to create a copy of the list so we can keep track of the visited nodes; however,
this requires as much memory as it has taken to allocate the original list. 

Thus we come to the Tortoise and Hare algorithm.  What if instead we used two pointers to keep track
of our progress through the list.  One pointer moving at a rate of `n` and another point moving at `n+2`.  
This tracking is analogous with two joggers running on a track, one running a fixed paced faster 
than the other. Eventually our faster paced jogger will lap the slower jogger.   

By moving one pointer `n` elements at a time and another at `n+2` elements at a time we will eventually come
to a point in time in which the two pointers are equal OR the the faster of the two pointers will find a NULL
node first.

Thus we can determine whether or not a list is cyclic or acyclic. 
