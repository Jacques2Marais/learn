# Chapter 13: Numerical Methods in Python

Welcome to Part 4: Python for Physics Applications! In this part, we'll focus on applying Python and the libraries we've learned to solve problems commonly encountered in physics. This chapter introduces numerical methods in Python, which are essential for solving equations and simulating physical systems when analytical solutions are not feasible or practical.

## Numerical Methods in Python

Numerical methods are algorithms that use numerical approximation to solve mathematical problems. In physics, we often encounter problems that are mathematically complex and cannot be solved analytically (i.e., with pen and paper). Numerical methods provide computational approaches to find approximate solutions. Python, with libraries like NumPy and SciPy, is well-suited for implementing and using numerical methods.

## Solving Differential Equations Numerically

Differential equations describe the relationships between a function and its derivatives. They are fundamental in physics for modeling various phenomena, from motion to heat transfer to quantum mechanics. Numerical methods are often necessary to solve differential equations, especially non-linear or complex ones.

We'll focus on two basic numerical methods for solving ordinary differential equations (ODEs): Euler's method and Runge-Kutta methods.

**1. Euler's Method:**

Euler's method is the simplest first-order numerical method for solving ODEs. It approximates the solution at the next time step based on the current solution and the derivative at the current time.

For a first-order ODE:  `dy/dt = f(t, y)` with initial condition `y(t0) = y0`, Euler's method approximates the solution as:

`y_{i+1} = y_i + h * f(t_i, y_i)`

where:
*   `y_{i+1}` is the approximate solution at time `t_{i+1} = t_i + h`
*   `y_i` is the approximate solution at time `t_i`
*   `h` is the step size (time step)

**Example: Solving dy/dt = -y (exponential decay) using Euler's method**

```python
# Code cell
import numpy as np
import matplotlib.pyplot as plt

def f_euler_example(t, y): # Define the ODE: dy/dt = -y
    return -y

# Parameters
t_start = 0
t_end = 5
h = 0.1 # Step size
t_points = np.arange(t_start, t_end + h, h) # Time points
y_initial = 1.0 # Initial condition

# Initialize array to store solutions
y_euler = np.zeros(len(t_points))
y_euler[0] = y_initial

# Euler's method iteration
for i in range(len(t_points) - 1):
    y_euler[i+1] = y_euler[i] + h * f_euler_example(t_points[i], y_euler[i])

# Analytical solution for comparison: y(t) = exp(-t)
y_analytical = np.exp(-t_points)

# Plotting
plt.figure(figsize=(8, 6))
plt.plot(t_points, y_euler, label='Euler Method Approximation', marker='o', linestyle='--')
plt.plot(t_points, y_analytical, label='Analytical Solution', linestyle='-')
plt.xlabel("Time (t)")
plt.ylabel("y(t)")
plt.title("Euler's Method for dy/dt = -y")
plt.legend()
plt.grid(True)
plt.show()
```

**2. Runge-Kutta Methods (RK4):**

Runge-Kutta methods are a family of higher-order numerical methods for solving ODEs, generally more accurate than Euler's method for the same step size. The 4th-order Runge-Kutta method (RK4) is commonly used and provides a good balance between accuracy and computational cost.

RK4 method involves calculating intermediate slopes (k1, k2, k3, k4) within each step to improve accuracy:

```
k1 = h * f(t_i, y_i)
k2 = h * f(t_i + h/2, y_i + k1/2)
k3 = h * f(t_i + h/2, y_i + k2/2)
k4 = h * f(t_i + h, y_i + k3)

y_{i+1} = y_i + (1/6) * (k1 + 2*k2 + 2*k3 + k4)
```

**Example: Solving dy/dt = -y using RK4 method**

```python
# Code cell
import numpy as np
import matplotlib.pyplot as plt

def f_rk4_example(t, y): # Define the ODE: dy/dt = -y
    return -y

# Parameters (same as Euler example)
t_start = 0
t_end = 5
h = 0.1 # Step size
t_points = np.arange(t_start, t_end + h, h)
y_initial = 1.0

# Initialize array to store solutions
y_rk4 = np.zeros(len(t_points))
y_rk4[0] = y_initial

# Runge-Kutta 4th order method iteration
for i in range(len(t_points) - 1):
    k1 = h * f_rk4_example(t_points[i], y_rk4[i])
    k2 = h * f_rk4_example(t_points[i] + h/2, y_rk4[i] + k1/2)
    k3 = h * f_rk4_example(t_points[i] + h/2, y_rk4[i] + k2/2)
    k4 = h * f_rk4_example(t_points[i] + h, y_rk4[i] + k3)
    y_rk4[i+1] = y_rk4[i] + (1/6) * (k1 + 2*k2 + 2*k3 + k4)

# Analytical solution (same as Euler example)
y_analytical = np.exp(-t_points)

# Plotting
plt.figure(figsize=(8, 6))
plt.plot(t_points, y_rk4, label='Runge-Kutta 4th Order Approximation', marker='o', linestyle='--')
plt.plot(t_points, y_analytical, label='Analytical Solution', linestyle='-')
plt.xlabel("Time (t)")
plt.ylabel("y(t)")
plt.title("Runge-Kutta 4th Order Method for dy/dt = -y")
plt.legend()
plt.grid(True)
plt.show()
```

**SciPy `solve_ivp` for ODE Solving:**

SciPy provides a more robust and efficient function `solve_ivp` (solve initial value problem) in `scipy.integrate` module for solving ODEs. It includes various solvers, including Runge-Kutta methods, with adaptive step size control for better accuracy and efficiency.

**Example: Solving dy/dt = -y using `solve_ivp`**

```python
# Code cell
from scipy.integrate import solve_ivp
import numpy as np
import matplotlib.pyplot as plt

def ode_function(t, y): # Define the ODE: dy/dt = -y (for solve_ivp format)
    return -y

# Time span and initial condition
t_span = (0, 5) # Time interval: [0, 5]
y0 = [1.0] # Initial condition: y(0) = 1.0 (as a list for solve_ivp)

# Solve ODE using solve_ivp (default method is RK45 - adaptive Runge-Kutta)
solution = solve_ivp(ode_function, t_span, y0, dense_output=True, max_step=0.1) # dense_output=True for continuous solution, max_step for max step size

# Get solution points at specified time points
t_points_ivp = np.linspace(t_span[0], t_span[1], 50) # Get 50 points in time span
y_ivp = solution.sol(t_points_ivp).flatten() # Evaluate solution at t_points and flatten to 1D array

# Analytical solution (same as before)
y_analytical = np.exp(-t_points_ivp)

# Plotting
plt.figure(figsize=(8, 6))
plt.plot(t_points_ivp, y_ivp, label='solve_ivp (RK45)', marker='o', linestyle='--')
plt.plot(t_points_ivp, y_analytical, label='Analytical Solution', linestyle='-')
plt.xlabel("Time (t)")
plt.ylabel("y(t)")
plt.title("solve_ivp for dy/dt = -y")
plt.legend()
plt.grid(True)
plt.show()
```

`solve_ivp` is generally recommended for solving ODEs in practice due to its robustness and adaptive step size control.

## Root Finding and Optimization Algorithms

Root finding algorithms are used to find the roots (zeros) of a function, i.e., values of x for which `f(x) = 0`. Optimization algorithms are used to find the minimum or maximum of a function. SciPy `optimize` module provides functions for both root finding and optimization.

**1. Root Finding:**

*   `scipy.optimize.fsolve()`: Solves for roots of a non-linear equation or system of equations.
*   `scipy.optimize.root_scalar()`: Finds roots of a scalar function in one variable, offers various solvers (e.g., bisection, Newton-Raphson, Brent's method).

**Example: Finding root of f(x) = x^2 - 2 (analytically roots are ±√2)**

```python
# Code cell
from scipy.optimize import fsolve, root_scalar
import numpy as np

def f_root_example(x): # Define the function: f(x) = x^2 - 2
    return x**2 - 2

# Using fsolve (for general non-linear equations) - needs initial guess
initial_guess = 1.0
root_fsolve = fsolve(f_root_example, initial_guess)
print("Root found by fsolve:", root_fsolve) # Output: [1.41421356] (approx. √2)

# Using root_scalar (for scalar functions, more options for solvers and bracketing) - needs bracketing interval or initial guess and method
# Bisection method (requires bracketing interval [a, b] where f(a) and f(b) have opposite signs)
result_bisect = root_scalar(f_root_example, method='bisect', bracket=[1, 2]) # Bracket around root √2
print("\nRoot found by root_scalar (bisection):", result_bisect.root) # Output: 1.4142135623730951

# Newton-Raphson method (needs initial guess and derivative if available, faster convergence if conditions met)
result_newton = root_scalar(f_root_example, method='newton', x0=1.0, fprime=lambda x: 2*x) # Provide initial guess and derivative f'(x) = 2x
print("\nRoot found by root_scalar (Newton-Raphson):", result_newton.root) # Output: 1.4142135623730951
```

**2. Optimization (Minimization):**

*   `scipy.optimize.minimize()`: General-purpose function for minimizing scalar functions of one or more variables, supports various optimization algorithms (e.g., BFGS, Nelder-Mead, Powell, CG).

**Example: Minimizing f(x) = x^2 + 2x + 5 (analytically minimum at x = -1)**

```python
# Code cell
from scipy.optimize import minimize
import numpy as np

def f_optimize_example(x): # Define the function to minimize: f(x) = x^2 + 2x + 5
    return x**2 + 2*x + 5

# Initial guess for minimum
initial_guess_opt = 0.0

# Minimize function using minimize (BFGS method by default)
result_minimize = minimize(f_optimize_example, initial_guess_opt, method='BFGS')

print("Optimization result:\n", result_minimize)
print("\nMinimum value found:", result_minimize.fun) # Function value at minimum
print("Optimal x (argmin):", result_minimize.x) # x value that minimizes the function
```

SciPy `optimize` module provides a wide range of optimization algorithms for constrained and unconstrained optimization problems.

## Integration and Differentiation

Numerical integration and differentiation are essential for approximating integrals and derivatives of functions, especially when analytical solutions are not available or when dealing with discrete data.

**1. Numerical Integration (Quadrature):**

*   `scipy.integrate.quad()`: General-purpose function for definite integration of a function of one variable, uses adaptive quadrature methods for accuracy.

**Example: Integrating f(x) = sin(x) from 0 to π (analytically integral is 2)**

```python
# Code cell
from scipy.integrate import quad
import numpy as np

def f_integrate_example(x): # Define the function to integrate: f(x) = sin(x)
    return np.sin(x)

# Perform definite integration using quad
integral_result, error_estimate = quad(f_integrate_example, 0, np.pi) # Integrate from 0 to pi

print("Numerical integral value:", integral_result) # Output: 2.0
print("Error estimate:", error_estimate) # Output: (small error estimate)
```

**2. Numerical Differentiation:**

*   NumPy `np.gradient()`:  Calculates the gradient (numerical derivative) of a function for discrete data points.

**Example: Numerical differentiation of y = x^2**

```python
# Code cell
import numpy as np
import matplotlib.pyplot as plt

x_diff = np.linspace(0, 5, 20) # Discrete x values
y_diff = x_diff**2 # Function values: y = x^2

# Calculate numerical derivative using np.gradient()
dy_dx_numerical = np.gradient(y_diff, x_diff) # np.gradient(y, x) - y values and corresponding x values

# Analytical derivative: dy/dx = 2x
dy_dx_analytical = 2 * x_diff

# Plotting
plt.figure(figsize=(8, 6))
plt.plot(x_diff, dy_dx_numerical, label='Numerical Derivative (np.gradient)', marker='o', linestyle='--')
plt.plot(x_diff, dy_dx_analytical, label='Analytical Derivative (2x)', linestyle='-')
plt.xlabel("x")
plt.ylabel("dy/dx")
plt.title("Numerical Differentiation of y = x^2")
plt.legend()
plt.grid(True)
plt.show()
```

Numerical methods are powerful tools for solving a wide range of problems in physics and data science. SciPy provides efficient and accurate implementations of many numerical algorithms, making Python a valuable platform for scientific computing.

**In this chapter, we've covered:**

*   Introduction to numerical methods and their importance in physics.
*   Numerical methods for solving ordinary differential equations (ODEs): Euler's method, Runge-Kutta 4th order method, and SciPy `solve_ivp`.
*   Root finding algorithms using SciPy `optimize` module: `fsolve`, `root_scalar`.
*   Optimization algorithms using SciPy `optimize` module: `minimize`.
*   Numerical integration using SciPy `integrate` module: `quad`.
*   Numerical differentiation using NumPy `gradient`.

In the next chapter, we'll explore simulation and modeling techniques in Python, building upon these numerical methods.
