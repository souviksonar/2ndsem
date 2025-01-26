# Filters

## 1. What is a Filter?

*   **Definition:** A small matrix (kernel) used to modify an image by performing a mathematical operation called **convolution**.
*   **Mechanism:** The filter slides across the image, pixel by pixel, applying its operation to each pixel neighborhood.
*   **Analogy:** Think of it like a "sliding window" that transforms the image as it moves.

## 2. Purpose of Filters

Filters are fundamental in image processing and computer vision, used for:

*   **Feature Extraction:**
    *   Highlighting patterns like edges, corners, textures, blobs.
*   **Image Enhancement:**
    *   Noise reduction
    *   Sharpening details
    *   Contrast adjustment
*   **Image Transformation:**
    *   Blurring
    *   Embossing
    *   Creating artistic effects

## 3. Types of Filters

### A. Linear Filters

*   **Definition:** Perform a **weighted sum** of pixel values in the neighborhood defined by the kernel.
    *   Output pixel = Linear combination of input pixel values.
*   **Properties:**
    *   Computationally efficient
    *   Easy to understand and implement
*   **Subtypes:**

    1. **Smoothing/Blurring Filters:**

        *   **Purpose:**
            *   Reduce noise
            *   Smooth out edges
            *   Create a blurring effect
        *   **Effect:**
            *   Less sharp image
            *   Removes fine details
        *   **Examples:**
            *   **Mean Filter (Box Blur):**  Each pixel becomes the average of its neighbors.
                *   *Note:* Larger kernel = more blur.
            *   **Gaussian Filter:** Weights neighbors using a Gaussian function (bell curve).
                *   *Note:* Closer pixels have higher weights, resulting in a more natural blur.

    2. **Sharpening Filters:**

        *   **Purpose:**
            *   Enhance edges and details
            *   Make the image appear sharper
        *   **Effect:**
            *   Increases contrast along edges
        *   **Examples:**
            *   **Laplacian Filter:** Highlights rapid intensity changes (edges) using the second derivative.
            *   **Unsharp Masking:** Sharpens by subtracting a blurred version from the original.

    3. **Edge Detection Filters:**

        *   **Purpose:**
            *   Detect edges (boundaries between regions of different intensity)
        *   **Effect:**
            *   Highlights sharp changes in pixel values
            *   Outlines edges in the image
        *   **Examples:**
            *   **Sobel Filter:** Calculates the image intensity gradient in horizontal and vertical directions.
            *   **Prewitt Filter:** Similar to Sobel, but with different coefficients.
            *   **Roberts Cross Filter:** Simple filter; computes the difference between diagonally adjacent pixels.

### B. Non-linear Filters

*   **Definition:** Output is based on a **non-linear function** applied to the pixel neighborhood (not just a weighted sum).
*   **Properties:**
    *   Can be better at preserving edges while removing noise
    *   Can handle specific types of features
    *   Computationally more expensive than linear filters
*   **Subtypes:**

    1. **Median Filter:**

        *   **Purpose:**
            *   Excellent for removing "salt-and-pepper" noise (random bright and dark pixels)
        *   **Effect:**
            *   Replaces each pixel with the *median* value of its neighbors
            *   Preserves edges better than mean filtering

    2. **Min Filter:**

        *   **Purpose:**
            *   Enhance dark features
            *   Remove bright noise
        *   **Effect:**
            *   Replaces each pixel with the *minimum* value in its neighborhood
            *   Darkens the image

    3. **Max Filter:**

        *   **Purpose:**
            *   Enhance bright features
            *   Remove dark noise
        *   **Effect:**
            *   Replaces each pixel with the *maximum* value in its neighborhood
            *   Brightens the image

    4. **Morphological Filters:**

        *   **Purpose:**
            *   Shape analysis
            *   Object manipulation
        *   **Effect:**
            *   Modify object shapes and structures based on a **structuring element** (a small shape used as a probe)
        *   **Examples:**
            *   Erosion
            *   Dilation
            *   Opening
            *   Closing

## 4. Filter Summary Table

| Filter Type        | Subtype           | Purpose                                   | Effect                                          |
| ------------------ | ----------------- | ----------------------------------------- | ----------------------------------------------- |
| **Linear**         | Smoothing/Blurring | Reduce noise, smooth edges                 | Less sharp, blurred image                     |
|                    | Sharpening        | Enhance edges, fine details                | Increased edge contrast, sharper image        |
|                    | Edge Detection   | Detect edges                            | Highlights sharp changes in intensity           |
| **Non-linear**     | Median            | Remove salt-and-pepper noise               | Preserves edges, reduces noise                 |
|                    | Min               | Enhance dark features, remove bright noise | Darker image, emphasizes dark areas            |
|                    | Max               | Enhance bright features, remove dark noise| Brighter image, emphasizes bright areas          |
|                    | Morphological     | Shape analysis, object manipulation       | Modifies object shapes and structure based on kernel |


> [!NOTE] 
> Median Filter is not linear filter

> [!NOTE] 
> Gaussian Filter is similar to human vision

