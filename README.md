# R&D Assignment – Parametric Curve Parameter Estimation

## 1. Objective

The objective of this assignment is to determine the unknown parameters `θ`, `M`, and `X` of a given parametric curve using the provided `x, y` data points.

The estimated parameters are then verified by reconstructing the curve and comparing the predicted points with the original data.

---

## 2. Problem Statement

The given parametric curve is:

\[
x=t\cos(\theta)-e^{M|t|}\sin(0.3t)\sin(\theta)+X
\]

\[
y=42+t\sin(\theta)+e^{M|t|}\sin(0.3t)\cos(\theta)
\]

The unknown variables are:

- `θ` – angle parameter
- `M` – exponential parameter
- `X` – horizontal shift

The parameter ranges given in the assignment are:

\[
0^\circ < \theta < 50^\circ
\]

\[
-0.05 < M < 0.05
\]

\[
0 < X < 100
\]

The curve parameter satisfies:

\[
6 < t < 60
\]

The provided CSV file contains 1,500 `x, y` points generated from the curve.

The goal is to determine the values of `θ`, `M`, and `X` that make the reconstructed curve match the provided data as closely as possible.

---

## 3. Understanding the Equations

The CSV file provides the `x` and `y` coordinates, but the corresponding value of `t` for each point is not directly provided.

To simplify the equations, the following quantity is defined:

\[
A=e^{M|t|}\sin(0.3t)
\]

The equations can then be written as:

\[
x-X=t\cos(\theta)-A\sin(\theta)
\]

\[
y-42=t\sin(\theta)+A\cos(\theta)
\]

Using projections of these equations:

\[
t=(x-X)\cos(\theta)+(y-42)\sin(\theta)
\]

and

\[
A=-(x-X)\sin(\theta)+(y-42)\cos(\theta)
\]

For the correct values of `θ`, `M`, and `X`, the calculated value of `A` should match:

\[
e^{M|t|}\sin(0.3t)
\]

---

## 4. Methodology

The following steps were followed:

1. Loaded the provided CSV file using Python.
2. Verified that the dataset contains 1,500 points.
3. Visualized the provided `x, y` data as a scatter plot.
4. Transformed the original equations to calculate the hidden parameter `t`.
5. Calculated the oscillating component `A`.
6. Used the relationship

   \[
   A=e^{M|t|}\sin(0.3t)
   \]

   to construct the residual used for optimization.
7. Used `scipy.optimize.least_squares` to estimate `θ`, `M`, and `X`.
8. Applied the parameter bounds specified in the assignment during optimization.
9. Used the estimated parameters to reconstruct the curve.
10. Compared the reconstructed curve with the original CSV data.
11. Calculated the prediction errors and checked the resulting range of `t`.

Python uses radians for trigonometric functions, so the estimated angle was converted between degrees and radians when required.

---

## 5. Parameter Estimation

The numerical optimization produced:

\[
\theta \approx 29.9999729^\circ
\]

\[
M \approx 0.0299999969
\]

\[
X \approx 54.9999821
\]

These values are effectively:

\[
\boxed{\theta=30^\circ}
\]

\[
\boxed{M=0.03}
\]

\[
\boxed{X=55}
\]

Therefore, the final estimated unknown variables are:

| Parameter | Final Value |
|---|---:|
| θ | 30° |
| M | 0.03 |
| X | 55 |

Since Python uses radians:

\[
30^\circ=\frac{\pi}{6}
\]

---

## 6. Final Parametric Curve

Using the estimated parameters, the curve becomes:

\[
x=t\cos\left(\frac{\pi}{6}\right)
-e^{0.03|t|}\sin(0.3t)\sin\left(\frac{\pi}{6}\right)+55
\]

\[
y=42+t\sin\left(\frac{\pi}{6}\right)
+e^{0.03|t|}\sin(0.3t)\cos\left(\frac{\pi}{6}\right)
\]

with:

\[
6<t<60
\]

---

## 7. Verification

The final values

\[
\theta=30^\circ,\quad M=0.03,\quad X=55
\]

were used to reconstruct the curve.

The reconstructed coordinates were compared with the original CSV coordinates.

### Verification Results

| Metric | Result |
|---|---:|
| Maximum X error | ≈ 2.03 × 10⁻⁵ |
| Maximum Y error | ≈ 3.51 × 10⁻⁵ |
| Mean L1 error | ≈ 2.06 × 10⁻⁵ |
| Total L1 error | ≈ 0.03083 |

The calculated range of `t` was:

\[
t_{\min}\approx6.0494
\]

\[
t_{\max}\approx59.9952
\]

Thus, the calculated values satisfy the required condition:

\[
6<t<60
\]

---

## 8. Curve Comparison

The original 1,500 data points were plotted together with the reconstructed curve using:

\[
\theta=30^\circ,\quad M=0.03,\quad X=55
\]

The predicted curve closely overlaps the original data points, showing that the estimated parameters reproduce the given curve with very small error.

The complete Python implementation, outputs, and visualization are included in the accompanying Google Colab notebook.

---

## 9. Conclusion

The unknown parameters of the given parametric curve were estimated using mathematical transformation and bounded numerical optimization.

The final values obtained are:

\[
\boxed{\theta=30^\circ,\quad M=0.03,\quad X=55}
\]

The reconstructed curve closely matches the provided 1,500 data points, with a total L1 error of approximately `0.03083`.

The calculated `t` values also remain within the required range of `6 < t < 60`.

The complete implementation and verification are provided in the accompanying Jupyter/Google Colab notebook.
