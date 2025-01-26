
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


$g(αx₁ + βx₂) = αg₁(x) + βg₂(y)$


Where:

*   **g()**: The filter function.
*   **α, β**: Scalar constants (scaling factors).
*   **x₁, x₂**: Input signals (e.g., pixel intensities or image patches).
*   **x, y**: Input signals (e.g., pixel intensities or image patches). Possibly a typo in the original notes, and it should be x<sub>1</sub> and x<sub>2</sub>
*   **g₁(), g₂()**:  Represent the filter function applied to individual inputs. Possibly a typo and might indicate different functions or instances of 'g'.

**Interpretation:** The filter's response to a linear combination of inputs is the same as the linear combination of the filter's responses to each input individually.

**Note:** in the original image, below this equation, it was written that this is the definition of a `linear function (convolution)`.

## Time and Space Invariance

*   **Time-Invariant (Shift-Invariant):** A filter is time-invariant (or shift-invariant) if its response does not change when the input is shifted in time (or space, in the case of images). Shifting the input image results in the same output, but shifted spatially.
*   **Space Invariant:** This is another term for shift-invariance. It emphasizes that the filter's behavior is consistent across all spatial locations in the image.

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