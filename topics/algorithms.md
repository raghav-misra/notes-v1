# algorithms.

## hello.

Self-studying **CMSC351** Algorithms before I actually take the course in a few weeks using Prof. Justin Wyss-Gallifent's lectures from spring 2021. The recordings are visible to all UMD students [here](https://umd.instructure.com/courses/1302400/external_tools/28827).

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

This method is very overkill, but does the job. I believe its time complexity is $O(n^3)$.

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

Turns out that this method is exactly what I did originally, so refer to the code for that. It has a time complexity of $O(n^2)$.

### divide-and-conquer approach.

The idea is that we can find the sum recursively. Imagine we repeatedly cut our list in half and find the maximum contiguous sum on each side. I tried to write something out on my own, and it seemed to get the test case correct. 

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

Given $d$ depths of recursion, we can deduce that the total time required is $d(cn)$. Note that $2^d = n$, because we need enough depths to accommodate $n$ lists, each of size $1$, at the lowest depth. Rearrange to find $d = \lg n$. A little substitution yields us $d(cn) = cn \lg n = O(n \lg n)$ as the time complexity for this algorithm.

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

Since there's just one loop iterating over $n$ items of our list, the time complexity is $O(n)$, making this our most time-optimized algorithm to solve this problem.

