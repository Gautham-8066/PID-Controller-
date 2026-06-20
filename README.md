# PID Controller Simulation in Simulink

A MATLAB/Simulink implementation of a closed-loop control system utilizing a Parallel PID (Proportional-Integral-Derivative) controller to stabilize a third-order dynamic plant. This repository contains the Simulink model and performance analysis configurations.

<img width="1707" height="628" alt="image" src="https://github.com/user-attachments/assets/e0d7f274-d299-4db2-9f41-9e02301db02a" />


## System Architecture

The simulation models a standard negative feedback control loop consisting of the following key stages:

1. **Input Signal:** A step input $u(t)$ acting as the reference command/setpoint.
2. **Error Detection:** A summing junction that calculates the instantaneous error signal, $e(t) = u(t) - y(t)$, where $y(t)$ is the plant output.
3. **PID Controller:** Processes the error signal through three parallel branches:
   * **Proportional Path:** Multiplies the error signal directly by a static proportional gain block, $K_p = 5$, to provide an immediate corrective response proportional to the error magnitude.
   * **Integral Path:** Integrates the error ($\frac{1}{s}$) to eliminate steady-state tracking error, scaled by an integral gain block, $K_i = 5$.
   * **Derivative Path:** Computes the rate of change of the error ($\frac{\Delta u}{\Delta t}$) to provide predictive damping and reduce overshoot, scaled by a derivative gain block, $K_d = 1$.
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
The plot below shows the closed-loop step response captured by the Scope block, comparing the reference input command $u(t)$ (yellow) against the plant's actual output response $y(t)$ (blue).
<img width="1919" height="1018" alt="Screenshot 2026-06-03 140137" src="https://github.com/user-attachments/assets/d5af0ace-bbf2-4450-a4ca-3dc3f541e3b7" />

---
