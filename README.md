# PID Controller Simulation in Simulink

A MATLAB/Simulink implementation of a closed-loop control system utilizing a Parallel PID (Proportional-Integral-Derivative) controller to stabilize a third-order dynamic plant. This repository contains the Simulink model and performance analysis configurations.

<img width="1707" height="628" alt="image" src="https://github.com/user-attachments/assets/e0d7f274-d299-4db2-9f41-9e02301db02a" />


## System Architecture

The simulation models a standard negative feedback control loop consisting of the following key stages:

![Simulink Model Architecture](docs/model_screenshot.png) **


1. **Input Signal:** A step input $u(t)$ acting as the reference command/setpoint.
2. **Error Detection:** A summing junction that calculates the instantaneous error signal, $e(t) = u(t) - y(t)$, where $y(t)$ is the plant output.
3. **PID Controller:** Processes the error signal through three parallel branches:
   * **Proportional Path:** Multiplies the error signal by a static gain block. *(Note: In the model diagram layout, the proportional and integral gain labels are inverted—the integrator path $\frac{1}{s}$ is routed to the block labeled $K_p$, while the direct proportional path is routed to $K_g$. Functionally, these gains scale the system as $K_i = 5$ and $K_p = 5$ respectively).*
   * **Integral Path:** Integrates the error ($\frac{1}{s}$) to eliminate steady-state error, scaled by a gain of 5.
   * **Derivative Path:** Computes the rate of change of the error ($\frac{\Delta u}{\Delta t}$) to provide predictive damping, scaled by a gain $K_d = 1$.
4. **Plant Dynamics:** A third-order Linear Time-Invariant (LTI) continuous-time system defined by the transfer function:
   $$G(s) = \frac{s^2 + 6s + 10}{s^3 + 7s + 1}$$
5. **Visualization:** A multi-port Scope capturing both the reference input $u(t)$ and the controlled plant output $y(t)$ simultaneously for transient response analysis (overshoot, rise time, settling time).

---

## Technical Specifications

| Parameter / Block | Value / Configuration |
| :--- | :--- |
| **Plant Transfer Function** | $\frac{s^2 + 6s + 10}{s^3 + 7s + 1}$ |
| **Proportional Gain ($K_p$)** | 5 |
| **Integral Gain ($K_i$)** | 5 |
| **Derivative Gain ($K_d$)** | 1 |
| **Feedback Type** | Negative Feedback |

---

## Performance & Results

![Step Response Output](docs/step_response.png) **

The Scope block plots the system's dynamic tracking capabilities. The controller adjusts the transient response characteristics to ensure the third-order plant accurately tracks the step input command with minimal steady-state error.

---

## Repository Structure

```text
├── .gitignore
├── README.md
├── PIDcontroller.slx          # Core Simulink model file
└── docs/
    ├── model_screenshot.png   # Block diagram image
    └── step_response.png      # Scope output graph
