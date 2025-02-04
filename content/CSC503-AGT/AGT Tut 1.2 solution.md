# Even Number of Odd-Degree Vertices

In any finite graph *$G = (V, E)$*, the number of vertices with an odd degree is always even.

## Proof

### **1. Apply the Handshaking Lemma:**

The Handshaking Lemma states:

$\sum_{v \in V} deg(v) = 2|E|$

This tells us that the sum of the degrees of all vertices in the graph is an even number (since it's twice the number of edges).

### **2. Separate Vertices into Odd and Even Degree Sets:**

Let *$V_{odd}$* be the set of vertices with odd degrees, and *$V_{even}$* be the set of vertices with even degrees. Clearly, *$V = V_{odd} \cup V_{even}$* and *$V_{odd} \cap V_{even} = \emptyset$*.

### **3. Rewrite the Sum of Degrees:**

We can rewrite the sum of degrees, splitting it into the sum over *$V_{odd}$* and the sum over *$V_{even}$*:

$\sum_{v \in V} deg(v) = \sum_{v \in V_{odd}} deg(v) + \sum_{v \in V_{even}} deg(v)$

### **4. Analyze the Even Degree Sum:**

The sum of even numbers is always even. Therefore:

$\sum_{v \in V_{even}} deg(v)$ is even.

Let's represent this even sum as *$2k$*, where *$k$* is an integer.

### **5. Analyze the Odd Degree Sum:**

From the Handshaking Lemma and steps *3* and *4*, we have:

$2|E| = \sum_{v \in V_{odd}} deg(v) + 2k$

Rearranging:

$\sum_{v \in V_{odd}} deg(v) = 2|E| - 2k = 2(|E| - k)$

Since *$|E|$* and *$k$* are integers, *$(|E| - k)$* is also an integer. Let's call it *$m$*. So:

$\sum_{v \in V_{odd}} deg(v) = 2m$

This shows that the sum of the degrees of vertices in *$V_{odd}$* is also an even number.


**Therefore, *$V_{odd}$* is even.**
