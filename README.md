# FlamAI R&D / AI Assignment

## Problem Statement

The objective of this assignment is to estimate the unknown parameters of a parametric curve using the provided dataset `xy_data.csv`.

The given parametric equations are:

$$
x = t\cos(\theta) - e^{M|t|}\sin(0.3t)\sin(\theta) + X
$$

$$
y = 42 + t\sin(\theta) + e^{M|t|}\sin(0.3t)\cos(\theta)
$$

The unknown parameters are:

- $\theta$
- $M$
- $X$

## Parameter Constraints

| Parameter | Range |
|---|---|
| $\theta$ | $0^\circ < \theta < 50^\circ$ |
| $M$ | $-0.05 < M < 0.05$ |
| $X$ | $0 < X < 100$ |
| $t$ | $6 < t < 60$ |

---

# Approach

The problem was treated as a bounded nonlinear parameter estimation problem.

The following steps were performed:

1. Loaded the provided `xy_data.csv` dataset.
2. Extracted the observed $x$ and $y$ coordinates.
3. Implemented the given parametric curve.
4. Uniformly sampled the parameter $t$ between 6 and 60.
5. Used the Manhattan ($L_1$) distance to measure the difference between the observed and predicted curves.
6. Used Differential Evolution for global optimization.
7. Applied Nelder-Mead optimization for local refinement.
8. Generated the final curve using the estimated parameters.
9. Calculated the final curve-matching loss.

---

# Optimization Method

## Global Optimization

Differential Evolution was used to search for the optimal values of $\theta$, $M$, and $X$ within the specified parameter bounds.

## Local Refinement

The solution obtained from the global optimization stage was further refined using the Nelder-Mead optimization algorithm.

---

# Distance Metric

The assignment evaluates the similarity between the expected and predicted curves using the $L_1$ distance.

The Manhattan distance between two points is:

$$
d_{L_1} = |x_1 - x_2| + |y_1 - y_2|
$$

A symmetric nearest-neighbour approach was used to calculate the distance between the observed and predicted curves.

The final loss was calculated as:

$$
L =
\frac{1}{2}
\left(
\text{Mean Distance from Observed to Predicted}
+
\text{Mean Distance from Predicted to Observed}
\right)
$$

---

# Final Estimated Parameters

The optimization produced the following results:

| Parameter | Estimated Value |
|---|---:|
| Theta (degrees) | **30.0003203°** |
| Theta (radians) | **0.523604366** |
| M | **0.02999924** |
| X | **55.0042683** |
| Final L1 Loss | **0.022590848** |

The estimated parameters are very close to the following values:

$$
\boxed{\theta = 30^\circ}
$$

$$
\boxed{M = 0.03}
$$

$$
\boxed{X = 55}
$$

---

# Final Parametric Equation

Using the estimated parameters, the fitted curve is:

$$
x =
t\cos(0.523604366)
-
e^{0.02999924|t|}
\sin(0.3t)
\sin(0.523604366)
+
55.0042683
$$

$$
y =
42
+
t\sin(0.523604366)
+
e^{0.02999924|t|}
\sin(0.3t)
\cos(0.523604366)
$$

where:

$$
6 < t < 60
$$

---

# Result Visualization

The graph below compares the observed points from the dataset with the predicted curve generated using the estimated parameters.

![Curve Fitting Result](results.png)

---

# Project Structure

```text
flamai-ai-assignment/
│
├── FlamAI.ipynb
├── README.md
├── estimated_parameters.csv
├── requirement.txt
├── results.png
└── xy_data.csv
