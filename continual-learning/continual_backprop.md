# Continual Backprop: Stochastic Gradient Descent with Persistent Randomness

## Overview
SGD degrades over time in continual learning. Proposal for solution: continually inject random features using a generate-and-test method (Continual Backprop).
Experiments show that this algo can adapt in moth SL and RL settings.

## Problem
Backprop does not work well for non-stationary problems. This paper is focused on adapting to new changes, and not on remembering previous info.
Focus on problems with large number of non-stationarities (thousands).

Special class of problem: semi-stationary. Online SL, where input distribution is non-stationary while the target function is stationary.

## Continual Backprop (CBP)
Hypothesis: Backprop's ability to adapt degrades because the benefits of initial random distribution are not present throughout lifetime.

CBP continually injects random features. Two parts:
- Generator: proposes new features.
- Tester: find and replace low utility features with proposed features.

## Experiments
Several non-stationary problems: bit-flipping (regression), permuted MNIST, slippery ant. Use target network that is more complex than learner network,
so that the best learner approximation must change as input changes. Tried various activation functions for learner network.

## Results
Error gets worse over time for all step sizes and activation functions.
