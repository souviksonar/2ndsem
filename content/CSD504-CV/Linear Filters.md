
# Image Filtering: Linear Filters

## Convolution

The fundamental operation in image filtering is **convolution**. It's represented as:

```
f' = g * f
```

Where:

*   **f'**: The output (filtered) image.
*   **g**: The filter (also known as the filter kernel).
*   **f**: The input image.
*   **\***: The convolution operator.

## Linearity

A crucial property of many filters is **linearity**. A linear filter satisfies the following condition:


$g(αx + βx) = αg(x) + βg(y)$


Where:

*   **g()**: The filter function.
*   **α, β**: Scalar constants (scaling factors).
*   **x, y**: Input signals (e.g., pixel intensities or image patches).

**Interpretation:** The filter's response to a linear combination of inputs is the same as the linear combination of the filter's responses to each input individually.

## Time and Space Invariance

### **Space Invariance (or Translational Invariance):**

> An operation or system is **space-invariant** if its response is the same regardless of the object's location in the image.  If you shift the input image, the output is simply shifted by the same amount.

**Example:**  A **convolutional filter** for edge detection is space-invariant.  It will detect an edge pattern whether it's in the top-left or bottom-right of the image.

### **Time Invariance (or Temporal Invariance):**

> In video processing, a system is **time-invariant** if a time delay in the input sequence results in only a corresponding time delay in the output, with no other changes in the output.  The system's behavior doesn't change over time itself.

**Example:**  A **frame differencing** algorithm for motion detection is time-invariant. If you apply it to a video starting at time T=0, it detects motion. If you start the *same* video at T=5, it will still detect the *same* motion events, just 5 time units later.

## Types of Linear Filters

Based on these properties, we can define:

*   **Linear Function Filter:** A filter that satisfies the linearity property.
*   **Linear Time-Invariant (LTI) Filter:** A filter that is both linear and time-invariant (shift-invariant).
*   **Linear Space Invariant (LSI) Filter:**  Equivalent to an LTI filter, emphasizing spatial invariance.

## Summary

Linear, shift-invariant (LSI or LTI) filters are fundamental in image processing. Their properties allow for efficient implementation and analysis. They are widely used for various tasks, including:

*   **Smoothing/Blurring:** Reducing noise and fine details.
*   **Sharpening:** Enhancing edges and details.
*   **Edge Detection:** Identifying boundaries between regions.
*   **Feature Extraction:**  Extracting meaningful information from images.
---

# Linear Transformation for Pixel Values

This derivation explains a common linear transformation used to map pixel intensity values from an input range to a desired output range.

**Formula:**

$$
\frac{{f' - f_{\text{min}}}}{{f_{\text{max}} - f_{\text{min}}}} = \frac{{g - g_{\text{min}}}}{{g_{\text{max}} - g_{\text{min}}}}
$$

Where:

*   **f'**: The output pixel value after transformation.
*   **f**: The input pixel value.
*   **f<sub>min</sub>**: The minimum input pixel value.
*   **f<sub>max</sub>**: The maximum input pixel value.
*   **g<sub>min</sub>**: The desired minimum output pixel value.
*   **g<sub>max</sub>**: The desired maximum output pixel value.
*   **g**: The input pixel value after applying the filter function.

**Derivation:**

The formula is derived from the general equation of a straight line:

$$
f' = m \cdot g + c
$$

By substituting the known input and output range boundaries (`f`<sub>min</sub>, `f`<sub>max</sub>, `g`<sub>min</sub>, `g`<sub>max</sub>) and solving for the slope (`m`) and y-intercept (`c`), we arrive at the given formula.

**1. Finding 'm' and 'c':**

We have two known points:

*   When `g = g`<sub>min</sub>, we want `f' = f`<sub>min</sub>
*   When `g = g`<sub>max</sub>, we want `f' = f`<sub>max</sub>

Substituting these into the linear equation, we get two equations:
$$
f_{\text{min}} = m \cdot g_{\text{min}} + c \quad (\text{Equation 1})
$$

$$
f_{\text{max}} = m \cdot g_{\text{max}} + c \quad (\text{Equation 2})
$$

**2. Solving for 'm' (Slope):**

Subtract Equation 1 from Equation 2:

$$
f_{\text{max}} - f_{\text{min}} = m \cdot (g_{\text{max}} - g_{\text{min}})
$$

Solve for `m`:

$$
m = \frac{{f_{\text{max}} - f_{\text{min}}}}{{g_{\text{max}} - g_{\text{min}}}}
$$

**3. Solving for 'c' (Y-intercept):**

Substitute the value of `m` back into Equation 1:

$$
f_{\text{min}} = \left[\frac{{f_{\text{max}} - f_{\text{min}}}}{{g_{\text{max}} - g_{\text{min}}}}\right] \cdot g_{\text{min}} + c
$$

Solve for `c`:

$$
c = f_{\text{min}} - \left[\frac{{f_{\text{max}} - f_{\text{min}}}}{{g_{\text{max}} - g_{\text{min}}}}\right] \cdot g_{\text{min}}
$$

**4. Substituting 'm' and 'c' back into the linear equation:**

$$
f' = \left[\frac{{f_{\text{max}} - f_{\text{min}}}}{{g_{\text{max}} - g_{\text{min}}}}\right] \cdot g + f_{\text{min}} - \left[\frac{{f_{\text{max}} - f_{\text{min}}}}{{g_{\text{max}} - g_{\text{min}}}}\right] \cdot g_{\text{min}}
$$

**5. Rearranging to get the equation in the notes:**

Subtract `f`<sub>min</sub> from both sides:

$$
f' - f_{\text{min}} = \left[\frac{{f_{\text{max}} - f_{\text{min}}}}{{g_{\text{max}} - g_{\text{min}}}}\right] \cdot (g - g_{\text{min}})
$$

Finally, divide both sides by (`f`<sub>max</sub> - `f`<sub>min</sub>):

$$
\frac{{f' - f_{\text{min}}}}{{f_{\text{max}} - f_{\text{min}}}} = \frac{{g - g_{\text{min}}}}{{g_{\text{max}} - g_{\text{min}}}}
$$

**Purpose:**

This linear transformation is often used for:

*   **Contrast Stretching:** Expanding the range of pixel values to improve the contrast of an image. For instance, mapping the input range \[50, 150] to the output range \[0, 255].
*   **Normalization:** Scaling pixel values to a standard range (e.g., \[0, 1]).
*   **Intensity Adjustment:** Shifting the brightness of an image.

---