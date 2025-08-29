A Bloom filter is a space-efficient probabilistic data structure used for answering if a set contains a query element (or element-element comparisons) based on hashing. False positives are possible with a calculable probability, but false negatives are not [WIki](https://en.wikipedia.org/wiki/Bloom_filter), [[@Bloom_1970]]. Bloom filters are used for approximate sequence matching in [[bioinformatics]] for searching Gen banks for sequences.

A Bloom filter designed to process elements from the population (universe) $U$ is instantiated as a $m$-bit array $B[0,\dots,m-1]$ of zeros with $k$ distinct hash functions $h_0,\dots,h_{k-1}$ of the form $h_i:U\to \{0,1,\dots,m-1\}$ each of which maps elements from $U$ to indices of the array; the hash function should generate a uniform random distribution over $\{0,1,\dots,m-1\}$.

In general, for a set $Y$ and a query element $x\not\in Y$ to have $P(x\in Y) = 0.01$, that is, a false positive rate of $1$%, fewer than $10$-bits are needed per element of $Y$.


# Counting bloom filter 
This variant of a bloom filter allows for the _removal_ of elements from sets, an operation not supported by the original variant.


# Optimal bloom filter replacement
[[@Pagh_2005]]