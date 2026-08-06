# Hodgkin-Huxley Neuron Model

A from-scratch Python implementation of the Hodgkin-Huxley model the
biophysical model of the action potential that Alan Hodgkin and Andrew
Huxley developed from experiments on the squid giant axon, earning them
the 1963 Nobel Prize in Physiology or Medicine. Built as a direct
follow-up to the [leaky integrate-and-fire model](../lif-neuron-model),
replacing that model's faked spike with the real ion channel dynamics
that generate the action potential naturally.

## The core idea

A neuron's membrane has voltage-gated ion channels "doors" that open
and close depending on the voltage itself. The action potential emerges
from the interplay of two of these channel types:

1. A stimulus nudges voltage up slightly.
2. **Sodium (Na⁺) channels** fly open fast. Sodium rushes in, and since
   it's positively charged, voltage shoots up sharply the spike's rise.
3. Almost immediately after, the sodium channels **inactivate** (shut
   themselves off, even though voltage is still high), and separately,
   **potassium (K⁺) channels** open more slowly. Potassium flows out,
   pulling voltage back down the spike's fall.
4. Because potassium is slow to close again, voltage briefly dips below
   resting level (the afterhyperpolarization) before settling back.

## The equations

Four coupled differential equations: one for voltage, three for the
gating variables that control channel opening.

```
C_m * dV/dt = I_ext - I_Na - I_K - I_L

I_Na = g_Na * m^3 * h * (V - E_Na)
I_K  = g_K  * n^4 * (V - E_K)
I_L  = g_L  * (V - E_L)

dn/dt = alpha_n(V)*(1-n) - beta_n(V)*n
dm/dt = alpha_m(V)*(1-m) - beta_m(V)*m
dh/dt = alpha_h(V)*(1-h) - beta_h(V)*h
```

- `V` — membrane voltage
- `m` — sodium activation gate (opens fast)
- `h` — sodium inactivation gate (closes shortly after, shutting sodium
  off even while voltage is still high)
- `n` — potassium activation gate (opens slower, repolarizes the
  membrane)
- `g_Na`, `g_K`, `g_L` — maximum conductance for each channel
- `E_Na`, `E_K`, `E_L` — reversal potentials each ion pushes voltage
  toward
- `alpha`/`beta` functions empirical rate functions Hodgkin and Huxley
  fit directly to their voltage-clamp recordings, describing how fast
  each gate opens and closes at a given voltage

Simulated using 4th-order Runge-Kutta (RK4) integration more accurate
than simple Euler integration, needed because the sodium dynamics are
fast and numerically "stiff."

## Project structure

```
hodgkin-huxley-model/
├── hodgkin_huxley_model.ipynb   # Full step-by-step build, in order
└── README.md
```

The notebook is organized into five sections, each building on the last:

**1. Rate functions and ionic currents**
The `alpha`/`beta` functions for each gate, and the three ionic current
equations. Includes a plot of the rate functions against voltage,
showing why sodium activation (`alpha_m`) rises so steeply near -40 mV
the trigger point for the spike.

**2. Resting gate values**
Steady-state values for `m`, `h`, `n` at rest, found the same way as the
LIF model's steady-state voltage: setting the rate of change to zero and
solving. At rest, sodium channels are mostly closed (`m` low) but
available to open (`h` high), while potassium sits at a moderate
baseline (`n` in between).

**3. Single action potential**
A short current pulse triggers one full spike the real shape this
time: sharp rise, peak, fast fall, and a brief undershoot, with no
faked reset rule. Also plots the gating variables underneath the voltage
trace, showing `m` shooting up first, `h` dropping right after, and `n`
rising more slowly.

**4. Repetitive spiking**
A sustained current produces a regular train of spikes at a stable,
repeatable rate.

**5. f-I curve**
Firing rate vs. input current. Unlike the LIF model's smooth ramp, the
Hodgkin-Huxley model shows a sharp jump in firing rate once current
crosses a critical value — a real, documented property known as "Class 2
excitability," distinct from the LIF model's "Class 1" smooth onset.

## LIF vs. HH comparison

Both models share the same core skeleton (leak + input + spike), but
generate the spike very differently. LIF fakes it with a
threshold/reset rule, HH generates it from real channel dynamics. This
leads to genuinely different f-I curve shapes: LIF ramps up smoothly
from zero, while HH stays silent then jumps sharply past a threshold
current. This distinction (Class 1 vs. Class 2 excitability) is a real
classification used to describe different real neuron types, and it
affects how neurons encode information — Class 1 neurons can fire
arbitrarily slowly and encode information in their rate, while Class 2
neurons behave more like an on/off switch.

## Usage

```bash
pip install numpy matplotlib jupyter
jupyter notebook hodgkin_huxley_model.ipynb
```

Run all cells in order later sections depend on variables and
functions defined earlier (rate functions, `steady_state_gates`,
`simulate`, etc.).

## What's next

Having built the mechanistic foundation (LIF and HH), the next phase
moves into cognitive computational neuroscience: reinforcement learning
and reward prediction error models, bridging into decision-making and
reward-based learning connecting to a background in economics and data
analysis.

## References

Hodgkin, A. L., & Huxley, A. F. (1952). A quantitative description of
membrane current and its application to conduction and excitation in
nerve. *The Journal of Physiology*, 117(4), 500–544.

Gerstner, W., Kistler, W. M., Naud, R., & Paninski, L. (2014).
*Neuronal Dynamics*. Cambridge University Press. (Free online at
neuronaldynamics.epfl.ch)
