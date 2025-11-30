# Damped Adaptive Momentum (DAM)

This repository contains all code and experiments for evaluating the **Damped Adaptive Momentum (DAM)** optimizer across classical optimization benchmarks and neural-network training.
All experiments can be reproduced using the two notebooks provided:

* **`benchmarks.ipynb`** – runs function-optimization benchmarks
* **`mnist.ipynb`** – trains a neural network on MNIST using DAM and baseline optimizers

---

## Installation

```bash
pip install numpy matplotlib scikit-learn
```

If using Jupyter:

```bash
pip install notebook numpy matplotlib scikit-learn
```

---

## File Structure

```bash
.
├── benchmarks.ipynb       # Quadratics, Rosenbrock, Rastrigin, Ackley, Himmelblau
├── mnist.ipynb            # MNIST NN training with DAM
└── README.md
```

---

## Benchmarks Explained

The following benchmarks evaluate convergence, stability, and consistency of optimizers:

### **1. Well-Conditioned Quadratic**

* Function: ( f(x) = \frac{1}{2} x^T Q x )
* Condition number: ( \kappa \le 10 )
* Tests smooth, easy curvature.

### **2. Ill-Conditioned Quadratic**

* Same function, but with ( \kappa \ge 100 )
* Stiff curvature exposes optimizer stability weaknesses.

### **3. Rosenbrock Function**

* Banana-shaped valley
* Tests long narrow valleys and curvature sensitivity.

### **4. Rastrigin Function**

* Highly multimodal (many local minima)
* Tests optimizer robustness to oscillatory landscapes.

### **5. Ackley Function**

* Flat outer region + sharp basin
* Tests ability to escape plateaus.

### **6. Himmelblau Function**

* Multiple basins of attraction
* Tests optimizer basin-selection behavior.

### **7. MNIST Neural Network Training**

* Simple 784–128–10 fully-connected network
* Evaluates optimization performance on a realistic non-convex task.

---

## Running the Benchmarks

Open:

```bash
benchmarks.ipynb
```

The notebook includes:

* Implementations of all benchmark functions
* Gradient functions
* SGD+Momentum, Adam, RMSprop, DAM
* Per-optimizer loss curves
* **5-seed evaluation with mean ± std**

To reproduce all benchmark figures:

1. Run all cells in order.
2. Each section contains:

   * Function definition
   * Optimizer calls
   * Plot of convergence
   * Summary table (mean ± standard deviation)

---

## Running MNIST Experiments

Open:

```bash
mnist.ipynb
```

This file contains:

* MNIST loading
* SimpleNN model (784 → 128 → 10)
* Adam, SGD+Momentum, RMSProp, DAM
* 5-seed evaluation
* Reporting:

  * **Test accuracy (mean ± std)**
  * **Training time per epoch (mean ± std)**
  * **Accuracy curves**
  * **Loss curves**

To reproduce MNIST results:

1. Run all cells in order.
2. The notebook logs:

   * Train/test accuracy each epoch
   * Loss curves
   * Timing per epoch
3. Final results are printed in summary format.

---

## DAM Optimizer (Summary)

DAM extends Adam by introducing a **gradient-flux–based momentum dampening mechanism**:

* Computes gradient at tentative future point
* Compares gradient change ( \Delta = g_{\text{new}} - g_{\text{old}} )
* If the step increases instability, momentum is damped
* Otherwise momentum is preserved

This yields a curvature-sensitive update rule that is both robust and lightweight.

---

## Reproducing Figures

Both notebooks automatically generate:

* **Loss vs. iterations** (for benchmark functions)
* **Accuracy & loss curves** (for MNIST)
* **Mean ± std tables for 5 seeds**
