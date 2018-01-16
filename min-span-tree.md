#Minimum Spanning Tree - Greedy Algorithm
##Review and Definitions
For **undirected graphs**:
* **Connected**: there is a path between any two vertices
* **Acyclic**: there is no cycle
* **Spanning tree**: subset of edges that forms a tree (is connected and acylcic).

Properties for any spanning tree $$T$$ of graph $$G = (V,E)$$:
* $$T$$ contains $$n-1$$ edges where $$n=|V|= $$ number of vertices.
* Removing any edge from $$T$$ disconnects it into two disjoint subtrees
* Adding any edge to T creates one cycle

So, the **Minimum Spanning Tree Problem** is :
* **input**: connected, undirected weighted graph $$G$$ with weights on the edges
* **output**: spanning tree $$T$$ with smallest  total weight

Brute force running time for the problem is $$\Omega(2^m)$$, even when limiting the search to spanning trees.

Some more definitions:
* `Cut(S,V-S)`: partition the graph vertices to $$S$$, $$V-S$$
* **Cross edges**: any edge with vertex in $$S$$ and another vertex in $$V-S$$.
* **Light edge**: a cross edge with the minimum weight.

## Prim's Algorithm
```
start from some arbitrary vertex r, root
X = {r}; T = {}
    while X != V:
        choose edge e = (x,y) with x in X, y in V-X, and smallest weight among all such edges
        T = T + {e}
        X = X + {y}
return T
```
Running time of this algorithm is $$O(m\log m)=O(m\log n)$$ where $$m=|E|$$ and $$n=|V|$$. Using a heap to implement a priority queue to keep track of edges and select next one.

## Kruscal's Algorithm
```
sort edges by nondecreasing weight
T = {}
for i = 1...m
    If endpoints of e_i are not already connected by edges in T
        T = T + e_i
return T
```
Running time is $$O(m\log n)$$ using sophisticated **union/find** data structure to keep track of connected components.
