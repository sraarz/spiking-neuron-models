# Spiking Neuron Models from Scratch

Numerical implementations of three integrate-and-fire neuron models, built directly
from their differential equations in NumPy — no neural simulation library.

## Models

| Notebook | Model | Governing equation |
|---|---|---|
| [`notebooks/LIF_Model.ipynb`](notebooks/LIF_Model.ipynb) | Leaky Integrate-and-Fire | `τ·du/dt = −(u − u_rest) + R·I(t)` |
| [`notebooks/ALIF_Model.ipynb`](notebooks/ALIF_Model.ipynb) | Adaptive LIF | adds adaptation current `τ_w·dw/dt = a(u − u_rest) − w + b·τ_w·Σδ(t − t_f)` |
| [`notebooks/AELIF.ipynb`](notebooks/AELIF.ipynb) | Adaptive Exponential LIF | adds exponential spike initiation `Δ_T·exp((u − θ_rh)/Δ_T)` |

Each model fires and resets on threshold crossing (`u → u_reset` when `u ≥ θ`).

## What is implemented

- Forward-Euler integration of the membrane potential at `dt = 2×10⁻⁵ s` over a 100 ms window
- Membrane potential traces `U(t)` alongside the driving current `I(t)`
- **F–I curves**: firing frequency as a function of injected current, swept across
  membrane time constants `τ = R·C` to show how membrane properties reshape the
  input–output relationship
- Spike-triggered adaptation (ALIF/AELIF), showing frequency adaptation under
  sustained current that the plain LIF model cannot reproduce
- Responses to constant, step, and noisy (Gaussian) input currents

## Running

```bash
pip install numpy matplotlib seaborn
jupyter notebook
```

Each notebook is self-contained and needs no data or GPU.

## Notes

Parameters use SI units throughout (volts, seconds, farads) rather than the
millivolt/millisecond convention, so values such as `U_rest = -0.065` are in volts.

## Author

Coursework in computational neuroscience, Spring 2022.
