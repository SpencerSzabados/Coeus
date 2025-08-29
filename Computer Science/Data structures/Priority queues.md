A priority queue is a data structure that maintains a set $S$ of elements, each of which is associated with a $key$ value (or priority), in order of their priority and extracts the most important elements first. [[Heaps]] (and [[Hashtables|hashtable]] data structures using chaining, if the key values are finite with a limited range) are commonly used as a data structure for implementing a priority queue.

Priority queues support the following operations: 
  + $Insert(S,x)$ used to insert element $x$ with associated key value $x.key$ into the queue;
  + $Extract-Max(S)$ returns the element in the queue with the highest key value (or lowest);
  + $Increase-key(S,x,k)$ increases the key value of $x$ within the heap to $k$.