#Min Spanning Tree Again

This is lec-03-01 on the website. It's kind of a repeat of [the previous lecture](/min-span-tree.md).

##Graphs Review
You can use and **adjacency matrix** or an **adjacency list** (or a list of edges per each vertex) to store the graph. For sparse graphs, the latter is more space efficient. Space complexity of matrix is $$\Theta(|V|^2)$$, and for the list it is $$\Theta(|V|+|E|)$$.

For an edge query (to see if two nodes $$v_i,v_j$$ are connected with an edge), the matrix is $$O(1)$$ while the list is $$O(|A[i]|)$$

##Generic MST Algorithm
Here's a generic one:
```
A = {}
while A does not form a min-spanning-tree
    find a promising edge e
    A = A + e
return A
```
We want it to be **loop invariant**. We want to use the standard approach of proving the correctness of greedy algorithms to prove the correctness of this generic MST algorithm.

##Correctness of MST
**Theorem**: greedy approach which selects light edges iteratively works for MST problem. Prove by induction.

##Prim's Algorithm
Implements the generic algorithm.

Start with a single node, add the edge that is the minimum cost of all edges that connect your tree with a node that is not inside the tree.

It makes the tree connected.

##Kruskal's Algorithm
Pick the smallest edge as long as it doesn't make a cycle. Resulting tree is not necessarily connected.
