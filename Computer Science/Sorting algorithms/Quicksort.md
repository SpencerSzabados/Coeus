---
doc type: Note
authors: Spencer Szabados
date: 
tags:
  - sorting
  - algorithms
  - random_algorithms
references:
  - "[[@Cormen_2009]]"
---
---
# Quickselect
Quickselect can be thought of a variation of quicksort that allows for the selection of the $i$-th smallest element from an unsorted array $A[0,1,\dots,n-1]$ (containing distinct elements) in $\Theta(n)$ expected time. [Wiki](https://en.wikipedia.org/wiki/Quickselect).

**Algorithm: (Quickselect)** Quickselect progressively partitions the array $A$ and discards all but one side in which the sought element lies.

```pseudocode
QuickSelect(A,l,r,i)    
    if l == r               //Base case
        return A[l]
        
    p = Random-Pivot(A,l,r) //Generate random pivot for partition 
    A = Partition(A,p)      //Partition A around p such that
                            //  all elements in A[l  ,...,m] <= p, and 
                            //  all elements in A[m+1,...,r] >= p
    k = m-l+1               //Number of elements in A[l,...,m]
    
    if i == k               //Inductive cases 
        return A[m]
    else if i < k
        return QuickSelect(A,l,m-1,i)
    else
        return QuickSelect(A,m+1,r,i-k)
```


In the worst case this algorithm runs in $\Theta(n^2)$ time, even to find the minimum. The expected running time for this algorithm is $\Theta(n)$.


## Application: selection in worst case linear time
The worst case bound on the performance of the given algorithm results from selecting bad pivots at each partition step; hence, to improve the worst case performance we need a better method of selecting the pivot. In particular, if we can ensure the selected pivot divides $A$ into two portions with a constant fraction (nonzero and not one) between their lengths, then we can achieve a worst case time bound of $\Theta(n)$. Median of medians selection is what is typically used.

The algorithm works by first dividing $A$, which we assume to contain $n$ elements, into $\lfloor n/5\rfloor$ subarrays of $5$ elements each and at most one group made up of the remaining $n \text{ mod } 5$ elements. The median of each of the groups is calculated by insertion-sorting the subarrays; the median of these medians is then selected as a pivot, call this median $med$. The subarrays are then reordered around $med$, so that subarrays with medians larger than $med$ are to the right and those with medians smaller than $med$ are to the left. Afterwards select the $k$ elements on the low side that are less than $med$; this can be done using the medians of the sorted groups. Now, If $i =k$ return $med$; otherwise, recurse on the low side if $i<k$, or on the $i-k$ smallest elements on the high side if $i>k$.

```pseudocode
QuickSelect(A,l,r,i)
```

### Limitations and performance
The overhead required for this method is often high in practice, and is not generally used as a result. Likewise, for its application to quicksort.

## Application: quicksort
A selection algorithm with a $\Theta(n)$ worst-case time allows us to improve the worst case time bound of quicksort, by instead of using a random pivot applying the above liner time selection method to finding each subarrays median pivot (or any pivot that partitions the array into constant ratio halves). Doing this improves the worst case time of quicksort to $\Theta(n\log n)$.

