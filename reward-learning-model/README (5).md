# Reinforcement Learning & Reward Prediction Error

A from-scratch Python implementation of reward-based learning, built to
understand how the brain (and simple algorithms) learn what's valuable
through trial and error — and how this directly explains a famous finding
in dopamine neuroscience. This is the first project in the cognitive
computational neuroscience phase, following the mechanistic modeling
foundation built in the [LIF](../lif-neuron-model) and
[Hodgkin-Huxley](../hodgkin-huxley-model) projects.

## The core idea

How does an animal, person, or algorithm learn which choices lead to good
outcomes? The core loop:

1. Try an action.
2. Get a reward (or don't).
3. Compare what you expected against what you actually got.
4. Use that gap to update your expectations.
5. Repeat — expectations get more accurate over time.

That gap between expected and actual reward is called the **reward
prediction error (RPE)**, and it's one of the most important ideas in
this field — because the brain appears to compute something
mathematically identical to it, using dopamine neurons.

## The famous neuroscience finding

Wolfram Schultz and colleagues recorded from dopamine neurons in monkeys
in the 1990s and found that dopamine neurons fire in proportion to
**reward prediction error, not reward itself**:

- Unexpected reward → strong dopamine burst (large positive RPE)
- Fully expected reward → no dopamine response at all (RPE ≈ 0)
- Expected reward that doesn't arrive → dopamine dip below baseline
  (negative RPE)

This reframed dopamine from a "pleasure chemical" into a **learning
signal** — mathematically equivalent to the error term in a
reinforcement learning algorithm.

## The equation

The Rescorla-Wagner rule (the ancestor of modern Q-learning):

```
V_new = V_old + alpha * (R - V_old)
```

- `V` — current expected value of an action
- `R` — actual reward received
- `(R - V_old)` — the reward prediction error
- `alpha` — learning rate: how much a single new experience updates the
  belief

Same structural pattern as the leak equation in the LIF model — current
state, nudged by the gap between where it is and where new evidence says
it should be.

## Project structure

```
reward-learning-model/
├── reward_learning_model.ipynb   # Full step-by-step build, in order
└── README.md
```

The notebook is organized into four sections:

**1. Single-option value learning**
One choice, with a fixed (but noisy) probability of reward. Watches `V`
converge toward the true reward probability over repeated trials, purely
through the RPE update rule. Also compares different learning rates
(alpha): high alpha reacts strongly to each trial and looks jumpy in a
noisy environment; low alpha is slower but more stable.

**2. Two-armed bandit (real decision-making)**
Two options, each with a different true reward probability. Introduces
softmax action selection — the agent picks probabilistically, favoring
higher-value options but still sometimes exploring the other one. As
`tau` (temperature) approaches 0, choice becomes nearly deterministic
(always the current best guess); larger `tau` pushes choice toward
random. This is the classic exploit-vs-explore tradeoff, central to both
reinforcement learning and economic decision theory.

**3. The RPE signal over time**
Plots reward prediction error trial by trial. Early trials show large
swings (lots of surprise, since expectations haven't formed yet); later
trials cluster near zero (expectations are accurate, so outcomes rarely
surprise the agent) — this is the direct model analogue of dopamine
firing shrinking as learning converges.

**4. Reproducing the Schultz dopamine finding**
Three manually constructed scenarios — fully expected reward, unexpected
reward, and expected reward omitted — directly recreate the real
dopamine recording pattern: no RPE (no bar) for the fully expected case,
a strong positive RPE for the unexpected reward, and a strong negative
RPE for the omitted reward.

## Usage

```bash
pip install numpy matplotlib jupyter
jupyter notebook reward_learning_model.ipynb
```

Run all cells in order — later sections reuse functions and variables
defined earlier.

## Why this connects to economics

The Rescorla-Wagner rule is structurally close to Bayesian belief
updating and rational expectations models in economics: hold a belief,
receive new information, revise the belief in proportion to how
surprising that information was. The exploit-vs-explore tradeoff in the
two-armed bandit is also a direct analogue of exploration decisions in
economic search theory. This overlap is a large part of why reward
learning sits at the center of neuroeconomics.

## What's next

Next up: a drift-diffusion model of decision-making — how choices form
over time from accumulating noisy evidence, the second core tool in the
cognitive computational neuroscience toolkit, focused on the moment of
choice rather than learning value over time.

## References

Schultz, W., Dayan, P., & Montague, P. R. (1997). A neural substrate of
prediction and reward. *Science*, 275(5306), 1593-1599.

Rescorla, R. A., & Wagner, A. R. (1972). A theory of Pavlovian
conditioning: Variations in the effectiveness of reinforcement and
nonreinforcement. *Classical Conditioning II*, 64-99.
