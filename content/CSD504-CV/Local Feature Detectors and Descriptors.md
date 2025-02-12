---
refer: "[[Local Feature Detectors and Descriptors]]"
---


# Motivation

*   Global features from the whole image are often not desirable.  Histograms of entire images can be significantly different even if they depict the same object, due to changes in viewpoint, lighting, etc.
*   Instead, we match local regions which are prominent to the object or scene in the image. These local regions offer more robustness to changes in the overall image.
*   **Application Areas:**
    *   Object detection
    *   Image matching
    *   Image stitching

# Requirements of a Local Feature

*   **Repetitive:** The detector should find the same physical points in the scene independently in each image, regardless of viewing conditions.
*   **Invariant to translation, rotation, scale:**  The feature should be detectable regardless of the object's position, orientation, or size in the image.
*   **Invariant to affine transformation:**  The feature should be robust to distortions like shearing.
*   **Invariant to the presence of noise, blur, etc.:** The feature should be detectable even with image degradation.
*   **Locality:** The feature should be robust to occlusion (parts of the object being hidden), clutter (other objects in the scene), and illumination changes.
*   **Distinctiveness:** The region around the feature should contain an "interesting" structure, making it easily distinguishable from other features.
*   **Quantity:** There should be enough feature points detected to adequately represent the image.
*   **Time efficient:**  The feature detection and description process should be computationally feasible.

# General Approach

1.  **Find the interest points.**  These are locations in the image that are likely to be stable and distinctive, such as corners.
2.  **Consider the region around each keypoint.** A patch of pixels surrounding the detected interest point is analyzed.
3.  **Compute a local descriptor from the region and normalize the feature.** This descriptor is a numerical representation of the region's appearance, designed to be invariant to various transformations.  Normalization helps with robustness to lighting changes.
4.  **Match local descriptors.**  Descriptors from different images are compared (e.g., using Euclidean distance), and matches are identified based on a similarity threshold. $d(f_A, f_B)$ < T, where $f_A$ and $f_B$ are feature vectors, and $T$ is a threshold.

# Some Popular Detectors

*   Hessian/Harris corner detection
*   Laplacian of Gaussian (LOG) detector
*   Difference of Gaussian (DOG) detector
*   Hessian/Harris Laplacian detector
*   Hessian/Harris Affine detector
*   Maximally Stable Extremal Regions (MSER)
*   Many others....

These detectors often look for changes in the image gradient in two directions, which typically indicates corners.
* **No change in any direction:** Indicates a flat region.
* **Change in one direction only:** Indicates an edge.
* **Change in both directions:** Indicates a corner.

# Hessian Corner Detector

[Beaudet, 1978]

Searches for image locations that have a strong change in gradient along both orthogonal directions.

The Hessian matrix captures the second-order derivatives of the image intensity:

$H(x, \sigma) = \begin{bmatrix} I_{xx}(x, \sigma) & I_{xy}(x, \sigma) \\ I_{xy}(x, \sigma) & I_{yy}(x, \sigma) \end{bmatrix}$

Where:

*   $I_{xx}$ is the second-order derivative of the image intensity with respect to x.
*   $I_{yy}$ is the second-order derivative of the image intensity with respect to y.
*   $I_{xy}$ is the mixed second-order derivative with respect to x and y.
*   $(x, \sigma)$ represents the location and scale.

The determinant of the Hessian is used as a measure of cornerness:

$\text{det}(H) = I_{xx}I_{yy} - I_{xy}^2$

*   **Non-maximum suppression:** A $3 \times 3$ window is used. Only points with a determinant value higher than all 8 neighbors are kept.
*  **Thresholding:** Select points where $\text{det}(H) > \theta$, where $\theta$ is a predefined threshold.

**Effect:** Responses are mainly on corners and strongly textured areas.

# Harris Corner Detector

[Forstner and Gulch, 1987]

Searches for local neighborhoods where the image content has two main directions (eigenvectors of the autocorrelation matrix).

*   **Second Moment Autocorrelation Matrix:**

$C(x, \sigma, \tilde{\sigma}) = G(x, \tilde{\sigma}) * \begin{bmatrix} I_x^2(x, \sigma) & I_x I_y(x, \sigma) \\ I_x I_y(x, \sigma) & I_y^2(x, \sigma) \end{bmatrix}$

Where:

*   $G(x, \tilde{\sigma})$ is a Gaussian kernel with standard deviation $\tilde{\sigma}$.
*  $\tilde{\sigma} \approx 2\sigma$
*   $I_x$ and $I_y$ represent the image gradients in the x and y directions, respectively.
*    $\ast$ denotes convolution.

*   The Gaussian kernel sums over all the pixels in a circular local neighborhood, weighting them according to a Gaussian distribution.

The autocorrelation matrix, C, can be decomposed and represented as:

$C = \begin{bmatrix} \sum I_x^2 & \sum I_x I_y \\ \sum I_x I_y & \sum I_y^2 \end{bmatrix} = R^{-1} \begin{bmatrix} \lambda_1 & 0 \\ 0 & \lambda_2 \end{bmatrix} R$

Where:

*   $\lambda_1$ and $\lambda_2$ are the eigenvalues of C.
*   R is a rotation matrix.
*    The summation happens on neighborhood of x.

*  **Corner Condition**: If  $\lambda_1$ or $\lambda_2$ is about 0, the point is not a corner.

## Harris Corner: Eigen Decomposition Visualization

*   **Edge:** One eigenvalue is much larger than the other ($\lambda_2 >> \lambda_1$ or $\lambda_1 >> \lambda_2$).
*   **Corner:** Both eigenvalues are large, and $\lambda_1 \sim \lambda_2$.  The change in intensity (E) increases in all directions.
*   **Flat Region:** Both eigenvalues are small.

## Harris Corner: Different Approach

Instead of explicitly computing the eigenvalues, the following equivalence is used:

$\text{det}(C) = \lambda_1 \lambda_2$

$\text{trace}(C) = \lambda_1 + \lambda_2$

If $r = \frac{\lambda_1}{\lambda_2} (\ge 1)$, then $\frac{\text{trace}^2(C)}{\text{det}(C)} = \frac{(\lambda_1 + \lambda_2)^2}{\lambda_1 \lambda_2} = \frac{(r\lambda_2 + \lambda_2)^2}{r\lambda_2^2} = \frac{(r+1)^2}{r} = r + 2 + (1/r)$

Define the Harris cornerness measure, $H_c$:

$H_c = \text{det}(C) - \alpha \cdot \text{trace}^2(C) > \text{threshold}$

*  $\alpha$ is a sensitivity parameter, typically in the range 0.04 - 0.25 (experimentally verified).
*  Consider points where the Harris measure is greater than threshold.
Let, $r=2$, then $\text{trc}^2 = dc \ast (4.5)$
* **For edge:** r>>1, say 5, $H_c = dc(1-7.2 \ast 0.1) = 0.3 \ast dc$
* **For r = 10:** $H_c = dc(1-12.1 \ast 0.05) = 0.4 \ast dc$
* **For corners, r = 2:** $H_c = dc(1 - 4.5 \ast 0.1) = dc \ast 0.55$

## Harris Corner: Example

5.  **Image Derivatives:** Compute the image derivatives $I_x$ and $I_y$.
6.  **Square of Derivatives:** Calculate the squared derivatives: $I_x^2$, $I_y^2$, and $I_x I_y$.
7.  **Gaussian Filter:** Apply a Gaussian filter $G(\sigma_I)$ to the squared derivatives: $g(I_x^2)$, $g(I_y^2)$, and $g(I_x I_y)$.
8.  **Cornerness Function:** Compute the Harris cornerness function $g(I_x I_y)$, where both eigenvalues are strong.

## Harris Corner: Result

Effect: A very precise corner detector.

# Scale Invariant Region Detection

Hessian and Harris corner detectors are *not* scale-invariant. The response of the detector changes significantly as the image is scaled.

$|LoG(x, \sigma_n)| = \sigma_n^2 |L_{xx}(x, \sigma_n) + L_{yy}(x, \sigma_n)|$

**Solution:** Use the concept of Scale Space.

# Laplacian of Gaussian (LOG) Detector

[Lindeberg, 1998]

*   Uses the concept of Scale Space.
*   Instead of taking zero-crossings (as used for edge detection), consider the point which is a maximum among its 26 neighbors (9 in the same scale + 9 in the scale above + 9 in the scale below = 27, minus the point itself).

$L(x, \sigma) = \sigma^2 (I_{xx}(x, \sigma) + I_{yy}(x, \sigma))$

*   LOG can be used for finding the *characteristic scale* for a given image location.  This is the scale at which the LOG response is maximized.
*   LOG can be used for finding scale-invariant regions by searching for 3D (location + scale) extrema of the LOG.
*   LOG is also used for edge detection (by finding zero-crossings).

## LOG Detector: Flowchart

1.  Compute the second derivatives: $I_{xx}(\sigma) + I_{yy}(\sigma)$
2.  Apply Gaussian smoothing at different scales ($\sigma$, $\sigma^2$, $\sigma^3$, $\sigma^4$,...).
3.  Construct a scale-space representation.
4.  Find local maxima in 3D (x, y, scale). This produces a list of (x, y, s) coordinates, where (x, y) is the location and s is the scale.

## LOG Detector: Result

The detector identifies blob-like regions at various scales.

# Difference of Gaussian (DOG) Detector

[Lowe, 2004]

Approximates the LOG using a Difference of Gaussians (DOG) for computational efficiency.

$D(x, \sigma) = (G(x, k\sigma) - G(x, \sigma)) * I(x)$

Where:

*   $G(x, \sigma)$ is a Gaussian kernel with standard deviation $\sigma$.
*   $k = 2^{1/K}$, where K is a constant (determines the number of scales per octave).
*   K = 0, 1, 2, ..., constant
*   $I(x)$ is the input image.

Consider the region where the DOG response is greater than a threshold and the scale lies in a predefined range \[$s_{min}$, $s_{max}$].

## DOG Detector: Flowchart

5.  Apply Gaussian smoothing at different scales to the input image.
6.  Compute the difference between successive Gaussian-smoothed images. This creates the Difference of Gaussian (DOG) images.
7.  Construct a scale-space pyramid (multiple octaves, where each octave represents a halving of the image resolution).
8.  Find local extrema (maxima or minima) in the 3D scale-space (x, y, scale).  A point X is selected if it is larger or smaller than all its neighbors in the current scale and adjacent scales.

## DOG Detector: Result

Similar to the LOG detector, the DOG detector identifies blob-like features at multiple scales.

# Local Descriptors

*   We have detected interest points (keypoints) in an image.
*   **How to match the points across different images of the same object?**

**Solution:** Use Local Descriptors.

# List of Local Feature Descriptors

*   Scale Invariant Feature Transform (SIFT)
*   Speed-Up Robust Feature (SURF)
*   Histogram of Oriented Gradient (HOG)
*   Gradient Location Orientation Histogram (GLOH)
*   PCA-SIFT
*   Pyramidal HOG (PHOG)
*   Pyramidal Histogram Of visual Words (PHOW)
*   Others (Shape Context, Steerable filters, Spin images).

Local descriptors should be robust to viewpoint change or illumination change.

# SIFT

[Lowe, 2004]

## Step 1: Scale-Space Extrema Detection

*   Detect interesting points (invariant to scale and orientation) using DOG.

## Step 2: Keypoint Localization

*   Determine the location and scale at each candidate location.
*   Select keypoints based on stability.
*   **Aim:** Reject low-contrast points and points that lie on edges.

    *   **Low contrast points elimination:**
        *   Fit keypoint at $\underline{x}$ to nearby data using a quadratic approximation:

            $D(\underline{x}) = D + \frac{\partial D^T}{\partial \underline{x}} \underline{x} + \frac{1}{2} \underline{x}^T \frac{\partial^2 D^T}{\partial \underline{x}^2} \underline{x}$

            Where,  $D(x,\sigma) = (G(x, k\sigma) - G(x,\sigma)) \ast I(x)$

        *   Calculate the local maxima of the fitted function.
       $\partial D / \partial \underline{x} = \left[D +  \frac{\partial D^T}{\partial \underline{x}} \underline{x} + \frac{1}{2} \underline{x}^T \frac{\partial^2 D}{\partial \underline{x}^2} \underline{x} \right] / \partial \underline{x} = 0$
       $\underline{\hat{x}} = - \frac{\partial^2 D^{-1}}{\partial \underline{x}^2} \frac{\partial D}{\partial \underline{x}}$
        *   Discard local minima (for contrast): $D(\underline{\hat{x}}) < 0.03$

    *   **Eliminating edge response:**
        *   DOG gives a strong response along edges.
        *   **Solution:** Check the "cornerness" of each keypoint.
        *   On an edge, one principal curvature is much bigger than another.
        *   High cornerness $\iff$ No dominant principal curvature component.
        *   Consider the concept of Hessian and Harris corner detection.

            Hessian Matrix:

            $H = \begin{bmatrix} I_{xx} & I_{xy} \\ I_{xy} & I_{yy} \end{bmatrix}$

            Harris corner criterion:

            $\frac{\text{Tr}(H)^2}{\text{Det}(H)} < \frac{(r+1)^2}{r}$  Discard points with a response below the threshold.

## Step 3: Orientation Assignment

*   **Aim:** Assign a consistent orientation to each keypoint based on local image properties to obtain rotational invariance.

    *   To transform relative data accordingly.

    *   The magnitude and orientation of the gradient of an image patch I(x, y) at a particular scale are:

        $m(x, y) = \sqrt{(I(x+1, y) - I(x-1, y))^2 + (I(x, y+1) - I(x, y-1))^2}$

        $\theta(x, y) = \tan^{-1} \frac{I(x, y+1) - I(x, y-1)}{I(x+1, y) - I(x-1, y)}$

*   Create a weighted (magnitude + Gaussian) histogram of local gradient directions computed at the selected scale.
*   Assign the dominant orientation of the region as that of the peak of the smoothed histogram.
*   For multiple peaks, create multiple keypoints (one for each significant peak).

## Step 4: Keypoint Descriptor

*   **Aim:** Obtain a local descriptor that is highly distinctive yet invariant to variations like illumination and affine change.

*   Consider a rectangular grid (e.g., 16x16) in the direction of the dominant orientation of the region.
*   Divide the region into 4x4 sub-regions.
*   Consider a Gaussian filter above the region, which gives higher weights to pixels closer to the center of the descriptor.
*   Create 8-bin gradient histograms for each sub-region.  The bins are weighted by the gradient magnitude and a Gaussian window (where $\sigma$ is half the window size).
*   This results in a feature vector of dimension 128 (8 bins * 4 * 4 subregions = 128).
*   Finally, normalize the 128-dimensional vector to make it illumination invariant.

# SIFT: Some Results

* **Object detection:** SIFT features can be used to detect objects in images.
* **Panorama stitching:** SIFT can be used to find corresponding points in overlapping images to create panoramas.

# GLOH

Gradient Location and Orientation Histogram (GLOH)

*   First 3 steps – same as SIFT.
*   **Step 4 – Local image descriptor:**
    *   Consider a log-polar location grid with 3 different radii and 8 angular directions for two of them, resulting in a total of 17 location bins.
    *   Form a histogram of gradients having 16 bins.
    *   Form a feature vector of 272 dimensions (17 * 16).
    *   Perform dimensionality reduction and project the features to a 128-dimensional space.

# Some Other Examples

*SURF, PHOW, HOG*

# References

9.  Kristen Grauman and Bastian Leibe, Visual Object Recognition, Synthesis Lectures on Artificial Intelligence and Machine Learning, April 2011, Vol. 5, No. 2, Pages 1-181.
10.  Beaudet, “Rotationally invariant image operators", in International Joint Conference on Pattern Recognition, pp. 579-583., 1978.
11.  Förstner, W. and Gülch, E., "A fast operator for detection and precise location of distinct points, corners and centers of circular features", in ISPRS Inter commission Workshop', pp. 281-305, 1987.
12.  Harris, C. and Stephens, M., “A combined corner and edge detector”, in 'Alvey Vision Conference', pp. 147–151, 1988.
13.  Lindeberg, T., 'Scale-space theory: A basic tool for analyzing structures at different scales', Journal of Applied Statistics 21(2), pp. 224–270, 1994.
14.  Lowe, D., 'Distinctive image features from scale-invariant keypoints', International Journal of Computer Vision 60(2), pp. 91–110, 2004.
15.  Mikolajczyk, K. and Schmid, C., 'A performance evaluation of local descriptors', IEEE Transactions on Pattern Analysis & Machine Intelligence 27(10), 31–37, 2005.
