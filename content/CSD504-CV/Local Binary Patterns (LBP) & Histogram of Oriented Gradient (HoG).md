## H1: Local Binary Patterns (LBP)

### H2: Introduction

*   **Definition:** LBP is an image operator that transforms an image into an array of integer labels. These labels describe the small-scale appearance (texture) of the image.
*   **Purpose:** These labels or their statistics are used for further image analysis, such as texture classification or object recognition.
*   **Original Use:** Primarily designed for monochrome still images.
*   **Extensions:**
    *   Extended for color images (multi-channel).
    *   Applicable to videos.
*   **Citation:** Introduced by Ojala et al. in the paper: "A comparative study of texture measures with classification based on feature distributions," Pattern Recognition, 29(1), 51-59 (1996).

### H2: Core Idea

*   **Texture Aspects:** LBP assumes that a texture has two complementary aspects at a local level:
    1. **Pattern:** The spatial structure of the local neighborhood.
    2. **Strength:** The intensity contrast of the pattern.
*   **3x3 Neighborhood:** The basic LBP operator works within a 3x3 pixel neighborhood.

### H2: LBP Operator - How it Works

1. **Thresholding:** The center pixel's value in a 3x3 block is used as a threshold. Neighboring pixels are compared to this threshold:
    *   If a neighbor's value is greater than or equal to the center pixel's value, it's assigned a value of 1.
    *   Otherwise, it's assigned a value of 0.
    As in the slide, example, if $c$ is the center and $n$ is the neighbor, then $n$ is $1$ if $n \geq c$ else $0$.
2. **Binary Code:** This results in an 8-bit binary code (since there are 8 neighbors).
3. **Decimal Conversion:** The binary code is multiplied by powers of two (starting from $2^0$ for the top-right neighbor and going counter-clockwise, similar to a binary representation, and then summed up to get a decimal value). This decimal value is the LBP label for the center pixel.
4. **Range:** With an 8-bit code, there are 256 possible LBP labels (0-255).

### H2: LBP Operator: Mathematical Representation

$LBP_{R,P} = \sum_{p=0}^{P-1} s(g_p - g_c) \cdot 2^p$

Where:

*   $LBP_{R,P}$: LBP value for a neighborhood with radius $R$ and $P$ sampling points.
*   $g_c$: Gray value of the center pixel.
*   $g_p$: Gray value of the neighbor pixel at sampling point $p$.
*   $s(x)$: Thresholding function:
    *   $s(x) = 1$ if $x \geq 0$
    *   $s(x) = 0$ if $x < 0$
*   $P$: Number of sampling points (usually 8 in a 3x3 neighborhood).
*   $R$: Radius of the neighborhood (usually 1 in a 3x3 neighborhood).
*   $p$: Sampling point index (0 to $P-1$).

### H2: Coordinates

*   Coordinates of "$g_c$" is (0,0)
*   Coordinates of "$g_p$" is $(x + R\cos(2\pi p/P), y - R\sin(2\pi p/P))$

### H2: Example Calculation
Let's consider a 3x3 neighborhood:

```
3  7  2
8  4  1
2  3  5
```
*Center pixel (gc) = 4*
**Binary code:** 01010010

*   **Top-right (7):** 7 >= 4, so 1
*   **Right (1):** 1 < 4, so 0
*   **Bottom-right (5):** 5 >= 4, so 1
*   **Bottom (3):** 3 < 4, so 0
*   **Bottom-left (2):** 2 < 4, so 0
*   **Left (8):** 8 >= 4, so 1
*   **Top-left (3):** 3 < 4, so 0
*   **Top (3):** 3 < 4, so 0

Now, multiply each bit by the corresponding power of 2 and sum:

$(0 \cdot 2^7) + (1 \cdot 2^6) + (0 \cdot 2^5) + (1 \cdot 2^4) + (0 \cdot 2^3) + (0 \cdot 2^2) + (1 \cdot 2^1) + (0 \cdot 2^0) = 0 + 64 + 0 + 16 + 0 + 0 + 2 + 0 = 82$

So, the LBP value for the center pixel is 82.

### H2: LBP Texture Primitives

Different LBP values correspond to different micro-patterns or texture primitives, such as:

*   **Spot:** Center pixel is significantly brighter or darker than the surrounding pixels.
*   **Flat:** All pixels in the neighborhood have similar values.
*   **Line end:** A line terminates within the neighborhood.
*   **Edge:** A transition between two regions of different intensities.
*   **Corner:** An intersection of two edges.

### H2: Advanced LBP (P, R)

*   **Flexibility:** The LBP operator can be extended to use different numbers of sampling points (P) and different radii (R), creating larger or differently shaped neighborhoods.
*   **Notation:** LBP(P, R) denotes an LBP operator with P sampling points and radius R.
*   **Examples:**
    *   LBP(8, 1): Standard 3x3 neighborhood (8 pixels, radius 1).
    *   LBP(16, 2): Larger neighborhood (16 pixels, radius 2).
    *   LBP(20,4): Even larger neighborhood (20 pixels, radius 4).

### H2: LBP Advantages

*   **High discriminative power:** LBP effectively captures texture information.
*   **Computational simplicity:** The operator is relatively easy to compute.
*   **Invariance to grayscale changes:** LBP is invariant to monotonic changes in grayscale (i.e., if you brighten or darken the entire image uniformly, the LBP values won't change).
*   **Good performance:** LBP has shown good results in various texture analysis tasks.

### H2: LBP Disadvantages

*   **Not invariant to rotations:** If you rotate the image, the LBP values will change.
*   **Feature size increases exponentially:** The number of possible LBP values increases exponentially with the number of neighbors, which can lead to high-dimensional feature vectors and increased computational complexity.
*   **Limited structural information:** LBP only considers the relationship between the center pixel and its immediate neighbors, ignoring larger-scale structural information and magnitude differences.

## H1: Uniform LBP (uLBP)

### H2: Uniformity Measure (U)

*   **Definition:** The uniformity measure U counts the number of bitwise transitions (0 to 1 or 1 to 0) in the circular binary LBP pattern.
*   **Example:**
    *   00000000 (0 transitions) - Uniform
    *   01110000 (2 transitions) - Uniform
    *   11001111 (2 transitions) - Uniform
    *   11001001 (4 transitions) - Non-uniform
    *   01010011 (6 transitions) - Non-uniform

### H2: Uniform LBP Definition

*   An LBP pattern is considered **uniform** if its uniformity measure U is at most 2 (i.e., U ≤ 2).

### H2: Why Use Uniform LBP?

*   **Dominance in natural images:** Most of the local binary patterns that occur in natural images are uniform.
*   **Ojala et al.'s findings:** In texture images, uLBP patterns account for:
    *   About 90% of all patterns when using LBP(8, 1).
    *   About 70% of all patterns when using LBP(16, 2).
*   **Facial images:**
    *   90.6% of patterns in LBP(8, 1)
    *   85.2% of patterns in LBP(8, 2)

### H2: Mapping in Uniform LBP

*   **Separate labels:** Each uniform pattern is assigned a unique output label.
*   **Single label for non-uniform:** All non-uniform patterns are grouped together and assigned to a single label.

### H2: Calculating Uniform Value

*   $U(LBP_{P,R}) = |s(g_{P-1} - g_c) - s(g_0 - g_c)| + \sum_{p=1}^{P-1} |s(g_p - g_c) - s(g_{p-1} - g_c)|$
*   If $U \leq 2$, the pattern is uniform; otherwise, it is non-uniform.
*   **Output values:** Uniform LBP has $P * (P - 1) + 2$ output values.
*   **Examples:** Examples of uniform and non-uniform patterns for P=8 are shown in the slide.

### H2: Advantages of uLBP

*   **Focus on common patterns:** Considers only the most frequent and significant patterns in natural images.
*   **Improved performance:** uLBP often provides better performance than basic LBP due to its focus on statistically significant patterns.
*   **Reduced dimensionality:** uLBP has a smaller number of output labels compared to basic LBP, leading to lower-dimensional feature vectors.

### H2: Disadvantages of uLBP

*   **No rotation invariance:** Like basic LBP, uLBP is not invariant to rotation.

## H1: Rotation Invariance and LBP Variants

### H2: Rotation Invariance

*   **Problem:** Basic LBP and uLBP are not rotation invariant. Rotating the image changes the LBP codes.
*   **Goal:** Develop rotation-invariant LBP variants.

### H2: Rotation Invariant LBP (riLBP or LBPri)

*   **Idea:** Rotate the LBP pattern to a canonical orientation before assigning a label.
*   **Formula:** $LBP_{P,R}^{ri} = \min_{i} ROR(LBP_{P,R}, i)$
    *   $ROR(x, i)$ is a circular bitwise right rotation of $x$ by $i$ steps.
    *   The minimum value obtained after rotating the LBP code is used as the rotation-invariant label.
*   **Example:** 8-bit LBP codes 10000010b, 00101000b, and 00000101b all map to the minimum code 00000101b.
*   **Property:** LBPri is rotation invariant.

**Advantages:**

*   **Scale and rotation invariance**

**Disadvantages:**

*   **Micro-pattern misclassification:** Two different images may be misclassified as the same class if they are composed of similar micro-patterns.

### H2: Rotated LBP (rLBP or RLBP)

*   **Idea:** Find the dominant direction of the gradient in the neighborhood and align the LBP code with that direction.
*   **Dominant direction:** The direction with the maximum difference between neighboring pixels and the central pixel.

$D = argmax_{p \in \{0, 1, ..., P-1\}} |g_p - g_c|$ (Dominant Direction)

$RLBP_{R,P} = \sum_{p=0}^{P-1} s(g_p - g_c) \cdot 2^{mod(|p-D|, P)}$ (Rotated LBP)

*   **Advantages:**
    *   Invariant to rotation.
    *   High discriminative power.
*   **Disadvantages:**
    *   Large feature vector size.
    *   High computational complexity.

These are the notes from pages 1-25. Let me know if you need notes on the remaining pages (HoG).
