[README.md](https://github.com/user-attachments/files/30757916/README.3.md)
# Computational Neuroscience

A running collection of computational neuroscience projects, built as I
teach myself the field from the ground up starting from simplified
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

## Focus: Cognitive Computational Neuroscience

After exploring the different subfields of computational neuroscience
(mechanistic modeling, systems/data neuroscience, cognitive computational
neuroscience, computational psychiatry, neuromorphic engineering, BCI,
connectomics), I've chosen to specialize in **cognitive computational
neuroscience**modeling higher-level processes like decision-making,
learning, and reward using quantitative tools. This connects directly to
my background: reinforcement learning and reward-based decision models
draw heavily on behavioral economics, and fitting models to real
behavioral data draws on my Data Analysis MSc.

The mechanistic modeling projects below (LIF, Hodgkin-Huxley) remain the
foundation understanding the biology from first principles before
moving into the cognitive/decision-making modeling projects that are the
actual focus going forward.

## Project

| Project | Description |
|---|---|
| [`lif-neuron-model/`](./lif-neuron-model) | Leaky integrate-and-fire neuron: leak dynamics, input current, threshold/reset spiking, and the f-I curve. The simplest model that still produces realistic spiking behavior. |
| `hodgkin-huxley-model/` | The classic Hodgkin-Huxley model replaces the LIF model's faked spike with real sodium/potassium channel gating dynamics that generate the action potential naturally. |
| `reward-learning-model/` | A reinforcement learning (Q-learning) agent and reward prediction error the bridge between economics, reinforcement learning, and dopamine neuroscience. |
| `drift-diffusion-model/` | A classic cognitive neuroscience model of how decisions form over time from accumulating evidence. |
| `behavioral-data-fitting/` | Fitting a cognitive model to real, open behavioral/decision-making data combining modeling with data analysis. |

## Learning approach

Each project follows the same build-up:

1. Understand the concept in plain terms before writing any code
2. Translate it into a mathematical/computational model
3. Build the simulation incrementally, checking intuition against results
   at each step (e.g., predicting what a parameter change should do,
   then verifying it)
4. Document what was learned in that project's own README

## Roadmap

**Phase 1 — Foundations**
- [x] Leaky integrate-and-fire (LIF) neuron
- [ ] Hodgkin-Huxley single neuron model

**Phase 2 — Core cognitive modeling tools**
- [ ] Reinforcement learning & reward prediction error (Q-learning)
- [ ] Bayesian models of belief updating
- [ ] Drift-diffusion model of decision-making

**Phase 3 — Applied / portfolio capstone**
- [ ] Fit a cognitive model to real open behavioral data
- [ ] Reproduce a result from a published cognitive neuroscience paper

## References

- Gerstner, W., Kistler, W. M., Naud, R., & Paninski, L. (2014).
  *Neuronal Dynamics*. Cambridge University Press. (Free online at
  neuronaldynamics.epfl.ch)
- Hodgkin, A. L., & Huxley, A. F. (1952). A quantitative description of
  membrane current and its application to conduction and excitation in
  nerve. *The Journal of Physiology*, 117(4), 500–544.
