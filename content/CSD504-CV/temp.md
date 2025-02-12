
# Computer Vision: Morphological Image Processing

## Preliminaries

Morphology provides a unified and powerful approach to various image processing problems.

*   The language of mathematical morphology is set theory.
*   We consider thresholded images containing only black and white pixels.
*   The "set of white pixels" contains the complete morphological description of the image.
*   These sets are subsets of $Z^{2}$ where each vector expresses coordinates of white (or black) pixels.

## Set Translation

The translation of a set $B$ by point $z = (z_1, z_2)$, denoted $(B)_z$, is defined as:

$(B)_{z}=\{c \mid c=b+z \text { for } b \in B\}$

If $B$ is the set of pixels representing an object in an image, then $(B)_z$ is the set of points in $B$ whose $(x, y)$ coordinates have been replaced by $(x+z_1, y+z_2)$.

## Set Reflection

The reflection of a set $B$, denoted $\hat{B}$, is defined as:

$\hat{B}=\{w \mid w=-b, \text { for } b \in B\}$

The reflection of $B$ is composed of the points whose coordinates are replaced with $(-x, -y)$.

## Structuring Elements

Morphological operations are based on structuring elements (SEs):

SEs are small sets or subimages used to probe an image under study for properties of interest.

Non-rectangular SEs are padded with background values (zeros).

## Erosion

With $A$ and $B$ as sets in $Z^{2}$, the erosion of $A$ by $B$, denoted $A \ominus B$, is defined as:

$A \ominus B=\left\{z \mid(B)_{z} \cap \bar{A}=\emptyset\right\}$

In words, the erosion of $A$ by $B$ is the set of all points $z$ such that $B$, translated by $z$, is contained in $A$ (the intersection between $(B)_z$ and the complement of $A$ is empty).

## Erosion Example

The document provides a series of images to illustrate the concept of erosion.

## Dilation

With $A$ and $B$ as sets in $Z^{2}$, the dilation of $A$ by $B$, denoted $A \oplus B$, is defined as:

The dilation of $A$ by $B$ is the set of all displacements such that the reflection of $B$ and $A$ overlap by at least one element.

The basic process of flipping $B$ about its origin and then successively displacing it so that it slides over set (image) $A$ is analogous to spatial convolution.

One of the simplest applications of dilation is for bridging gaps.

## Opening and Closing

Given an image $A$ and a SE $B$:

*   **Opening:** Erosion followed by a dilation.
*   **Closing:** Dilation followed by an erosion.

### Opening

*   Smoothes the contour of an object.
*   Breaks narrow isthmuses.
*   Eliminates thin protrusions.

### Closing

*   Smooth sections of contours.
*   Fuses narrow breaks and long thin gulfs.
*   Eliminates small holes.
*   Fills gaps in the contour.

## Opening and Closing Examples

The document provides a series of images to illustrate the effects of opening and closing operations on noisy images and images with breaks/ridges.

## Hole Filling

A hole may be defined as a background region surrounded by a connected border of foreground pixels.

Given an initial point inside a hole, the goal is to fill the hole with 1s.

Let $X_0$ be the initial array with the same size as $A$, filled with 0s except at the location of a given point in each hole.

The following iterative procedure fills all holes with 1s: (The specific iterative procedure is not defined in the text).

## Connected Components

Let $X_0$ be the initial array with the same size as $A$, filled with 0s except at the location of a known point in each region.

The following iterative procedure fills the connected component with 1s: (The specific iterative procedure is not defined in the text).

## Boundary Extraction

The boundary of a set $A$ can be obtained by first eroding $A$ by $B$ and then performing the set difference between $A$ and its erosion:

## Moore Boundary Tracking

Several algorithms require extracting an ordered sequence of foreground boundary points from a region.

### Assumptions:

1.  We are working with binary thresholded images: 0: background, 1: foreground.
2.  Images are padded with a border of 0s so that no foreground region touches the image border.

### Algorithm:

1.  Let the starting point, $b_0$, be the uppermost, leftmost point in the image that is labeled 1.
    *   Let $c_0$ be the west neighbor of $b_0$.
2.  (Initialization) Examine the 8-neighbors of $b_0$, starting at $c_0$ and proceeding in a clockwise direction.
    *   Let $b_1$ denote the first neighbor encountered whose value is 1.
    *   Let $c_1$ be the (background) point immediately preceding $b_1$ in the sequence.
3.  Let $b = b_1$ and $c = c_1$.
4.  Let the 8-neighbors of $b$, starting at $c$ and proceeding in a clockwise direction, be denoted by $n_1, n_2, ..., n_8$. Find the first $n_k$ labeled 1.
5.  Let $b = n_k$, $c = n_{k-1}$.
6.  Repeat Steps 3 and 4 until $b = b_0$ and the next boundary point found is $b_1$. The sequence of $b$ points found when the algorithm stops constitutes the set of ordered boundary points.

The document includes a series of diagrams illustrating the steps of the Moore boundary tracking algorithm.

## Gray-Scale Morphology

So far, we considered thresholded images to derive a set of morphological operations using set theory.

Erosion, dilation, opening, and closing can also be defined for grayscale images.

The structuring element $b$ is used as a "probe" to examine a given image for specific properties. Can be non-flat or flat (more common).

### Erosion

The erosion of $f$ by a flat structuring element $b$ at any location $(x, y)$ is defined as the minimum value of the image in the region defined by $b$ when the origin of $b$ is at $(x, y)$:

The operation is conceptually similar to convolution. The structuring element $b$ is shifted at every pixel location of the image, and the minimum operation is performed among all the pixels in the region coincident with $b$.

### Dilation

The dilation of $f$ by a flat structuring element $b$ at any location $(x, y)$ is defined as the maximum value of the image in the region defined by the reflection of $b$ when the origin of it is at $(x, y)$.

Note the negative sign of the displacement resulting from the relation.

### Effect of Erosion

Since erosion computes minimum intensity values over every neighborhood of $(x, y)$, the resulting image is darker, and the size of bright features is, in general, reduced.

### Effect of Dilation

Dilation gives opposite results with respect to erosion. The resulting image is brighter, bright features are thickened, and the intensities of the dark features are reduced.

### Opening and Closing

The expressions for opening and closing gray-scale images have the same form as their binary counterparts.

### Geometric Interpretation:

Suppose that $f$ and $b$ are 3D surfaces.

*   The opening of $f$ by $b$ is like pushing the structuring element up from below against the undersurface of $f$.
*   The closing operation is like pushing down the structuring element on top of the curve while being translated to all locations.

### Effect of Opening

Opening attenuates bright features and has a negligible effect on the dark features and the background of the image.

### Effect of Closing

Closing attenuates dark features and has a negligible effect on the bright features and the background of the image.

## Morphological Smoothing

Because opening suppresses bright details, and closing suppresses dark details, they are often used in combination for image smoothing and noise removal.

## Morphological Gradient

The dilation thickens regions in an image, and the erosion shrinks them. Their difference is an operation with the effect of emphasizing the boundaries between regions.

The net result is an image in which the edges are enhanced, and the contribution of the homogeneous areas is suppressed, thus producing a "derivative-like" (gradient) effect.

## Top-Hat, Bottom-Hat

The top-hat transformation of a grayscale image $f$ is defined as $f$ minus its opening:

The bottom-hat transformation of $f$ is defined as the closing of $f$ minus $f$:

Goal: Select objects from an image by using a structuring element in the opening or closing operation that does not fit the objects to be removed. The difference then removes just the selected objects.

### Top-Hat to Correct Illumination

If images exhibit uneven illumination, a global thresholding operation may fail in some areas.

The document mentions using a top-hat transformation to correct illumination issues, followed by Otsu thresholding for improved results.

```

Citations:
[1] https://ppl-ai-file-upload.s3.amazonaws.com/web/direct-files/52995484/64e1ec0b-878e-4bab-9956-a19c703835b8/6_Morphological_image_processing.pdf