## Median Filter in Image Processing:

**What it is:** A non-linear digital filtering technique used to remove noise from images, particularly salt-and-pepper noise (impulse noise).  It works by replacing the center pixel value in a sliding window with the median value of all pixels within that window.

**How it works:**

1. **Sliding Window:** A window (usually square, e.g., 3x3, 5x5) is moved pixel by pixel over the image.
2. **Sorting:** The pixel values within the window are sorted.
3. **Median Replacement:** The center pixel of the window is replaced with the median value from the sorted list.

**Properties:**

* **Effective Noise Reduction:** Excellent at removing impulse noise without significantly blurring edges or other sharp details like linear filters (e.g., averaging filters) might.
* **Edge Preservation:** Preserves sharp edges better than linear filters as it doesn't average pixel values.  The median value is likely to be close to the original value of edge pixels.
* **Non-linear Filter:**  Not based on weighted averaging like linear filters. The output is not a linear combination of the input pixels.
* **Computational Cost:** Can be computationally more expensive than linear filters due to the sorting step, especially with larger window sizes.
* **Window Size Effect:**  Larger window sizes remove more noise but can also blur the image. Smaller window sizes preserve details but may not remove all noise effectively.  Selecting the appropriate window size depends on the level of noise and the desired level of detail preservation.


**Why we use it:**

* **Salt-and-pepper Noise Removal:**  Highly effective at removing this type of noise, which appears as randomly scattered black and white pixels.
* **Edge Preservation:**  Crucial in applications where edge information is important (e.g., medical imaging, object recognition).
* **Robustness:** Less sensitive to outliers (noise) than linear filters. The median value is less affected by extreme values within the window.

