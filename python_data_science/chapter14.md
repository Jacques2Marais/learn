# Chapter 14: Simulation and Modeling with Python

In this chapter, we'll explore how to use Python for simulation and modeling of physical systems. Simulation and modeling are essential tools in physics for understanding complex phenomena, testing theories, and making predictions. We'll cover building simulations of physical systems, Monte Carlo methods, and agent-based modeling techniques using Python.

## Building Simulations of Physical Systems

Simulations involve creating computational models of physical systems and running them to observe their behavior over time or under different conditions. Python, with libraries like NumPy, SciPy, and specialized simulation packages, is well-suited for building various types of simulations.

**Example: Simple Harmonic Motion Simulation**

Let's simulate a simple harmonic oscillator, a fundamental system in physics, using numerical methods to solve its equation of motion.

The equation of motion for a simple harmonic oscillator is:

`m * d^2x/dt^2 = -k * x`

where:
*   `m` is mass
*   `k` is spring constant
*   `x` is displacement from equilibrium

We can rewrite this second-order ODE as a system of two first-order ODEs:

`dv/dt = - (k/m) * x`
`dx/dt = v`

where `v = dx/dt` is velocity.

We can use SciPy's `solve_ivp` to solve this system numerically.

```python
# Code cell
import numpy as np
import matplotlib.pyplot as plt
from scipy.integrate import solve_ivp

def harmonic_oscillator_ode(t, state, k_over_m): # ODE function for solve_ivp
    x, v = state # State variables: displacement (x) and velocity (v)
    dv_dt = -k_over_m * x
    dx_dt = v
    return dv_dt, dx_dt # Return derivatives

# Parameters
mass = 1.0 # kg
spring_constant = 10.0 # N/m
k_over_m = spring_constant / mass # k/m ratio

initial_displacement = 1.0 # m
initial_velocity = 0.0 # m/s
initial_state = [initial_displacement, initial_velocity] # Initial state: [x0, v0]

t_span = (0, 10) # Simulation time span: 0 to 10 seconds

# Solve ODE using solve_ivp
solution_ho = solve_ivp(harmonic_oscillator_ode, t_span, initial_state, args=(k_over_m,), dense_output=True, max_step=0.01) # args=(k_over_m,) pass parameters to ODE function

# Get solution at time points
t_eval = np.linspace(t_span[0], t_span[1], 200) # Evaluate solution at 200 time points
sol_ho_evaluated = solution_ho.sol(t_eval)
x_solution = sol_ho_evaluated[0] # Displacement solution
v_solution = sol_ho_evaluated[1] # Velocity solution

# Plotting
plt.figure(figsize=(10, 6))
plt.plot(t_eval, x_solution, label='Displacement (x)')
plt.plot(t_eval, v_solution, label='Velocity (v)')
plt.xlabel("Time (t)")
plt.ylabel("Displacement, Velocity")
plt.title("Simple Harmonic Oscillator Simulation")
plt.legend()
plt.grid(True)
plt.show()

# Phase space plot (velocity vs. displacement)
plt.figure(figsize=(6, 6))
plt.plot(x_solution, v_solution)
plt.xlabel("Displacement (x)")
plt.ylabel("Velocity (v)")
plt.title("Phase Space Plot (v vs. x)")
plt.axhline(0, color='black', linewidth=0.5, linestyle='--') # Add horizontal line at v=0
plt.axvline(0, color='black', linewidth=0.5, linestyle='--') # Add vertical line at x=0
plt.grid(True)
plt.show()
```

This example demonstrates how to simulate a basic physical system by numerically solving its equations of motion using Python and SciPy. You can extend this approach to simulate more complex systems by defining appropriate ODE functions and using numerical solvers.

## Monte Carlo Methods

Monte Carlo methods are computational algorithms that rely on repeated random sampling to obtain numerical results. They are particularly useful for problems that are probabilistic or have many degrees of freedom, making analytical solutions difficult. In physics, Monte Carlo methods are used in various areas, including statistical mechanics, particle physics, and astrophysics.

**Key Concepts in Monte Carlo Methods:**

*   **Random Sampling:** Generating random numbers from appropriate probability distributions to simulate random processes or sample from probability spaces.
*   **Repeated Trials (Simulations):** Running simulations or trials many times to obtain statistical estimates of desired quantities.
*   **Statistical Estimation:** Using statistical measures (e.g., mean, standard deviation, histograms) from the simulation results to estimate properties of the system or problem.

**Example: Monte Carlo Estimation of π**

A classic example of Monte Carlo method is estimating the value of π (pi). We can do this by randomly sampling points in a square and calculating the ratio of points falling inside a inscribed circle to the total number of points.

```python
# Code cell
import numpy as np
import matplotlib.pyplot as plt

def estimate_pi_monte_carlo(n_points):
    """Estimates pi using Monte Carlo method with n_points."""
    points = np.random.rand(n_points, 2) # Generate n_points random points in a 2D unit square [0, 1] x [0, 1]
    points_inside_circle = 0

    for point in points:
        x, y = point
        if x**2 + y**2 <= 1: # Check if point is inside the unit circle (radius 1)
            points_inside_circle += 1

    pi_estimate = 4 * (points_inside_circle / n_points) # Ratio * area of square (4)
    return pi_estimate

# Number of random points
num_points = 10000

# Estimate pi using Monte Carlo
pi_estimated = estimate_pi_monte_carlo(num_points)
print(f"Estimated value of pi using {num_points} points:", pi_estimated) # Output: (approximate value of pi)

# Visualize Monte Carlo simulation
points_mc = np.random.rand(num_points, 2)
inside_points = []
outside_points = []

for point in points_mc:
    x, y = point
    if x**2 + y**2 <= 1:
        inside_points.append(point)
    else:
        outside_points.append(point)

inside_points = np.array(inside_points)
outside_points = np.array(outside_points)

plt.figure(figsize=(7, 7))
if len(inside_points) > 0:
    plt.scatter(inside_points[:, 0], inside_points[:, 1], color='blue', marker='.', label='Inside Circle')
if len(outside_points) > 0:
    plt.scatter(outside_points[:, 0], outside_points[:, 1], color='red', marker='.', label='Outside Circle')
circle = plt.Circle((0, 0), 1, color='green', fill=False, linewidth=2, label='Unit Circle') # Unit circle for reference
plt.gca().add_patch(circle) # Add circle to plot
plt.xlabel("x")
plt.ylabel("y")
plt.title("Monte Carlo Estimation of π")
plt.xlim(0, 1)
plt.ylim(0, 1)
plt.aspect('equal') # Equal aspect ratio for circle to appear circular
plt.legend()
plt.show()
```

Monte Carlo methods are powerful for simulating random processes, estimating integrals in high dimensions, and solving problems in statistical physics and other fields.

## Agent-Based Modeling

Agent-based modeling (ABM) is a computational modeling approach that simulates the actions and interactions of autonomous agents to understand the emergent behavior of complex systems. Agents are individual entities with defined behaviors and rules, and the system-level behavior emerges from their interactions. ABM is used in various fields, including ecology, social sciences, and increasingly in physics-inspired modeling.

**Key Concepts in Agent-Based Modeling:**

*   **Agents:** Individual entities with attributes, behaviors, and decision-making rules.
*   **Environment:** The space or context in which agents interact.
*   **Interactions:** Rules defining how agents interact with each other and the environment.
*   **Emergence:** System-level patterns and behaviors that arise from agent interactions, which may not be obvious from individual agent rules.

**Example: Simple Agent-Based Model - Flocking Behavior (Boids Model)**

The Boids model, developed by Craig Reynolds, is a classic example of ABM that simulates flocking behavior of birds (or "boids"). Boids follow simple rules:

1.  **Separation:** Avoid crowding neighbors (maintain minimum distance).
2.  **Alignment:** Steer towards the average heading of local neighbors.
3.  **Cohesion:** Steer to move toward the average position of local neighbors.

We can implement a simplified 2D Boids model in Python.

```python
# Code cell
import numpy as np
import matplotlib.pyplot as plt
import matplotlib.animation as animation

class Boid:
    def __init__(self, position, velocity):
        self.position = np.array(position, dtype=float) # Agent position (x, y)
        self.velocity = np.array(velocity, dtype=float) # Agent velocity (vx, vy)

    def update(self, boids, separation_weight=0.5, alignment_weight=0.3, cohesion_weight=0.2, separation_distance=1.0, neighborhood_radius=3.0, max_velocity=5.0):
        # Rules implementation (simplified) - weights and parameters can be tuned
        separation_force = np.array([0.0, 0.0])
        alignment_force = np.array([0.0, 0.0])
        cohesion_force = np.array([0.0, 0.0])
        
        close_boids = 0
        avg_heading = np.array([0.0, 0.0])
        avg_position = np.array([0.0, 0.0])

        for other_boid in boids:
            if other_boid != self:
                distance = np.linalg.norm(self.position - other_boid.position)
                if distance < neighborhood_radius:
                    close_boids += 1
                    avg_position += other_boid.position
                    avg_heading += other_boid.velocity
                    if distance < separation_distance:
                        separation_force -= (other_boid.position - self.position) # Repel from nearby boids

        if close_boids > 0:
            avg_position /= close_boids
            avg_heading /= close_boids
            cohesion_force = (avg_position - self.position) # Move towards average position
            alignment_force = (avg_heading - self.velocity) # Align with average heading

        # Apply forces with weights
        force = separation_force * separation_weight + alignment_force * alignment_weight + cohesion_force * cohesion_weight
        self.velocity += force
        
        # Limit velocity
        speed = np.linalg.norm(self.velocity)
        if speed > max_velocity:
            self.velocity = self.velocity / speed * max_velocity

        self.position += self.velocity # Update position based on velocity

# Simulation parameters
num_boids = 100
simulation_box_size = 50 # Simulation area: [-box_size/2, box_size/2] x [-box_size/2, box_size/2]
boids = []
for _ in range(num_boids):
    position = np.random.uniform(-simulation_box_size/2, simulation_box_size/2, 2) # Random initial positions
    velocity = np.random.uniform(-5, 5, 2) # Random initial velocities
    boids.append(Boid(position, velocity))

# Animation setup
fig, ax = plt.subplots(figsize=(7, 7))
ax.set_xlim(-simulation_box_size/2, simulation_box_size/2)
ax.set_ylim(-simulation_box_size/2, simulation_box_size/2)
scatter = ax.scatter([boid.position[0] for boid in boids], [boid.position[1] for boid in boids], color='blue', marker='o', s=20) # Initialize scatter plot

def animate(frame):
    for boid in boids:
        boid.update(boids) # Update boid positions based on rules

        # Boundary conditions - toroidal (wrap-around) boundaries
        if boid.position[0] > simulation_box_size/2:
            boid.position[0] = -simulation_box_size/2
        elif boid.position[0] < -simulation_box_size/2:
            boid.position[0] = simulation_box_size/2
        if boid.position[1] > simulation_box_size/2:
            boid.position[1] = -simulation_box_size/2
        elif boid.position[1] < -simulation_box_size/2:
            boid.position[1] = simulation_box_size/2

    scatter.offsets = np.array([boid.position for boid in boids]) # Update scatter plot positions
    return scatter,

ani = animation.FuncAnimation(fig, animate, frames=200, interval=50, blit=True) # Create animation
plt.title("Boids Flocking Simulation (Agent-Based Model)")
plt.show() # Show animation (requires a suitable Matplotlib backend, e.g., 'TkAgg' or 'notebook')
```

Agent-based modeling is a powerful approach for simulating complex systems with interacting agents and studying emergent phenomena. It has applications in various fields, including physics-inspired modeling of collective behavior, traffic flow, and social systems.

This chapter provides an introduction to simulation and modeling techniques in Python. You've learned how to build simulations of physical systems by solving ODEs numerically, use Monte Carlo methods for probabilistic problems, and implement basic agent-based models to simulate emergent behavior. These techniques are valuable tools for exploring and understanding complex systems in physics and data science.

**In this chapter, we've covered:**

*   Building simulations of physical systems by numerically solving ODEs using SciPy `solve_ivp`.
*   Monte Carlo methods for probabilistic estimation, with π estimation example.
*   Introduction to Agent-Based Modeling (ABM) and the Boids flocking model example.

In the next chapter, we'll focus on data analysis in physics research, including analyzing experimental data and data visualization for scientific publications.
