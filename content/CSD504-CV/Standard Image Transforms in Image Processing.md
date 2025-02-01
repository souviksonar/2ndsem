## Introduction

Image transforms are fundamental operations in image processing that convert an image from its original domain (e.g., spatial domain) to another domain (e.g., frequency domain). This transformation often makes certain image characteristics or features more explicit and easier to analyze or manipulate.

## General Form of Image Transforms

A general 2D image transform can be expressed as:

$$
T(u, v) = \int_{-\infty}^{\infty} \int_{-\infty}^{\infty} f(x, y) K(x, y, u, v) \, dx \, dy
$$

Where:

*   $f(x, y)$: The original image in the spatial domain (x, y are spatial coordinates).
*   $T(u, v)$: The transformed image in the new domain (u, v are the transform domain coordinates, often representing frequencies or other basis components).
*   $K(x, y, u, v)$: The **transform kernel** or **basis function**. This function defines the specific transformation being applied. It determines how the original image is projected onto the new domain.

### **In discrete form (for digital images):**

$$
T(u, v) = \sum_{x=0}^{M-1} \sum_{y=0}^{N-1} f(x, y) K(x, y, u, v) 
$$

Where:

*   **M, N:**  Dimensions of the image (width and height).
*   **x, y:** Pixel coordinates (0 to M-1, 0 to N-1).
*   **u, v:** Transform domain coordinates.

## Spatial Frequency Representation: F(u,v)

In many important transforms (like the Fourier Transform), the transform domain coordinates (u, v) represent **spatial frequencies**.

*   **Spatial frequency** refers to the rate of change of pixel intensity values in the spatial domain.
*   **Low frequencies** correspond to slow variations (e.g., gradual changes in brightness across the image).
*   **High frequencies** correspond to rapid variations (e.g., sharp edges, fine details, noise).
*   **F(u, v)** often denotes the transformed image in the frequency domain, where each point F(u, v) represents the magnitude and phase of a particular spatial frequency component (u, v) present in the original image.

## Separable Image Transforms

A transform is considered **separable** if its 2D kernel can be expressed as the product of two 1D kernels:

$$
K(x, y, u, v) = K_1(x, u) K_2(y, v) 
$$

Where:

*   $K_1(x, u)$: A 1D kernel applied along the x-dimension.
*   $K2(y, v)$: A 1D kernel applied along the y-dimension.

### **Significance of Separability:**

*   **Computational Efficiency:** Separable transforms can be computed much faster. Instead of performing a full 2D transformation, we can perform two 1D transformations sequentially: first along the rows (x-dimension) and then along the columns (y-dimension) of the intermediate result.

### **Forward transform using separable kernels:**
$$
T(u, v) = \sum_{y=0}^{N-1} K_2(y,v) \left[ \sum_{x=0}^{M-1} f(x,y) K_1(x,u) \right] 
$$

*   We can compute the inner summation for each row `y` first to obtain an intermediate result.
*   Then, we compute the outer summation over the intermediate results to obtain the final transform.

### **Inverse transform using separable kernels:**
$$
f(x, y) = \sum_{v=0}^{N-1} K_2^*(y,v) \left[ \sum_{u=0}^{M-1} T(u,v) K_1^*(x,u) \right] 
$$

*   $K_1^*(x,u)$ is the complex conjugate of $K_1(x,u)$.
*   $K_2^*(y,v)$ is the complex conjugate of $K_2(y,v)$.
*   Similar to the forward transform, the inverse transform can be computed efficiently by applying the 1D transforms sequentially.

## Common Examples of Separable Transforms

### 1. Discrete Fourier Transform (DFT)

*   **Kernel:** $K(x, y, u, v) = e^{-j2\pi(\frac{ux}{M} + \frac{vy}{N})} = e^{-j2\pi\frac{ux}{M}} e^{-j2\pi\frac{vy}{N}}$
    Where $j = \sqrt{-1}$

*   **Separable:**
    $K_1(x, u) = e^{-j2\pi\frac{ux}{M}}$
    $K_2(y, v) = e^{-j2\pi\frac{vy}{N}}$

*   **Spatial Frequency:**  The DFT directly provides the spatial frequency representation F(u, v) of the image.

### 2. Discrete Cosine Transform (DCT)

*   **Kernel:** (Type-II DCT, most common)
    $$
    K(x, y, u, v) = \alpha(u) \alpha(v) \cos\left[\frac{\pi(2x+1)u}{2M}\right] \cos\left[\frac{\pi(2y+1)v}{2N}\right] 
    $$
    Where:
    $\alpha(u) = \begin{cases} \sqrt{\frac{1}{M}}, & u = 0 \\ \sqrt{\frac{2}{M}}, & 1 \le u \le M-1 \end{cases}$
    $\alpha(v) = \begin{cases} \sqrt{\frac{1}{N}}, & v = 0 \\ \sqrt{\frac{2}{N}}, & 1 \le v \le N-1 \end{cases}$

*   **Separable:**
    $K_1(x, u) = \alpha(u) \cos\left[\frac{\pi(2x+1)u}{2M}\right]$
    $K_2(y, v) = \alpha(v) \cos\left[\frac{\pi(2y+1)v}{2N}\right]$

*   **Used in JPEG compression:** The DCT is excellent at energy compaction, concentrating most of the image's energy in the low-frequency coefficients.
