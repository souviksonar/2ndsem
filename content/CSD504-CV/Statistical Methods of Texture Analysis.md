# Statistical Methods of Texture Analysis

*   **Concept**: Texture analysis often relies on spatial relationships between pixel gray levels, not just individual pixel values.
*   **Gray-Level Co-occurrence Matrix (GLCM)**:
    *   Defined by a displacement vector $\mathbf{d} = (dx, dy)$, representing the spatial relationship between pixel pairs.
    *   $P[i, j]$ counts the number of pixel pairs separated by $\mathbf{d}$ with gray levels $i$ and $j$.
    *   Normalized $P[i, j]$ can be treated as a probability mass function.
Okay, here's a breakdown of the Texture Features derived from the Gray-Level Co-occurrence Matrix (GLCM), designed for better understanding:

**What is the GLCM ?**

*   The GLCM captures how often different combinations of pixel gray levels occur next to each other in an image, based on a defined spatial relationship (the displacement vector **d**).
*   Think of it as a matrix that summarizes the spatial distribution of gray levels in a textured region.

**Texture Features from the GLCM: What do they tell us?**

These features quantify different aspects of the texture based on the probabilities in the GLCM. They help us distinguish between different types of textures.

1. **Entropy:**

    *   **What it measures:** The randomness or disorder in the texture.
    *   **Intuition:**
        *   High entropy = Many different gray-level pairs occur with similar probability (like a noisy or very complex texture). The GLCM will have values spread out.
        *   Low entropy = Only a few gray-level pairs dominate (like a very regular or uniform texture). The GLCM will have a few large values.
    *   **Formula:**
        $$
        \text{Entropy} = - \sum_{i}\sum_{j} P[i, j] \log P[i, j]
        $$
        *   $P[i, j]$ is the probability of gray levels $i$ and $j$ occurring together (from the GLCM).

2. **Energy (also called Angular Second Moment):**

    *   **What it measures:** The uniformity or homogeneity of the texture.
    *   **Intuition:**
        *   High energy = The texture is very uniform (only a few gray-level pairs are common). The GLCM will have a few large values, possibly close to the diagonal if the pixel pairs often have similar gray level values.
        *   Low energy = The texture is less uniform, with many different gray-level pairs present.
    *   **Formula:**
        $$
        \text{Energy} = \sum_{i}\sum_{j} P^2[i, j]
        $$
        *   We square the probabilities, so larger $P[i, j]$ values contribute much more to the sum.

3. **Contrast:**

    *   **What it measures:** The amount of local variation in gray levels in the texture.
    *   **Intuition:**
        *   High contrast = Large differences between gray levels of neighboring pixels are common (like a texture with sharp edges or large variations between light and dark areas). Values further away from the diagonal of the GLCM will be larger.
        *   Low contrast = Neighboring pixels tend to have similar gray levels (like a smooth texture). Values along the diagonal will be larger.
    *   **Formula:**
        $$
        \text{Contrast} = \sum_{i}\sum_{j} (i - j)^2 P[i, j]
        $$
        *   The $(i - j)^2$ term emphasizes large differences in gray levels.

4. **Homogeneity:**

    *   **What it measures:** How close the distribution of elements in the GLCM is to the GLCM diagonal. This indicates how similar the pixel pairs are in terms of their gray level values.
    *   **Intuition:**
        *   High homogeneity = Pixel pairs tend to have very similar gray level values (the texture is locally smooth). Values are concentrated along the diagonal of the GLCM.
        *   Low homogeneity = Pixel pairs often have different gray level values (the texture has more local variations).
    *   **Formula:**
        $$
        \text{Homogeneity} = \sum_{i}\sum_{j} \frac{P[i, j]}{1 + |i - j|}
        $$
        *   The $1 + |i - j|$ term in the denominator gives more weight to pixel pairs with similar gray levels (where $|i - j|$ is small).

**In Summary**

*   These four features (Entropy, Energy, Contrast, and Homogeneity) provide a statistical summary of texture characteristics based on the GLCM.
*   They are often used together in texture classification and segmentation tasks.
*   The specific values of these features will depend on the choice of the displacement vector **d** used to create the GLCM.

I hope this more detailed explanation makes these texture features easier to understand!


**Page 6: Structural Analysis & Autocorrelation**

*   **Structural Analysis of Ordered Texture**: Used when texture primitives are large and can be individually segmented.
    *   Involves describing primitives (e.g., shape, size) and their spatial arrangement (placement rules).
    *   Morphological methods can be helpful for extracting primitives in noisy images.
*   **Autocorrelation**: Measures self-similarity of an image at different spatial lags.
    *   For an $N \times N$ image, the autocorrelation function $p[k, l]$ is defined as:
        $$
        p[k, l] = \frac{\sum_{i=1}^{(N-k)} \sum_{j=1}^{(N-l)} f[i, j] f[i+k, j+l]}{\sum_{i=1}^{N} \sum_{j=1}^{N} f^2[i, j]}, \quad 0 \leq k, l \leq N-1 \qquad (7.5)
        $$
        where:
        *   $f[i, j]$ is the pixel value at location $(i, j)$.
        *   $k$ and $l$ are spatial lags.
    *   Periodic textures show periodic behavior in the autocorrelation function.
    *   Coarse textures: autocorrelation drops off slowly.
    *   Fine textures: autocorrelation drops off rapidly.

