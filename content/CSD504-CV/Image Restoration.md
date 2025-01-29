# Image Restoration in Computer Vision

## Introduction

The primary goal of image restoration is to recover an "ideal" image from a degraded version. This process attempts to reverse the effects of imperfections introduced during image acquisition or transmission.

## Key Concepts

### Inverse Filtering (Idealized)

The fundamental concept can be represented by the following equation:

$\text{Ideal Image} = (\text{DM})^{-1} * \text{Restored Image}$

Where:
*   **Ideal Image:** The original, uncorrupted image (what we want).
*   **Restored Image:** The image *after* applying a restoration technique (our best estimate).
*   **DM:** Degradation Model (also called Degradation Function or Point Spread Function - PSF).
*   **(DM)⁻¹:** Inverse of the Degradation Model.

### Degradation Model (DM)

*   The DM mathematically describes how the image was degraded.
*   It models the blurring, noise, or geometric distortions that affected the original image.

#### Common Types of Degradation:

*   **Blur:**
    *   Motion blur (camera or subject movement).
    *   Out-of-focus blur (lens not properly focused).
    *   Atmospheric turbulence (for aerial or astronomical images).
*   **Noise:**
    *   Random variations in pixel values.
    *   Often introduced by image sensors (sensor noise) or during transmission (transmission errors).
*   **Geometric Distortions:**
    *   Warping, twisting, or other spatial transformations of the image.
