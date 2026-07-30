# Leaky Integrate-and-Fire (LIF) Neuron Model

A from-scratch Python implementation of the leaky integrate-and-fire model,
built step by step to understand *why* each part of the model exists before
writing it. This is the simplest neuron model that still produces realistic
spiking behavior, and it's the natural stepping stone toward more detailed
biophysical models like Hodgkin-Huxley.

## The core idea

Think of the neuron's voltage as a leaky bucket of water:

- Input current pours water in — voltage rises.
- The membrane "leaks" — voltage naturally drains back toward a resting
  level over time.
- When voltage crosses a **threshold**, the neuron fires a spike and resets
  back down — like the bucket tipping over and emptying.

## The equation

```
tau * dV/dt = -(V - V_rest) + R * I(t)
```

- `V` — membrane voltage right now
- `V_rest` — resting voltage (-65 mV)
- `I(t)` — input current
- `R` — membrane resistance
- `tau` — time constant, controls how fast voltage leaks back to rest

Simulated numerically using Euler's method: at each small time step `dt`,
compute `dV/dt` from the equation above, then nudge `V` forward by
`dV/dt * dt`.

## Project structure

```
lif-neuron-model/
├── lif_neuron_model.ipynb   # Full step-by-step build, in order
└── README.md
```

The notebook is organized into four sections, each building on the last:

**1. Leak only**
Starting above rest with zero input, voltage decays smoothly back to
`V_rest`. This is exponential decay, driven entirely by the leak term.
Also compares different values of `tau`: smaller `tau` means faster decay,
since `tau` divides the rate of change in the equation.

**2. Constant input current**
With input current flowing in, voltage rises and settles at a new
steady-state level (`V_rest + R*I`) rather than rising forever — the
leak term grows stronger as voltage rises, until it balances the input.

**3. Threshold and reset (spiking)**
Adding a threshold and reset rule produces genuine repetitive spiking:
voltage climbs toward the steady-state, crosses threshold, resets, and
repeats — as long as the steady-state voltage is above threshold.

**4. f-I curve**
Firing rate vs. input current. Below a critical current (where
steady-state voltage equals threshold), the neuron never fires. Above
it, firing rate rises smoothly and continuously — unlike the Hodgkin-Huxley
model's sharp jump, which is a genuine biological difference between
neuron excitability classes (Class 1 vs. Class 2).

## Usage

```bash
pip install numpy matplotlib jupyter
jupyter notebook lif_neuron_model.ipynb
```

Run all cells in order — later sections depend on variables defined earlier
(`V_rest`, `tau`, `R`, `dt`).

## What's next

This model fakes the spike itself (snap up, reset down). The next step is
the **Hodgkin-Huxley model**, which replaces that shortcut with the real
sodium and potassium channel dynamics that generate the spike shape
naturally — same core skeleton (leak + input + integration), with real
ion channel gating added on top.

## References

Gerstner, W., Kistler, W. M., Naud, R., & Paninski, L. (2014).
*Neuronal Dynamics*. Cambridge University Press. (Free online at
neuronaldynamics.epfl.ch) — Chapter 1 covers the LIF model in depth.
