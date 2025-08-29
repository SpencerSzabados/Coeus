A heap is a particular kind of [[Binary trees|tree data structure]] that, at every instant, obeys the _heap condition_ (for max sorted heap):
  1) The value of each node is greater than of equal to the values stored in each of its children;
  2) The tree is perfectly balanced, and the leaves in the last level are all in the leftmost position; i.e., values are populated from left to right and maintained in this way.
This property ensure that the largest elements are near the root of the tree, and the number of high of the tree is always maintained at $O(\log n)$;. however, element in the heap are not perfectly ordered. 

Heaps typically support $Insert$, $Delete$, $Peek$, $Extract-max$, $Increase-key$, $Heapify$, and $Merge$, methods; the second last of which is responsible for restructuring the tree to satisfy the heap conditions after a series of operations are performed that may lead to its violation. 


# Binary heap
Binary heaps are the most common type of heap data structure, where every node has at most two children.

Heaps are commonly implemented using an array $A[0,1,\dots,m-1]$. Using binary indexing (the indexing used in binary trees for storing them in arrays with $left(i)=2*i+1$ and $right(i)=2*i+2$) the heap condition can be written as: 
  1) $A[i]\geq A[2*i+1], \text{ for }0\leq i\leq (m-1)/2$, and 
  2) $A[i]\geq A[2*i+2]\text{ for }0\leq i\leq (n-2)/2$.

A function $Heapify(A,i)$ takes as inputs the heap array $A$ and an index $i$ in the array; that when called assumes the binary trees rooted at $left(i)$ and $right(i)$ are valid heaps, but $A[i]$ might be smaller than its children (invalid heap), and is responsible for rebalancing the heap starting from $i$.
```pseudocode
Heapify(A,i)
    l = left(i)
    r = right(i)
    if l<=A.heap-size && A[l]>A[i]
        largest = l
    else
        largest = i
    if r<=A.heap-size && A[r]>A[largest]
        largest = r
    if largest != i
        swap(A[i], A[largest])
        Heapify(A, largest)   //recurse up or down the heap
```

Insertions are performed by $insert$-ing a new node at the leftmost valid leaf position and calling $Heapify$ on the parent node, which will reorder the tree accordingly.

A congruent array $A$ of unordered values can be converted to a heap by calling $Heapify$ in a bottom up manner:
```pseudocode
Build-Heap(A)
    A.heap-size = A.length
    for i=floor(A.length/2) to 1
        Heapify(A,i)
```
which takes $O(n)$ time to build the heap.

Elements are $deleted$ from the heap by first searching the heap for the element to be deleted - it takes $O(n)$ time to search for an arbitrary element in a heap - if we are deleting the maximum element this step takes $O(1)$ time. Next, the node to be deleted is swapped with the last node in the heap and marked as deleted. Lastly, $Heapify$ is called on the newly swapped node.
```pseusdocode
Delete(A,key)
    i = search(A,key)            //get index of key in A
    swap(A[i],A[A.heap-size-1]) 
    A.heap-size = A.heap-size-1  //remove key element from heap
    Heapify(A,i)                 //restore heap condition
```


## Limitations and performance 
As a binary heap is a completed binary tree, for $n$ does the heap will have height $O(\log n)$. Consequently, are most operations are dependent on the height of the tree, the heap property can be maintained in $O(\log n)$ time. In the worst case:
  + $Insert$ takes $O(\log n)$ time;
  + $Delete$ takes $O(\log n)$ time;
  + $Peek$ takes $O(1)$ time;
  + $Extract-max$ takes $O(1)$ time, but the heap would be left in a invalid state and must be rebalanced using $Heapify$ afterwards which takes $O(\log n)$ time;
  + $Increase-key$ takes $O(\log n)$ time, as it must traverse at most $O(\log n)$ branches while searching for the node;
  + $Merge$ takes $O(n\log n)$ time to merge two binary heaps of $O(n)$ size.


# Fibonacci heap


# Brodal queue
[Wiki](https://en.wikipedia.org/wiki/Brodal_queue), [Stackoverflow](https://stackoverflow.com/questions/30782636/are-fibonacci-heaps-or-brodal-queues-used-in-practice-anywhere)
