
# Space-time reduction techniques
## Fractional cascading

# Binary search on sorted arrays
The principle of binary search trees can be applied to sorted arrays, say $A[1,\dots, n]$, to locate elements efficiently in $O(\log n)$ time. Just as for trees, the array is progressively halved at each stage until either the element is found or no elements remain and we conclude the element is not present within the array.

```pseudocode
Let A[0,1,...,n-1] be a sorted array of numbers
Let 'key' be the query value
_______________________________________________
BinarySearch(A, key)
    result = -1       //Found index of key
    l = 0             //Low pointer
    h = n-1           //High pointer
    mid = -1          //Middle of two pointers
    while result == -1 and l < h do
        mid = (l+h)/2
        if key < A[mid] do
            h = mid-1
        else if A[mid] < key do
            l = mid+1
        else
            result = mid
        end
    end
    return result
end
```

## Limitations and performance