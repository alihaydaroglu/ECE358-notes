#Lecture 5
##Example 5: Selection
Last example of *Divide and Conquer* algorithms.

**Input**: list `A`, rank `k`.
**Output**: k-th smallest element in `A`.

The most obvious solution is to sort and return the $$k^{th}$$ element. In this case, the time complexity is $$O(n\log n)$$. For special cases, like $$k=1$$, the complexity can be less, like $$O(n)$$. A better algorithm would do this without having to sort the whole thing. Let's find a divide-and-conquer solution.

**The idea**: take some element, and in linear time, compare all elements with the selected element. If the number of elements smaller than the chosen element is equal to $$k-1$$, then we have found the answer. This is kind of like **Quicksort**, where the chosen element is the *pivot*.

```python
def kth_smallest_in_A():
    pick pivot element p;
        partition A into B = [elements < p]; p; C = [elements > p]
        if k = |B| + 1;
            return B
        if k < |B| + 1
            return k-th smallest in B
        if k > |B| + 1
            return (k-|B|-1)-th smallest in C
```
###Complexity
Size of recursive calls is not fixed, it depends on pivot, so Master Theorem does not apply.

* **Worst-case pivot**: p is the mainimum or maximum, so algorithm performs $$\Theta(n^2)$$ operations $$(n + (n-1)+...+1)$$
* **Best-case pivot**: p is median, so recurrence has the form $$T(1)=\Theta(1)$$. So, $$T(n) = T(\frac{n}{2})+\Theta(n)$$ for $$n > 1$$.
* **Average case**: more difficult to analyze, on average $$p$$ will be close to the median, and runtime is still $$\Theta(n)$$.

The input cannot be assumed to be truly *random*. So, use randomized algorithm:
* Pick pivot element uniformly at random from list
* Behaviour of algorihtm varies from run to run, but worst-case runtime is expected to be close to $$\Theta(n)$$ on average.
