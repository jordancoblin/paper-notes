## Deep Reinforcement Learning with Double Q-learning

Q-learning overestimates action values in some circumstances, and can negatively affect perf of learned policies. Double Q-Learning can be applied to DQN to 
mitigate this.

Over-estimation bias: when we sample from a stochastic distribution (with noise/function approx), max is biased to be larger than it should.

Double Q-Learning: train two independent networks on distinct streams of experience. Take the argmax of Q_phi1 to find the optimal action, but evaluate this
action using Q_phi2 to compute the target. One network for action selection (the network being trained), another for action evaluation. Both networks should be trained
in unison to keep them up-to-date.
- Uses double estimator approach over single estimator (which has been shown to be a biased estimator of max_i E{X_i}).

Double DQN: instead of maintaining two independent networks (as would be the case for standard Double Q-Learning), can use the DQN target network as the
second value function. Target network = periodic copy of the online/training network. Reasoning: introduce minimal changes/computational overhead to original
DQN algo.

Over-estimation does not always negatively affect quality of learned policies (e.g. DQN achieves optimal behabiour in Pong despite overestimation). However, 
reducing overestimation has been shown to significantly benefit learning stability in many cases.
