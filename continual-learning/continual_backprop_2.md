# Maintaining Plasticity in Deep Continual Learning

Exploring how deep networks lose plasticity when trained on sequences of different tasks (i.e. non-stationary classification problem). Varied learning rate, network size, and frequency of tasks switch.
Found loss of plasticity in most cases - less for larger networks, and less when task switching occurred more infrequently.

## Understanding loss of plasticity

**Insight**: the only difference in the agent across time is the weights in the network. It must be some properties of these weights that cause decrease in plasticity, and some
properties of the initial weight distribution that make it plastic. Some possible properties: diversity, non-saturation, small in magnitude, etc.

**Causes**
- Accumulation of dead neurons: neurons that produce same output regardless of input -> zero gradient, hence no longer get updated + can no longer contribute towards learning.
- Increase in weight magnitude: large weights have been associated with learning instability (e.g. exploding gradients), as gradients/weights can be unbounded. Can use L2-regularization to limit weight magnitudes.
- Decreasing effective rank: effective rank = measure how concentrated the influence of features is on matrix transformation (i.e. high effective rank means most features contribute roughly equally to transformation). Hypothesis: lower effective rank = lower capacity of network to represent functions.

## Existing Methods




## Questions
- Where did effective rank come from? Why not stable rank?
