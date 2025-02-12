

## Wavelets

-   Fourier transform has its basis functions in sinusoids.
-   Wavelets based on small waves of varying frequency and limited duration.
    -   Account for frequency and location of the frequency.
-   In addition to frequency, wavelets capture temporal information.
    -   Bound in both frequency and time domains.
    -   Localized wave and decays to zero instead of oscillating forever.
-   Form the basis of an approach to signal processing and analysis known as multiresolution theory.
    -   Concerned with the representation and analysis of images at different resolutions.
    -   Features that may not be prominent at one level can be easily detected at another level.
-   Comparison with Fourier transform:
    -   Fourier transform used to analyze signals by converting signals into a continuous series of sine and cosine functions, each with a constant frequency and amplitude, and of infinite duration.
        -   Real world signals (images) have a finite duration and exhibit abrupt changes in frequency.
        -   Wavelets are based on a *mother wavelet*, denoted by  $\psi(x)$.
            -   Wavelet transform converts a signal into a series of wavelets.
            -   Wavelet transform basis functions are obtained by scaling and shifting the mother wavelet:

                $\psi_{a,b}(x) = \frac{1}{\sqrt{a}}\psi(\frac{x - b}{a})$

                where $b$ is the translation to determine the location of wavelet and $a > 0$ is scaling to govern its frequency.

 
## Background

-   Objects in images are connected regions of similar texture and intensity levels.
-   Use high resolution to look at small objects; coarse resolution to look at large objects.
-   If you have both large and small objects, use different resolutions to look at them.
-    Images are 2D arrays of intensity values with locally varying statistics


## Image pyramids

-   Structure to represent images at more than one resolution.
-   Collection of decreasing resolution images arranged in the shape of a pyramid.
-   Figure 7.2a
    -   Highest resolution image at the pyramid base.
    -   As you move up the pyramid, both size and resolution decrease.
    -   Base level of size $2^J \times 2^J$.
    -   General level $j$ of size $2^j \times 2^j$, $0 \leq j \leq J$.
    -   Pyramid may get truncated at level $P$, $1 \leq P \leq J$.
    -   Number of pixels in a pyramid with $P + 1$ levels ($P > 0$) is:

        $N^2(1 + \frac{1}{4} + \frac{1}{4^2} + \dots + \frac{1}{4^P}) \leq \frac{4}{3}N^2$

-   Figure 7.2b
    -   Building image pyramids.
        -   Level $j - 1$ approximation output provides the images needed to build an *approximation pyramid*.
        -   Level $j$ prediction residual output is used to build a complementary *prediction residual pyramid*.
            -   Contain only one reduced-resolution approximation of the input image at the top level.
            -   All other levels contain prediction residuals where level $j$ prediction residual is the difference between level $j$ approximation and an estimate of the level $j - 1$ approximation based on the level $j - 1$ approximation.
    -   Both approximation and prediction residual pyramids are computed in an iterative fashion.
    -   Start by placing the original image in level $J$ of the approximation pyramid.
    -   Three step procedure:
        1.  Compute a reduced-resolution approximation of level $j$ input image; done by filtering and downsampling the filtered result by a factor of 2; place the resulting approximation at level $j - 1$ of approximation pyramid.
        2.  Create an estimate of level $j$ input image from the reduced resolution approximation generated in step 1; done by upsampling and filtering the generated approximation; resulting prediction image will have the same dimensions as the level $j$ input image.
        3.  Compute the difference between the prediction image of step 2 and input to step 1; place the result in level $j$ of prediction residual pyramid.
    -   After $P$ iterations, the level $J - P$ approximation output is placed in the prediction residual pyramid at level $J - P$.
    -  Variety of approximation and interpolation filters
        - Neighborhood averaging producing *mean* pyramids.
        - Lowpass Gaussian filtering producing *Gaussian* pyramids.
        - No filtering producing *subsampling* pyramids
        - Interpolation filter can be based on nearest neighbor, bilinear, and bicubic.

-   Upsampling:
    -   Doubles the spatial dimensions of approximation images.
    -   Given an integer $n$ and 1D sequence of samples $f(n)$, upsampled sequence is given by

        $f_{2\uparrow}(n) = \begin{cases} f(n/2) & \text{if } n \text{ is even} \\ 0 & \text{otherwise} \end{cases}$
    -   Insert a 0 after every sample in the sequence.

-   Downsampling:
    -   Halves the spatial dimensions of the prediction images.
    -   Given by

        $f_{2\downarrow}(n) = f(2n)$
    -   Discard every other sample.



## Haar Wavelet

-   Oldest and simplest orthonormal wavelets.
-   Expressed in matrix form as

    $T = HFH^T$

    -   $F$ is an $N \times N$ image matrix, $N = 2^n$.
    -   $H$ is an $N \times N$ Haar transformation, and contains the basis function $h_k(z)$ for the wavelet.
        -   Basis function defined over continuous closed interval $z \in [0, 1]$ for $k = 0, 1, \dots N$ where $N = 2^n$.
    -   $T$ is resulting $N \times N$ transform.
    -   Transform is required because $H$ is not symmetric.
    -   $H$ generated by defining the integer $k = 2^p + q - 1$ where $0 \leq p \leq n - 1, q = 0$ or $1$ for $p = 0$, and $1 \leq q \leq 2^p$ for $p \ne 0$.
        -   Haar basis functions are

            $h_0(z) = h_{00}(z) = \frac{1}{\sqrt{N}}, \quad z \in [0, 1]$

            $h_k(z) = h_{pq}(z) = \frac{1}{\sqrt{N}}\begin{cases} 2^{p/2} & (q - 1)/2^p \leq z < (q - 0.5)/2^p \\ -2^{p/2} & (q - 0.5)/2^p \leq z < q/2^p \\ 0 & \text{otherwise}, \quad z \in [0, 1] \end{cases}$

   



-   Haar scaling function is denoted by $\phi(t)$ and Haar wavelet function is denoted by $\psi(t)$.
-   Haar scaling function (averaging or lowpass filter) at level 0 (in the original signal) is given by

    $\phi(x) = \begin{cases} 1 & 0 \leq x < 1 \\ 0 & \text{otherwise} \end{cases}$

-   Translation by $j$ is denoted by $\phi_j(x)$

    $\phi_j(x) = \phi(x - j)$
-  Figure below shows both $\phi(x)$ and $\phi_j(x)$

      (Diagram showing phi and phi_j.  phi is a box from 0 to 1.  phi_j is a box from j to j+1.)

-   Coefficients of the signal $f$ indexed by $j$ are given by

    $c_j(f) = \int f(x)\phi_j(x)dx$
    $= \text{Average of } f \text{ over the interval } [j, j + 1]$
-   An approximate reconstruction of $f$ from $c_j(f)$ is given by

    $f_0(x) = \sum_j c_j(f)\phi_j(x)$


## Discrete Wavelet Transform
- CWT is redundant as the transform is calculated by continuously shifting a continuously scalable function over a signal and calculating the corelation between the two
- The discrete form is normally a [piecewise] continuous function obtained by sampling the time-scale space at discrete intervals.
- The process of transforming a continous signal into a series of wavelet coefficients is known as *wavelet series decomposition*.
- Scaling function can be expressed in wavelets from $ -\infty$ to $j$
- Adding a wavelet spectrum to the scaling function yields a new scaling function, with a spectrum twice as wide as the first.
	- Addition allows us to express the first scaling function in terms of the second
	- The formal expression of this phenomenon leads to multiresolution formulation or two-scale relation as

    $\phi(2^jt) = \sum_k h_{j+1}(k)\phi(2^{j+1}t - k)$

    -   This equation states that the scaling function (average) at a given scale can be expressed in terms of translated scaling functions at the next smaller scale, where the smaller scale implies more detail.
-   Similarly, the wavelets (detail) can also be expressed in terms of translated scaling functions at the next smaller scale as

    $\psi(2^jt) = \sum_k g_{j+1}(k)\phi(2^{j+1}t - k)$

-   The functions $h(k)$ and $g(k)$ are known as *scaling filter* and *wavelet filter*, respectively.
    -   These filters allow us to implement the *discrete wavelet transform (DWT)* as an iterated digital filter bank.

## Subsampling property

-   Gives a step size of 2 in the variable $k$ for scaling and wavelet filters.
-   Every iteration of filter banks reduces the number of samples by half so that in the
    -   In the last case, we are left with only one sample.

## Implementation of Haar Wavelets

-   Any wavelet implemented by the iteration of filters with rescaling.
    -   Set of filters form the *filter bank*.
    -   Let $k$ be an integer.
    -   Averaging and detail filters implemented using two $2^{k-1} \times 2^k$ filtering matrices $H$ and $G$ given by

        $$H = \begin{bmatrix}
        \frac{1}{2} & \frac{1}{2} & 0 & 0 & \cdots & 0 & 0 \\
        0 & 0 & \frac{1}{2} & \frac{1}{2} & \cdots & 0 & 0 \\
        \vdots & \vdots & \vdots & \vdots & \ddots & \vdots & \vdots \\
        0 & 0 & 0 & 0 & \cdots & \frac{1}{2} & \frac{1}{2}
        \end{bmatrix}
        $$

        $$G = \begin{bmatrix}
        \frac{1}{2} & -\frac{1}{2} & 0 & 0 & \cdots & 0 & 0 \\
        0 & 0 & \frac{1}{2} & -\frac{1}{2} & \cdots & 0 & 0 \\
        \vdots & \vdots & \vdots & \vdots & \ddots & \vdots & \vdots \\
        0 & 0 & 0 & 0 & \cdots & \frac{1}{2} & -\frac{1}{2}
        \end{bmatrix}$$
    -   Let $H^t$ and $G^t$ denote the transpose of $H$ and $G$, respectively.
    -   Let $I_k$ denote a $2^k \times 2^k$ identity matrix.
    -   Then, the following facts about $H$ and $G$ are true:

        $H^t \times H + G^t \times G = \frac{1}{2}I_k$
        $H \times H^t = G \times G^t = \frac{1}{2}I_{k-1}$
        $H \times G^t = G \times H^t = 0$

    -   For simplicity, consider the original signal to be sampled as a vector of length $2^k$.
    -   The filtering process includes downsampling ($\downarrow 2$) and decomposes $b$ into two vectors $b_1$ (for block average) and $d_1$ (for detail) given by

        $b_1 = H \times b$
        $d_1 = G \times b$
    -   $b_1$ and $d_1$ can be combined to reconstruct the original signal $b$

        $b = 2 \times (H^t \times b_1 + G^t \times d_1)$

        -   A lossy compression can be achieved by discarding the detail vector $d_1$, or setting it to be zero.

-   Haar filter is applied to an image by the application of $H$ and $G$ filters in a tensorial way.
    -   Let $P$ be a picture image represented as an $r \times c$ matrix of pixels.
    -   Applying the $H$ filter to $P$, we get a new image $P'$ as

        $P' = H \times P \times H^t$

    -   $P'$ is an $r' \times c'$ matrix such that

        $r' = \frac{r}{2}$
        $c' = \frac{c}{2}$

- Application of H and G filters results into four matrices given by.
    $P_{11} = H \times P \times H^t$
    $P_{12} = H \times P \times G^t$
    $P_{21} = G \times P \times H^t$
    $P_{22} = G \times P \times G^t$
    - $P_{11}$ is called the *fully averaged picture*.
    - $P_{12}$ and $P_{21}$ are called *partially averaged and partially differenced pictures*.
    - $P_{22}$ is called the *fully differenced picture*.

- The four components can be used to reconstruct the original image $P$ as.
    $P = [H^t \quad G^t] \times \begin{bmatrix} P_{11} & P_{12} \\ P_{21} & P_{22}\end{bmatrix} \times \begin{bmatrix} H \\ G \end{bmatrix}$
    - Above equation is known as a synthesis filter bank.
    - The matrix $\begin{bmatrix} H \\ G \end{bmatrix}^t$ is orthogonal as its inverse is the transpose, or

    $\begin{bmatrix} H \\ G \end{bmatrix}^{-1} =  \begin{bmatrix} H^t & G^t \end{bmatrix}$
    - Matrices in synthesis bank are also known as *orthogonal filter bank*.
    - Note that
       $\begin{bmatrix} H^t & G^t \end{bmatrix} \begin{bmatrix} H \\ G \end{bmatrix} = H^tH + G^tG = I$

        - The synthesis bank is the inverse of the analysis bank.
        - Analysis bank contains the steps for filtering and downsampling.
        - Synthesis bank reverses the order and performs upsampling and filtering.
 - Analysis of a picture (for two levels) is shown below

  (Diagram of a wavelet decomposition of an image, showing two levels.  The first level splits the original image into four quadrants:  top-left is the averaged image, top-right and bottom-left are partially averaged/differenced, and bottom-right is fully differenced.  The top-left quadrant is then further decomposed in the same way.)
- Figure below shows an original texture, and its compression and reconstruction

 (Diagram of wavelet compression/reconstruction. A satellite image is decomposed into four quadrants. The averaged quadrant is then further decomposed. The reconstruction uses only the final averaged image, with the detail images set to zero.)
    - Top left shows the original $256 \times 256$ pixel texture.
    -   Application of Haar wavelet results into four $128 \times 128$ pixel components which are combined into a $256 \times 256$ pixel image shown on top right.
        -   Top left quarter of this image shows the fully averaged part.
        -   Top right quarter contains the partially averaged part.
        -   Bottom left quarter contains the partially differenced part.
        -   Bottom right quarter contains the fully differenced component.
    -   Haar wavelet is applied to the fully averaged part again and the assembled components are shown in the bottom left picture.
    -   This picture is then used for reconstruction of the texture and the reconstructed texture is shown in the bottom right picture.
-   Lossy compression is achieved by discarding the differenced pictures (setting the matrices to zero) and retaining only $P_{11}$ during the reconstruction phase.
    -   The process can be carried through several processing steps, thus removing a large amount of detail information.

## Other wavelets

-   Haar wavelet transform, as described above, may not be able to take good advantage of the continuity of pixel values within images.
-   Other wavelets may perform better at this, and achieve higher compression of textures, specially if the textures are smooth images.

## JPEG 2000 Standard<sup>1</sup>

-   Based on wavelets to achieve compression.
-   Scalable in nature.
    -   Can be decoded in a number of ways.
    -   By truncating the codestream at any point, we can get the image representation at a lower resolution.
    -   Encoders and decoders are computationally demanding.
        -   Standard JPEG produces ringing artifacts at lower resolutions, specially near image edges.
            -   It also produces blocking artifacts due to its $8 \times 8$ blocks.
-   Comparison with standard JPEG
    -   Much better scalability and editability.
        -  In standard JPEG, you have to reduce the resolution of the input image before encoding if you want to go below a certain bit limit.
        -  Comes for free in JPEG 2000 because it does so automatically through multiresolution decomposition.
    - Superior Compression
        - Nearly imperceptible artifacts at higher bit rates.
        - At lower bit rates ($< 0.25$ bits/pixel for grayscale images), JPEG 2000 has less visible artifacts than standard JPEG and almost no blocking.
        - Compression gains are due to DWT and more sophisticated entropy coding.
    - Multiresolution representation
        - Use of DWT allows for decomposition of image at different resolutions.
        - Allows for other purposes (such as presentation) in addition to compression.
    - Progressive transmission by pixel and resolution accuracy.
        - Efficient code stream organization
        - Progressive by pixel accuracy (SNR scalability) and image resolution.
        - Quality can be gradually improved by downloading more data bits.
        - Designed with web applications in mind.
    - Choice of lossless or lossy compression in a single compression architecture.
    - Random code-stream access and processing.
        - Access to different regions of interest at varying degrees of granularity.
        - Possible to store different parts of same picture using different quality.
    - Error resilience
        - Robust to bit errors from noisy communication channels.
    - Flexible file format, specially for color-space information and metadata.
    - High dynamic range support
        - Support any bit depth, including 16-bit and 32-bit floating point images.
    - Side channel spatial information for transparency and alpha planes.
- Color components transformation
    - Images are transformed from RGB to another color space to handle the components separately.
    - Two Possible choices.
        1.  Irreversible color transform
            - Uses YCBCR color space.
            - Irreversible because it has to implemented using floating point or fixpoint and causes round-off errors.
        2. Reversible Color Transform
            - Uses a modified YUV color space that does not introduce quantization errors.
            - Fully reversible.
            - Transformation given by
                Forward:
                $Y = \lfloor \frac{R + 2G + B}{4} \rfloor$
                $C_B = B - G$
                $C_R = R - G$

                Reverse:
                $G = Y - \lfloor\frac{C_B + C_R}{4}\rfloor$
                $R = C_R + G$
                $B = C_B + G$
                - Chrominance components can be down-scaled in resolution.
                - Downsampling effectively handled by separating images into scales and dropping the finest wavelet scale.
    - Divides an image into two-dimensional array of samples, known as *components*.
        - As an example, a color image may consist of several components representing base colors red, green, and blue.
- Tiling
    - Image and its components are decomposed into rectangular *tiles*, which form the basic unit of original or reconstructed image.
    - All the components (for example different color components) that form a tile are kept together so that each tile can be independently extracted/decoded/reconstructed.
    - Tiles can be any size, but *all* the tiles in the image are the *same size*.
        - Possible to have different sized tiles on right and bottom border.
        - Decoder needs less memory to decode the image.
        - You can also opt for partial decoding by decoding only a subset of tiles.
    - Quality of the image may decrease due to lower peak SNR.
    - Using many tiles may lead to blocking artifacts.
- Wavelet transform
    - Tiles are analyzed using wavelets to create multiple decomposition levels.
        - Yields a number of coefficients to describe the horizontal and vertical spatial frequency characteristics of the original tiles, within a local area.
        - Different decomposition levels are related by powers of 2.
    - Wavelet transformation to arbitrary depth.
    - Two different wavelet transforms used.
       1. Irreversible: CDF 9/7 wavelet transform
            - CDF - Cohen Daubechies Feauveau
            - Introduces quantization noise that depends on the precision of the decoder.
       2. Reversible: a rounded version of the biorthogonal CDF 5/3 wavelet
            - Uses only integer coefficients; no rounding and hence, no quantization noise.
            - Used in lossless coding
    - Wavelet transform implemented by the *lifting scheme* or convolution.

- Quantization
    - Transformed coefficients are scalar-quantized to reduce the number of bits used in representation
    - Information content of a large number of small-magnitude coefficients reduced by quantization, giving *code-blocks*.
    - Leads to a loss of quality.
    - Code blocks are sets of integers that are encoded bit-by-bit.
    - Greater quantization step leads to greater compression and loss in quality.
    - Quantization step of 1 implies no quantization; used in lossless compression.
- Coding
    - At this point, we have a collection of sub-bands representing several approximation scales.
        - Each sub-band a set of coefficients
        - Real numbers representing aspects of image associated with certain frequency range as well as a spatial area of the image.
    - Precincts
        - Quantized sub-bands split into precincts, regular regions in the wavelet domain.
        - Selected so that coefficients in a precinct across sub-band form approximate spatial block in the reconstructed image.
    - Code blocks
        - Precincts split into code blocks.
        - Code blocks located in a single sub-band
        - All code blocks have the same size, except at the end of the image.
     - Additional compression is achieved by entropy coding of bit-planes of the coefficients in code-blocks to reduce the number of bits required to represent quantized coefficients.

---

<sup>1</sup>From Wikipedia

