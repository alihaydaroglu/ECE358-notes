#Greedy Algorithms

**Definition**: greedy algorithms choose the best solution locally, so *myopic* decisions. Choosing a local optimum at each step, hoping you end up with a global optimum.

**Example**: *Dijkstra's Shortest Path* algorithm. Though, it does assume that the weights are positive.

##Greedy vs Divide-and-Conquer Algorithms
* It is easy to propose a greedy algorithm
* It is easy to analyze runtime
* It is hard to establish correctness

##Example: Activity Scheduling
There are a few approaches:
* **earliest start time**: does not work
* **earliest finishing time**: works
* **shortest interval** does not work
* **fewest conflicts** does not work

Check slides for counterexamples.

###Earliest Finish Time
```
sort jobs by finish times, lowest to highest
A < O
for j = 1 to n
    if job j compatible with A
        A += j
return A
```
This is done in $$O(n\log n)$$.

## General technique for proving correctness
Generally use induction.

Assume $$S_0, S_1,...S_n$$ are partial solutions from a greedy algorithm.
*

Say $$S_i$$ is **promising** if there is some optimal solution $$S'_i$$ that extends $$S_i$$ using only activities from $${i+1, ...,n}$$. Note that $$S'_i$$ does not have to be unique. Intuitively, it means that you can keep going from $$S_i$$ and reach some optimal solution.

Prove that "$$S_i$$ is promising" is a **loop invariant** (true at the end of every iteration of the loop). Use induction to prove it.

###Correctness of Activity Scheduling
Use base case, inductive hypotheses and inductive step to prove that it is correct.

Did not understand anything from her proof.

Something about an **exchange lemma**. It is typically used to prove the correctness of greedy algorithms.
