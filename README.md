# FlamAI R&D / AI Assignment

## Final Submission

### Estimated Unknown Parameters

| Parameter | Estimated Value |
|---|---:|
| **Theta (θ)** | **30.0003203°** |
| **Theta (radians)** | **0.523604366** |
| **M** | **0.02999924** |
| **X** | **55.0042683** |
| **Final L1 Loss** | **0.022590848** |

The estimated parameters are approximately:

- **θ = 30°**
- **M = 0.03**
- **X = 55**

### Final Parametric Equation

Using the estimated values:

$$
x =
t \cdot \cos(0.523604366)
-
e^{0.02999924|t|}
\cdot
\sin(0.3t)
\cdot
\sin(0.523604366)
+
55.0042683
$$

$$
y =
42
+
t \cdot \sin(0.523604366)
+
e^{0.02999924|t|}
\cdot
\sin(0.3t)
\cdot
\cos(0.523604366)
$$

where:

$$
6 < t < 60
$$

### Desmos-Compatible Submission

```text
(t*cos(0.523604366)-e^(0.02999924*|t|)*sin(0.3*t)*sin(0.523604366)+55.0042683,42+t*sin(0.523604366)+e^(0.02999924*|t|)*sin(0.3*t)*cos(0.523604366))
```

---

# Problem Statement

The objective of this assignment is to estimate the unknown parameters of a parametric curve using the provided dataset `xy_data.csv`.

The given parametric equations are:

$$
x =
t\cos(\theta)
-
e^{M|t|}
\sin(0.3t)
\sin(\theta)
+
X
$$

$$
y =
42
+
t\sin(\theta)
+
e^{M|t|}
\sin(0.3t)
\cos(\theta)
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

The problem was formulated as a bounded nonlinear parameter estimation problem.

The following process was used:

1. Loaded the provided `xy_data.csv` dataset.
2. Extracted the observed $x$ and $y$ coordinates.
3. Implemented the given parametric curve.
4. Uniformly sampled the parameter $t$ over the range from 6 to 60.
5. Generated predicted points from the parametric equation.
6. Used Manhattan ($L_1$) distance to measure the difference between the observed and predicted curves.
7. Used Differential Evolution for global optimization.
8. Applied Nelder-Mead optimization for local refinement.
9. Generated the final curve using the estimated parameters.
10. Calculated the final curve-matching loss.

---

# Optimization Method

## Global Optimization

Differential Evolution was used to search for the optimal values of $\theta$, $M$, and $X$ within the specified parameter bounds.

This method helps explore the complete search space and reduces the risk of converging to a poor local solution.

## Local Refinement

The solution obtained from the global optimization stage was further refined using the Nelder-Mead optimization algorithm.

This two-stage approach combines global exploration with local refinement.

---

# Distance Metric

The similarity between the observed and predicted curves was evaluated using the $L_1$ distance.

The Manhattan distance between two points is:

$$
d_{L_1}
=
|x_1-x_2|
+
|y_1-y_2|
$$

A symmetric nearest-neighbour approach was used to measure the distance between the observed and predicted curves.

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

# Result Visualization

The graph below compares the observed points from the dataset with the predicted parametric curve generated using the estimated parameters.

![Curve Fitting Result](results.png)

---

# Project Structure

```text
flamai-ai-assignment/
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

The project uses the following Python libraries:

```text
numpy
pandas
matplotlib
scipy
```

Install the required dependencies using:

```bash
pip install -r requirements.txt
```

---

# How to Run

### 1. Clone the repository

```bash
git clone <repository-url>
```

### 2. Navigate to the project directory

```bash
cd flamai-ai-assignment
```

### 3. Install the required dependencies

```bash
pip install -r requirements.txt
```

### 4. Open the notebook

Open and run:

```text
FlamAI.ipynb
```

The notebook will:

- Load the provided dataset.
- Generate the parametric curve.
- Optimize the unknown parameters.
- Calculate the final $L_1$ loss.
- Visualize the observed and predicted curves.
- Save the estimated parameters.

---

# Output Files

The project generates the following outputs:

- `results.png` — Visualization comparing the observed points and predicted curve.
- `estimated_parameters.csv` — Final estimated parameter values and L1 loss.

---

# Tools and Libraries

- Python
- NumPy
- Pandas
- SciPy
- Matplotlib
- Google Colab
