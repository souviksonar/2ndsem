> [!PDF|255, 208, 0] [[agt 3.pdf#page=7&annotation=3568R|p.7]] #defintion
> > - An **Euler path** in a graph $G$ is a simple path containing every edge in $G$. 
> > - An **Euler circuit** (or **Euler cycle**) is a cycle which is an Euler path. 
> > 
> > NOTE: The definition applies both to undirected as well as directed graphs of all types.

> [!PDF|255, 208, 0] [[agt 3.pdf#page=10&annotation=3571R|p.10]] #defintion 
> > - A  **Hamilton path**  in a graph  $G$  is a path which visits ever vertex in  $G$  exactly once. 
> > - A  **Hamilton circuit**  (or  **Hamilton cycle**) is a cycle which visits every vertex exactly once,  except for the first vertex, which is also visited at the end of the cycle. 
> > 
> >NOTE: Again, the definition applies both to undirected as well as directed graphs of all types.

> [!PDF|255, 208, 0] [[agt 3.pdf#page=12&annotation=3574R|p.12]] #statement
> > - Finding Euler paths can be done in $O(n)$ time 
> > - Finding Hamilton paths is NP-complete!

> [!PDF|255, 208, 0] [[agt 3.pdf#page=13&annotation=3577R|p.13]] #theorem
> > An undirected graph $G$ has an Euler circuit iff it is connected and every vertex has even degree.

> [!PDF|255, 208, 0] [[agt 3.pdf#page=33&annotation=3580R|p.33]] #defintion 
> >  **region** is a part of the plane completely disconnected off from other parts of the plane by the edges of the graph.

> [!PDF|255, 208, 0] [[agt 3.pdf#page=36&annotation=3583R|p.36]] #theorem 
> > The number of regions defined by a connected planar graph is invariant of how it is drawn in the plane and satisfies the formula involving edges and vertices: 
> > $$
> > r = |E| - |V| + 2
> > $$
> > $k = r - |E| + |V|$ must equal 2 for planar graphs. $k$ is called the **Euler characteristic**.

> [!PDF|255, 208, 0] [[agt 3.pdf#page=55&annotation=3586R|p.55]] #defintion 
> > The **degree** of a **region** $F$ is the number of edges at its boundary, and is denoted by $deg(F)$.

> [!PDF|255, 208, 0] [[agt 3.pdf#page=55&annotation=3589R|p.55]] #theorem 
> > Let $G$ be a planar graph with region set $R$. Then:
> > $$
> > |E| = \frac{1}{2} \sum_{F \in R} \deg(F) \geq \frac{1}{2} rg
> > $$



> [!PDF|255, 208, 0] [[agt 3.pdf#page=56&annotation=3592R|p.56]] #defintion 
> > The **girth** of a graph is the length of the smallest simple cycle in the graph.

> [!PDF|255, 208, 0] [[agt 3.pdf#page=59&annotation=3595R|p.59]] #question
> > Proving that $Q_4$ is Non-Planar


> [!PDF|255, 208, 0] [[agt 3.pdf#page=61&rect=51,240,492,406|agt 3, p.61]] #question 
> ![[CSC503-AGT/media/media/agt 3.webp]]

> [!PDF|255, 208, 0] [[agt 3.pdf#page=72&annotation=3598R|p.72]] #theorem 
> > ### 4-Color Theorem
> > - Any planar map of regions can be depicted using 4 colors so that no two regions that share a positive-length border have the same color. 
> > 
> > Proof by Haaken and Appel used exhaustive computer search.

> [!PDF|255, 208, 0] [[agt 3.pdf#page=79&annotation=3601R|p.79]] #defintion 
> > DEF: The ***dual graph*** $G^ˆ$ of a planar graph $G = (V, E, R)$ [Vertices, Edges, Regions] is the graph obtained by setting
> > *   Vertices of $G^ˆ$: $V(G^ˆ) = R$
> > *   Edges of $G^ˆ$: $E(G^ˆ)$ = set of edges of the form $\{F_1, F_2\}$ where $F_1$ and $F_2$ share a common edge.
> 

> [!PDF|255, 208, 0] [[agt 3.pdf#page=82&annotation=3604R|p.82]] #defintion 
> > DEF: Let $n$ be a positive number. A simple graph is $n$-colorable if the vertices can be colored using n colors so that no two adjacent vertices have the same color. 
> > 
> > The **chromatic number** of a graph is smallest number $n$ for which it is $n$ colorable. 
> > 
> > E.G: A graph is bipartite iff it is 2-colorable.

> [!PDF|255, 208, 0] [[agt 3.pdf#page=86&annotation=3607R|p.86]] #theorem 
> > Any planar graph is 4-colorable.

> [!PDF|255, 208, 0] [[agt 3.pdf#page=87&annotation=3610R|p.87]] #question 
> > Suppose want to schedule some final exams for CS courses with following call numbers: 
> > **1007, 3137, 3157, 3203, 3261, 4115, 4118, 4156** 
> > Suppose also that there are no common students in the following pairs of courses because of prerequisites: 
> > - 1007-3137 
> > - 1007-3157, 3137-3157 
> > - 1007-3203 
> > - 1007-3261, 3137-3261, 3203-3261 
> > - 1007-4115, 3137-4115, 3203-4115, 3261-4115 
> > - 1007-4118, 3137-4118 
> > - 1007-4156, 3137-4156, 3157-4156 
> > How many exam slots are necessary to schedule exams?
> 

