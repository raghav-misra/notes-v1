# cmsc351 / exam02

## insertion sort.

**Splits list into sorted and unsorted parts.** Keeps adding one unsorted element (from the right) into the sorted part (on the left) until the whole list is sorted.

Iterate across a list, until we encounter an element that is out of order, i.e. smaller than the ones before. If this element is found, we shift previous elements to the right until the out-of-order element is correctly placed. We do this until all $n$ elements are in the correct place. Let's take the example list of $[2, 9, 8, 5, 1]$​.

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

## binary search.

**Efficiently searches a sorted list.** Given a sorted list $A$ and a target value $T$, the binary search returns the index of $A$ where $T$ is located. (Or, return $-1$ if $T$ does not exist in $A$.)

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

## recurrence relations.

A **recurrence relation** is basically just a recursive equation lol. We will often want to find a closed form or big theta-bound for a recurrence. There are multiple ways we can do this.

### digging down.

Let's find a closed form/explicit formula for the following recurrence:
$$
T(n) = 2T(\frac{n}{2}) + \frac{1}{2}n, \text{where } T(1) = 7
$$
We basically want to keep substituting:
$$
\begin{align*}
T(n) 
&= 2T(\frac{n}{2}) + \frac{1}{2}n \\
&= 2\left[2T(\frac{n}{4})  + \frac{1}{2}(\frac{n}{2})\right] + \frac{1}{2}n \\
&= 2\left[2\left[2T(\frac{n}{8}) + \frac{1}{2}(\frac{n}{4})\right]  + \frac{1}{2}(\frac{n}{2})\right] + \frac{1}{2}n \\
&= 8T(\frac{n}{8}) + \frac{3n}{2} \\ 
&= \dots
\end{align*}
$$
This process of expansion will occur $k$ times, until $2^k = n$, when $T(1)$ will resolve to $7$. When the digging down process stops, $k = \lg n$:
$$
\begin{align*}
T(n) &= 2^kT(\frac{n}{2^k}) + \frac{kn}{2} \\
&= 2^{\lg n} T(\frac{n}{n}) + \frac{1}{2}n \lg n \\
&= 7n + \frac{1}{2}n \lg n
\end{align*}
$$
**Steps for digging down:**

1. Express $T(n)$ in terms of $k$, where $k$ is the level of recursion.
2. Find the value of $k$​ when the recursive call can be simplified to the base case. 
3. Plug that value in for $k$ and simplify, i.e. replace the recursive call with the base case.

Another example,
$$
T(n) = 4T(\frac{n}{3}) + 5n^2, \text{where } T(1) = 5
$$
Do stuff:
$$
\begin{align*}
T(n) &= 4T(\frac{n}{3}) + 5n^2 \\
&= 4\left[4T(\frac{n}{9}) + 5(\frac{n}{3})^2\right] + 5n^2 \\
&= 16T(\frac{n}{9}) + \frac{5n^2}{9} + 5n^2 \\
&= 16T(\frac{n}{9}) + \frac{50n^2}{9} \\
&= 16\left[4T(\frac{n}{27})+5(\frac{n}{9})^2\right] + \frac{50n^2}{9} \\
&= 64T(\frac{n}{27}) + \frac{5n^2}{81} + \frac{50n^2}{9} \\
&= 64T(\frac{n}{27}) + \frac{455n^2}{81}
\end{align*}
$$
From the above expanding behavior, let's find a relation that involves a $k$:
$$
T(n) = 4^kT(\frac{n}{3^k}) + \sum_{i = 0}^{k} \frac{5n^2}{3^k}
$$
Plugging in $k = \log_3 n$:
$$
T(n) = 5(4^{\log_3 n}) + 5n^2\sum_{i = 0}^{k} \frac{1}{3^i}
$$


## recurrence trees.

## master theorem.

## merge sort.

## heaps.

## heap sort.

## quick sort.



