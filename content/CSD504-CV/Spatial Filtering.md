
# Spatial Filtering in Computer Vision

## 1. Spatial Frequency

*   **Concept:** Spatial frequency refers to the rate at which pixel intensity values change within an image.
    *   **High Spatial Frequency:**  Represents rapid changes in intensity over a short distance. This corresponds to sharp details, edges, and textures in an image.
    *   **Low Spatial Frequency:** Represents gradual changes in intensity over a larger distance. This corresponds to smooth regions, overall shapes, and the general background of an image.
*   **Visual Representation:**
    *   The handwritten notes depict this with a square and sine waves:
        *   Sharp, vertical/horizontal lines within the square represent high frequencies (edges).
        *   Sine waves with different wavelengths (frequencies) are used to illustrate how quickly the intensity is changing. Higher frequency waves represent faster changes.

*   **Bit Planes:**
    *   In some applications, analyzing the bit planes of an image is important.
    *   Each bit plane represents a specific bit position (e.g., most significant bit, least significant bit) across all pixels in the image.
    *   Higher-order bit planes often contain information about the overall structure and lower spatial frequencies, while lower-order bit planes might reveal finer details and higher spatial frequencies.

## 2. Spatial Filtering

*   **Concept:** Spatial filtering is the process of modifying an image by applying a filter (kernel) directly to its pixels in the spatial domain (i.e., directly on the image grid).
*   **Process:**
    *   The notes show a simplified diagram:
        *   `Org img` (Original Image) --> `Transfer` (Filter/Kernel applied) --> `Spectral Domain` or `Image`
        * The "Transfer" step represents a function, typically a kernel, that transforms the original image. It can either lead to the `Spectral Domain`, which is the representation of the image in frequency space (we'll cover that next), or it results in a modified image directly in the spatial domain (as with the filters discussed in previous notes).
*   **Relationship to Frequency:**
    *   **High frequencies correspond to edges and details.**
    *   **Low frequencies correspond to smoothness and general shapes.**
    *   Spatial filters can be designed to selectively enhance or suppress certain spatial frequencies.

## 3. Frequency Domain (Spectral Domain)

*   **Concept:** While spatial filtering operates directly on pixel values, the frequency domain offers an alternative representation of an image.
*   **Transformation:**
    *   Mathematical transforms, most notably the **Fourier Transform**, are used to convert an image from the spatial domain to the frequency domain.
    *   The Fourier Transform decomposes an image into its constituent frequencies (like decomposing a musical chord into its individual notes).
*   **In the Frequency Domain:**
    *   The center of the frequency domain representation typically corresponds to low frequencies.
    *   Pixels further away from the center represent higher frequencies.
*   **Filtering in the Frequency Domain:**
    *   Filters can be designed to operate in the frequency domain as well.
    *   For example, a **low-pass filter** would allow low frequencies to pass through (keeping smooth areas) while attenuating high frequencies (reducing noise and detail).
    *   A **high-pass filter** would do the opposite, preserving edges and details while suppressing smooth regions.
