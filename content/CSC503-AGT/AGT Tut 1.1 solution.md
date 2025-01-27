# Handshaking Lemma: Proof by Induction

## Theorem

For any finite graph *$G = (V, E)$*, the sum of the degrees of all vertices is equal to twice the number of edges:

$\sum_{v \in V} deg(v) = 2|E|$

## Proof by Induction

We will use induction on the number of edges, *$m = |E|$*.

### **Base Case:** (*$m = 0$*)

If *$|E| = 0$*, then the graph has no edges. Therefore, all vertices have a degree of *$0$*. Thus:

$\sum_{v \in V} deg(v) = 0 = 2 \cdot 0 = 2|E|$

The base case holds.

### **Inductive Hypothesis:**

Assume the theorem holds for any graph with *$k$* edges, where *$k \geq 0$*. That is, for a graph *$G = (V, E)$* with *$|E| = k$*:

$\sum_{v \in V} deg(v) = 2k$

### **Inductive Step:**

We need to show that the theorem holds for a graph with *$k + 1$* edges.

Consider a graph *$G' = (V', E')$* with *$|E'| = k + 1$*.

Remove an arbitrary edge *$e = \{u, v\}$* from *$G'$*. This results in a new graph *$G = (V, E)$* where *$V = V'$* and *$E = E' \setminus \{e\}$*, with *$|E| = k$*.

By the inductive hypothesis, for graph *$G$*:

$\sum_{v \in V} deg_G(v) = 2k$

Now, add the edge *$e = \{u, v\}$* back to *$G$* to obtain the original graph *$G'$*.

*   If *$u \neq v$*, then *$deg_{G'}(u) = deg_G(u) + 1$* and *$deg_{G'}(v) = deg_G(v) + 1$*. For all other vertices *$x$*, *$deg_{G'}(x) = deg_G(x)$*.
*   If *$u = v$* (loop), then *$deg_{G'}(u) = deg_G(u) + 2$*.

In either case, the sum of degrees in *$G'$* increases by *$2$* compared to *$G$*.

Therefore:

$\sum_{v \in V'} deg_{G'}(v) = \sum_{v \in V} deg_G(v) + 2 = 2k + 2 = 2(k + 1) = 2|E'|$

Thus, the theorem holds for a graph with *$k + 1$* edges.

### **Conclusion:**

By the principle of mathematical induction, the Handshaking Lemma holds for all finite graphs:

$\sum_{v \in V} deg(v) = 2|E|$
