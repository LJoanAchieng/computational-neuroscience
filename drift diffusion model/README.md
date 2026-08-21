# Drift-Diffusion Model & Confirmation Bias

A from scratch Python implementation of the drift-diffusion model (DDM) —
the standard model of how decisions form moment-to-moment from
accumulating noisy evidence extended to model confirmation bias
quantitatively. This is the second core tool in the cognitive
computational neuroscience / neuroeconomics phase, following the
[reward learning & RPE project](../reward-learning-model).

## The core idea

Reward learning (the previous project) is about learning *value* slowly,
over many trials, through experience. This project asks a different
question: when faced with a choice right now, how does a decision
actually form, moment by moment, within a single instant?

The classic example: shown a cloud of moving dots, mostly drifting
right but mixed with random noise, how do you decide "left" or "right"?
The drift-diffusion model's answer: the brain accumulates evidence over
time a noisy tally that climbs toward one of two boundaries. The
moment it crosses a boundary, that's the decision, and the time it took
is the reaction time. This single mechanism explains, from one process,
why easier decisions are both faster and more accurate.

## The equation

```
dx = v * dt + sigma * dW
```

- `x` — accumulated evidence so far
- `v` — drift rate: the average speed and direction evidence pushes the
  tally (positive = toward one boundary, negative = toward the other)
- `sigma` — the amount of random noise added at each moment
- `dW` — a random nudge at each instant (a Wiener process)

Simulated the same way as the other projects in this series: tiny time
steps, updating `x` a little each step, until it crosses an upper or
lower boundary.

## Project structure

```
drift-diffusion-model/
├── drift_diffusion_model.ipynb   # Full step-by-step build, in order
└── README.md
```

The notebook is organized into five sections:

**1. The core model**
A single decision trial: evidence accumulates from zero, jittering
noisily, until it crosses a boundary. Confirms that stronger, one-sided
evidence (larger `v`) produces a rising path that reaches the correct
boundary quickly and reliably.

**2. Strong vs. weak evidence**
Sweeps drift rate across several values and measures both accuracy and
mean reaction time. Confirms the model's signature result: stronger
evidence produces both faster *and* more accurate decisions, from one
mechanism, not two separate rules. In this run: weak evidence (v=0.2)
produced only 64% accuracy at ~3.7s average, while strong evidence
(v=2.0) produced 100% accuracy at ~0.5s.

**3. Starting-point bias**
Models prior conviction: instead of always starting at zero, the tally
can start already biased toward one boundary (`x0`). With genuinely
near-neutral evidence (v=0.05), a neutral starting point led to
choosing "right" only 22% of the time but a strong starting bias
(x0=0.9) led to choosing "right" 91.5% of the time, despite the
underlying evidence barely favoring either side. A follow-up experiment
found that overturning a strong starting bias required roughly 10-20x
stronger contrary evidence than a neutral starting point would need to
reach the same decision.

**4. Drift-rate bias (confirmation bias)**
A second, more literal model of confirmation bias: rather than starting
biased, the momentary evidence itself is weighted unevenly — evidence
confirming a preferred belief counts at full strength, while evidence
contradicting it gets dampened. Tested against a clear case (true
evidence favors "left", agent prefers "right", contrary evidence
dampened to 30% strength): accuracy dropped from 100% (unbiased) to 0%
(biased) on the same evidence conditions. Reaction time did not
consistently increase biased decisions can be just as fast as
unbiased ones, since the bias creates an artificially strong, unopposed
pull toward the preferred answer rather than a weak, hesitant signal.

**5. Side-by-side comparison**
The same underlying random evidence stream (same seed, same true
direction) run through unbiased vs. biased processing. Both start
identically; only the weighting of contrary evidence differs. The
unbiased trace correctly reaches the true boundary; the biased trace,
given the identical raw information, steadily and confidently arrives
at the wrong one.

## Key finding: what confirmation bias actually looks like

The most important result from this project is not that biased
reasoning is more error-prone (expected) it's that biased reasoning
does not necessarily look uncertain or hesitant. A confirmation-biased
decision process can be just as fast, and just as smooth, as a correct
one. There is no built-in hesitation signal distinguishing a confident
wrong answer from a confident right one, from the outside, without
seeing the underlying evidence-weighting process itself.

## Why this connects to economics and neuroeconomics

The drift-diffusion model is a workhorse in behavioral economics and
neuroeconomics for modeling choice under uncertainty. Starting-point and
drift-rate bias are the standard quantitative mechanisms researchers use
to model real phenomena like anchoring, prior belief resistance, and
motivated reasoning the same territory as the "why do people make the
decisions they make" question driving this whole project series.

## Usage

```bash
pip install numpy matplotlib jupyter
jupyter notebook drift_diffusion_model.ipynb
```

Run all cells in order — later sections reuse functions defined earlier.

## What's next

Fitting a model from this series to real, open behavioral data
moving from simulation to actually estimating model parameters from
real human choices, the project that most directly draws on a Data
Analysis background.

## References

Ratcliff, R. (1978). A theory of memory retrieval. *Psychological
Review*, 85(2), 59-108.

Ratcliff, R., & McKoon, G. (2008). The diffusion decision model: Theory
and data for two-choice decision tasks. *Neural Computation*, 20(4),
873-922.
