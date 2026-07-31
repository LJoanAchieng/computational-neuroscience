[README.md](https://github.com/user-attachments/files/30580280/README.2.md)
# Computational Neuroscience

A running collection of computational neuroscience projects, built as I
teach myself the field from the ground up — starting from simplified
models and working toward the full biophysical detail. This repo is part
of my preparation for a master's in Computational Neuroscience.

## Background

Coming from an Electrical Engineering degree, an Economics background, and
currently pursuing an MSc in Data Analysis, I'm building this repo to
learn computational neuroscience hands-on: understanding each model well
enough to build it from scratch before moving to the next level of detail,
rather than just running existing code.

Each project folder is self-contained, with its own README explaining the
biology, the math, and what the code does.

## Projects

| Project | Description |
|---|---|
| [`lif-neuron-model/`](./lif-neuron-model) | Leaky integrate-and-fire neuron: leak dynamics, input current, threshold/reset spiking, and the f-I curve. The simplest model that still produces realistic spiking behavior. |
| `hodgkin-huxley-model/` | The classic Hodgkin-Huxley model — replaces the LIF model's faked spike with real sodium/potassium channel gating dynamics that generate the action potential naturally. |
| `spiking-network/` | Small networks of connected spiking neurons, exploring emergent dynamics like synchronization. |

## Learning approach

Each project follows the same build-up:

1. Understand the biology in plain terms before writing any code
2. Translate the biology into a differential equation
3. Build the simulation incrementally, checking intuition against results
   at each step (e.g., predicting what a parameter change should do,
   then verifying it)
4. Document what was learned in that project's own README

## Roadmap

- [x] Leaky integrate-and-fire (LIF) neuron
- [ ] Hodgkin-Huxley single neuron model
- [ ] Small spiking neural network
- [ ] Analysis of real open neural data (e.g. Allen Brain Observatory)
- [ ] A machine-learning-for-neuroscience project

## References

- Gerstner, W., Kistler, W. M., Naud, R., & Paninski, L. (2014).
  *Neuronal Dynamics*. Cambridge University Press. (Free online at
  neuronaldynamics.epfl.ch)
- Hodgkin, A. L., & Huxley, A. F. (1952). A quantitative description of
  membrane current and its application to conduction and excitation in
  nerve. *The Journal of Physiology*, 117(4), 500–544.
