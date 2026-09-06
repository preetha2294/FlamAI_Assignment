# FlamAI R&D / AI Assignment

## Final Answer

### Estimated Unknown Parameters

| Parameter | Estimated Value |
|---|---:|
| Theta (θ) | **30.0003203°** |
| Theta (radians) | **0.523604366** |
| M | **0.02999924** |
| X | **55.0042683** |
| Final L1 Loss | **0.022590848** |

The estimated parameters are approximately:

- **θ = 30°**
- **M = 0.03**
- **X = 55**

---

## Final Parametric Equation

Using the estimated parameters:

```text
x = t*cos(0.523604366) - e^(0.02999924*|t|)*sin(0.3*t)*sin(0.523604366) + 55.0042683

y = 42 + t*sin(0.523604366) + e^(0.02999924*|t|)*sin(0.3*t)*cos(0.523604366)
```

For:

```text
6 < t < 60
```

### Desmos-Compatible Equation

Copy and paste the following into a single expression in Desmos:

```text
(t*cos(0.523604366)-e^(0.02999924*abs(t))*sin(0.3*t)*sin(0.523604366)+55.0042683,42+t*sin(0.523604366)+e^(0.02999924*abs(t))*sin(0.3*t)*cos(0.523604366)){6<t<60}
```

---

# Problem Statement

The objective of this assignment is to estimate the unknown parameters of a parametric curve using the provided dataset `xy_data.csv`.

The given parametric equations are:

```text
x = t*cos(θ) - e^(M*|t|)*sin(0.3*t)*sin(θ) + X
```

```text
y = 42 + t*sin(θ) + e^(M*|t|)*sin(0.3*t)*cos(θ)
```

The unknown parameters are:

- θ
- M
- X

---

# Parameter Constraints

| Parameter | Range |
|---|---|
| θ | 0° < θ < 50° |
| M | -0.05 < M < 0.05 |
| X | 0 < X < 100 |
| t | 6 < t < 60 |

---

# Approach

The problem was treated as a bounded nonlinear parameter estimation problem.

The following steps were performed:

1. Loaded the provided `xy_data.csv` dataset.
2. Extracted the observed x and y coordinates.
3. Implemented the given parametric curve.
4. Uniformly sampled the parameter `t` between 6 and 60.
5. Generated predicted points using the candidate parameter values.
6. Used Manhattan (L1) distance to measure the difference between the observed and predicted curves.
7. Used Differential Evolution for global optimization.
8. Applied Nelder-Mead optimization for local refinement.
9. Generated the final fitted curve.
10. Calculated the final L1 curve-matching loss.

---

# Optimization Method

## Global Optimization

Differential Evolution was used to search for the optimal values of θ, M, and X within the specified parameter bounds.

This method provides global exploration of the search space and helps avoid poor local solutions.

## Local Refinement

The solution obtained from Differential Evolution was further refined using the Nelder-Mead optimization algorithm.

This two-stage optimization approach combines global search with local refinement.

---

# Distance Metric

The similarity between the observed and predicted curves was evaluated using the Manhattan (L1) distance.

The L1 distance between two points is:

```text
d = |x1 - x2| + |y1 - y2|
```

A symmetric nearest-neighbour approach was used to compare the two curves:

1. Calculate the mean L1 distance from observed points to the predicted curve.
2. Calculate the mean L1 distance from predicted points to the observed curve.
3. Average both values to obtain the final loss.

The final loss is:

```text
L = 0.5 * (Mean observed-to-predicted distance
         + Mean predicted-to-observed distance)
```

---

# Final Results

The optimization produced:

| Parameter | Value |
|---|---:|
| Theta (degrees) | 30.0003203 |
| Theta (radians) | 0.523604366 |
| M | 0.02999924 |
| X | 55.0042683 |
| Final L1 Loss | 0.022590848 |

The estimated values are extremely close to:

```text
θ = 30°
M = 0.03
X = 55
```

---

# Result Visualization

The visualization below compares the observed points from the provided dataset with the fitted parametric curve.

![Curve Fitting Result](results.png)

---

# Project Structure

```text
FlamAI_Assignment/
│
├── FlamAI.ipynb
├── README.md
├── estimated_parameters.csv
├── requirements.txt
├── results.png
└── xy_data.csv
```

---

# Requirements

The project uses:

- NumPy
- Pandas
- SciPy
- Matplotlib

Install the dependencies using:

```bash
pip install -r requirements.txt
```

---

# How to Run

1. Clone or download the repository.

2. Install the required libraries:

```bash
pip install -r requirements.txt
```

3. Open the notebook:

```text
FlamAI.ipynb
```

4. Run all cells.

The notebook will:

- Load the dataset.
- Generate candidate parametric curves.
- Optimize θ, M, and X.
- Calculate the L1 loss.
- Generate the result visualization.
- Save the estimated parameters.

---

# Output Files

The project produces:

- `estimated_parameters.csv` — Estimated parameter values and final loss.
- `results.png` — Visualization of observed points and the fitted curve.

---

## Conclusion

The unknown parameters of the parametric curve were estimated through bounded nonlinear optimization using Differential Evolution followed by Nelder-Mead refinement.

The final estimated values are approximately:

```text
θ = 30°
M = 0.03
X = 55
```

The resulting curve achieved a final L1 loss of approximately **0.02259**.
