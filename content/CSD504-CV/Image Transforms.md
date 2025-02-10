---
refer: "[[DIP Unit 3 Vijay Chakole_1.pdf]]"
---

## Basic Geometric Transformations

- **Transform theory** is fundamental in image processing.
- Working with the transform of an image can provide more insight than working with the image itself.
- Applications: image enhancement, restoration, encoding, and description.


### Properties of 2D DFT

- **Linearity:** $af(x, y) + bg(x, y) \iff aF(u, v) + bG(u, v)$
- **Shifting:** $f(x - x_0, y - y_0) \iff e^{-j2\pi(ux_0 + vy_0)}F(u, v)$
- **Modulation:** $e^{j2\pi(u_0x + v_0y)}f(x, y) \iff F(u - u_0, v - v_0)$
- **Convolution:** $f(x, y) * g(x, y) \iff F(u, v)G(u, v)$
- **Multiplication:** $f(x, y)g(x, y) \iff F(u, v) * G(u, v)$
- **Separability:** $f(x, y) = f(x)f(y) \iff F(u, v) = F(u)F(v)$

### Separability in Detail
- 2D Fourier Transforms can be done as a sequence of 1D Fourier Transforms along each axis.
$F(u,v) = \int_{-\infty}^{\infty}\int_{-\infty}^{\infty} f(x,y)e^{-j2\pi(ux+vy)}dxdy$
$= \int_{-\infty}^{\infty} e^{-j2\pi vy} \left[ \int_{-\infty}^{\infty} f(x,y)e^{-j2\pi ux}dx \right] dy$
$= \int_{-\infty}^{\infty} F(u,y)e^{-j2\pi vy}dy = F(u,v)$

```mermaid
graph LR
    A[2D DFT] --> B(1D DFT along the rows)
    B --> C(1D DFT along the cols)
```
- If functions are separable, i.e. $f(x,y) = f(x)g(y)$.
- The FT of a separable function is the product of the FTs of individual functions.
$F(u,v) = H(u)G(v)$ if $f(x,y) = h(x)g(y)$.


## Discrete Cosine Transform (DCT)

- Separates the image into parts of differing importance (spectral sub-bands).
- Similar to DFT but uses only cosine functions.

### 1D DCT

$F(u) = \left(\frac{2}{N}\right)^{\frac{1}{2}} \sum_{i=0}^{N-1} \Lambda(i) \cdot \cos\left[\frac{\pi u}{2N}(2i+1)\right] f(i)$

where:

$$
\Lambda(i) = \begin{cases}
\frac{1}{\sqrt{2}} & \text{for } \xi = 0 \\
1 & \text{otherwise}
\end{cases}
$$

### 2D DCT
$F(u,v) = (\frac{2}{N})^{\frac{1}{2}} (\frac{2}{M})^{\frac{1}{2}} \sum_{i=0}^{N-1} \sum_{j=0}^{M-1} \Lambda(i) \Lambda(j) \cos[\frac{\pi u}{2N}(2i+1)] \cos[\frac{\pi v}{2M}(2j+1)] f(i,j)$

where:
$$
\Lambda(\xi) = \begin{cases}
\frac{1}{\sqrt{2}} & \text{for } \xi = 0 \\
1 & \text{otherwise}
\end{cases}$$

### DCT Basic Operation

- Input image: *N* by *M*.
- $f(i, j)$: intensity of the pixel at row *i* and column *j*.
- $F(u, v)$: DCT coefficient at row *u* and column *v*.
- Most signal energy lies at low frequencies (upper-left corner of the DCT matrix).
- Compression: Achieved because higher frequencies (lower-right values) are often small and can be neglected.
- DCT input is typically an 8x8 array of integers, representing pixel gray scale levels (0-255 for 8-bit pixels).
