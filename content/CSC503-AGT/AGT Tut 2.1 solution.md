# Theorem: Degree Sum Equality in Bipartite Graphs

For a bipartite graph *$G = (V, E)$* with partite sets *$X$* and *$Y$* (where *$V = X \cup Y$* and *$X \cap Y = \emptyset$*), the sum of the degrees of vertices in *$X$* equals the sum of the degrees of vertices in *$Y$*:

$\sum_{x \in X} deg(x) = \sum_{y \in Y} deg(y)$

## Proof by Induction

We will use induction on the number of edges, *$m = |E|$*.

### **Base Case:** (*$m = 0$*)

If *$|E| = 0$*, the graph has no edges. Thus, all vertices have a degree of *$0$*. Therefore:

$\sum_{x \in X} deg(x) = 0 = \sum_{y \in Y} deg(y)$

The base case holds.

### **Inductive Hypothesis:**

Assume the theorem holds for any bipartite graph with *$k$* edges, where *$k \geq 0$*. That is, for a bipartite graph *$G = (V, E)$* with partite sets *$X$* and *$Y$*, and *$|E| = k$*:

$\sum_{x \in X} deg(x) = \sum_{y \in Y} deg(y)$

### **Inductive Step:**

We need to show that the theorem holds for a bipartite graph with *$k + 1$* edges.

Consider a bipartite graph *$G' = (V', E')$* with partite sets *$X'$* and *$Y'$*, and *$|E'| = k + 1$*.

Remove an arbitrary edge *$e = \{u, v\}$* from *$G'$*. Since *$G'$* is bipartite, one vertex of *$e$* must be in *$X'$* and the other in *$Y'$*. Without loss of generality, let *$u \in X'$* and *$v \in Y'$*.

This removal results in a new graph *$G = (V, E)$* where *$V = V'$*, *$X = X'$*, *$Y = Y'$*, and *$E = E' \setminus \{e\}$*, with *$|E| = k$*.

By the inductive hypothesis, for graph *$G$*:

$\sum_{x \in X} deg_G(x) = \sum_{y \in Y} deg_G(y)$

Now, add the edge *$e = \{u, v\}$* back to *$G$* to obtain the original graph *$G'$*. This increases the degree of *$u$* (in *$X' = X$*) by *1* and the degree of *$v$* (in *$Y' = Y$*) by *1*.

Therefore:

$\sum_{x \in X'} deg_{G'}(x) = \sum_{x \in X} deg_G(x) + 1$

and

$\sum_{y \in Y'} deg_{G'}(y) = \sum_{y \in Y} deg_G(y) + 1$

Combining these with the inductive hypothesis:

$\sum_{x \in X'} deg_{G'}(x) = \sum_{y \in Y'} deg_{G'}(y)$

Thus, the theorem holds for a bipartite graph with *$k + 1$* edges.

**Conclusion:**

By the principle of mathematical induction, the theorem holds for all finite bipartite graphs:

$\sum_{x \in X} deg(x) = \sum_{y \in Y} deg(y)$
