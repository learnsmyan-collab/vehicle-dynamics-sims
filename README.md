# Longitudinal Vehicle Performance & Aero Sensitivity Engine

A MATLAB simulation framework I built to model straight-line vehicle acceleration under realistic physical constraints—specifically handling tire grip limits, dynamic power curves, and aerodynamic drag, all while running a drag coefficient ($C_d$) sensitivity sweep.

---

## How It Works

Instead of assuming constant acceleration, the model calculates a few moving parts at every time step:
* **Tire Grip:** Clamps the maximum push using a high-grip friction coefficient ($\mu = 1.6$).
* **Power Limits:** Shifts from a controlled launch phase into a standard power-limited curve ($F = P / v$) as speed builds up.
* **Aero Sweep:** Tests $C_d$ values from $0.6$ to $1.2$ to map out how much drag kills terminal velocity.

---

## The Math Simplified

At any given point, the net force ($F_{net}$) comes down to whatever the tires or engine can give minus the aerodynamic drag ($F_d$):

$$F_{net} = \min\left(\frac{P_{max}}{v}, \mu \cdot m \cdot g\right) - \left(0.5 \cdot \rho \cdot v^2 \cdot C_d \cdot A\right)$$

Velocity updates iteratively using a standard forward Euler step:

$$v_{i+1} = v_i + \left(\frac{F_{net}}{m}\right) \cdot \Delta t$$


### 1. Velocity Profile Across Aero Configurations
![Vehicle Acceleration Profile](outputs/vehicle_acceleration.png)

### 2. Aerodynamic Efficiency Sensitivity Analysis
![Aero Sensitivity Result](outputs/aero_sensitivity.png)

---

## Repository Structure

```text
vehicle-dynamics-sims/
│
├── src/
│   └── vehicle_performance_sim.m   # Core simulation & sensitivity analysis script
├── outputs/

└── README.md
