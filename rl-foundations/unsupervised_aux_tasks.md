## Reinforcement Learning with Unsupervised Auxiliary Tasks

https://arxiv.org/pdf/1611.05397.pdf

Idea: learning to predict and control various aspects of the agent's data stream will lead to more useful representations for agent's long-term goals.

Architecture:
- Aux control and prediction tasks share the same conv. NN and LSTM that the base agent uses.
