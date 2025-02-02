## **$GF(2^2)$ Addition and Multiplication Tables**

**Elements:**  $\{0, 1, x, x+1\}$ (where $x^2 + x + 1 = 0$)

### **Addition Table:**

$$
\begin{array}{c|cccc}
+ & 0 & 1 & x & x+1 \\
\hline
0 & 0 & 1 & x & x+1 \\
1 & 1 & 0 & x+1 & x \\
x & x & x+1 & 0 & 1 \\
x+1 & x+1 & x & 1 & 0 \\
\end{array}
$$

### **Multiplication Table:**

$$
\begin{array}{c|cccc}
\times & 0 & 1 & x & x+1 \\
\hline
0 & 0 & 0 & 0 & 0 \\
1 & 0 & 1 & x & x+1 \\
x & 0 & x & x+1 & 1 \\
x+1 & 0 & x+1 & 1 & x \\
\end{array}
$$


## **Inverse of $(x^2 + 1)$ in GF(2<sup>4</sup>) modulo $(x^4 + x + 1)$ using a Table **

### **Problem:**

Find the inverse of $(x^2 + 1)$ in GF(2<sup>4</sup>) using the irreducible polynomial $p(x) = x^4 + x + 1$.

### **Solution using the Extended Euclidean Algorithm (Tabular Form):**

$$
\begin{array}{c|c|c|c|c|c|c}
q & r_1 & r_2 & r & t_1 & t_2 & t \\
\hline
(x^2 + 1) & (x^4 + x + 1) & (x^2 + 1) & (x) & (0) & (1) & (x^2 + 1) \\
\hline
(x) & (x^2 + 1) & (x) & (1) & (1) & (x^2 + 1) & (x^3 + x + 1) \\
\hline
(x) & (x) & (1) & (0) & (x^2 + 1) & (x^3 + x + 1) & (0) \\
\hline
 & (1) & (0) &  & (x^3 + x + 1) & (0) & \\
\end{array}
$$

### **Answer:**

The inverse of $(x^2 + 1)$ in GF(2<sup>4</sup>) modulo $(x^4 + x + 1)$ is:

$x^3 + x + 1$

Okay, I understand. I will use the same tabular method to find the result of multiplying $P_1 = (x^5 + x^2 + x)$ by $P_2 = (x^7 + x^4 + x^3 + x^2 + x)$ in GF(2<sup>8</sup>), with the irreducible polynomial $p(x) = x^8 + x^4 + x^3 + x + 1$.

## **Multiplication of P<sub>1</sub> and P<sub>2</sub> in GF(2<sup>8</sup>) using a Table (MathJax)**

### **Problem:**

Find the result of multiplying $P_1 = (x^5 + x^2 + x)$ by $P_2 = (x^7 + x^4 + x^3 + x^2 + x)$ in GF(2<sup>8</sup>), assuming the irreducible polynomial is $p(x) = x^8 + x^4 + x^3 + x + 1$.

### **Solution using an Efficient Algorithm (Tabular Form):**

$$
\begin{array}{c|c|c|c}
\text{Powers} & \text{Operation} & \text{New Result} & \text{Reduction} \\
\hline
x^0 \otimes P_2 &  & x^7 + x^4 + x^3 + x^2 + x & \text{No} \\
\hline
x^1 \otimes P_2 & x \otimes (x^7 + x^4 + x^3 + x^2 + x) & x^5 + x^2 + x + 1 & \text{Yes} \\
\hline
x^2 \otimes P_2 & x \otimes (x^5 + x^2 + x + 1) & x^6 + x^3 + x^2 + x & \text{No} \\
\hline
x^3 \otimes P_2 & x \otimes (x^6 + x^3 + x^2 + x) & x^7 + x^4 + x^3 + x^2 & \text{No} \\
\hline
x^4 \otimes P_2 & x \otimes (x^7 + x^4 + x^3 + x^2) & x^5 + x + 1 & \text{Yes} \\
\hline
x^5 \otimes P_2 & x \otimes (x^5 + x + 1) & x^6 + x^2 + x & \text{No} \\
\hline

\end{array}
$$
$$
{\begin{array}{l}
\mathbf{P_1 \times P_2} = (x^6 + x^2 + x) + (x^6 + x^3 + x^2 + x) + (x^7 + x^4 + x^3 + x^2 + x) \\ = \mathbf{x^7 + x^4 + x^2 + x}
\end{array}}
$$
**Explanation:**

-   **Powers:** Represents the powers of  `x`  from  $P_1$ (x<sup>5</sup>, x<sup>2</sup>, x<sup>1</sup>).
-   **Operation:** Shows the multiplication of the current power of  `x`  with  $P_2$.
-   **New Result:** The result of the multiplication before any reduction.
-   **Reduction:** Indicates whether the "New Result" needs to be reduced modulo  $p(x)$ (if the degree is 8 or greater). The reduction involves replacing $x^8$ with $x^4 + x^3 + x + 1$.

**Example of Reduction:**

- For $x^1 \otimes P_2$, we get $x^8 + x^5 + x^4 + x^3 + x^2$.
- We replace $x^8$ with $x^4 + x^3 + x + 1$.
- Resulting in: $(x^4 + x^3 + x + 1) + x^5 + x^4 + x^3 + x^2 = x^5 + x^2 + x + 1$

### **Answer:**

The result of multiplying $P_1$ by $P_2$ in GF(2<sup>8</sup>) is:

$x^7 + x^4 + x^2 + x$
