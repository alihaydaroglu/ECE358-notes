#Quiz 1 Review: Introduction and Divide & Conquer Algorithms

##Introduction to Algorithm Analysis

Figuring out the **complexity** of algorithms, e.g. the amount of **resources** (time, memory) they use.

###Asymptotic Bounds
To compare functions, we use the concept of **asymptotic bounding**.  There are three notations we are going to be using, called Big-O, Theta and Omega. These are defined in the next three sections.

It should also be noted that this analysis can be run for different cases:
* **Average Case**: Expected value considering probability distribution over all inputs
* **Best case**: Minimum complexity over *all* possible inputs
* **Worst case**: Maximum complexity over the entire sample space.

####1. Big-O
$$f(n) \leq_f g(n)$$ or $$f(n) \in O(g(n))$$ implies that there exists $$n_0,c_0>0$$ such that for all $$n>n_0$$, we have $$0 \leq f(n) \leq c_0*g(n)$$.

In other words, $$g(n)$$ grows faster than $$f(n)$$. $$O(n)$$ gives the **upper bound**.

####2. Omega
$$f(n) \geq_f g(n)$$ or $$f(n) \in \Omega(g(n))$$ implies that there exists $$n_0,c_0>0$$ such that for all $$n>n_0$$, we have $$f(n) \geq c_0*g(n) \geq 0$$.

In other words, $$g(n)$$ grows slower than $$f(n)$$. $$\Omega(n)$$ gives the **lower bound**.

####3. Theta
$$f(n) =_f g(n)$$ or $$f(n) \in \Theta(g(n))$$ implies that there exists $$n_0,c_0, c_{ 1}>0$$ such that for all $$n>n_0$$, we have $$0 \leq c_0*g(n) \leq f(n) \leq c_2*g(n)$$.

In other words, $$g(n)$$ grows at the same speed as $$f(n)$$. $$\Theta(n)$$ gives the **tight bound**. To prove that a function is a tight bound, you prove that it is a lower bound *and* an upper bound at the same time.

##Divide and Conquer Algorithms
The idea is to break the problem apart into multiple sparts, and solve each recursively. Once solved, combine solutions to find overall solution.

Most typically, the problem is broken into two equal parts of size $$\frac{n}{2}$$. These are solved, and combined in linear time. The result is typically a complexity of $$n\log n$$, as opposed to the brute force result of $$n^2$$.

First, we talk a little bit about computing runtimes for these types of algorithms. Next, we give examples of a few.

###Computing Runtime
There are three methods of computing runtime for recursive functions.
####1. Recursion Tree
Basically brute-forcing it. Draw the breakdown of the recursive structure and calculate the amount of time spent on each level of the tree:
![quiz1_tree](/assets/quiz1_tree.jpg)
This sucks.
####2. Substitution/Induction
You have two options here: you can substitute the recursive structure to get the final running time, or you can make a guess and try to prove it inductively.

The first option of substituting the recursive structure looks like this:
![quiz1_subs](/assets/quiz1_subs.jpg)
The last line for the calculation for this specific function comes from the fact that there are $$\log n$$ calls to $$\Theta(n)$$.

The second option, after you have guessed a runtime of, say, $$n \log n$$ goes something like this:
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Base case: $$n=1, T(1) = 0$$
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Inductive hypothesis: $$T(n)=n\log n$$
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Goal: Show that $$T(2n) = 2n\log(2n)$$
The proof for the final step is this:
![quiz1_ind](/assets/quiz1_ind.JPG)

This method is alright.

####3. Master Theorem
Assuming recurrence relation is of form

$$
T(n) = aT(\frac{n}{b})+f(n)
$$

Where $$a\geq 1, b > 1$$, there may be three general cases, each with some math that will tell you what the answer is.

* **Case 1**: if $$f(n)=O(n^{\log_{b}{a}-\epsilon})$$, for some $$\epsilon > 0$$, then $$T(n) = \Theta(n^{log_{b}{a}})$$.
* **Case 2**: if $$f(n)=\Theta(n^{\log_{b}{a}})$$, for some $$\epsilon > 0$$, then $$T(n) = \Theta(n^{log_{b}{a}}\log n)$$.
* **Case 3**: if $$f(n)=\Omega(n^{\log_{b}{a}+\epsilon})$$, for some $$\epsilon > 0$$ then $$T(n) = \Theta(f(n))$$. There is an additional condition here: $$af(\frac{n}{b}) \leq cf(n)$$ for some constant $$c>1$$.

Sometimes, the Master Theorem doesn't solve your problem.

#####Exceptions to the Master Theorem

You can't use the Master Theorem if you don't have a polynomial difference between $$f(n)$$ and $$n^{\log_ba}$$. In other words, $$\frac {f(n)}{n^{\log_ba}} = n^ {\epsilon}$$ for some $$\epsilon > 0$$. Some exceptions include $$f(n)=n\log n, f(n)= \frac{n}{\log n}$$.

###Example 1: Mergesort
Divide array into two halves, recursively sort each half. Then merge two halves to make a sorted whole.

The merging of two arrays is done with a linear number of comparisons, so the recurrence relation will be $$T(n) = 2T(\frac{n}{2})+\Theta(n)$$. You can solve it.

###Example 2: Multiplication of Large Integers
####Attempt 1
Say you have two binary numbers, $$X$$ and $$Y$$ with n digits in arrays of size n. Set $$X_1$$ to be the most significant $$\frac n2$$ bits, and $$X_0$$ to be the least significant.

So, $$xy=2^nX_1Y_1 + 2^{\frac{n}{2}}X_1Y_0+2^{\frac{n}{2}}X_0Y_1+X_0Y_0$$

Implement this:

```python
def multiply (x,y): # arrays of size n
	if n = 1:
		return x*y
	else:
		# set arrays X_1, X_0, Y_1, Y_0
		p1 = multiply(X1, X0)
		p2 = multiply(X1, Y0)
		p3 = multiply(X0, Y1)
		p4 = Multiply(X0, Y0)

		return 2^n * p1 + 2^(n/2) * p2 + 2^(n/2) * p3 + p4
```

Apply master theorem to it:
$$
T(n) = 4T(\frac{n}{2})+\Theta(n)
$$
So, we have $$T(n) = O(n^2)$$.

####Attempt 2
$$
xy=2^nX_1Y_1+X_0Y_0+2^{\frac{n}{2}}((X_1+X_0)(Y_1+Y_0)-X_1Y_1-X_0Y_0)
$$

This way we can reduce the number of sub-problems. Now we have three subproblems, with size $$n/2+1$$

```python
def multiply2 (x,y):
    if n = 1:
        return x * y
    else
    	p1 = multiply(x1,y1)
        p2 = multiply(x1+x0,y1+y0)
        p3 = multiply(x0,y0)
    return 2^n * p1 + 2^(n/2) * (p2-p1-p3) + p3
```

$$T(n) = 3T(n/2)+\Theta(n)$$ and with master theorem we get $$T(n)=\Theta(n^{\log_2(3)})=\Theta(n^{1.58})$$.

###Example 3: Maximum Subarray Problem
Given an array `A`, try to find the indices `i,j` of A such that `A[i...j]` has the greatest possible sum.

The general idea is:
* Divide array into `A[low...mid]` and `A[mid+1...high]`
* Solve recursively for two subarrays
* Combine results by finding maximum subarray that crosses the midpoint and use the best solution of the three

When combining, you look at each subarray starting from the end that corresponds to the midpoint (where they were separated), iterate until the end of array, and find the point where the running sum is maximized. Then, add the running sums of both subarrays and compare with the results from each subarrays (without crossing).

The relation is $$T(n)=2T(n/2)+\Theta(n)$$, so $$T(n)=n \log n$$.

###Example 4: Closest pair of points
Given n points on a plane, find the pair with the smallest distance between them. The input will have a set of points $$P$$, a sorted list of x-coordinates $$P_x$$, a sorted list of y-coordinates $$P_y$$, with pointers from each list into the other. Assume no two points have the same x and y coordinate.

Steps are:
1. Using a vertical $$L$$ to split $$P$$ horizontally to have the rightmost and leftmost $$n/2$$ points separated.
2. Find closest pair in each side recursively (brute force if < 4 pairs)
3. Find closest pair with one point on each side
4. Return best of 3 solutions

```python
def closestPairRect(Px, Py):
    if |P| <= 3:
        find closest points by brute force
    else:
        m := x-coordinate of the midpoint in Px
        construct Rx, Ry, Qx, Qy
        #Rx and Ry are the x and y coordinates of the rightmost half points
        #Qx and Qy are the same for the leftmost

        (q0, q1) := closestPairRec(Qx, Qy)
        (r0, r1) := closestPairRec(Rx, Ry)
        delta = min{distance(q0,q1), distance(r0,r1)}

        Take the points in a 2*delta wide band between Q and R
        Order them by their y coordinates
        This constructs Sx and Sy

        for each s in Sy
            compute distance to next 11 points in the Sy list

        return closest of (q0,q1) or (r0,r1) or (s0,s1)
```

The relation is $$T(n) \leq 2T(\frac n2) + O(n) = \Theta(n \log n)$$, so by the master theorem $$T(n) = \Theta(n \log n)$$.

###Example 5: Selection
Take a list `A` and a rank `k` as input, and output the `k`th smallest element. If you sort and then return, it is $$O(n \log n)$$, but there is a faster way to do this.

```python
def kth_smallest(A, k):
    pick pivot element p
    partition A into B, [p], and C
        B = [elements less than p]
        C = [elements greater p]
    if k = |B| + 1
        return p
    if k < |B| + 1
        return kth_smallest(B, k)
    if k > |B| + 1
        return kth_smallest(B, k-|B|-1)
```

Size of recursive calls is not fixed - it depends on the pivot. We cannot apply master theorem. The cases are:
* **Worst-case pivot**: p is minimum or maximum element every time, so $$\Theta(n^2)$$ operations (from $$n + (n-1) + ... 1$$)
* **Best-case pivot**: p is median, so $$T(n)=T(\frac n2)+\Theta(n)$$. Solve to get $$T(n)=\Theta(n)$$
* **Average-case pivot**: On average, p is close to the median and it is still $$\Theta(n)$$.
