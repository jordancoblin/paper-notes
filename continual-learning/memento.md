# On Catastrophic Interference in Atari 2600 Games

Catastrophic interference is present WITHIN single games, not just multi-task - for deep RL.

Memento experiment: 
- Agent perf reaches plateau -> copy value network to new Memento agent.
- Memento agent begins each episode from final position of preceding agent, and trains from there.
- Whereas original agent needs to start from initial state in each episode.
- Difference between agents is the _contents of the agent's replay buffer_.

Measuring interference:
- Train on one context, evaluate on others.

