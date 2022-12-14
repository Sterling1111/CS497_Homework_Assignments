# CS497 Homework 1
## Two Sum
The algorithm iterates through nums and checks for the appropriate complement in a hash map of previously
seen nums. If found the indices are returned otherwise the current element is added to the hashmap.
Iterating through nums is O(n) and inserting and searching a hash map is O(1). So the time complexity
of the algorithm is O(n). We need to store the elements of nums in a hash map so space complexity is O(n).

## Find First and Last Position of Element in Sorted Array
The algorithm performs two binary searches. One to find the minimum index
of the target value and one to find the maximum index of the target value.
The main distinction of these binary searches from a regular binary search
is that when the element is found the first check either the right of left
element to determine if the current element in max or min index. If not the
binary search continues to the left or right. Since binary search divides
the search space roughly in half on each iteration it is O(log n). The space
complexity is O(1) as constant space is used. 

## Median of Two Sorted Arrays
The algorithm partitions both of the arrays so that the sum of the 
number of elements on the left partitions are the same as the sum of the 
number of elements on the right partitions(roughly depending on even or odd).
The goal is to shift the partitions with the goal of maintaining this 
property while also gaining the property that the max elem in left partition
of array a <= the min element in the right part of array b and min element in
the right of array a >= the max element in the left of array b. If these two 
properties are true then we can immediately compute the median. The partitions
are adjusted by removing elements from the smaller array by comparing the max
element in the right party of array a to the minimum element in the right part 
of array b. Since the algorithm performs a binary search on the smaller array it is
O(log(min{m, n})) = O(log(m + n)). Space complexity is O(log(m + n)) as a recursive call is made
for each slicing of the search space in half. 

## Remove Nth Node From End of List
The algorithm computes the number of elements in the list by traversing to the
end. Then the nth node from the end can be deleted by traversing to just before the correct
element and setting its next pointer to next pointer of the element to be deleted. 
The list must be traversed and so time complexity is O(n). Space complexity is
O(1) since constant space is used. 

## Merge k Sorted Lists
The algorithm puts all iterates through all the lists and puts all of their
nodes into an array. Then the array is sorted and reconstructed in a linked list.
Time complexity to insert the list into a vector is O(n). C++ 11 and beyond guarantee 
O(n log n) time complexity for std::sort(). Time complexity to reconstruct the list
is O(n) and so overall time complexity is O(n). Space complexity to store the elements 
of all the lists is O(n). Sorting is not guaranteed space complexity, but it is probably 
not worse than O(n) and so overall space complexity is O(n). 

# CS497 Homework 2

## Majority Element
The algorithm puts all the elements of nums into an unordered map with the key as the
value and the value as the frequency of occurrence. Then return the value that occurs
most frequently. Insertion is O(1) and it occurs n times. Searching all elements for
the max is O(n) and so time complexity is O(n). Space is O(n) for the map of n elements. 

## Kth Largest Element in an Array
The algorithm puts all elements of nums into a priority queue with min element at top and
size of k. Then the top element is returned. It is O(log n) for inserting into a heap and 
insertion occurs O(n) times with a heap of size k. So time complexity is O(n log k). Space
complexity is O(k) for the priority queue. 

## Maximum gap
The algorithm computes the minimum possible max gap and then puts all elements into buckets such
that none of the elements in the same bucket are farther away than the min possible max gap. So if
the answer is larget than that it must occur between the max and min of adjacent non-empty buckets.
There are n -1 buckets so space complexity is O(n). Time complexity is O(n) for placing n elements
into buckets and for iterating through the buckets. 

## Remove Duplicate Letters
The algorithm finds the left-most element that cannot be deleted either because it is the only
of its kind remaining or it is less than all the other elements in the string. Then it removes
all elements to the left of it and all of its kind to the right. Then it calls itself on the right 
remaining part of the string. There are max of 26 function calls, and they do n work and allocate n 
memory each time so the time complexity is O(n) and the space complexity is O(n).

## Shortest Sub-Array with Sum at Least K
The algorithm uses the sliding window technique except we need to make sure that eliminating 
previous elements always results in a decrease. So we use a deque where each element is a region
in the array where there is increase. If we encounter a negative element we remove elements from
the deque from the end until we pay off the debt. Then the sliding window technique will work. The time
is O(n) as we iterate through the elements once and only put 1 element in the deque and if the inner
loops ever run they remove one element. The space complexity is O(n) for the dequeue. 

# CS497 Homework 3

## Convert Sorted List to Binary Search Tree
The algorithm first converts the linked list to a vector. Then calls a function which
recursively calculates the mid-element of a given subsequence of the array. Everything
to the left of mid will be less than mid and everything to the right of mid with be greater than mid. 
Create a new node with the mid-element as the value and set the left and right pointers to the recursive
call of the function with appropriately adjusted start and end pointers. Then return the node. The function
returns nullptr if start is greater than end. The tree will be balanced because we divide each subsequence
roughly in half(never differing by more than 1 element) each time so each node will be balanced. Time 
complexity to convert list to array is O(n). There is constant work done in each recursive call and there is
one invocation of recursive function for each node with n nodes so O(n). So overall time complexity is O(n). 
Space complexity is O(n) for storing linked list in array with constant space and O(log n) recursive stack height(balanced).
So overall space complexity is O(n).

## Construct Binary Tree from Preorder and Inorder Traversal 
First all elements are inserted into an unordered map with key as value and value as index.
Then we call a recursive function that takes the preorder vector with an index, and start and 
end pointers for a subsequence of the inorder array. If start is greater than end we return nullptr.
Then we get the node we will create from the preorder array from left to right with index. We need
to then establish the correct left and right pointers for this node. Since inorder traversal results
in left elements - root - right elements. we know that left of this node will be from start to
root index - 1. We get this index from the unordered map of value. We know that the right of this
node will be elements from root index + 1 to end with the first index gotten in the same way. Then we 
return root. Time complexity is O(n) for putting all elements in the map. There will be about n recursive
calls for the n nodes and each call does constant work since hashmap lookup is O(1). So overall time
complexity will be O(n). Space complexity is O(n) for hashmap creation and O(n) for max recursive depth as
the tree may be ordered. So overall space complexity is O(n).

## Binary Tree Maximum Path Sum 
The problem is very simple if you think about the details. From a high level you can include
some parent node with some path of left and right children and nothing above, or you can include 
the parent node with either the left child or right child with some other path above the root node. 
For the details set a global variable maxSum as smallest possible integer. Call recursive function
maxPathSumRec with root. If nullptr return 0 as nothing can be added. Then calculate the max you could
get with some path from the left and max you could get with some path on the right. If they are less
than 0 then make them 0 to say that we won't take them. Now suppose we will take this node + some path
left and right. Then we could not proceed up, so we see if this is larger than maxSum so far. Now if
we would proceed we would take the current node and the largest of left and right. There is constant
work in each recursive iteration and the recursive stack is O(n) deep so time complexity is O(n). 
Similar analysis gives O(n) space complexity. 

## Find largest value in each Tree row
Simply put the root into a queue. Then keep track of the current size of the queue. As you
pop elements up to that size compare for the max element and push new elements into the back
of the queue if they are non-null. At the end of each inner iteration push the max of that
level into the result vector. Time complexity is O(n) for constant time work to process n elements
of the tree. The maximum number of elements in a full tree at the last row is n/2 so space complexity
is O(n).

## Balance a Binary Search Tree 
The algorithm first inserts the elements of the tree into a vector with an inorder traversal.
This will result in a vector that is sorted in ascending order. Then simply construct the tree in
the same manner as in [Convert Sorted List to Binary Search Tree](#convert-sorted-list-to-binary-search-tree).
Time complexity is O(n) for inorder traversal and O(n) to construct the tree. So overall is O(n).
Space complexity is O(n) for the construction of the vector and O(log n) for the max recursion depth(balanced tree).
So overall is O(n).

# CS497 Homework 4

## Top K Frequent Elements
The algorithm puts all elements in an unordered map with the element
as the key and frequency as the value. Then the elements of the
map are inserted into a min heap with the sorting criteria as the
frequency. They are only inserted if there is less than k elements in
the heap or if the top element which is the min is smaller than the
element at hand. Then all the elements of the heap are added to the vector
and returned. Time complexity is O(n log k) and space complexity is O(n).

## Find K Closest Elements
The algorithm first finds the lower bound of where x could be inserted
without changing the order of the vector. If the lower bound is the start
of the array then return the first k elements. If it is the end then return
the end then return the last k elements. Otherwise, start adjusting left and
right iterators comparing the value of the iterators each time to see which
one to adjust until one of them goes of the cliff, or we have k elements. Then
return the appropriate elements according to the left and right iterators. The
time complexity is O((log n) + k). Space complexity is O(k).

## K Largest Elements of a Max Heap
The performs k iteration of insertion and removal from a priority queue. Each element 
in the queue will contain an index and a value at that index. Start 
with the first element on the heap which will always be the largest. Now
remove the top of the queue which is the largest and push the children of
the largest onto the queue. Then add the element just popped to the result. 
Every iteration adds 2 to the queue and removes 1 so 1 is added k iterations for a space
complexity of O(k). Since there are a max of k elements in the queue the time 
complexity is O(k log k).

## [Shortest Subarray with Sum at least K ](#shortest-sub-array-with-sum-at-least-k)

## Kth Smallest Prime Fraction
The algorithm uses a struct which contains the decimal value of the fraction and the 
index in the vector for the numerator and denominator. Fill the priority queue with the smallest
possible fraction for each given numerator. Then for k elements remove the smallest fraction
and push onto the queue the next smallest fraction for that given numerator. The last one
to be popped will be the kth smallest. Time complexity will be O(max(n, k) log n). Space complexity
will be O(n) for the queue. 

# CS497 Homework 5

## Remove Invalid Parenthesis 
The algorithm at each recursion considers the scenario to keep the given char or to
remove the given char. When it gets to the end if the parentheses are valid then they are
compared for size with what is already accepted. If they are larger, then remove everything
else and accept them. Time complexity is O(2^n) as there is a choice for each element whether
to keep it or not. Space complexity is O(n) as the stack is as deep as the number of chars in 
the string.

## Minimum Absolute Difference in BST
The algorithm first inserts all elements into a vector using inorder traversal. 
This provides a sorted order for BST. Next scan through the sorted array and compare
all adjacent elements for the minimum elements. Both operations are O(n) and so overall 
time complexity is O(n). Space complexity is O(n) for the vector.

## Shortest Path Visiting all Nodes
The algorithm performs bfs on all the states where the state is a combination of the node
we are on and the nodes that have been visited. When we reach a state such that all of
the nodes have been visited then we know that we have found the shortest path. There are 2^n
possible masks and n nodes so the total states is n * 2^n. Also in each iteration we loop
through n nodes and so the time complexity is O(2^n * n^2) which is really really bad. Space
complexity is O(2^n * n) because we push onto the queue the same elements we search.

## [Binary Tree Maximum Path Sum](#Binary-Tree-Maximum-Path-Sum).

## Lexicographical Numbers
The algorithm performs a dfs starting with 1. It returns if the number it is
trying to add is greater than n or if it has added n numbers to the array. Time complexity
is O(n) because it adds one operation per stack call and adds n numbers. Space complexity
is O(n) for the same reason.

# CS497 Homework 6

## Find if Path Exists in Graph
The algorithm uses the edges to construct a graph. Then it runs dfs on the graph starting
from the source and if it ever finds the destination it returns true else false. The time 
complexity is O(v + E) for dfs. Space complexity is O(V + E) for the vector of vertices and
the stack depth for dfs edge traversals.

## Longest Cycle in a Graph
The algorithm runs through the nodes according to the connections given and stops
when it encounters a dead end(-1) or until it reaches a node whose source node is
the same as the source node of the given node. Then it subtracts from the total
distance the distance it took to get there the first time. If this is larger than
the current result then it becomes the new result. This occurs until there are no more
nodes to process. Time complexity is O(n) for the outer loop. There is an innter loop
which processes nodes but once processed they can be skipped in the future so O(n). Space
complexity is O(n) for the vector which contains source node and distance from source node.

## Connecting Cities with minimum Cost
The algorithm uses Kruskals MST algorithm implemented with union find. The time complexity
is O(m log m) for sorting the edges. Kruskals runs as (m log n) so overall time complexity is
O(m log m + m log n). Space complexity is O(n) for the parent vector.

# CS497 Homework 7

## Course Schedule
The algorithm builds a graph where a -> b means that you must take a in order to take b.
Once the graph is built run Kahn's algorithm to build a topological ordering of the graph.
each time the q is popped increment the count of the courses that can be taken. If the number
of courses that can be taken is equal to the number of courses that need to be taken then return 
true else return false. The space complexity of Kahn's is O(V + E) and the time complexity is the same.

## Network Delay Time
The algorithm that is run is Djkstras algorithm to determine the shortest
amount of time for each node to receive the signal. We first build the
graph and then run the algorithm. The time complexities of Djakstras with
this implementation are O(V + E log V). The space complexities is given as
O(V + E).

## Optimize water distribution in a village
The algorithm constructs a new graph with an added well node. This node is connected to each other node
with the cost of the connection as the cost of the well for that node. Then Kruskal's is run on that graph. 
The time complexity of my implementation of Kruskals is O(V log V + E * log V). Space complexity is O(V) for the parent vector.

# CS497 Homework 8

## Course Schedule 2
The algorithm builds a graph and runs Kahns algorithm to build a topological ordering of
the graph. If the topological ordering contains all the nodes then the vector is returned. 
Otherwise, the empty vector is returned. The time complexity for Khans is given as O(V + E). The
space complexity is the same.

## Divide Two Integers
The algorithm relies on the fact that ln(x/y) = ln(x) - ln(y). Since we want x/y then we use
exp to get x / y. we add a little to it because if they numbers divide evenly then it will be
a little small for instance 3 = 2.99999, so we need to correct for that. Space complexity is O(1) and
time complexity is O(O(exp) + O(log)).

## Coin Change
The algorithm uses bottom up dynamic programming to compute the solution. That is to say it
computes the min for 0 then 1 then 2... up to amount. The time complexity is O(amount * coins.size()).
The space complexity is O(amount).

# CS497 Homework 9

## Longest Valid Parenthesis
The algorithm builds up the solution from the bottom up with dynamic programming. The idea is to keep
a cache that is the largest subsequence of elements that ends in position i. It will be initialized to
0 at first. If we encounter a ')' then we compute the result based off the cache. It it is '(' then it 
could not be the end so cache will remain 0. The time complexity is O(n) and the space complexity is O(n)
for the cache. 

## Maximum Subarray
The algorithm keeps track of the sum of the current subarray and a running sum
which is the max of all subarrays seen so far. On each iteration of the loop it
adds the next element to the subarray and keeps the larger of the sum and the elem.
Then it compares that max to the running max and takes the larger. At the end it
returns the max. The time complexity is O(n) and space is O(1).

## Unique Paths
The algorithm uses dp to build the solution. There is only 1 path
to get to the end of the first row and end of first column. For the middle section it
is the number of paths from above + the number of paths from the left. The time complexity
is O(n * m) and the space complexity is O(n * m).

## Unique Paths 2
The algorithm is similar to the unique path solution. First we need to set the values for the
first row and first column. They are all 1 until we encounter a 1 and then the rest after that will
be 0 as they can never be reached. Then we proceed with the dp as before except if we encounter a 1
then we set dp at the index to 0 as it can never be reached. The time complexity is O(n * m) and the
space complexity is O(n * m).