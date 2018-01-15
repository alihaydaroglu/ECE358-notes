



# Lecture 2

Do the problems that are handed out to review the O(n) stuff.

## Divide and Conquer

Break up problem into smaller sub-problems, and solve them

Complexity of
$$
n\log(n)
$$

### Example: Mergesort

Divide into two halves, recursively sort two halves. Merge two halves to make sorted whole.

### Computing Recursive running Time

#### 1. Recursion Tree

Draw the breakdown of the recursive structure and calculate the amount of time spent on each level of the tree.

#### 2. Substitution/Induction Method

If you have a guess, you can use induction?

- Substitute the recursive structure to get the final runtime
- OR, guess the runtime and prove by induction

Proof with induction:

```
Base Case =: n = 1
Inductive Hypothesis: T(n) = nlogn
Goal: Show that T(2n) = 2nlogn(2n)
```

Expanded version of induction method:
$$
T(2n) = 2T(n) + 2n = 2n \log(n) + 2n = 2n(\log(2n)-1)+2n=2n\log(2n)
$$


Using the method of substitution:
$$
T(n) = 2T(\frac{N}{2}) + \theta(n) = 2( 2T(\frac{n}{4}) + \theta(\frac{n}{2}))= (...)
$$
Solve the recurrence with the above substitution.

#### 3. Master Theorem

Assuming recurrence relation is of form
$$
T(n) = aT(\frac{n}{b})+f(n)
$$
Where a>=1, b > 1, there may be three general cases, each with some math that will tell you what the answer is.
