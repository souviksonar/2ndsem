Geometric transformations are fundamental operations in image processing and computer graphics that alter the spatial arrangement of pixels in an image. They can be represented efficiently using matrix operations.

**1. Translation**

*   **Concept:**  Shifting an image horizontally and/or vertically.
*   **Parameters:**
    *   $t_x$: Translation distance along the x-axis.
    *   $t_y$: Translation distance along the y-axis.
*   **Transformation Equations:**
    Let $(x, y)$ be the original pixel coordinates and $(x', y')$ be the translated coordinates.
    $x' = x + t_x$
    $y' = y + t_y$

*   **Matrix Form (Homogeneous Coordinates):**
    To represent translation in matrix form, we use homogeneous coordinates. A 2D point $(x, y)$ is represented as a 3D vector $(x, y, 1)$.

    $\begin{bmatrix} x' \\ y' \\ 1 \end{bmatrix} = \begin{bmatrix} 1 & 0 & t_x \\ 0 & 1 & t_y \\ 0 & 0 & 1 \end{bmatrix} \begin{bmatrix} x \\ y \\ 1 \end{bmatrix}$

    Where:
    *  $\mathbf{T} = \begin{bmatrix} 1 & 0 & t_x \\ 0 & 1 & t_y \\ 0 & 0 & 1 \end{bmatrix}$ is the translation matrix.

**2. Rotation**

*   **Concept:** Rotating an image around a specific point (usually the origin).
*   **Parameters:**
    *   $\theta$: Rotation angle (in radians or degrees). Positive values usually indicate counterclockwise rotation.
*   **Transformation Equations:**
    Let $(x, y)$ be the original pixel coordinates and $(x', y')$ be the rotated coordinates.
    $x' = x \cos(\theta) - y \sin(\theta)$
    $y' = x \sin(\theta) + y \cos(\theta)$

*   **Matrix Form (Homogeneous Coordinates):**

    $\begin{bmatrix} x' \\ y' \\ 1 \end{bmatrix} = \begin{bmatrix} \cos(\theta) & -\sin(\theta) & 0 \\ \sin(\theta) & \cos(\theta) & 0 \\ 0 & 0 & 1 \end{bmatrix} \begin{bmatrix} x \\ y \\ 1 \end{bmatrix}$

    Where:
    *  $\mathbf{R} = \begin{bmatrix} \cos(\theta) & -\sin(\theta) & 0 \\ \sin(\theta) & \cos(\theta) & 0 \\ 0 & 0 & 1 \end{bmatrix}$ is the rotation matrix.
- [[Derivation of Rotation Geometric Transformation]]

**3. Scaling**

*   **Concept:** Enlarging or shrinking an image along the x and/or y axes.
*   **Parameters:**
    *   $s_x$: Scaling factor along the x-axis.
    *   $s_y$: Scaling factor along the y-axis.
*   **Transformation Equations:**
    Let $(x, y)$ be the original pixel coordinates and $(x', y')$ be the scaled coordinates.
    $x' = s_x \cdot x$
    $y' = s_y \cdot y$

*   **Matrix Form (Homogeneous Coordinates):**

    $\begin{bmatrix} x' \\ y' \\ 1 \end{bmatrix} = \begin{bmatrix} s_x & 0 & 0 \\ 0 & s_y & 0 \\ 0 & 0 & 1 \end{bmatrix} \begin{bmatrix} x \\ y \\ 1 \end{bmatrix}$

    Where:
    * $\mathbf{S} = \begin{bmatrix} s_x & 0 & 0 \\ 0 & s_y & 0 \\ 0 & 0 & 1 \end{bmatrix}$ is the scaling matrix.

**Combining Transformations**

Multiple transformations can be combined by multiplying their corresponding matrices. The order of matrix multiplication matters, as matrix multiplication is not commutative.

For example, to perform a rotation followed by a translation, the combined transformation matrix $\mathbf{M}$ would be:

$\mathbf{M} = \mathbf{T} \cdot \mathbf{R}$

Then, to apply this combined transformation to a point:

$\begin{bmatrix} x' \\ y' \\ 1 \end{bmatrix} = \mathbf{M} \begin{bmatrix} x \\ y \\ 1 \end{bmatrix}$

**Note:** In general, to apply a sequence of transformations represented by matrices $\mathbf{M}_1, \mathbf{M}_2, ..., \mathbf{M}_n$, the combined transformation matrix is:

$\mathbf{M} = \mathbf{M}_n \cdot ... \cdot \mathbf{M}_2 \cdot \mathbf{M}_1$ (multiply from right to left in the order of operations).


Okay, here are concise digital notes on Euclidean, affine, and projective transformations, emphasizing their mathematical representations:

# Other Transformation
**1. Euclidean Transformation**

*   **Concept:** Preserves distances and angles. Includes rotations, translations, and reflections. Also known as a **rigid-body transformation** or **isometry**.
*   **Degrees of Freedom:** 3 in 2D (one rotation angle, two translation parameters).
*   **General Form:**
    $\mathbf{x'} = \mathbf{R}\mathbf{x} + \mathbf{t}$
    Where:
    *   $\mathbf{x}$, $\mathbf{x'}$: Original and transformed points (2x1 vectors in 2D).
    *   $\mathbf{R}$: Rotation matrix (2x2 in 2D), orthogonal with determinant 1.
    *   $\mathbf{t}$: Translation vector (2x1 in 2D).
*   **Matrix Form (Homogeneous Coordinates):**
    $\begin{bmatrix} x' \\ y' \\ 1 \end{bmatrix} = \begin{bmatrix} \mathbf{R} & \mathbf{t} \\ \mathbf{0}^T & 1 \end{bmatrix} \begin{bmatrix} x \\ y \\ 1 \end{bmatrix} = \begin{bmatrix} r_{11} & r_{12} & t_x \\ r_{21} & r_{22} & t_y \\ 0 & 0 & 1 \end{bmatrix} \begin{bmatrix} x \\ y \\ 1 \end{bmatrix}$
    Where:
    *  $r_{11}^2 + r_{21}^2 = 1$
    *  $r_{12}^2 + r_{22}^2 = 1$
    *  $r_{11}r_{12} + r_{21}r_{22} = 0$
    * $r_{11} = \cos \theta, r_{12} = - \sin \theta, r_{21} = \sin \theta, r_{22} = \cos \theta$

**2. Affine Transformation**

*   **Concept:** Preserves parallelism of lines but not necessarily distances and angles. Includes shearing and scaling in addition to Euclidean transformations.
*   **Degrees of Freedom:** 6 in 2D.
*   **General Form:**
    $\mathbf{x'} = \mathbf{A}\mathbf{x} + \mathbf{t}$
    Where:
    *   $\mathbf{x}$, $\mathbf{x'}$: Original and transformed points (2x1 vectors in 2D).
    *   $\mathbf{A}$: Arbitrary 2x2 matrix (not necessarily orthogonal).
    *   $\mathbf{t}$: Translation vector (2x1 in 2D).
*   **Matrix Form (Homogeneous Coordinates):**
    $\begin{bmatrix} x' \\ y' \\ 1 \end{bmatrix} = \begin{bmatrix} \mathbf{A} & \mathbf{t} \\ \mathbf{0}^T & 1 \end{bmatrix} \begin{bmatrix} x \\ y \\ 1 \end{bmatrix} = \begin{bmatrix} a_{11} & a_{12} & t_x \\ a_{21} & a_{22} & t_y \\ 0 & 0 & 1 \end{bmatrix} \begin{bmatrix} x \\ y \\ 1 \end{bmatrix}$

**3. Projective Transformation**

*   **Concept:** Most general linear transformation of homogeneous coordinates. Preserves straight lines but not necessarily parallelism, lengths, or angles. Used to model perspective projections. Also known as a **homography**.
*   **Degrees of Freedom:** 8 in 2D.
*   **General Form:**
    Cannot be expressed in the simple $\mathbf{x'} = \mathbf{A}\mathbf{x} + \mathbf{t}$ form.
*   **Matrix Form (Homogeneous Coordinates):**
    $\begin{bmatrix} x' \\ y' \\ w' \end{bmatrix} = \begin{bmatrix} h_{11} & h_{12} & h_{13} \\ h_{21} & h_{22} & h_{23} \\ h_{31} & h_{32} & h_{33} \end{bmatrix} \begin{bmatrix} x \\ y \\ 1 \end{bmatrix}$
    Where:
    *   $x_{inh}' = x'/w'$
    *   $y_{inh}' = y'/w'$
    *   $(x_{inh}', y_{inh}')$ are inhomogeneous coordinates of the transformed point.
    *   $\mathbf{H}$ is a 3x3 homogeneous matrix defined up to a scale factor (only the ratios of the elements matter).
    *   We can usually set $h_{33} = 1$ (unless it's zero).

**Summary Table**

| Transformation          | Degrees of Freedom | Preserves                      | Matrix Form (2D)                                                                                                                      |
| :---------------------- | :----------------: | :----------------------------- | :------------------------------------------------------------------------------------------------------------------------------------ |
| Euclidean               |         3          | Distances, angles, parallelism | $\begin{bmatrix} \mathbf{R} & \mathbf{t} \\ \mathbf{0}^T & 1 \end{bmatrix}$, $\mathbf{R}$ is orthogonal, det($\mathbf{R}$) = 1        |
| Affine                  |         6          | Parallelism                    | $\begin{bmatrix} \mathbf{A} & \mathbf{t} \\ \mathbf{0}^T & 1 \end{bmatrix}$, $\mathbf{A}$ is arbitrary                                |
| Projective (Homography) |         8          | Straight lines                 | $\begin{bmatrix} h_{11} & h_{12} & h_{13} \\ h_{21} & h_{22} & h_{23} \\ h_{31} & h_{32} & h_{33} \end{bmatrix}$, defined up to scale |
