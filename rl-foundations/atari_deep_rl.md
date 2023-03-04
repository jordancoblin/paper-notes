## Playing Atari with Deep Reinforcement Learning

https://arxiv.org/pdf/1312.5602.pdf

Playing Atari with Deep RL Paper

Experience replay: 
- Store all experience in buffer.
- Sample experience randomly from this buffer for Q-learning updates.
Advantages:
- Can use each experience for many updates -> better sample efficiency.
- Learning from consecutive samples is inefficient b/c of strong correlation between samples (non iid). Random sampling breaks correlation and reduces variance of updates?
- Experience replay can smooth out sample distribution.
Note that: off-policy learning is required for ER.

Deep Q-Learning with Experience Replay:
On each timestep:
- Take one action -> add this to replay buffer.
- Sample minibatch from buffer and perform gradient descent update on Q-function.

Architecture:
- Separate output unit per action -> vs. passing action in as input. Avoids need for multiple forward passes.

Evaluation:
- Average reward
- Q-value estimates -> collect fixed set of states from running random policy prior to training and track average Q-values for these states.

DQN appears to work despite lack of theoretical convergence guarantees.
