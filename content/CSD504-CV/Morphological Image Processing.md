

## Preliminaries

Morphology provides a unified and robust approach to many image processing problems. The foundation of mathematical morphology is **set theory**.

We will focus on thresholded images, which consist only of black and white pixels.  The complete morphological description of such an image is contained within the "set of white pixels". These sets are subsets of $\mathbb{Z}^2$, where each vector represents the coordinates of a white (or black) pixel.

## Set Translation

The translation of a set $B$ by a point $z = (z_1, z_2)$, denoted as $(B)_z$, is defined as:

$(B)_z = \{c \mid c = b + z \text{ for } b \in B\}$

**Explanation:**

If $B$ represents a set of pixels forming an object in an image, $(B)_z$ is the set of points in $B$ where the $(x, y)$ coordinates are shifted by $(z_1, z_2)$.  In simpler terms, every point in $B$ is moved by the same amount, defined by $z$.

## Set Reflection

The reflection of a set $B$, denoted as $\hat{B}$, is defined as:

$\hat{B} = \{w \mid w = -b, \text{ for } b \in B\}$

**Explanation:**
The reflection of $B$ consists of points whose coordinates are replaced with $(-x, -y)$. Geometrically, this flips the set $B$ across both the x and y axes, relative to the origin.

## Structuring Elements

Morphological operations rely on *structuring elements* (SEs).

**Definition:** SEs are small sets or subimages used to analyze an image and extract specific properties of interest.

*   SEs are typically small.
*   They "probe" the image.
*   Non-rectangular SEs are often padded with background values (zeros).
* The center of the SE is an important reference point.

## Erosion

Given sets $A$ and $B$ in $\mathbb{Z}^2$, the erosion of $A$ by $B$, denoted as $A \ominus B$, is defined as:

$A \ominus B = \{z \mid (B)_z \cap \bar{A} = \emptyset\}$

**Explanation:**

The erosion of $A$ by $B$ is the set of all points $z$ such that when $B$ is translated by $z$, it is *completely contained within* $A$. Another way to express the condition is: the intersection of the translated $B$, $(B)_z$, and the complement of $A$, denoted as $\bar{A}$, is empty. This means no part of the translated structuring element falls outside of set A.

**Erosion Example:**

(Illustrative examples from the PDF are described here)

*   A rectangular region ($A$) is eroded by a smaller square structuring element ($B$).
*   Points where the translated $B$ overlaps with the complement of $A$ are removed.
*   The resulting eroded image is smaller than the original.
*   The size of eroded region shrinks as the structuring element increases in dimension.

## Dilation

Given sets $A$ and $B$ in $\mathbb{Z}^2$, the dilation of $A$ by $B$, denoted as $A \oplus B$, is defined as:

$A \oplus B = \{z \mid (\hat{B})_z \cap A \neq \emptyset\}$

**Explanation:**

The dilation of $A$ by $B$ is the set of all displacements, $z$, such that the *reflection* of $B$ (i.e., $\hat{B}$), translated by $z$, overlaps with $A$ by at least one element.  This is analogous to spatial convolution.  The structuring element $B$ is reflected and then moved across the image $A$.

**Dilation Example:**

(Illustrative examples from the PDF are described here)

*   Dilation can bridge gaps in text.
*   A simple $3 \times 3$ structuring element with 1s in the center cross and 0s elsewhere is used.

## Opening and Closing

Given an image $A$ and a structuring element $B$:

**Opening:**

$A \circ B = (A \ominus B) \oplus B$

*   Erosion followed by dilation.
*   Smoothes the contour of an object.
*   Breaks narrow connections (isthmuses).
*   Eliminates thin protrusions.

**Closing:**

$A \bullet B = (A \oplus B) \ominus B$

*   Dilation followed by erosion.
*   Smoothes sections of contours.
*   Fuses narrow breaks and long, thin gulfs.
*   Eliminates small holes.
*   Fills gaps in the contour.

**Opening and Closing Example (Fingerprint):**

*   **Opening:** Removes noise but creates holes. Subsequent dilation partially closes the induced holes.
*   **Closing:** Restores breaks in the ridges but thickens them. Subsequent Erosion thins the ridges.
*   **Sequence:** Opening followed by closing eliminates noise *and* closes breaks caused by imperfect thresholding.  $(A \circ B) \bullet B$

## Hole Filling

A hole is a background region surrounded by a connected border of foreground pixels.

**Procedure:**

1.  Let $X_0$ be an array of the same size as $A$, initialized with 0s except for a seed point inside the hole, which is set to 1.
2.  Iteratively apply the following:
    $X_k = (X_{k-1} \oplus B) \cap \bar{A}$
    Where $B$ is a suitable structuring element (e.g., a $3\times3$ cross).
3.  The iteration continues until $X_k = X_{k-1}$.
4. The union between $X_k$ and $A$ gives the filled hole.

**Explanation:**

The procedure starts from a point inside the hole and iteratively dilates it.  The intersection with the complement of $A$ ($\bar{A}$) prevents the dilation from extending beyond the boundaries of the hole (defined by the foreground pixels of $A$).

## Connected Components

Similar to hole filling, but the intersection is performed with $A$ instead of $\bar{A}$.

**Procedure:**

1.  Let $X_0$ be an array the same size as $A$, filled with 0s except for a known point within the connected component, which is set to 1.
2.  Iteratively apply:
    $X_k = (X_{k-1} \oplus B) \cap A$
    Where $B$ is a structuring element.
3.  The iteration stops when $X_k = X_{k-1}$.

**Explanation:**

This iteratively expands a seed point within a connected component.  The intersection with $A$ confines the expansion to the connected component.

## Boundary Extraction

The boundary of a set $A$, denoted as $\beta(A)$, can be obtained by:

$\beta(A) = A - (A \ominus B)$

**Explanation:**

First, $A$ is eroded by $B$.  Then, the set difference between the original $A$ and its erosion is calculated.  This leaves only the boundary pixels.

## Moore Boundary Tracking

The Moore boundary tracking algorithm extracts an ordered sequence of foreground boundary points.

**Assumptions:**

4.  Binary thresholded images (0: background, 1: foreground).
5.  Images are padded with 0s to prevent foreground regions from touching the image border.

**Algorithm:**

6.  **Initialization:**
    *   $b_0$: The uppermost, leftmost point in the image labeled 1.
    *   $c_0$: The west neighbor of $b_0$.
    *   Examine the 8-neighbors of $b_0$ starting from $c_0$ in a clockwise direction.
    *   $b_1$: The first neighbor encountered with a value of 1.
    *   $c_1$: The background point immediately preceding $b_1$.

7.  **Iteration:**
    *   $b = b_1$, $c = c_1$.
    *   Let $n_1, n_2, ..., n_8$ be the 8-neighbors of $b$, starting from $c$ and proceeding clockwise.
    *   Find the first $n_k$ labeled 1.
    *   $b = n_k$, $c = n_{k-1}$.

8.  **Termination:**
    *   Repeat steps 2 and previous until $b = b_0$ and the next boundary point found is $b_1$.
    *   The sequence of $b$ points found constitutes the ordered boundary.

## Gray-Scale Morphology

So far, we've dealt with binary images.  Morphological operations can also be defined for grayscale images.

*   $f(x, y): \mathbb{Z}^2 \rightarrow \mathbb{R}$ (grayscale image)
*   $b(x, y): \mathbb{Z}^2 \rightarrow \mathbb{R}$ (structuring element)

The structuring element, $b$, acts as a "probe" to examine the image. It can be *non-flat* or *flat* (more common).

### Gray-Scale Erosion

The erosion of $f$ by a *flat* structuring element $b$ at location $(x, y)$ is:

$[f \ominus b](x, y) = \min_{(s, t) \in b} \{f(x + s, y + t)\}$

**Explanation:**

It's the *minimum* value of the image within the region defined by $b$ when the origin of $b$ is at $(x, y)$.  Conceptually similar to convolution, but using the minimum operation.

### Gray-Scale Dilation

The dilation of $f$ by a *flat* structuring element $b$ at location $(x, y)$ is:

$[f \oplus b](x, y) = \max_{(s, t) \in b} \{f(x - s, y - t)\}$

**Explanation:**
It's the maximum value of the image within the region defined by the *reflection* of $b$, with the origin of reflection of $b$ at $(x, y)$. The negative signs in the equation $(x-s, y-t)$ account for the reflection of the structuring element.

### Effect of Erosion and Dilation (Grayscale)

*   **Erosion:** The resulting image is darker, and bright features are reduced in size.
*   **Dilation:** The resulting image is brighter, bright features are thickened, and dark features are reduced.

### Gray-Scale Opening and Closing

The expressions are the same as for the binary case:

*   **Opening:** $A \circ B = (A \ominus B) \oplus B$
*   **Closing:** $A \bullet B = (A \oplus B) \ominus B$

**Geometric Interpretation:**

Imagine $f$ and $b$ as 3D surfaces.

*   **Opening:** Pushing the structuring element $b$ *up* from below against the undersurface of $f$.
*   **Closing:** Pushing the structuring element $b$ *down* from the top of the surface of $f$.

### Effect of Opening and Closing (Grayscale)
* **Opening:** Attenuate bright features, negligible on dark.
* **Closing:** Attenuate dark features, negligible on bright.

## Morphological Smoothing

Opening suppresses bright details, and closing suppresses dark details.  They are often combined for smoothing and noise removal.

## Morphological Gradient

$g = (f \oplus b) - (f \ominus b)$

**Explanation:**

The difference between dilation and erosion emphasizes boundaries between regions. Edges are enhanced, and homogeneous areas are suppressed, resulting in a "derivative-like" (gradient) effect.

## Top-Hat and Bottom-Hat Transformations

*   **Top-Hat:** $T_{hat}(f) = f - (f \circ b)$
    *   $f$ minus its opening.
*   **Bottom-Hat:** $B_{hat}(f) = (f \bullet b) - f$
    *   Closing of $f$ minus $f$.

**Goal:** Select objects by using a structuring element that *does not fit* the objects to be removed.  The difference then isolates the selected objects.

**Top-Hat for Illumination Correction:**

Top-hat can help correct uneven illumination.

9.  Original image with uneven illumination.
10.  Opening with a large structuring element (e.g., 40x40 disc) to estimate the background illumination.
11.  Top-hat (Original - Opening) to isolate the objects on a more uniform background.
12. Applying Otsu thresholding after Top-hat correction leads to better results.