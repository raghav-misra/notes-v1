# cmsc351 / exam03

## limitations of cbsas.

In the process of comparing elements and sorting them, our algorithm implicitly builds and traverses a **decision tree** to determine the sorted list. Consider the number of permutations of the list is $n!$, so it takes $\Omega(\lg n!)$ to make the decision. 

Proved in the notes, $\Omega(\lg n!) \rightarrow \Omega(n \lg n)$, and we find that even the most efficient CBSA is upper bounded by $\Omega(n \lg n)$​.

> Consider the decision tree of selection sort, applied to the list $[XYZ]$:
>
> - Is $Y < X$?
>   - **Yes**, is $Z < Y$​?
>     - **Yes**, swap $X, Z \rightarrow [Z|YX]$​​. Is $Y < X$?
>       - **Yes**, swap nothing $\rightarrow [ZY|X]$​. **Done!**
>       - **No**, swap $X, Y \rightarrow [ZX|Y]$. **Done!**
>     - **No**, swap $X, Y \rightarrow [Y|XZ]$. Is $X < Z$?
>       - **Yes**, swap nothing $\rightarrow [ZY|X]$. **Done!**
>       - **No**, swap $X, Z \rightarrow [Y|ZX]$. **Done!**
>   - **No**, is $Z < X$?
>     - **Yes**, swap $X, Z \rightarrow [Z|YX]$​. Is $Y < X$?
>       - **Yes**, swap nothing $\rightarrow [ZY|X]$. **Done!**
>       - **No,** swap $X, Y \rightarrow [ZX|Y]$. **Done!**
>     - **No,** swap nothing $\rightarrow [X|YZ]$. Is $Y < Z$?
>       - **Yes**, swap nothing $\rightarrow [XY|Z]$. **Done!**
>       - **No**, swap $Y, Z \rightarrow [XZ|Y]$. **Done!**

## counting sort.

### the concept.

Take the list $A = [3, 10, 4, 3, 4, 5, 4, 3, 5, 6, 1, 3, 0]$. Knowing the list max is $10$, we build a list `pos` of indices $0$ to $10$, and set each index to be the amount of times the index number shows up in a list:
$$
\texttt{pos} = \begin{cases}
	\text{indices.. }[00, 01, 02, 03, 04, 05, 06, 07, 08, 09, 10] \\
	\text{values... }[01, 01, 00, 04, 02, 02, 01, 00, 00, 00, 01]
\end{cases}
$$
We have a (sort of) idea of our sorted list? The non-zero entries are all elements of the list, and they do appear least to greatest. Next, we modify `pos` to be cumulative:
$$
\texttt{pos} = \begin{cases}
	\text{indices.. }[00, 01, 02, 03, 04, 05, 06, 07, 08, 09, 10] \\
	\text{values... }[01, 02, 02, 06, 08, 10, 11, 11, 11, 11, 12]
\end{cases}
$$
Observe that any occurrences $i$ of `pos` must end at the position `pos[i] - 1` in the sorted list. Now, we iterate through $A$ right-to-left, place each element $i$​ in `pos[i]`, and decrement `pos[i]`.
$$
\texttt{sorted} = [0, 1, 3, 3, 3, 3, 4, 4, 5, 5, 6, 10]
$$

> We iterate right-to-left to preserve stability. Since `pos[i]` is highest for the rightmost occurrence of $i$, we know that the identical elements are relatively placed in the same order as they appeared in $A$.

### the code.

```python
def counting_sort(A):
    A_max = max(A) # largest element in A
    pos = [0] * (A_max + 1) # initialize a list with indices 0...A_max
    
    # populate pos with occurrences:
    for num in A:
        pos[num] += 1
        
    # make pos cumulative:
    for i in range(1, len(pos)):
        pos[i] = pos[i] + pos[i - 1]
        
    B = [0] * len(A) # our sorted list
    
    # traverse through A in backwards:
    i = len(A) - 1
    while i >= 0:
        num = A[i] # grab the current element from A
        new_i = pos[num] - 1 # find this element's new index in B
        B[new_i] = num # place in B
        pos[num] -= 1 # decrement to place the next occurrence before
        
        i -= 1 # traverse
        
    # modify A to look like B:
    for i in range(len(A)):
        A[i] = B[i]
```

### properties.

Let $k = \max A$ for some (unsorted) list $A$ of length $n$.

**Time complexity:** best, worst, and average cases are all $\Theta(n + k)$.

- $n$ iterations to do anything with $A$, and $k$ iterations to do anything with `pos`.
- If we know that $k \leq n$, or that $k$ is constant, then we can simplify to $\Theta(n)$​.

**Space complexity**: clearly $\Theta(n + k)$.

- `pos` is length $k$ and $B$ is length $n$. 
- If $k \leq n$, or is constant, then we can simplify to $\Theta(n)$.

**In-place?** No. Requires additional space to store sorted elements.

**Stable?** Yes. This is guaranteed by the way we traverse $A$ to build $B$.

## bucket sort.

### the concept.

Let $A$ be our unsorted list. To **bucket sort** $A$, 

- Make an array of a bunch of arrays, which will be our *buckets*. Each bucket is designated to contain a certain range of elements. 
- Copy each item from $A$​ in its assigned bucket.
- Sort each bucket individually.
- Traverse through the list of buckets and copy the ordered elements back to $A$.

The way we designate the range of each bucket is dependent on the maximum value in the list:

- Say you want to use exactly $n$ buckets. Then $\text{floor}(\frac{\max a}{n}) + 1$​ is the number of buckets.
- At least for the exam, **the number of buckets is the length of the list!**

### the code.

```python
from math import ceil, floor

def bucket_sort(A, b):
    # init n empty lists
    buckets = [[]] * floor(len(A) / b) + 1
    
    # assign each element to bucket
    for num in A:
        buckets[floor(b * num / len(A))].append(num)
        
    # sort each bucket
    for bucket in buckets:
        some_sort(bucket)
    
    sorted_A = []
    
    # add back in sorted order
    for bucket in buckets:
        for num in bucket:
            sorted_A.append(num)
            
    return sorted_A
```

### properties.

**Time complexity:**

- **Worst case:** Depends on the underlying sort. Manipulating the elements into and out of respective buckets is $O(n)$, but the actual sorting algorithm likely dominates this time. If insertion sort is used, worst case is clearly $O(n^2)$.
- **Best case:** If each bucket ends up with at most one element, then any underlying sort would very obviously run in $O(1)$. The bucket manipulation takes $O(n)$, which dominates the overall time complexity.
- **Average case:** This is kind of funny. Realistically, it is unlikely that the number of elements per bucket exceeds some constant, say $4$. Sorting $4$ elements would always take constant time, which means the $O(n)$ bucket manipulation dominates the overall time complexity.

**Auxiliary space:** $O(n)$​ to place elements into buckets.

**Stable?** If the underlying sort is, then yes, otherwise no.

**In-place?** The above implementation is not in-place, but it can be modified to be in-place?

## radix sort.

### the concept.

Radix sort works by **stable sorting** the elements by their least significant digit, then the "next-least" significant digit, etc. Stable sorting means that it relies on an underlying stable sorting algorithm (like counting sort) to work. It is good for the following situations:

- Binary numbers sorted from $000000$ to $111111$, inclusive.
- $x$-digit strings that match $[A-Z]*$, where $x$​ is a constant.
- You probably get the idea.

Take the list $[170, 045, 075, 090, 802, 024, 002, 066]$:

- We stable sort by the "one's place."
  - $[17|0, 09|0, 80|2, 00|2, 02|4, 04|5, 07|5, 06|6]$
- Next, we stable sort by the "ten's place."
  - $[8|02, 0|02, 0|24, 0|45, 0|66, 1|70, 0|75, 0|90]$
- Lastly, we stable sort by the "hundred's place."
  - $[002, 024, 045, 066, 075, 090, 170, 802]$
  - **Done!**

Let $d$ be the number of digits in each element, and $b$ be the base, or number of characters allowed. In the above example, we had $d = 3$ digits, and $b = 10$, as we allowed $0$ through $9$​, inclusive, for each position.

### properties.

Let the underlying stable sort take $\Theta(f(n, b))$ time.

- We care about $b$ in the case of counting sort, where $f(n, b) = n + b$. But if $b$ is fixed, then it becomes $f(n, b) = n$.

**Time complexity:** using the above expression for the underlying sort, $\Theta(d \cdot f(n, b))$. 

- In the case of counting sort, if we know $d$ and $b$ are constant/independent of $n$, then the time complexity simplifies to $\Theta(n)$.
- If we use a CBSA, like bubble sort, then it definitely doesn't depend on $b$, i.e., $f(n, b) = n^2$. If $d$ was $n$-dependent, then $\Theta(dn^2)$. Otherwise, just $\Theta(n^2)$.

**Space complexity:** equivalent to that of the underlying sort. In the case of counting sort, it is $\Theta(n)$ when $b$ is constant.

**In-place?** Dependent on the underlying sort. In the case of counting sort, very much not.

**Stable?** Since our underlying sort should be stable, radix sort will be stable.

## karatsuba's algorithm.

### schoolbook method.

This is basically the "intuitive method" to multiply. Split the numbers into expanded notation (digits * place value) and then add the products of the combinations.

> How would we multiply $123$ and $357$ with this method?
> $$
> \begin{align*}
> 	123 \cdot 357 &= [1(10^2) + 2(10^1) + 3(10^0)][3(10^2) + 5(10^1) + 7(10^0)] \\
> 	&= 1(3)(10^4) + 1(5)(10^3) + 1(7)(10^2) \\
> 	&+ 2(3)(10^3) + 2(5)(10^2) + 2(7)(10^1) \\
> 	&+ 3(3)(10^2) + 3(5)(10^1) + 3(7)(10^0) \\
> 	&= 43911
> \end{align*}
> $$

**Time complexity:** Notice how multiplying two $3$-digit numbers results in a sum of $3^2=  9$ addends? If both numbers have $n$ digits, the time complexity is already $\Theta(n^2)$​.

### sneaky approach.

Consider two $2$-digit numbers, $A$ (digits $a_1 a_0$) and $B$ (digits $b_1 b_0$):
$$
\begin{align*}
	AB &= (10a_1 + a_0)(10b_1 + b_0) &\text{schoolbook method} \\
	&= 100a_1b_1 + 10(a_1 b_0 + a_0 b_1) + a_0 b_0 &\text{expand above} \\
\end{align*}
$$
The expansion contains $4$ distinct multiplications. Take the middle term (ignore the $10$):
$$
a_1 b_0 + a_0 b_1 = (a_1 + a_0)(b_1 + b_0) - a_0 b_0 - a_1 b_1
$$
This version has $3$​ multiplications, two of which we've done already! Altogether,
$$
AB = 100a_1b_1 + 10[(a_1 + a_0)(b_1 + b_0) - a_0b_0 - a_1b_1] + a_0b_0
$$
Adding numbers and multiplying by $10$ and $100$​​ (decimal shifts) occur in linear time.

### generalizing.

This "sneaky" optimization will generalize to any multiplications of two $n$-digit numbers. This consists of three multiplications of $\frac{n}{2}$-digit numbers, and addition/shifts that occur in linear time. We can write a recurrence relation:
$$
T(n) = 3T(\frac{n}{2}) + \Theta(n)
$$

> Consider the tree diagram of multiplying $12 \cdot 34$​ with Karatsuba's algorithm:
>
> - $12 \cdot 34$
>   - $\Rightarrow 1 \cdot 3$
>   - $\Rightarrow (1 + 2)(3 + 4) = 3 \cdot 7$
>   -  $\Rightarrow 2 \cdot 4$
>
> This has a total of $3$ single-digit multiplications (SDMs).

**Time complexity:** Applying the Master theorem where $a = 3, b = 2, c = 1, f(n) = \Theta(n)$, since $\log_b a < c$, we find the time complexity of this recurrence to be $\Theta(n^{\log_2 3})$. As $n$ gets larger, this approach gets significantly faster than the $\Theta(n^2)$​ schoolbook method.

## graphs.

### terminology.

A **graph** is defined by a set of **vertices**, or nodes, that are connected by **edges**. Two vertices are **adjacent** if they are connected by an edge. The **degree** of a vertex is the number of edges leaving it. A **loop** is an edge that connects a vertex to itself. 

A graph is **simple** if it contains no loops and no multiple edges. A graph is **weighted** if its edges have numerical weight associated with them.

- The weight of an edge can often represent a cost of traversing it, such as a road network where each weight is the distance (in miles?).

A **walk** of length $k$ is from vertex $u$ to vertex $v$ is a sequence of $k$ edges that start at $u$ and end at $v$. 

- A **trail** is a walk in which all edges traversed are distinct. 
  - We can have a trail of length zero, where the start and end vertices are the same and no edges are traversed.
- A **path** is a walk in which all vertices traversed are distinct. Note that distinct vertices implies distinct edges.
  - We can't have a path of length zero; at least one vertex must be traversed.
- A **cycle** is a trail where all vertices are distinct, except for the start and end, which are the same. 
  - Note that a cycle $a \rightarrow b \rightarrow c \rightarrow a$ would be equal to $c \rightarrow a \rightarrow b \rightarrow c$.

A graph is **connected** if any two vertices are connected by at least one path. A **tree** is considered a **minimally connected graph**, where two vertices are connected by *exactly one* path.

### data structures.

For a graph $G$ with $n$ vertices, its **adjacency matrix** $AM$ is a $n \times n$ two-dimensional array where:

- If $G$ is unweighted, $A[i][j] = 1$, if vertices $i$ and $j$ have an edge connecting them, otherwise $A[i][j] = 0$.
- If $G$ is weighted, $A[i][j] = w$, if vertices $i$ and $j$ have an edge with weight $w$ connecting them, else $A[i][j] = 0$​​.

For a graph $G$, its **adjacency list** $AL$ is a list where $A[i]$ contains the vertices in the neighborhood of vertex $i$​. 

**Storage:** An adjacency matrix always requires $V^2$ values ($V$ total vertices), while an adjacency list will require $2E$ values to reflect both directions of each undirected edge. If the edges are directed then it would just b

> Suppose a graph $G$ has the following adjacency list:
> $$
> [[7], [2, 4], [1, 4], [6, 7], [1, 2, 6, 7], [7], [3, 4], [0, 3, 5]]
> $$
> Write out the adjacency matrix.
>
> ---
>
> $G$ has vertices $0$ through $7$, based on the length of the adjacency list. As such, we'll need an $8 \times 8$ matrix:
> $$
> \begin{bmatrix}
> 	0 & 0 & 0 & 0 & 0 & 0 & 0 & 1 \\
> 	0 & 0 & 1 & 0 & 1 & 0 & 0 & 0 \\
> 	0 & 1 & 0 & 0 & 1 & 0 & 0 & 0 \\
> 	0 & 0 & 0 & 0 & 0 & 0 & 1 & 1 \\
> 	0 & 1 & 1 & 0 & 0 & 0 & 1 & 1 \\
> 	0 & 0 & 0 & 0 & 0 & 0 & 0 & 1 \\
> 	0 & 0 & 0 & 1 & 1 & 0 & 0 & 0 \\
> 	1 & 0 & 0 & 1 & 0 & 1 & 0 & 0 \\
> \end{bmatrix}
> $$

## shortest path algorithm.

### the concept.

For any two vertices $s$ and $t$ in graph $G$, how might we algorithmically find the shortest path between them?

1. Create a distance list $D$, and assign $\infty$ to all vertices in $G$, except assign $0$ to $s$​​​.
2. Create a predecessor list $P$ and assign `X` (null) to all vertices in $G$.
3. Push $s$ to a queue $Q$.
4. While there are elements in the queue,
   1. Pop element $x$ off the queue.
   2. Assign all its $\infty$ neighbors a distance of $D[x] + 1$​​​​.
   3. Assign all its $\infty$ neighbors a predecessor of $x$.
   4. Push all the previously-$\infty$​ neighbors to the queue.
   5. If $t$ is one of the $\infty$ neighbors, break from the loop.
5. $D[t]$ holds the length of the shortest path from $s$ to $t$.

> Trace out the shortest path from $0$ to $5$ in the following graph:
>
> ```mermaid
> flowchart LR
> 	2 --- 5
> 	5 --- 8
> 	2 --- 1
> 	1 --- 4
> 	4 --- 7
> 	1 --- 0
> 	0 --- 3
> 	3 --- 6
> 	6 --- 8
> 	4 --- 3
> 	
> ```
>
> Initialize $D$, $P$, and $Q$.
> $$
> \begin{align*}
> 	D &= [0, \infty, \infty, \infty, \infty, \infty, \infty, \infty, \infty] \\
> 	P &= [\texttt{X}, \texttt{X}, \texttt{X}, \texttt{X}, \texttt{X}, \texttt{X}, \texttt{X}, \texttt{X}, \texttt{X}] \\
> 	Q &= [0]
> \end{align*}
> $$
> Pop $0$ off $Q$, calculate the distances for its $\infty$-neighbors ($1, 3$), and push them onto $Q$:
> $$
> \begin{align*}
> 	D &= [0, 1, \infty, 1, \infty, \infty, \infty, \infty, \infty] \\
> 	P &= [\texttt{X}, 0, \texttt{X}, 0, \texttt{X}, \texttt{X}, \texttt{X}, \texttt{X}, \texttt{X}] \\
> 	Q &= [1, 3]
> \end{align*}
> $$
> Pop $1$ off $Q$, calculate the distances for its $\infty$-neighbors ($1, 4$), and push them onto $Q$:
> $$
> \begin{align*}
> 	D &= [0, 1, 2, 1, 2, \infty, \infty, \infty, \infty] \\
> 	P &= [\texttt{X}, 0, 1, 0, 1, \texttt{X}, \texttt{X}, \texttt{X}, \texttt{X}] \\
> 	Q &= [3, 2, 4]
> \end{align*}
> $$
> Pop $3$ off $Q$, calculate the distances for its $\infty$-neighbors ($6$), and push them onto $Q$:
> $$
> \begin{align*}
> 	D &= [0, 1, 2, 1, 2, \infty, 2, \infty, \infty] \\
>     P &= [\texttt{X}, 0, 1, 0, 1, \texttt{X}, 3, \texttt{X}, \texttt{X}] \\
> 	Q &= [2, 4, 6]
> \end{align*}
> $$
> Pop $2$ off $Q$, calculate the distances for its $\infty$-neighbors ($5$), and push them onto $Q$:
> $$
> \begin{align*}
> 	D &= [0, 1, 2, 1, 2, 3, 2, \infty, \infty] \\
> 	P &= [\texttt{X}, 0, 1, 0, 1, 2, 3, \texttt{X}, \texttt{X}] \\
> 	Q &= [4, 6, 5]
> \end{align*}
> $$
> We have assigned $D[5] = 3$, which is our shortest path length. Backtracking through list $P$, we find the shortest path itself to be $5 \leftarrow 2 \leftarrow 1 \leftarrow 0$.

### the code.

```python
from collections import deque
from math import inf

def shortest_path(AL, s, t):
    D = [inf] * len(AL) # initialize distance list
    P = [None] * len(AL) # initialize predecessor list
    Q = deque() # initialize queue
    
    D[s] = 0 # s -> s is zero
    Q.append(s) # add s to queue
    
    while len(Q) > 0:
        x = Q.popleft()
    	for neighbor in AL[x]:
            if D[neighbor] != inf: continue # if distance is finite, ignore
            
            D[neighbor] = D[x] + 1 # set distance of neighbor
           	P[neighbor] = x # set predecessor of neighbor
            Q.append(neighbor)
        
        if D[t] != inf:
            break
    
    if D[t] == inf:
        print(f"No path exists between {s} and {t}.")
    else:
        path = [t]
        
        for i in range(D[t]):
            path.append(P[path[-1]])
        print(f"Shortest path is length {D[t]}; order is", path)
        
```

### properties.

**Auxillary space:** $\Theta(V)$, in the worst-case, $D$, $P$, and $Q$, can all have $V$​ vertices in them.

**Time complexity:**

- **Best case** is $\Theta(V)$, if $s$ and $t$ are neighbors as it takes that long to initialize $D$ and $P$​.
- **Worst case** is $\Theta(V + E)$, as we must also traverse all edges.

The above assumes that we have the graph stored as an adjacency list.  

## breadth-first traversal.

### the concept.

A **breadth-first traversal** of a graph starts at vertex $s$ and visits other vertices in layers of distances.

- First it will visit direct connections of $s$.
- Then it will visit the direct connections of the direct connections of $s$.
- Et cetera, until all vertices have been visited.

> Perform a breadth-first traversal on the following graph starting at $0$.
>
> ```mermaid
> flowchart
> 	0 --- 1
> 	0 --- 4
> 	0 --- 5
> 	1 --- 2
> 	1 --- 6
> 	4 --- 8
> 	5 --- 6
> 	5 --- 8
> 	5 --- 9
> 	2 --- 3
> 	2 --- 6
> 	2 --- 7
> 	6 --- 11
> 	8 --- 13
> 	9 --- 10
> 	11 --- 15
> 	13 --- 12
> 	10 --- 14
> ```
>
> The flowchart visualization makes this pretty easy:
> $$
> [0, 1, 4, 5, 2, 8, 6, 9, 3, 7, 13, 11, 10, 12, 15, 14]
> $$

The way BFT works algorithmically, is that it adds the starting element to a queue.

1. While the queue is not empty, it pops the queue, adds popped vertex to traversal, and pushes the popped vertex's neighborhood to the queue. Vertices that have been visited are added to a set, allowing us to not revisit them if they show up again.

### the code.

```python
from collections import deque

def bft(AL, s):
    traversal = [s] # initialize with starting node
    Q = deque()
    seen = set()
    
    Q.append(s)
    
   	while len(Q) > 0:
    	curr = Q.popleft()
        for neighbor in AL[curr]:
            if neighbor not in seen: # no duplicate elements
                Q.append(neighbor)
                seen.add(neighbor)
                traversal.append(neighbor)    	
    
    return traversal
```

### properties.

**Time complexity:** The inner `for` runs twice for each edge in the graph. Every vertex is pushed and popped once. As such, the total time is $\Theta(V + E)$.

**Auxillary space:** The `seen` set will eventually grow to size $V$, so it's just $\Theta(V)$.

## depth-first traversal.

### the concept.

A **depth-first traversal** of a graph starts at vertex $s$​​ and visits other vertices by completely traversing an individual path and then backtracking.

### the code: recursion method.

Basically calling some function `dft` some node will proceed to call `dft` on all of that node's neighbors. As a result, it will traverse recursively down a path until a dead end, and then backtrack to the next possible node.

```python
# s = start node.
def dft(s, AL):
    traversal = []
    seen = set()
    
    def helper(curr):
        # add to traversal + mark as seen
        traversal.append(curr)
        seen.add(curr)
        
        # recurse on neighbors/children
        for neighbor in AL[curr]:
            if neighbor not in seen:
                helper(neighbor)
    
    helper(s)
    return traversal
```

### the code: stack method.

Not going to write it out, but it is identical to BFS code, except instead of a queue we use a stack. This method works because it immediately traverses the most recently pushed vertex. As a result, it will opt to traverse an entire path before returning to traverse down other children.

### the code: stack + doubly linked list method.

Too tired for this. Something about not pushing an element if it's already present in the stack or whatever. 

## djikstra's algorithm.

### the concept.

**Djikstra's algorithm** is essentially an adaptation of the shortest path algorithm to weighted graphs. It will find the minimum-weight path from vertex $s$ to all other vertices in the graph (sum of traversed edges is minimized).

- Create set $S$​ to store seen nodes.
- Create an array $D$ of length $V$ to store the distances from $s$ to all the other vertices.
  - Set all values in $D$ to be $\infty$, except $D[s]$ which is obviously $0$​.	
- Create a predecessor array $P$ of length $V$ where all values are `null`.
- While there exists a vertex $x$ with the smallest $D[x]$ that isn't in $S$:
  - Add it to $S$ (no infinite looping teehee).
  - For every neighbor vertex $y$ of $x$,
    - If $D[x] + 1 < D[y]$, we have found a new shortest path from $s$ to $y$!
      - Set $D[y] = D[x] + 1$ and set $P[y] = x$, as $x$ now precedes $y$​ in the path.

- All vertices are in $S$, so we have seen everything.

>Run Djikstra's algorithm from vertex $0$ on the following graph:
>
>```mermaid
>flowchart LR
>	0 --- 3
>	3 --- 6
>	4 --- 6
>	6 --- 7
>	7 --- 8
>	7 --- 4
>	8 --- 5
>	8 --- 4
>	4 --- 5
>	4 --- 1
>	4 --- 3
>	5 --- 2
>	2 --- 1
>	1 --- 0
>
>```
>
>Initialize our data structures: 
>$$
>\begin{align*}
>	S &= \{\} \\
>	D &= [0, \infty, \infty, \infty, \infty, \infty, \infty, \infty, \infty] \\
>	P &= [X, X, X, X, X, X, X, X, X]
>\end{align*}
>$$
>Smallest $D[x]$ not in $S$ when $x = 0$, we add it to $S$ and try minimizing neighbor distances.
>$$
>\begin{align*}
>	S &= \{0\} \\
>	D &= [0, 1, \infty, 1, \infty, \infty, \infty, \infty, \infty] \\
>	P &= [X, 0, X, 0, X, X, X, X, X]
>\end{align*}
>$$
>Smallest $D[x]$ not in $S$ when $x = 1$...
>$$
>\begin{align*}
>	S &= \{0, 1\} \\
>	D &= [0, 1, 2, 1, 2, \infty, \infty, \infty, \infty] \\
>	P &= [X, 0, 1, 0, 1, X, X, X, X]
>\end{align*}
>$$
>Smallest $D[x]$ not in $S$ when $x = 2$...
>$$
>\begin{align*}
>	S &= \{0, 1, 2\} \\
>	D &= [0, 1, 2, 1, 2, 3, \infty, \infty, \infty] \\
>	P &= [X, 0, 1, 0, 1, 2, X, X, X]
>\end{align*}
>$$
>Et cetera...

 	