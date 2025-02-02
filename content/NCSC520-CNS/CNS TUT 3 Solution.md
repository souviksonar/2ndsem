# **Tutorial-IV (Mathematical Background)**

## **Elliptic Curve Cryptography**

### **1. Find the points on elliptic curve  E<sub>23</sub> (1,1)**

The elliptic curve is defined by the equation:

$y^2 \equiv x^3 + ax + b \pmod{p}$

where $a=1$, $b=1$, and $p=23$. So, the equation becomes:

$y^2 \equiv x^3 + x + 1 \pmod{23}$

We need to find the pairs $(x, y)$ that satisfy this equation for $x = 0, 1, 2, ..., 22$ and $y = 0, 1, 2, ..., 22$.

By trying all possible values for $x$ and finding corresponding $y$ we get these points:

$(0,1),(0,22),(1,7),(1,16),(3,10),(3,13),(4,0),(5,4),(5,19),(6,4),(6,19),(7,11),(7,12),(9,7),(9,16)$
$(11,3),(11,20),(12,4),(12,19),(13,7),(13,16),(17,3),(17,20),(18,3),(18,20),(19,5),(19,18)$

### **2. Perform the addition on the following 2D points**

$P = (3, 10)$, $Q = (9, 7)$

**Point Addition:**

If $P = (x_1, y_1)$ and $Q = (x_2, y_2)$, then $R = P + Q = (x_3, y_3)$ is calculated as follows:

- **Case 1: P ≠ Q**
  - $\lambda = \frac{y_2 - y_1}{x_2 - x_1} \pmod{23}$
  - $x_3 = \lambda^2 - x_1 - x_2 \pmod{23}$
  - $y_3 = \lambda(x_1 - x_3) - y_1 \pmod{23}$

- **Case 2: P = Q (Point Doubling)**
  - $\lambda = \frac{3x_1^2 + a}{2y_1} \pmod{23}$
  - $x_3 = \lambda^2 - 2x_1 \pmod{23}$
  - $y_3 = \lambda(x_1 - x_3) - y_1 \pmod{23}$

**Calculations:**

Since $P \neq Q$, we use Case 1:

- $\lambda = \frac{7 - 10}{9 - 3} = \frac{-3}{6} = \frac{20}{6} \equiv 20 \cdot 4 \equiv 80 \equiv 11 \pmod{23}$
- $x_3 = 11^2 - 3 - 9 = 121 - 12 = 109 \equiv 17 \pmod{23}$
- $y_3 = 11(3 - 17) - 10 = 11(-14) - 10 = -154 - 10 = -164 \equiv 3 \pmod{23}$

Therefore, $P + Q = (17, 3)$

### 3. Consider $E_{13}(1,1)$and perform the following scalar multiplication and show the resultant point obtained.

$y^2 \equiv x^3 + x + 1 \pmod{13}$
#### **(i) 4\*P where P = (1,4)**
   - **2P:**
     - $\lambda = \frac{3(1)^2 + 1}{2(4)} = \frac{4}{8} = \frac{17}{8} \equiv 17 \cdot 5 \equiv 85 \equiv 7 \pmod{13}$
     - $x_3 = 7^2 - 2(1) = 49 - 2 = 47 \equiv 8 \pmod{13}$
     - $y_3 = 7(1 - 8) - 4 = -49 - 4 = -53 \equiv 1 \pmod{13}$
     - $2P = (8, 1)$
   - **4P = 2P + 2P:**
     - $\lambda = \frac{3(8)^2 + 1}{2(1)} = \frac{193}{2} = \frac{2}{2} = 1 \pmod{13}$
     - $x_3 = 1^2 - 2(8) = 1 - 16 = -15 \equiv 11 \pmod{13}$
     - $y_3 = 1(8 - 11) - 1 = -3 - 1 = -4 \equiv 9 \pmod{13}$
     - $4P = (11, 9)$

#### **(ii) 3\*Q where Q = (8,1)**
   - **2Q:**
     - $\lambda = \frac{3(8)^2 + 1}{2(1)} = \frac{193}{2} \equiv \frac{2}{2} = 1 \pmod{13}$
     - $x_3 = 1^2 - 2(8) = 1 - 16 = -15 \equiv 11 \pmod{13}$
     - $y_3 = 1(8 - 11) - 1 = -3 - 1 = -4 \equiv 9 \pmod{13}$
     - $2Q = (11, 9)$
   - **3Q = 2Q + Q:**
     - $\lambda = \frac{9 - 1}{11 - 8} = \frac{8}{3} \equiv 8 \cdot 9 \equiv 72 \equiv 7 \pmod{13}$
     - $x_3 = 7^2 - 11 - 8 = 49 - 19 = 30 \equiv 4 \pmod{13}$
     - $y_3 = 7(8 - 4) - 1 = 28 - 1 = 27 \equiv 1 \pmod{13}$
     - $3Q = (4, 1)$
