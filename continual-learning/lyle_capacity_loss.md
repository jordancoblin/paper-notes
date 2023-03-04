## Understanding and Preventing Capacity Loss in Reinforcement Learning

https://arxiv.org/pdf/2204.09560.pdf

Lots of non-stationarity in RL -> difficult for nns.

**Capacity loss**: networks trained on sequence of target values lose ability to quickly update their predictions over time.

Target-fitting capacity:
Understand when agent's parameters are flexible enough to allow good continual updates.
Capacity: ability of network to reach a new set of targets within limited optimization budget from current params + optimizer state. Ability of network to eventually represent a new target function (non-stationarity?).

**Hypothesis 1**: Networks trained to fit a sequence of dissimilar targets will lose capacity to fit new target functions.
Found: decreasing ability to fit later target funcs. Sufficiently over-parameterized networks (1 mill params for 1k data points) exhibit positive forward transfer.
**Hypothesis 2**: non-stationary prediction problems result in capacity loss (for Deep RL).

Measure of capacity: "feature rank" - how easily states can be distinguished by updating only the final layer of the network. Captures network's ability to quickly adapt to changes in target func.

Representation collapse: network features converge to zero.

Approach to reduce capacity loss:
- Initial feature regularization (InFeR): l2 regularization penalty on output-space by regressing a set of auxiliary outputs towards their values at initialization. Similar approach has been used to prevent catastrophic forgetting in continual learning.
	- Effect: preserve subspace of features present at initialization.

Could borrow some ideas from EWC for tackling the 

Terms: 
- Forward transfer.

Questions:
- Hypothesis 2: "We generate target functions by randomly initializing neural networks with new
parameters, and use the outputs of these networks as targets for regression." Don't understand how we can use these arbitrary targets? RL agent should require expected return as target?
