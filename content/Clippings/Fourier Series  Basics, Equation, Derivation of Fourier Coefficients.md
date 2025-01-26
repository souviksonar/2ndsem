---
title: "Fourier Series | Basics, Equation, Derivation of Fourier Coefficients"
source: "https://www.electronicshub.org/fourier-series/"
author:
  - "[[Leela Prasad]]"
published: 2024-05-05
created: 2025-01-15
description: "Learn about Fourier Series. Using Fourier Series, we can represent any periodic waveform as infinite sum of sine and cosine functions."
tags:
  - "clippings"
---
When Joseph Fourier introduced his mathematical model on conduction of heat to the Academy of Sciences in Paris in 1807, they criticized and rejected his work. But later, when he published this work in his ‘Théorie analytique de la Chaleur’ (or The Analytical Theory of Heat) in 1822, it became an integral part of engineering.

Even though the original mathematical analysis was a study of conduction of heat in metals, engineers found that they could apply the same technique for other mathematical, engineering and physics problems.

Today, you can see Fourier Series is very important in the fields of Communication (RADAR, Satellite, Wireless in general), Acoustics, Image Processing (Signal Processing in general), Electrical, Optics and many more.

- [What is the Fourier Series?](https://www.electronicshub.org/fourier-series/#What_is_the_Fourier_Series "What is the Fourier Series?")
- [Derivation of Fourier Coefficients](https://www.electronicshub.org/fourier-series/#Derivation_of_Fourier_Coefficients "Derivation of Fourier Coefficients")
- [Expression for a0](https://www.electronicshub.org/fourier-series/#Expression_for_a0 "Expression for a0")
- [Expression for an](https://www.electronicshub.org/fourier-series/#Expression_for_an "Expression for an")
- [Expression for bn](https://www.electronicshub.org/fourier-series/#Expression_for_bn "Expression for bn")
- [How to Obtain Fourier Series of a Function f(x)?](https://www.electronicshub.org/fourier-series/#How_to_Obtain_Fourier_Series_of_a_Function_fx "How to Obtain Fourier Series of a Function f(x)?")
- [Fourier Series Applications](https://www.electronicshub.org/fourier-series/#Fourier_Series_Applications "Fourier Series Applications")
- [Conclusion](https://www.electronicshub.org/fourier-series/#Conclusion "Conclusion")

## What is the Fourier Series?

Okay. Enough introduction. Let us now focus on the main question: What is the Fourier Series? Fourier Series is an Infinite Series of a periodic function in terms of Sine and Cosine functions.

Fourier Series of a periodic waveform is an infinite sum sine and cosine waveforms, where the frequency of each wave (sine and cosine) is an integral multiple of the periodic waveform’s fundamental frequency.

Without any mathematical analysis, these statements might sound ridiculous: why are we turning a simple waveform into a complex combination of trigonometric functions?

Actually, the resulting Fourier Series simplifies the process of signal analysis of the main function (or waveform) at different frequencies. We can derive Fourier Series for any periodic or continuous functions or functions with discontinuous values and its derivatives.

Before proceeding further, we need to understand the basic terminology we mentioned earlier: the Periodic Function. A function f(x) is periodic if for a constant T>0, f(x + T) = f(x). Here, T is known as the Period of the function.

***Periodic Function: f(x + T) = f(x), T>0***

f(x) = f(x +2T) = f(x + 3T) = … T is the period of the function f(x). The function f(x) repeats itself after equal intervals. Trigonometric functions such as sin(x), cos(x), tan(x) etc. are some simple examples of periodic functions.

Now, coming back to the Fourier Series, if f(x) is a periodic function, then we can express it as an infinite sum of sine and cosine functions as follows:

![Fourier-Series-Image-1](https://www.electronicshub.org/wp-content/smush-webp/2022/05/Fourier-Series-Image-1-1024x229.png.webp)

![zxcc](https://www.electronicshub.org/wp-content/smush-webp/2022/05/Fourier-Series-Image-1.png.webp)

Here, a<sub>0</sub>, a<sub>n</sub> and b<sub>n</sub> are known as Fourier Coefficients. The values of these coefficients are what define the Fourier Series of a function. Constant a<sub>0</sub> is the average value of the periodic function while a<sub>n</sub> and b<sub>n</sub> are the amplitudes of various sinusoidal functions.

We can calculate a<sub>0</sub>, a<sub>n</sub> and b<sub>n</sub> using the following expressions. For example, if f(x) is a periodic function, then Fourier Coefficients of its Fourier Series in the interval T ≤ x ≤ T+2π are as follows:

[![Fourier-Series-Image-2](https://www.electronicshub.org/wp-content/smush-webp/2022/05/Fourier-Series-Image-2-300x292.png.webp)](https://www.electronicshub.org/wp-content/smush-webp/2022/05/Fourier-Series-Image-2.png.webp)

The equations of a<sub>0</sub>, a<sub>n</sub> and b<sub>n</sub> are known as Euler’s Formulae.

In the previous Fourier Series equation, we used both sine and cosine functions. But we can further modify the equation to give an equation only in terms of sinusoids.

We have the term a<sub>n</sub>cos(nx) + b<sub>n</sub>sin(nx) in the equation. We can re-write this as follows:

[![Fourier-Series-Image-3](https://www.electronicshub.org/wp-content/smush-webp/2022/05/Fourier-Series-Image-3-1024x401.png.webp)](https://www.electronicshub.org/wp-content/smush-webp/2022/05/Fourier-Series-Image-3.png.webp)

Using these terms, we can derive the sinusoid only Fourier Series Expression of a function as:

[![Fourier-Series-Image-4](https://www.electronicshub.org/wp-content/smush-webp/2022/05/Fourier-Series-Image-4-1024x223.png.webp)](https://www.electronicshub.org/wp-content/smush-webp/2022/05/Fourier-Series-Image-4.png.webp)

In the above equation, notice that for n = 1, the sinusoidal quantity has the same frequency as the main function (which is ‘x’ in this case) and it is the Fundamental Frequency of the main waveform. All the subsequent frequencies (for n = 2, n = 3 and so on) are integral multiples of this fundamental frequency which we call as Harmonic Frequencies.

So, for n = 2, the frequency of the corresponding sinusoid is known as Second Harmonic. Similarly, for n = 3, it is Third Harmonic etc.

## Derivation of Fourier Coefficients

From the above discussion, it is clear that the Fourier Coefficients a<sub>0</sub>, a<sub>n</sub> and b<sub>n</sub> are the critical values that we need to calculate for any Fourier Series. We have already seen the expressions for these constants but let us try to derive them.

For this, let us assume that f(x) is a periodic function and its Fourier Series for the interval \[T, T+2π\] i.e., T ≤ x ≤ T+2π is given by:

[![Fourier-Series-Image-5](https://www.electronicshub.org/wp-content/smush-webp/2022/05/Fourier-Series-Image-5.png.webp)](https://www.electronicshub.org/wp-content/smush-webp/2022/05/Fourier-Series-Image-5.png.webp)

### Expression for a<sub>0</sub>

In the above equation, let us integrate both sides from x=T to x=T+2π. We get:

[![Fourier-Series-Image-6](https://www.electronicshub.org/wp-content/smush-webp/2022/05/Fourier-Series-Image-6.png.webp)](https://www.electronicshub.org/wp-content/smush-webp/2022/05/Fourier-Series-Image-6.png.webp)

From the above equation, we can get the expression for a<sub>0</sub> as:

[![Fourier-Series-Image-7](https://www.electronicshub.org/wp-content/smush-webp/2022/05/Fourier-Series-Image-7-300x126.png.webp)](https://www.electronicshub.org/wp-content/smush-webp/2022/05/Fourier-Series-Image-7.png.webp)

### Expression for a<sub>n</sub>

Now, consider the original Fourier Series expression once again. Multiply both sides by ‘cos(mx)’ and integrate the resulting equation from x=T to x=T+2π.

[![Fourier-Series-Image-8](https://www.electronicshub.org/wp-content/smush-webp/2022/05/Fourier-Series-Image-8.png.webp)](https://www.electronicshub.org/wp-content/smush-webp/2022/05/Fourier-Series-Image-8.png.webp)

In the above expression, if you observe closely, the integrals corresponding to a<sub>0</sub> and b<sub>n­</sub> (first and third) are always zero. Coming to the second integral corresponding to a<sub>n</sub>, for all m ≠ n cases, it becomes zero and the only possible outcome is for value m = n. Therefore,

[![Fourier-Series-Image-9](https://www.electronicshub.org/wp-content/smush-webp/2022/05/Fourier-Series-Image-9.png.webp)](https://www.electronicshub.org/wp-content/smush-webp/2022/05/Fourier-Series-Image-9.png.webp)

From the above equation, we can get the expression for a<sub>n</sub> as:

[![Fourier-Series-Image-10](https://www.electronicshub.org/wp-content/smush-webp/2022/05/Fourier-Series-Image-10-300x108.png.webp)](https://www.electronicshub.org/wp-content/smush-webp/2022/05/Fourier-Series-Image-10.png.webp)

### Expression for b<sub>n</sub>

Now, consider the original Series expression once again. Multiply both sides by ‘sin(mx)’ and integrate the resulting equation from x=T to x=T+2π.

[![Fourier-Series-Image-11](https://www.electronicshub.org/wp-content/smush-webp/2022/05/Fourier-Series-Image-11.png.webp)](https://www.electronicshub.org/wp-content/smush-webp/2022/05/Fourier-Series-Image-11.png.webp)

In the above expression, the integrals corresponding to a<sub>0</sub> and a<sub>n­</sub> (first and second) are always zero. Coming to the third integral corresponding to b<sub>n</sub>, for all m ≠ n cases, it becomes zero and the only possible outcome is for value m = n. Therefore,

[![Fourier-Series-Image-12](https://www.electronicshub.org/wp-content/smush-webp/2022/05/Fourier-Series-Image-12.png.webp)](https://www.electronicshub.org/wp-content/smush-webp/2022/05/Fourier-Series-Image-12.png.webp)

From the above equation, we can get the expression for b<sub>n</sub> as:

[![Fourier-Series-Image-13](https://www.electronicshub.org/wp-content/smush-webp/2022/05/Fourier-Series-Image-13-300x110.png.webp)](https://www.electronicshub.org/wp-content/smush-webp/2022/05/Fourier-Series-Image-13.png.webp)

## How to Obtain Fourier Series of a Function f(x)?

Peter Gustav Lejeune Dirichlet formulated sufficient conditions that a periodic function must satisfy in order to derive Fourier Series. These are popularly known as ‘Dirichlet’s Conditions’.

We can express any function f(x) in its Fourier Series form as:

[![Fourier-Series-Image-5](https://www.electronicshub.org/wp-content/smush-webp/2022/05/Fourier-Series-Image-5.png.webp)](https://www.electronicshub.org/wp-content/smush-webp/2022/05/Fourier-Series-Image-5.png.webp)

Where a<sub>0</sub>, a<sub>n</sub> and b<sub>n</sub> are constants if the following “sufficient conditions” are satisfied.

- The function f(x) is a periodic, single-valued, well-defined and finite function.
- It has a finite number of discontinuities in any period.
- f(x) has finite number of maxima and minima in a bounded interval.

If these conditions are met, then we can obtain the Fourier Series of any function using the following steps:

Assume the generic form of Series with respect to the function as follows:

[![Fourier-Series-Image-5](https://www.electronicshub.org/wp-content/smush-webp/2022/05/Fourier-Series-Image-5.png.webp)](https://www.electronicshub.org/wp-content/smush-webp/2022/05/Fourier-Series-Image-5.png.webp)

Calculate the value of a<sub>0</sub> using the following formula:

[![Fourier-Series-Image-7](https://www.electronicshub.org/wp-content/smush-webp/2022/05/Fourier-Series-Image-7-300x126.png.webp)](https://www.electronicshub.org/wp-content/smush-webp/2022/05/Fourier-Series-Image-7.png.webp)

Compute the value of a<sub>n</sub> using the following expression:

[![Fourier-Series-Image-10](https://www.electronicshub.org/wp-content/smush-webp/2022/05/Fourier-Series-Image-10-300x108.png.webp)](https://www.electronicshub.org/wp-content/smush-webp/2022/05/Fourier-Series-Image-10.png.webp)

Calculate the value of b<sub>n</sub> using the following formula:

[![Fourier-Series-Image-13](https://www.electronicshub.org/wp-content/smush-webp/2022/05/Fourier-Series-Image-13-300x110.png.webp)](https://www.electronicshub.org/wp-content/smush-webp/2022/05/Fourier-Series-Image-13.png.webp)

Now, substitute the values of a<sub>0</sub>, a<sub>n</sub> and b<sub>n­</sub> in the original expression (from Step 1) and you have the final Fourier Series of the function f(x).

## Fourier Series Applications

The concept of representing any waveform (or function) purely in terms of sinusoids is a powerful tool in mathematics, engineering (electronics, communication, mechanical, etc.), acoustics, image and video processing.

Fourier Series and Fourier Transforms, which together form a new set of mathematical modelling known as Fourier Analysis, are very important in several scientific applications to solve ordinary and partial differential equations, signal processing, statistics, seismography, oceanography, sonar, cryptography etc.

## Conclusion

This was an introductory guide on Fourier Series. Joseph Fourier developed a mathematical model of conduction of heat in metals, which later became the Fourier Series. In this, we can represent any continuous, periodic function (waveform) purely in the form of sinusoids. We have seen the basic Fourier Series expression, Fourier Coefficients, Dirichlet’s Conditions and many more.

### Related Posts:

- [What is Circuit Simulation? Its Advantages and Types](https://www.electronicshub.org/circuit-simulation/)
- [RMS Voltage of AC Waveform](https://www.electronicshub.org/rms-voltage-of-ac-waveform/)
- [Thermal Paste Vs Thermal Pad | Which is Better?](https://www.electronicshub.org/thermal-paste-vs-thermal-pad/)
- [Series Circuit | Basics, Characteristics,…](https://www.electronicshub.org/series-circuit/)
- [What Is Kirchhoff's Law | KCL & KVL Guide](https://www.electronicshub.org/kirchhoffs-laws/)
- [What is a Heat Sink? Types of Heat Sinks](https://www.electronicshub.org/heat-sink/)