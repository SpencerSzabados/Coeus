Radixsort sorts numbers by progressively grouping and reordering (recombining) elements based on the value of their least significant digit upwards to their most significant digit; importantly, radixsort works indirectly, and does not directly compare any two elements together. Radixsort typically makes use of Countsort or Bucketsort to bin elements and then rearrange them at each stage. [[@Cormen_2009]], [happycoders](https://www.happycoders.eu/algorithms/radix-sort/).

Let $A[1,\dots,n]$ be an an array of numbers to be sorted (or anything that is encoded using finite digits) of the form $x=b_{d}\dots b_1$ with $b_i\in \{0,1,\dots,k-1\}$ for $i=1,\dots,d$, that is, each element of $A$ is assumed to have $d$-digts (with leading zeros for smaller values) with $k$ possible values per digit. Then to sort $A$, for each digit $i = 1,\dots, d$ (right-to-left ordering) place each element $A[j]$ into the bucket $B[A[i][i]]$, index equals the digit value, based on FIFO inserted order; i.e., Bucketsort $A$ based on each digits value. After all elements of $A$ are inserted into a bucket, concatenate the lists of elements in each bucket together (end-to-end) in order of the digit values to yield the intermediately sorted array. This is repeated for each digit, working on the intermediate array from the previous step, to finally yield the sorted array.

```pseudocode
Let A[1,...,n] be an array to be sorted
_______________________________________
RadixSort(A)
    d = maximum number of digits used by a number in A
    for i from 1 to d
        BucketSort A based on digit i
```

For an array $A$ with $n$ numbers that require at most $d$ digits to store, in which each digit can take on upto $k$ possible values, Radixsort takes $\Theta(d(n+k))$ total time to sort $A$ if the digit-wise sorting method used (is stable) takes $\Theta(n+k)$ time for each digit. For $n$ many $b$-bit numbers (i.e., binary encodings of length $b$) Radixsort takes $\Theta((b/r)(n+2^r))$ time, for any integer $r\leq b$ where each digit in the number takes $r$ bits to encode (byte size).


# Bucketsort
Bucketsort assumes the input sequence to be sorted is drawn from a uniform distribution on $[0,1]$ (or any sale transform); under  this condition, Bucketsort has a average-case running time of $O(n)$. Bucketsort divides the interval $[0,1]$ into $n$ equal-size subintervals (called buckets), and then distributes the $n$ input numbers into the buckets. Due to the assumption of the input number being iid on $[0,1]$ we do not expect many values to lie in any singular bucket. The buckets are then sorted and stripped together to generate the final sorted array.

```pseudocode
Let A[0,...,n-1] be an array to be sorted
_________________________________________
BucketSort(A)
    Let B[0,...,n-1] be an array of linked list pointers
    
    for i from 0 to n-1
        B[floor(n*A[i])].insert(A[i]) //Insert into linked list
        
    for i from 0 to n-1
        Sort(B[i])                    //Sort each linked list
        
    concatenate the lists B[0],B[1],...,B[n-1] together end to end in order
         
```


# Countingsort