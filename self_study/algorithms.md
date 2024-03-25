# algorithms.

## maximum contiguous sum.	

### the problem.

Find the sum of the elements of a contiguous sub-list whose elements have the largest sum.

- The MCS of $[-9, 3, 1, 1, 4, -2, -8]$ would be the sum of $[3, 1, 1, 4]$ which is $9$.

I wrote out an $O(n^2)$ solution to the problem on my own, but my guess is that it is likely not the most optimal solution. My solution calculates a running sum starting at every index and repeatedly checks if that sum is the largest.

```python
def mcs(lst):
    maxSum = lst[0]
    for i in range(len(lst)):
        currSum = 0
        for j in range(i, len(lst), 1):
            currSum += lst[j]
            maxSum = max(maxSum, currSum)

    return maxSum

print(mcs([-9, 3, 1, 1, 4, -2, -8]) == 9) # True
```

### "extreme" brute force approach.

This method is very overkill, but does the job, albeit with a worst-case time complexity is $O(n^3)$.

```py
def mcs(lst):
    maxSum = lst[0]
    for i in range(len(lst)):
        for j in range(i, len(lst)):
            currSum = 0
            for k in range(i, j + 1):
                currSum += lst[k]
            maxSum = max(maxSum, currSum)
	return maxSum

print(mcs([-9, 3, 1, 1, 4, -2, -8]) == 9) # True
```

Technically, this method does what I did: checking each individual sum. The only difference is that I repeatedly add to a running sum rather than recalculating the entire sum every time. 

### "refined" brute force approach.

Turns out that this method is exactly what I did originally, so refer to the code for that. It has a worst-case time complexity of $O(n^2)$.

### divide-and-conquer approach.

The idea is that we can find the sum recursively. Imagine we repeatedly cut our list in half and find the maximum contiguous sum on each side. In addition, it needs to account for a "straddling sum," or the largest subarray that crosses the halfway point. I tried to write something out on my own, and it seemed to get the test case correct. 

```python
def mcs(lst):
	def split(left, right):
        if left == right: 
            return lst[left]
    	
        midpoint = (left + right) // 2
        
        # find maximum half sums
        lSplit = split(left, midpoint)
        rSplit = split(midpoint + 1, right)
        
        # straddling sums (that reach over the half)
        lMax, lSum = lst[midpoint], 0
        for i in range(midpoint, left - 1, -1):
        	lSum += lst[i]
            lMax = max(lMax, lSum)
            
        rMax, rSum = lst[midpoint + 1], 0
        for j in range(midpoint + 1, right - 1):
        	rSum += lst[j]
            rMax = max(rMax, rSum)
        
        return max(lSplit, rSplit, lMax + rMax)
	
    return split(0, len(lst) - 1) 

print(mcs([-9, 3, 1, 1, 4, -2, -8]) == 9) # True
```

Let's see if we can figure out the time complexity by writing out some of the recursion depths for a list of length $n$. We'll use a constant $c$ to represent $n$-proportional computations being done at each recursion level.

- **Depth 0:** There is 1 list of length $n$, so we need $cn$ time.
- **Depth 1:** There are two lists of length $\frac{n}{2}$, so we need $2c(\frac{n}{2}) = cn$ time.
- **Depth 2:** There are four lists of length $\frac{n}{4}$, so we need $4c(\frac{n}{4}) = cn$ time.
- $...$

Given $d$ depths of recursion, we can deduce that the total time required is $d(cn)$. Note that $2^d = n$, because we need enough depths to accommodate $n$ lists, each of size $1$, at the lowest depth. Rearrange to find $d = \lg n$. A little substitution yields us $d(cn) = cn \lg n = O(n \lg n)$ as the worst-case time complexity for this algorithm.

### kadane's algorithm.

Kadane observed that within a list, the MCS from index $0$ to $i$, inclusive is one of the following:

- The MCS from $0$ to $i - 1$ plus the value at position $i$.
- Or, just the value at position $i$.

Let's look at a more concrete example with the list $[-9, 3, 1, 1, 4, -2, -8]$.

- Say we're looking at index $1$ (where the $3$ is). Kadane's observation states that there are two possible options for the MCS from index $0$ to $1$ (inclusive).
  - Option 1: The MCS from $0$ to $0$ plus the value at position $i$. In our case, that would be $-9 + 3 = -6$.
  - Option 2: The value at position $1$, or $3$.
  - Since $3 > -6$, the running MCS from index $0$ and $1$, inclusive, is just $3$.

Repeatedly applying and storing this observation as we iterate through the list will allow us to efficiently find the maximum MCS of the entire list.

```python
def mcs(lst):
    maxOverall = lst[0]
    maxUpToI = lst[0]
    
    for i in range(1, len(lst)):
        maxUpToI = max(maxUpToI + lst[i], lst[i]) # the key observation
        maxOverall = max(maxUpToI, maxOverall) # updating the current largest MCS
        
    return maxOverall 
```

Since there's just one loop iterating over $n$ items of our list, the worst-case time complexity is $O(n)$, making this our most time-optimized algorithm to solve this problem.

## bubble sort.

### how it works.

Iterate through the list, from left to right, and swap elements that are out of order. If we perform this iteration once, we know that the last entry is in the correct place. Doing it again will ensure the second to last entry is in place, and so on and so forth. The idea is that the larger elements *bubble up* into their respective positions. Essentially, we perform $n$ iterations over at most $n$ elements, resulting in a time complexity of $O(n^2)$. As an example, I'll perform bubble sort to re-order the list $[2, 9, 8, 5, 1]$ to be ascending. 

**Iteration 1:**

- $2 < 9$, so no swap needed.
- $9 > 8$, so we swap, resulting in $[2, 8, 9, 5, 1]$.
- $9 > 5$, so we swap, resulting in $[2, 8, 5, 9, 1]$.
- $9 > 1$, so we swap, resulting in $[2, 8, 5, 1, 9]$.

Notice that one iteration only guarantees that the last element is correctly placed. We can't assume that any of the other elements are also placed in the correct positions. This is why we need $n$ iterations.

**Iteration 2:** our list currently looks like $[2, 8, 5, 1, 9]$.

- $2 < 8$, so no swap needed.
- $8 > 5$, so we swap, resulting in $[2, 5, 8, 1, 9]$.
- $8 > 1$, so we swap, resulting in $[2, 5, 1, 8, 9]$.

**And so on...**

Now, we have correctly placed the last $2$ elements. The pattern from here is to continue iterating in the same manner, until we have correctly placed the last $n$ elements, i.e. sorted the entire list to become $[1, 2, 5, 8, 9]$.

### an implementation.

Based on my understanding of the sort from above, I've written an implementation.

```python
def bubble(lst):
    for i in range(len(lst)):
        for j in range(len(lst) - 1 - i):
            if lst[j + 1] < lst[j]: # if out of order...
                lst[j], lst[j + 1] = lst[j + 1], lst[j] # swap the two
            
a = [2, 9, 8, 5, 1]
bubble(a) # modifies array in-place
print(a) # [1, 2, 5, 8, 9]
```

Writing out the algorithm, it's a lot easier to see why the worst-case time complexity is $O(n^2)$. 

### notes on the algorithm.

Bubble sort will sort from right to left. So if we stop a sort early, we can assume that between some index and the end, the list is sorted.

Notice that the auxiliary space of the algorithm is $O(1)$, as we are not storing anything besides indices and swap variable, neither of which grow with input size. Bubble sort also modifies the list **in-place**, as opposed to creating a new sorted list. 

Another note is that bubble sort is a **stable** sorting algorithm. A stable sort maintains the relative order of equivalent elements. To understand what that means, let's perform bubble sort on the list $[4, 2, 3, 2]$. Solely for the purposes of distinguishing between the two $2$s, I'll put a subscript on them, but their values are the exact same.

**Iteration 1:** for the list $[4, 2_1, 3, 2_2]$:

- $4 > 2_1$, so we swap, resulting in $[2_1, 4, 3, 2_2]$.
- $4 > 3$, so we swap, resulting in $[2_1, 3, 4, 2_2]$.
- $4 > 2_2$, so we swap, resulting in $[2_1, 3, 2_2, 4]$.

**Iteration 2:**

- $2_1 < 3$, so no swap needed.
- $3 > 2_2$, so we swap, resulting in $[2_1, 2_2, 3, 4]$.

**Iteration 3:**

- $2_1 = 2_2$, so no swap needed. 

Our final, sorted list is $[2_1, 2_2, 3, 4]$. Notice that because bubble sort is **stable**, $2_2$ still is positioned after $2_1$. 

Stability of a sorting algorithm has real-world ramifications. Let's say we're sorting a `User[]` list by one feature, `User.age`. A stable sort would ensure that users of same ages remain in the same relative order as before the sort. What if `User.name` was already sorted alphabetically? We might want to ensure that the alphabetical ordering remains the intact among users with the same ages.

## selection sort.

### how it works.

It *selects* the smallest entry, and positions it at the front. Clearly, doing this once will only sort one of the elements, so we will need to perform this selection process $n$ times to sort all $n$ elements. Let's try sorting $[2, 9, 8, 5, 1]$ with selection sort. 

**Selection 1:** the smallest element in $[2, 9, 8, 5, 1]$ is $1$. 

- We want to place $1$ at index $0$.

- We swap $1$ with $2$, resulting in $[1_f, 9, 8, 5, 2]$.
- The first element has been placed, so we now only worry about the rest of the list.

Remember, we're excluding the already sorted ($f$-subscripted) elements, so our window of selection shrinks every time.

**Selection 2:** the smallest element in the window $[9, 8, 5, 2]$ is $2$. 

- We want to place $2$ at the front.
- We swap $2$ with $9$, resulting in $[1_f, 2_f, 8, 5, 9]$.

**Selection 3:** the smallest element in the window $[8, 5, 9]$ is $5$.

- We want to place $5$ at the front.
- We swap $5$ with $8$, resulting in $[1_f, 2_f, 5_f, 8, 9]$.

**Selection 4:** the smallest element in the window $[8, 9]$ is $8$.

- $8$ is already at the front.
- No swap needed, resulting in $[1_f, 2_f, 5_f, 8_f, 9]$.

Since there's only one element left in our window of $[9]$, we know it is placed correctly and have sorted our list to be: $[1, 2, 5, 8, 9]$.

### an implementation.

Based on the example sort I worked out above, I implemented selection sort.

```python
def selection(lst):
    for i in range(len(lst) - 1):
        smallestVal = lst[i]
        smallestInd = i
        for j in range(i, len(lst)): # find smallest value in window
        	if lst[j] < smallestVal:
                smallestVal = lst[j]
                smallestInd = j
        
        # swap smallest and leftmost values
        lst[i], lst[smallestInd] = lst[smallestInd], lst[i]

a = [2, 9, 8, 5, 1]
selection(a) # modifies array in-place
print(a) # [1, 2, 5, 8, 9]
```

Looking over the implementation code, it's pretty easy to deduce the worst-case time complexity of $O(n^2)$. We have one loop that runs $n$ times over the entire list. Within each iteration, we have another loop to determine the smallest subsequent value that runs at most $n$ times. 

### notes on the algorithm.

Selection sort will sort from left to right. So if we stop a sort early, we can assume that between the start and some index, the list is sorted.

Just like bubble sort, selection sort has an $O(1)$ space complexity. However, a key difference is that selection sort is **not stable**. In the process of swapping the smallest and leftmost elements, relative orders of equivalent elements can be lost, such as with $[5, 2, 3, 5, 1]$.

**Selection 1:** the smallest element in $[5_1, 2, 3, 5_2, 1]$ is $1$.

- We want to place $1$ at the front.
- We swap $1$ with $5_1$, resulting in $[1_f, 2, 3, 5_2, 5_1]$.

Already, we can see that $5_2$ is now positioned in front of $5_1$, making selection sort **unstable**.

## insertion sort.

### how it works.

Iterate across a list, until we encounter an element that is out of order, i.e. smaller than the ones before. If this element is found, we shift previous elements to the right until the out-of-order element is correctly placed. We do this until all $n$ elements are in the correct place. Let's take the example list of $[2, 9, 8, 5, 1]$.

**Index 0 $[2, 9, 8, 5, 1]$:** $2$ is the leftmost element.

- No swaps needed.

**Index 1 $[2, 9, 8, 5, 1]$:** $9 > 2$, which is to the left.

- No swaps needed.

**Index 2 $[2, 9, 8, 5, 1]$:** $8 < 9$, which is to the left.

- $8 < 9$, so we swap, resulting in $[2, 8, 9, 5, 1]$.
- $8 > 2$, so no swap needed.

**Index 3 $[2, 8, 9, 5, 1]$:** $5 < 9$, which is to the left.

- $5 < 9$, so we swap, resulting in $[2, 8, 5, 9, 1]$.
- $5 < 8$, so we swap, resulting in $[2, 5, 8, 9, 1]$.
- $5 > 2$, so no swap needed.

**Index 4 $[2, 5, 8, 9, 1]$:** $1 < 9$, which is to the left.

- $1 < 9$, so we swap, resulting in $[2,5,8,1,9]$.
- $1 < 8$, so we swap, resulting in $[2,5,1,8,9]$.
- $1 < 5$, so we swap, resulting in $[2,1,5,8,9]$.
- $1 < 2$, so we swap, resulting in $[1,2,5,8,9]$.
- $1$ is the leftmost element.

### an implementation.

Based on the example above and my intuition, I have implemented insertion sort.

```python
def insertion(lst):
    for i in range(len(lst)):
        el = lst[i]
        j = i - 1
        
        # shift any larger elements forward
        while j >= 0 and lst[j] > el:
            lst[j + 1] = lst[j]
            j -= 1
            
        # place current element before larger elements
        lst[j + 1] = el
		

a = [2, 9, 8, 5, 1]
insertion(a) # modifies array in-place
print(a) # [1, 2, 5, 8, 9]
```

The outer loop runs exactly $n$ times, once to place each element. The inner loop will run at most $n$ times. We can deduce the worst-case time complexity to be $O(n^2)$.

### notes on the algorithm.

As with both bubble and selection sort, this algorithm sorts **in-place** and has an auxiliary space of $O(1)$.

Insertion sort is **stable**, as equal elements never get swapped out of their initial relative orders.

Another thing to note is that if the sort is stopped mid-way, we have no guarantee that the start or end is sorted absolutely. However, we do now that the starting elements are ordered correctly amongst themselves, but there could be values missing from them.

## binary search.

### how it works.

Given a sorted list $A$ and a target value $T$, the binary search returns the index of $A$ where $T$ is located. (Or, return $-1$ if $T$ does not exist in $A$.)

To do so, it checks the middle element of $A$.

- If the middle element is equal to $T$, congratulations! We've found our position.
- If the middle element is greater than $T$, retry in the lower half of $A$.
- If the middle element is less than $T$, retry in the upper half of $A$.

By narrowing down the search space by $\frac{1}{2}$ every iteration, binary search achieves a $O(\lg n)$ worst-case time complexity, as opposed to the $O(n)$ linear search algorithm.

Let's try an example: use binary search to find the index of $6$ in $[1, 2, 6, 7, 9, 14, 24]$.

**Search 1:** Our search space is the whole list. The middle element is $7$ at position $3$.

- $6 < 7$, so we narrow our search space to the sub-list $[1, 2, 6]$.

**Search 2:** Our search space is $[1, 2, 6]$. The middle element is $2$ at position $1$.

-  $6 > 2$, so we narrow our search space to $[6]$.

**Search 3:** Our search space is $[6]$. The middle element is $6$ at position $2$.

- Success! We've found the element $6$ at index $2$ of the original list.

### an implementation.

I have attempted to implement binary search recursively based on the above description.

```python
def binary_search(lst, target):
    def search(lst, target, low, high):
        if low > high: # element doesn't exist in list
        	return -1
        
        mid = (low + high) // 2
        
        if lst[mid] == target:
            return mid
        elif lst[mid] > target: # too high
            return search(lst, target, low, mid - 1)
        else: # too low
			return search(lst, target, mid + 1, high)
    
    return search(lst, target, 0, len(lst) - 1)
```

Since the `search` function halves the search sub-list's length upon every search, we can see that doubling the length of the initial list would require at most one more search.

In other words, $2^s = n$, where $s$ is the number of searches and $n$ is the length of the list. Rearranging, we find that $s = \lg n$, so our function's worst-case time complexity is $O(\lg n)$.

## big notation.

### upper bound ~ big $O$.

We know that $f(x) = O(g(x))$ if $\exists (C > 0, x_0 > 0)$ such that if $x \geq x_0$, then $f(x) \leq Cg(x)$. In other words, $Cg(x)$ is an upper bound for $f(x)$ as $x$ approaches $\infin$​.

Using the limit theorem, we know that $f(x) = O(g(x))$ if $\lim_{x \rightarrow \infin} \frac{f(x)}{g(x)} \neq \infin$.

**Show** that $f(x) = 50x^{100} = O(3^x)$.

- Even visually, it's clear that this may be a bit hard to prove with the definition itself. Let's try using the limit theorem:
  $$
  \begin{equation}
  \begin{split}
  \lim_{x \rightarrow \infin} \frac{f(x)}{g(x)} 
  &= \lim_{x \rightarrow \infin} \frac{50(100)x^{99}}{\ln 3(3^x)} \\ 
  &= \lim_{x \rightarrow \infin} \frac{50(100)(99)x^{98}}{(\ln 3)^2(3^x)}  \\ 
  &= \text{ ...} \\ 
  &= \lim_{x \rightarrow \infin} \frac{50(100!)}{(\ln 3)^{100}(3^x)} \\
  &= 0 \neq \infin
  \end{split}
  \end{equation}
  $$
  Note that the repeated simplifications are a result of L'Hopital's rule. But as a result, we can say that $f(x) = O(3^x)$ by the limit theorem.

  $\blacksquare$

### lower bound ~ big $\Omega$.

We know that $f(x) = \Omega(g(x))$ if $\exists (B > 0, x_0 \geq 0)$ such that if $x \geq x_0$ then $f(x) \geq Bg(x)$. In other words, $Bg(x)$ is a lower bound for $f(x)$ as $x$ approaches $\infin$.

Using the limit theorem, we know that $f(x) = O(g(x))$ if $\lim_{x \rightarrow \infin} \frac{f(x)}{g(x)} \neq 0$.

### "tight" bound ~ big $\Theta$​​.

We know that $f(x) = \Theta(g(x))$ if $\exists(B > 0, C > 0, x_0 \geq 0)$ such that if $x \geq x_0$, then $Bg(x) \leq f(x) \leq Cg(x)$​.

Using the limit theorem, we know that $f(x) = O(g(x))$ if $\lim_{x \rightarrow \infin} \frac{f(x)}{g(x)} \neq 0, \infin$. This makes sense, as if something is a tight bound, it is also both a lower and upper bound.

The best constraint, known as a tight bound. Often hard to find!

**Note** that if $f(x) = \Theta(g(x))$, then $f(x) = \Omega(g(x))$ and $f(x) = O(g(x))$​ as well!

**Show** that $f(x) = 10x \lg x + x^2 = \Theta(x^2)$​.

- We first want to show $f(x) = O(x^2)$. Since $x > \lg x$, we know that $10x^2 + x^2 = 11x^2 > f(x)$​. Let $g(x) = x^2$ and $C = 11$. 

  It follows that $f(x) \leq Cg(x)$ so $f(x) = O(x^2)$.

  Next, we want to show that $f(x) = \Omega(x^2)$. Since $10x \lg x > 0$, we know that $f(x) = 10x \lg x + x^2 > x^2$. Let $g(x) = x^2$ and $B = 1$.

  It follows that $f(x) \geq Bg(x)$ so $f(x) = \Omega(x^2)$.

  Since $f(x) = O(x^2)$ and $f(x) = \Omega(x^2)$, we know that $f(x) = \Theta(x^2)$. 

  $\blacksquare$​

