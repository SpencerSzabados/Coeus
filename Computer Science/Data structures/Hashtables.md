Hash tables are a quick direct access (slow to search) dynamic dictionary data structure; supporting $Insert$, $Search$, and $Delete$ operations. Hashing methods calculate the position of a key in a table based on the value of the key (or some function of that value) directly.  [[@Cormen_2009]], [[@Drozdek_2005]]


# Direct-addressing
Direct addressing is a very simple technique that works well when the universe $U=\{0,1,\dots,n$ of possible values considered is quite small and every value is distinct. To store the dynamic set, we use a partially full array $T[0,\dots,n]$, in which each position corresponds to a key value in $U$, where if element $k$ hasn't been interested $T[k]=Nil$.

Direct-address hastables are a form of [[bitmap]].

Direct-addressing is self limiting as it requires a large amount of memory to store even a few values. Moreover, dictionary data structures suffer from sparsity as there is frequently many empty cells for element that have not been encountered but have space allocated for the possibility of encountering them. This is unavoidable for such a sample method. 


# Open-addressing (Closed hashing)
In open hashing all keys occupy the cells of the hash table itself, rather than a referenced structure. In open addressing a hash table $T[0,1,\dots,m-1]$ can only store $m$ elements before it needs to be resized; consequently $\alpha\leq 1$ at any given point. 

Keys are inserted into $T$ by successively inspecting, or _probing_, the hash table based on the value of the key $k$ to be inserted (or some hashed value $h(k)$) until a empty slot is found. Collisions are dealt with by shifting where keys are stored (according to some specified rule) until empty slot is found. In particular the hashing function $h:U\to \{0,1,\dots,m-1\}$ is modified to accept a iterative index used during probing to be of the form $h:U\times\{0,1,\dots,m-1\}\to \{0,1,\dots,m-1\}$. If we are trying to insert key $k$ into slot $h(k)$ then either (1) $T[h(k)]=nil$ and the value can be inserted or, (2) $T[h(k,0)]\neq nil$ and we probe the cells $T[h(k,1)],\dots$ until a empty cell is found; it is necessary that the sequence $h(k,0),h(k,1),\dots$ is capable of reaching every cell of $T$ to function appropriately.

Deletion is more difficult using open-addressing as the positions of elements are interdependent due to how full cells are skipped over during insertion, as a result cells cannot simply be marked as empty. A simple solution to this problem is to rewrite a deleted key with a reserved value used to indicate the cell can be written over. however, this method slows down search times as deleted cells must also be integrated over during the search.


## Collision handling
### Linear probing
### Cuckoo hashing
In Cuckoo hashing two hash functions are used to resolve collisions, opposed to using a single hash function and probing along the array until a empty cell is found, where preoccupied items removed to make way for newly inserted values are shuffled between until the last item being moved around is inserted into an empty cell the maximum number of allowed iterations is reached. [Wiki](https://en.wikipedia.org/wiki/Cuckoo_hashing)

Cuckoo hashing is commonly implemented by splitting the main table in to two equally sized arrays and matching each with a different hash function. Keys are then shuffled between one or the other table depending on availability, that is, if a key collides with an existing value in one table we remove the preoccupying key, insert the new key, and attempt to insert the newly removed key in the second table using the sample process as used for the new key.


#### Limitations and performance
Cuckoo hashing in practice is about $20\%-30\%$ slower than [[Hashtables#Linear probing|linear probing]] due to frequent cash misses, a result of modern CPU architectures. 


# Dynamic size hash addressing
In order of overcome the sparsity of direct-addressing, we employ a method of mapping values into fewer cells based on how full the hash table is.

Let $U=\{0,1,\dots,n\}$ be the universe of values and $m\leq |U|$ a parameter that controls how larger the hash table is; the initial value of $m$ is typically chosen based on the expected number of values and then later doubled (and the hash table rebuilt) once the number of values within the table reaches a certain threshold of $m$.

Now instead of using the value of the key direction, we make use of a _hash function_ $h:U\to \{0,\dots,m-1\}$ that takes as its input the key to be stored and outputs an index. That is, for a key $k$ to be stored we set $$T[h(k)] = k.$$The choice of $h$ is important to consider, for if two values gets hashed to the same index, a situation called _collision_, we have to have a way to deal with this. Avoiding _collision_ entirely, called _perfect hashing_, is not in general possible except for when the structure of the data is very restricted.


## Collision handling
### Chaining
In chaining, the hash table $T[0,1,\dots,m-1]$ is implemented has a array of length $m$ in which each entry holds a pointer to the start of a [[linked list]] (double linked) in which all elements hashed to the same index are inserted. 


#### Limitations and performance
Analysis of hash tables is carried out in terms of the _load factor_ of $T$ which is equal to $\alpha=M/m$; the average number of elements stored in each chain. As a rule of thumb $T$ is increased in size (based on whatever method best suits the chosen hashing function) in size once $\alpha$ reaches a threshold value. Then we see:
  + $Insert$ takes $O(1)$ worst case time (for prepending elements to the linked lists or appending using a end-of-list pointer); this also assumes the element being inserted is not already present in the list, if duplicates are not allowed to occur we must search the linked list (chain) to ensure the key to be inserted is not already present. 
  + $Delete$ takes time proportional the length of the list the key to be deleted is stored in, so takes $O(\alpha)$ expected time. 
  + $Search$takes $O(M)$ time in the wort case where all $M$ keys are hashed to the same entry in the table. If we assume $h(k)\sim U[0,1,\dots,m-1]$ (simple uniform hashing) then $E[length(T[i])]=\alpha$. Thus, the expected time for a successful (or unsuccessful) search is $O(\alpha+1)$. Consequently, if $m$ is proportional to $M$, that is $m\in O(M)$, then we achieve expected search time of $O(1)$. 


## Fixed hash functions 
In practice heuristic techniques are used to create well performing hash functions; however, if you know the distribution (occurrences of keys) generating keys you can better optimize the hash function used.

#### Prime modulo hashing (division method)
For integer key values, the hashing function  $$h(k) = k\text{ mod }p,$$where $p$ is a prime not near a power of two, typically yields good results when using chaining for collision handling. 


## Universal hash functions 
A randomly chosen hash function that is built independent of the type of data to be store is called a _universal hash function_ and, if well designed, can deliver provably good average case performance.

The randomized selection of the hash function (from a well designed class of functions) helps guarantee that no single input sequence will always evoke the worst case performance.

Specifically, let $\mathcal{H}$ denote a finite collection of functions of the form $h:U\to \{0,1,\dots,m-1\}$. Such a collection is said to be _universal_ if for each pair $k_1,k_2\in U$, the number of hash functions $h\in\mathcal{H}$ for which $h(k_1)=h(k_2)$ is not larger than $|\mathcal{H}|/m$. If a hash function is randomly selected from a universal set $\mathcal{H}$, then after hashing $M$ entries into a table $T$ of size $m$ the expected search time is $O(\alpha+1)$. Hence, a sequence of $M$ $Insert$, $Delete$, and $Search$ operations takes $\Theta(M)$ expected time.

The most common class of universal hash functions for hashing keys in range $\{0,1,\dots,p-1\}=\mathbb{Z}_p$ for a sufficiently large prime $p$ into hash table $T$ of size $m$ is equal to $$\mathcal{H}_{p,m} = \{h_{a,b} = (ak+b\text{ mod }p)\text{ mod }m\mid a,b\in\mathbb{Z}_p, a>0\}.$$This set contains $p(p-1)$ hash functions (linear combinations).


