# Falling Film Mass Transfer & Penetration Theory (Python)

This repository contains Python scripts for calculating mass transfer characteristics in falling liquid films. It compares the **Infinite Penetration** (Higbie's theory) and **Finite Penetration** models to determine how deep a solute penetrates a moving film under various physical conditions.

---

## Mathematical Logic

The scripts solve the governing equations for convective mass transfer in a laminar falling film.

### 1. Film Hydrodynamics
The film thickness ($\delta$) and average velocity ($u$) are calculated based on the film flow rate ($\Gamma$) and fluid properties (density $\rho$, viscosity $\mu$):

$$\delta = \left( \frac{3 \mu \Gamma}{\rho^2 g} \right)^{1/3}$$
$$u = \frac{\Gamma}{\rho \delta}$$

### 2. Infinite Penetration Model
For short contact times or thick films, the solute is assumed not to reach the wall. The local mass transfer coefficient ($k_c$) is:

$$k_c(y) = \sqrt{\frac{3 u D}{2 \pi y}}$$

### 3. Finite Penetration Model
When the solute reaches the wall (finite depth), the concentration profile is solved using a Fourier series expansion. The code determines a characteristic parameter ($\xi$) by solving for the root of the error function:

$$\text{Error} = \left( \sum_{n=0}^{\infty} \frac{(-1)^n}{2n+1} \exp\left( - \left[ \frac{(2n+1)\pi}{2\xi} \right]^2 \cdot \frac{D y}{u} \right) \right) - \frac{\pi}{4}$$

### 4. Mass Flux Calculation ($N_A$)
The local mass flux at the interface is determined by:

$$N_A = k_c \cdot (c_{Ai} - c_{A0})$$

Where $c_{Ai}$ is the interfacial concentration and $c_{A0}$ is the bulk concentration.

---

## File Structure

| File | Variable Focus | Description |
| :--- | :--- | :--- |
| `2019_UT_MRL_dPen_varD.py` | **Diffusivity ($D$)** | Analyzes how different diffusion coefficients impact the penetration depth and flux. |
| `2019_UT_MRL_dPen_varG.py` | **Flow Rate ($\Gamma$)** | Analyzes the effect of film velocity and thickness on mass transfer efficiency. |

---

## Usage Instructions

### Prerequisites
* Python 3.x
* **NumPy** library: `pip install numpy`

### Execution
1. Open the desired script (e.g., `2019_UT_MRL_dPen_varD.py`).
2. Adjust the **Test Data** section to match your physical system:
   ```python
   L = 1         # Wall length (m)
   gamma = 0.05  # Film flow rate (kg/m.s)
   cAi = 0.0366  # Interfacial concentration
