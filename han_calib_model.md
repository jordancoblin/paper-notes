# No More Pesky Hyperparameters: Offline Hyperparameter Tuning for RL

https://arxiv.org/pdf/2205.08716.pdf

Agents often highly sensitive to hyperparams. Typically need sweeps to tune. 

Tune hyper-parameters from a learned calibration model.

**Data2Online**: use offline data to tune hypers. 

## Section 3:
Example hypers: alpha, # of layers in NN, initial NN weights, e.g.
Perf(lambda) = online performance of agent, when deployed with hypers.
Challenge: must evaluate Perf(lambda) against a learning (rather than fixed) policy. What does this mean exactly?

## Section 4:
AgentPerfInEnv -> actions sample from Agent(s). Is this policy fixed?

Calibration model should be:
1) Stable: starting from any initial state in a region, the model remains in that region.
   Self-correcting: even if some non-real states are produced -> will come back to space of real states.
2) Handle actions with low coverage: common choice -> *could assume pessimistic transitions (non-observed actions have bad outcomes). But optimism could also make sense, since it encourages exploration.
3) Focus on initialization params, since can only test each hyperparam for limited number of steps in calibration model. Focus on early learning.

## Section 5 (KNN Calibration Model):

- Stored tuples (s_i, a_i, r_i, s_i')
- Calc distances between input (s_t, a_t) and stored tuples. Similar state action tuples are more likely to be chosen by calibration model as outcome.
- Distance metric is tricky: Euclidian distance may be innacurate (e.g. if there is a wall). Use Laplacian representation.
- Alternatives: kernel density estimator (KDE), NN.
- Fast lookup: cache k-nearest neighbors for each data point.

5.2 Distance Metric
- Idea: map state/actions that have similar outcomes in terms of next states + rewards to similar vectors (similarity in transition dynamics) -> laplace representations. 

5.3 Insufficient data coverage
- Pessimistic approach: truncate episode when encountering un-seen pair. Return minimum return experienced in dataset (making the agent less likely to visit this state-action pair again in future episodes).

## Section 6 (Experiments):

1. Collect data: 5000 transitions from near-optimal policy.
2. Evaluate true performance of each hyper-param: sweep each hyper-param in deployment env.
3. Construct calibration models (i.e. KNN, FQI, etc.) using transition data log.
4. Evaluate performance of each model: sweep each hyperparam and choose best for each model.

Only need steps 3 and 4 for water treatment.
Maybe just pick one hyperparameter to try on deployment env.

Questions:
- Which of the K nearest neighbors does the model actually select? Probability distro, 1 - softmax().
- What policy does the agent follow during hyper-param tuning/deployment? Start from scratch?
- Do we need to use the same agent between data collection/hyperparam tuning/deployment phases?
- Pessimistic strategy when encountering action-states that we haven't seen before. How does this work for a continuous action space? Could we default to regular Euclidian distance in this case?
- 4.2 states that we should focus only on initialization params -> Is this just because we don't want each sweep to take too long?
- How did you make Figure 1??
- Figure 3: experiments. How does FQI have more variance than random in Puddle World?
- How long did it take you to write this paper?
- Code in https://github.com/hwang-ua/WTP_calibration/: did you write this all from scratch? E.g. DQN agent


Baseline:
- Current policy + hyperparams.
- Calibration model selected hyperparam.



Further reading:
- Adam Optimizer
- KL divergence dynamic policy programming:
 	- https://jmlr.org/papers/volume13/azar12a/azar12a.pdf
 	- KL divergence (in value func) important for sample efficiency?
 - Fitted Q iteration
