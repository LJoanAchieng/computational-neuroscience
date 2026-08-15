# Social Media & Reward Prediction Error: Why You Can't Stop Scrolling

An extension of the [reward learning & RPE project](../reward-learning-model),
applying the same reward prediction error model to a very different
question: why is it so hard to stop scrolling social media feeds, even
when most of what you see isn't interesting?

This project was sparked by noticing the exact mechanism happening in
real time scrolling through a string of irrelevant content, refusing
to stop, and getting a small jolt of satisfaction the moment something
relevant finally appeared. It turns out that's not a coincidence or a
personal quirk it's the same reward prediction error system modeled in
the previous project, just being deliberately exploited by unpredictable
content delivery.

## The core idea: predictable vs. unpredictable reward

A feed with a **fixed, learnable reward rate** (e.g. always roughly 50%
interesting) eventually stops surprising you once your brain learns
the pattern, reward prediction error settles near zero, and the pull
fades. This is a fully expected reward: no surprise, no dopamine jolt,
low incentive to keep checking.

A feed with a **randomly drifting reward rate** sometimes great,
sometimes boring, with no stable pattern can never be fully learned.
Your brain's belief about how good the feed is always lags behind the
constantly-moving true rate, so nearly every check carries some
surprise. This is a variable ratio reinforcement schedule the same
principle behind slot machines, and (not by coincidence) heavily present
in how social media feeds are designed.

## Project structure

```
social-media-dopamine-model/
├── social_media_dopamine_model.ipynb   # Full step-by-step build, in order
└── README.md
```

The notebook has three sections:

**1. Predictable vs. unpredictable feed comparison**
Two simulated feeds: one with a fixed reward probability, one where the
true reward probability drifts randomly over time. The learner's belief
(`V`) tracks the fixed feed's true rate closely and settles down. Against
the drifting feed, `V` visibly lags behind the constantly-moving true
rate, producing persistently larger and messier reward prediction
errors direct evidence that unpredictability, not just reward itself,
is what sustains a strong RPE signal over time.

**2. RPE comparison over time**
Plots reward prediction error for both feed types side by side. The
predictable feed's RPE shrinks and stabilizes near zero as learning
converges. The unpredictable feed's RPE stays elevated and variable
throughout, since the target it's trying to learn never stops moving.

**3. Checking cost**
Adds a small fixed cost to every "check" (representing time, attention,
or opportunity cost), and tracks whether the learned value of checking
stays positive despite that cost. Even with a cost applied every single
trial, the learned value stayed positive on effectively all trials in
this simulation modeling why the small "cost" of checking a feed
rarely outweighs the pull of a possible surprise reward.

## What this connects to

This is a direct application of the same Rescorla-Wagner reward
prediction error rule from the previous project, combined with a classic
finding from behavioral psychology: **variable reinforcement schedules
produce more persistent behavior than fixed, reliable rewards** a
result B.F. Skinner demonstrated with animals decades before app design
made deliberate use of it. The dopamine mechanism this exploits is the
same one described by Schultz's reward prediction error findings covered
in the previous project.

## Usage

```bash
pip install numpy matplotlib jupyter
jupyter notebook social_media_dopamine_model.ipynb
```

## Caveats

This is a simplified illustrative model, not a validated account of
social media's psychological effects real platforms involve social
reward, notification design, variable content length, and many other
factors not captured here. The point of this project is to demonstrate
the core mechanism (unpredictable reward sustains stronger, more
persistent RPE signals than predictable reward) using the same modeling
tools built in the reward-learning project, not to make strong claims
about real-world platform design.

## References

Schultz, W., Dayan, P., & Montague, P. R. (1997). A neural substrate of
prediction and reward. *Science*, 275(5306), 1593-1599.

Skinner, B. F. (1957). *Schedules of Reinforcement*. Appleton-Century-Crofts.
