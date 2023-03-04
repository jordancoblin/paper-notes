## Implicit under-parameterization inhibits data-efficient deep reinforcement learning

Rank of network features drops during training in deep RL. This effect is exaggerated for algorithms that perform more gradient updates (e.g. several gradient updates per environment step). Bootstrapping is a driver of this effect - it does not occur when using MC updates.

### Proposed mitigation
Introduce a penalty/regularizer that penalizes low srank in the network. Results: srank found to be much more stable (and even increasing in some cases). Penalty improves performance in all Atari games for DQN, with median improvement of 74.5% and in 11/16 games for CQL, with median improvement of 14.1%.

Another possible mitigation technique could be to develop new auxiliary losses that learn useful features while "passively preventing underparameterization" - https://arxiv.org/abs/1611.05397?context=cs.

Author also suggests that the general path forward is to leverage deep learning theory tools to understand the effects of neural nets + associated pieces like initialization, optimizer, etc. on learning behaviour.
