# cmsc351 / final

## big $O$, $\Omega$ and $\Theta$.

1. $f(x) = O(g(x))$ when we can find a $c$ and $x_0$ such that for $x > x_0$, $f(x) < cg(x)$.
2. $f(x) = \Omega(g(x))$ when we can find a $b$ and $x_0$ such that for $x > x_0$, $f(x) > bg(x)$.
3. $f(x) = \Theta(g(x))$ when we can find a $b$, $c$, and $x_0$ such that $bg(x) < f(x) < cg(x)$.

## coin changing.

General takeaways:

1. Greedy algorithms *can* be correct, but often aren't. When they are, they're usually pretty good.
2. Dynamic programming algorithms are cool.

Specific to coin changing, we can do the whole thing with *dynamic programming* in $O(nk)$ to make $n$ cents of change with $k$ coins to choose from. We need to store the running minimums, which needs $O(n)$ auxillary space.

## maximum contiguous sum.

There is a pretty obvious brute force method that runs in $O(n^2)$. Start at each position and calculate the largest sum onwards from there.

There is a divide and conquer method that runs in $O(n \lg n)$​. Divide the array in half. At each division, calculate the MCS in the left division, the MCS in the right division, and the MCS that crosses over the halves. Take the largest of the three and return it to the "parent division."

**Kadane's algorithm:** Runs in $O(n)$ time and $O(1)$ space. It's one `for` loop! Let $A$ be our list. Observe that the MCS that ends at $A[i]$ is either $MCS(A[i - 1]) + A[i]$, or just $A[i]$. We just calculate the larger of the two for every $i$ and return the biggest one.

## bubble sort.

Say we have an unsorted list of size $n$.

1. We want to bubble up elements to their highest position.

Things to note:

1. It has a worst, average, and best case time complexity of $O(n^2)$.
2. For each pass through the elements, the latter part of the array gets "more and more sorted." After $k$ passes, the last $k$ elements will be sorted absolutely (as they appear in the final list).
3. Bubble sort can be written to bubble up identical elements in the order they appear, making it stable.

Max questions:

- **Why would we want to use bubble sort?** If the algorithm dies at any given pass, we can at least guarantee that a subset of the elements are sorted. Neither quicksort nor mergesort have such a guarantee.
- **What is true about the list after the first pass?** The last element in the list is the largest one in the list.

## selection sort.

Say we have an unsorted list of size $n$​.

1. We want to keep picking the smallest element and pulling it forward.

Things to note:

1. It has a worst, average, and best case time complexity of $O(n^2)$.
2. For each pass through the elements, the front part of the array gets "more and more sorted." After $k$ passes, the first $k$​ elements will be sorted absolutely (as they appear in the final list).
3. Selection sort can be written to pick earlier identical elements before later ones, making it stable.

Max questions:

1. **What is true after the first pass of selection sort?** The first element of the list is the smallest one in the list.
2. **Does selection sort use more or less operations than bubblesort? Why or why not.** Selection sort definitely uses less operations (swaps) than bubble sort. The process of searching and "picking" leads to one swap for each pass. However, in bubble sort, each element is swapped up to its correct position, making it possible to have up to $n - 1$ swaps in a given pass.

## insertion sort.

Say we have any unsorted list of size $n$.

1. We slide elements left until they are sorted relative to the elements left of them.

Things to note:

1. It has a worst and average case time complexity of $O(n^2)$. However, it has a best case time complexity of $O(n)$, i.e., when the input list is sorted.
2. For each pass through the elements, the front part of the array gets "more and more sorted." After $k$ passes, the first $k$ elements will be sorted *relatively* (amongst themselves; not necessarily how they appear in the final list).
3. We will never slide identical elements over each other, so relative ordering is maintained and the sort is stable.

Max questions:

1. **Do you actually know the difference between this one and selection sort?** I would say so. Selection sort works by picking the elements and arranging them in the correct order. Insertion sort re-places an element that is misplaced among the elements to its left.

## binary search.

Say we have a sorted list of size $n$, and we want to find index of $k$.

1. Choose the middle element `mid`. If $k <$ `mid`, restart on the left half. If $k >$ `mid`, restart on the right half. If $k = $​ `mid`, we can return the index of `mid`.
2. If we don't find it, return like `-1` or something.

That's it! Things to note:

1. Operates on the assumption that smaller elements are on the left, larger on the right. 
   1. "How can we modify binary search to work over lists with [property]."
2. Every subsequent lookup halves the search space. $O(\lg n)$ worst case time complexity.

## recurrence relations.

A recurrence relation is a function that calls itself in some fashion (also has a base case). Algorithmically reflected with recursion. 

We can use "digging down" to find a closed form for the recursion:

1. $T(n) = 2T(n / 2) + \frac{1}{2} n$ with $T(1) = 7$.
   1. $T(n) = 2[2T(n/4) + \frac{1}{2} \frac{n}{2}] + \frac{1}{2} n$.
   2. $T(n) = 2[2[T(n / 8) + \frac{1}{2} \frac{n}{4}] + \frac{1}{2} \frac{n}{2}] + \frac{1}{2} n$.
   3. $T(n) = 4T(n / 8) + \frac{n}{2} + \frac{n}{2} + \frac{n}{2}$.
   4. $T(n) = 2^k T(n / 2^k) + k \frac{n}{2}$
2. $k = \lg n$ so $T(n) = 7n + \frac{n \lg n}{2}$.
3. Remember that $2^k = n$ when $k = \lg n$​.

For drawing trees, remember that the value of the node is the non recursive component, and the child nodes are the number of times it calls the recurrence again.

The **master theorem** is as follows for some $T(n) = a T(n / b) + f(n)$ with $a \geq 1$ and $b > 1$.

1. If $f(n) = O(n^c)$ and $\log_a{b} > c$, then $T(n) = O(n^{\log_a{b}})$.
2. If $f(n) = \Theta(n^c \lg^k n)$ and $\log_a{b} = c$, then $T(n) = \Theta(n^{\log_b{a}} \lg^{k + 1} n)$​.
3. If $f(n) = \Omega(n^c)$ and $\log_a {b} < c$, then $T(n) = \Theta(n^c)$​.

## merge sort.

Say we have an unsorted list $n$.

1. Recursively split the list into halves, and merge the sorted halves together.
2. Merging two sorted lists is an $O(n)$ operation.
3. So doing a merge at each split level takes $O(n \lg n)$.

Things to note:

1. Merge sort has best, worst, and average cases of $O(n \lg n)$.
2. It uses auxillary space $O(n)$​ to hold the sorted sublists at any given time.
3. The BEST ONE.
4. It has a recurrence of $T(n) = 2T(n / 2) + O(n)$.

Max questions:

1. **Do you actually know the difference between this one and selection sort?** I'd hope so. Merge sort has a splitting process and makes auxillary arrays that it "merges" back together. Selection sort chooses and arranges elements in their sorted order.
2. **What makes mergesort parallelizable?** Consider the recurrence tree of merge sort. At each level, we have multiple merge operations that occur. Since these all operate on different portions on the data, these merges can be parallelized.

## quick sort.

Say we have an unsorted list of length $n$.

1. Choose a position to partition the list, and ensure that all elements in the right partition are greater than those in the left partition (this is the `partition` algorithm). 
2. Call quick sort on these two partitions. 

Things to note:

1. Quick sort is not stable, elements can be thrown over each other in the `partition` function.
2. It has $O(n \lg n)$ best and average case time complexity, but $O(n^2)$ in the worst case.

How does `partition` work?

1. Given a pivot, it will push all elements less than the pivot before it, and all elements greater than the pivot after it.

2. ```
   function partition(A, left, right, pivot_index):
   	pivotkey = A[pivot_index]
   	
   	t = left
   	
   	for (i = left; i < right; i++):
   		if A[i] < pivotkey:
   			swap A[t] with A[i]
   			t = t + 1
   			
       swap A[t] with A[pivot_index]
       
       return t
   ```

3. What's happening here? The index $t$ will become the sorted position of the pivot, and all values less than the pivot are pushed before $t$. It follows that all values greater than the pivot are pushed after $t$.

Max questions:

1. **What is the recurrence for Quicksort? Is it different in the best, worst, and average case?** 
   1. For some partition index $k$, we have $T(n) = T(k) + T(n - k - 1) + O(n)$.
   2. In the best case, $k$ is always the median, so $T(n) = 2 T(n / 2) + O(n)$.
   3. In the worst case, $k$ is the first/last index, so $T(n) = T(n - 1) + O(n)$​.
   4. The average case one is annoying. Sum the recurrences for all possible $k$ values (there are $n$ of them) and divide by $\frac{1}{n}$. This gives you an actual average.
2. **Why is having the partition be the median better?** If the partition is the median every time, the two halves will be equal in size, which means that the time complexity will actually be $O(n \lg n)$​​.

## heap sort.

Say we have an unsorted list of length $n$.

1. Build a max heap from the list using `converttomaxheap`.
2. While there are nodes left in the heap, swap the first and last node, call `maxheapify` on the first node, and exclude the  last node from the heap.
3. When our heap is out of nodes, our list will be sorted.

On `converttomaxheap`:

1. We just call `maxheapify` for every element from index $0$ to $n / 2$. Why $n / 2$? Because all nodes after that are leaves. 
2. This runs in $O(n \lg n)$ time. 

On `maxheapify` (takes in a parameter node):

1. If this input node is smaller than one of its children, swap it with that child and call `maxheapify` on the new location. (If both children are larger, swap the node with larger child.)

Max questions:

1. **Does heapsort have any worst cases or best cases?** No worst cases, but if all elements are identical then `converttomaxheap` runs in $O(n)$, and `maxheapify` in $O(1)$, so the sort would take $O(1)$ time.
2. **Suppose when we remove the root of a max-heap, we are magically allowed to rebuild the heap in constant time. How does this affect the time complexity of heap sort in the average case?** Assume that the initial heap building still takes $O(n \log n)$. Even if other operations were faster, the time complexity is still dominated by this operation and overall must still be $O(n \log n)$.
3. **Suppose we are magically allowed to run the floatkeydown component of heapsort in constant time. How does this affect the time complexity of heap sort in the average case?** The initial heap building would become an $O(n)$ time operation. Swapping the maximum node with a leaf and running `floatkeydown` would become an $O(1)$ operation that is performed a number of times that grows linearly with $n$. As such, we have heap sort to be $O(n)$.

## counting sort.

Say we have any unsorted list $A$ of length $n$.

1. Make a frequency array $F$ of length $\max A + 1$, where $F[i] =$ the number of times $i$ occurs in $A$.
2. Make the frequency array cumulative (loop over it and add the previous value to the current value).
3. Create to-be-sorted list $A'$ with length $n$.
4. Loop over $A$ backwards, and for each element $i$ encountered, place it in $A'$ at position $F[i] - 1$. 
5. Decrement $F[i]$​ (the next occurrence is place before).

Things to note:

1. Counting sort runs in best, worst, and average case $O(n + k)$, where $k$ is the maximum element in $A$. This is valid complexity because $k$ doesn't *really* depend on $n$​.

Max questions:

1. **On midterm 2, Max asked for a sort to minimize swaps, as a swap had a chance of causing the algorithm to halt. What sort is ideal?** Counting sort doesn't use any swaps. So it is the ideal option.
2. **On Max’s third midterm, we saw that counting sort is a poor choice for input data like $[1, 2^{40}]$ since it will create auxiliary arrays with $2^{40} + 1$ elements each, which is far too large for a normal computer to store in memory. ($16$ GB of RAM $\approx 2^{34}$ bytes.) Consider a modified version of counting sort that subtracts the minimum of the list from all values before performing the sort, then re-adds this value at the end.**
   1. *Does this version suffer from the same issue as the original?* Yes, it would still fail in this case. $2^{40} - 1 > 2^{34}$. 
   2. *If we used radix + counting sort?* In this case, it would work fine. There is a maximum of $k = 10$, so we will not run out of memory.
   3. *Consider bucket sort with this modified version as the underlying sort. Does this suffer from the same problem?* Yes. $2^{40}$ would end up in a bucket, and then counting sort with need to allocate an array of size far larger than memory capacity.

## bucket sort.

By default:

1. Number of buckets is $\text{floor}{\frac{\max A}{n}} + 1$.
2. 

Max questions:

1. **Is bucket sort appropriate for sorting normally-distributed data points? If not, explain why not and provide a modification that would make it more appropriate.** Not really, as the spread would be heavily centered around the middle buckets. We should instead modify the bucket sizes to account for the amount of data in the range. For instance, middle buckets would have smaller ranges and farther away buckets would have larger ranges.

## radix sort.

Say we have an unsorted list of length $n$, where all elements are $3$ digit numbers.

1. Sort by the third digit.
2. Sort by the second digit.
3. Sort by the first digit.

Things to note:

1. We likely want to use counting sort for the algorithm, as we likely have an idea about the $k$​​ value. 

## karatsuba's multiplication.

Basically we make multiplying numbers faster. Things to note:

1. Recurrence: $T(n) = 3T(n / 2) + \Theta(n)$​​.
2. Apply Master Theorem (first case):
   1. $log_2{3} > 1$ and $f(n) = O(n)$​.
   2. $T(n) = O(n^{\log_2{3}})$.

3. Equation: $AB = 100a_1b_1 + 10[(a_1 + a_0)(b_1 + b_0) - a_0b_0 - a_1b_1] + a_0b_0$.
4. Decimal shifts, i.e. multiplying by powers of $10$, can occur in linear time.

## graphs.

I'm the goat at this. Path, walk, trail, degree, vertex, edge, adjacency list, adjacency matrix. I know all these things.

BFS uses a queue, DFS can use a stack or just be entirely recursive, and Djikstra's uses a priority queue.

## floyd's algorithm.

Floyd's algorithm finds the shortest distance between every two vertices on a graph. It works by allowing new vertices to be used to discover new paths on every iteration through the vertices. This is done repeatedly until all vertices have been considered as possible intermediate vertices and results in the shortest paths.

1. Create `dist`, our adjacency matrix of shortest distances.
2. Original matrix has diagonal $0$s. Takes no distance to go from $x$ to $x$.
3. It also has the `dist[u][v] = ` the edge weight of $(u, v)$, if it exists.
4. 

## prim's algorithm.

We want to create a **minimum spanning tree** from a graph $G$, or a tree with minimum cost to travel to each vertex on the vertices of $G$. The edges of the MST are a subset of $G$​'s edges. 

1. We have a list called `visited`. And a list called `edges`.
2. If we start at node $A$, add it to `visited`.
3. For all unvisited vertices connected to $A$, choose the one with smallest edge (add to `edges`). Say $B$.
4. Add $B$ to visited.
5. Now examine all unvisited vertices connected to $A$ and $B$, and pick one with smallest edge (add to `edges`) from either.
6. Continue until no more unvisited nodes.

## kruskal's algorithm.

Another MST building algorithm. 

1. Keep choosing smallest edges that don't create a cycle.
2. Continue this until all nodes are in the tree.

## p/np.

$P$ is the set of all decision problems that are solveable by a **deterministic Turing machine** in polynomial time.

$NP$ is the set of all decision problems that are solveable by a **nondeterministic Turing machine** in polynomial time, and the solutions can be *verified* by a DTM in polynomial time.

Examples of $NP$-complete problems:

- The $k$-coloring problem.
- Traveling salesman problem.
- Hamiltonian graph problem.
- The $k$-clique problem.
- Boolean satisfiability.

