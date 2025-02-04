## Texture Definition and Analysis

### Definition of Texture

Texture is defined as the regular repetition of an element or pattern on a surface.

### Purpose of Texture Analysis

1. **Identify and differentiate:** To identify different textured and non-textured regions within an image.
2. **Classify and segment:** To classify or segment different texture regions within an image.
3. **Extract boundaries:** To extract boundaries between major texture regions.
4. **Describe texel unit:** To describe the basic texture element (texel unit).
5. **3-D shape from texture:** To infer 3-D shape from texture variations.
### Texture Regions and Edges

Texture regions can be identified by examining the spatial variations in pixel intensities. Edges between texture regions represent abrupt changes in these spatial patterns.

## Texture Classification Process

### Typical Flow-chart

A typical texture classification method involves the following steps:

6. **Input Image:** The original image to be analyzed.
7. **Filtering:** Applying filters to enhance texture features.
8. **Smoothing:** Reducing noise and creating a more uniform representation.
9. **Classifier:** Using an algorithm to assign texture labels.
10. **Segmented Image:** The output image with segmented texture regions.

## Gabor Filters for Texture Analysis

### 2-D Gabor Filter

The 2-D Gabor filter is defined as:

$f(x, y, \omega, \theta, \sigma_x, \sigma_y) = \frac{1}{2\pi\sigma_x\sigma_y} \exp\left[-\frac{1}{2}\left(\left(\frac{x}{\sigma_x}\right)^2 + \left(\frac{y}{\sigma_y}\right)^2\right) + j\omega(x\cos\theta + y\sin\theta)\right]$

Where:

*   $\sigma$: spatial spread
*   $\omega$: frequency
*   $\theta$: orientation

![[CSD504-CV/media/media/GF.webp]]

[[GF.pdf#page=10&rect=190,59,576,776|GF, p.10]]
### Components of Gabor Filter

*   **Gaussian component:** Provides localization in the spatial domain.
*   **Sinusoidal component:** Provides frequency and orientation selectivity.

### 1-D Gabor Filter and Gaussian Function

**1-D Gabor Filter:**

$f(x, \omega, \sigma) = \frac{1}{\sqrt{2\pi}\sigma} \exp\left(-\frac{x^2}{2\sigma^2} + j\omega x\right)$

**1-D Gaussian Function:**

$g(x) = \frac{1}{\sqrt{2\pi}\sigma_1} \exp\left(-\frac{x^2}{2\sigma^2}\right)$

### Asymmetric 2-D Gaussian Function

An asymmetric Gaussian function can be used to create Gabor filters with varying shapes and orientations.

### General Form of Gabor Filter

$gab(x, y) = K \exp(-\pi(a^2(x-x_0)_\theta^2 + b^2(y-y_0)_\theta^2)) \exp(j(2\pi F_0 (x \cos \omega_0 + y \sin \omega_0) + P))$

Where:

*   $K$: Scales the magnitude of the Gaussian envelope.
*   $(a, b)$: Scale the two axes of the Gaussian envelope.
*   $\theta$: (Rotation) angle of the Gaussian envelope.
*   $(x_0, y_0)$: Location of the peak of the Gaussian envelope.
*   $(u_0, v_0)$: Spatial frequencies of the sinusoidal carrier in Cartesian coordinates. It can also be expressed in polar coordinates as $(F_0, \omega_0)$.
*   $P$: Phase of the sinusoidal carrier.

### Gabor Filter Parameters

*   **Spatial width ($\sigma$)**: Controls the size of the filter.
*   **Frequency ($\omega$)**: Determines the preferred frequency of the filter.
*   **Orientation ($\theta$)**: Specifies the preferred orientation of the filter.

### Fourier Transform of Gaussian and Gabor

**Gaussian:**

$g(t) = e^{-t^2/a}$

$G(u) = (\sqrt{a\pi})e^{-au^2/4}$

**Gabor:** The Fourier transform of a Gabor filter is a shifted Gaussian in the frequency domain.

### Dyadic Bank of Gabor Filters

A dyadic bank consists of Gabor filters with frequencies scaled by powers of 2, providing octave band decomposition.

### Properties of Gabor Filters

*   **Tunable bandpass filter:** Can be adjusted to select specific frequencies.
*   **Similar to STFT:** Similar to a Short-Time Fourier Transform or windowed Fourier transform.
*   **Uncertainty principle:** Satisfies the lower-most bound of the time-spectrum resolution.
*   **Multi-scale, multi-resolution:** Analyzes textures at different scales and resolutions.
*   **Selectivity:** Has selectivity for orientation, spectral bandwidth, and spatial extent.
*   **Human visual cortex:** Response is similar to that of the human visual cortex.
*   **Applications:** Used in texture segmentation, iris, face, and fingerprint recognition.
*   **Computational cost:** Often high due to the need for a large filter bank.

## Examples of Texture Segmentation Using Gabor Filters

### Texture Image Segmentation

Examples demonstrate how Gabor filters can be used to segment images based on texture:

17. **Texture Image:** Input image with different texture regions.
18. **Magnitude of the Gabor Responses:** Shows the strength of the filter responses.
19. **Smoothed Features:** Creates a more uniform representation of the filter responses.
20. **Initial and Final Classification:** Illustrates the process of assigning texture labels and refining the segmentation.

### SIR-C/X-SAR Image Segmentation

Gabor filters can also be applied to Synthetic Aperture Radar (SAR) images for texture-based classification.
Examples show:

21. **SIR-C/X-SAR image of Lost City of Ubar**
22. **Classification using multispectral information**
23. **Classification using multispectral and textural information**
## Filtering Methods, Non-linearity, Smoothing, Feature Vectors, and Classification

*   **Filtering methods:** Various methods like Discrete Wavelet Transform (DWT), Gabor Filter, Discrete Cosine Transform (DCT), Gaussian Markov random field models, and combinations of these can be used for texture analysis.
*   **Non-linearity:** The magnitude (|.|) operation is often used as a non-linearity.
*   **Smoothing:** Gaussian filters are commonly used for smoothing.
*   **Feature vectors:** The mean computed in a local window around a pixel can be used as a feature vector.
*   **Classification:** Fuzzy-C Means (FCM) is an example of an unsupervised classifier used for texture classification.
