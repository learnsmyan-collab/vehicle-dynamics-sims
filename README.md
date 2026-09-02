# Longitudinal Vehicle Performance & Aero Sensitivity Engine

A MATLAB script I put together to simulate straight-line vehicle acceleration when it's actually constrained by real-world physics—specifically tire grip limits, power curves, and aerodynamic drag. It also runs a sweep across different drag coefficients ($C_d$) to see how aero efficiency affects top-end speed over a 10-second run.

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

---

## Running the Code

1. **Clone the repo:**
   ```bash
   git clone [https://github.com/learnsmyan-collab/vehicle-dynamics-sims.git](https://github.com/learnsmyan-collab/vehicle-dynamics-sims.git)
   cd vehicle-dynamics-sims
