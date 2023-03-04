## Learning Latent Dynamics for Planning from Pixels

https://arxiv.org/pdf/1811.04551.pdf


## Latent-space planning

Assuming access to a learned dynamics model, how to plan. Use POMDPs to model image-based environment. PlaNet learns a transition model, observation model, and reward model from previous experience. Also learn an encoder to infer approximate belief of current hidden state from history. Policy is planning algorithm that uses dynamics model to search for best sequuence of future actions. Do not use value or policy network like many other algos.

Collect new experience during planning experience to refine the dynamics model - add small Gaussian noise to each action and use repeat actions when collecting this additional experience.

Use a latent dynamics model (instead of directly predicting from one image to the next) to allow for fast and efficient planning, i.e. by eliminating computation that would be needed to encode and decode images. Recurrent state-space model uses an RNN to yield deterministic state transitions, and feeds the output of this RNN into the stochastic transition model. This allows for the transition model to remember multiple time steps in the past, and give accurate predictions many steps forward.


## Summary:

This paper introduces a novel model-based reinforcement learning agent called PlaNet that learns a latent dynamics model which can be used for planning in high-dimensional environments. A latent dynamics model generates trajectories in latent space instead of the input space (i.e. in this case, pixel-based images), allowing for fast computation during planning. The authors propose a dynamics model that has both deterministic and stochastic components, in order to more accurately predict transitions multiple time-steps into the future. This hybrid model, which they name a "recurrent state space model" (RSSM) is shown to exceed performance of purely stochastic or purely deterministic models across several control tasks.
This dynamics model learned over real experience is then used to train an agent solely via planning, using the "cross entropy method" to infer a distribution over optimal action sequences. Basically, this involves sampling action sequences from a Gaussian distribution, evaluating each sequence using the dynamics model, and then adjusting the Gaussian distribution parameters based on the top K sequences. In order to enhance the dynamics model (i.e. provide data for unexplored parts of the environment), the agent also injects trajectories that are sampled from its dynamics model into the dataset used to train the model.

Lastly, the paper also introduces the idea of latent overshooting...

Since image data provides only partial observability over the environment state, use a variational encoder to infer an approximate belief of state, conditioned on previous observations and actions.



Results:
When compared with state of the art model-free methods, PlaNet achieves similar (and sometimes better) performance, using an average of 500x less interaction with the environment.

Questions
- Why do we refine the dynamics model by sampling from the dynamics model? Shouldn't we only refine the model through real (non-simulated) experience?
- Why use MPC over some other planning algorithm? What are other alternatives?
- How does the RSSM model compare to other approaches at model learning/system identification?



Terms I did not understand

- Model predictive control (MPC)
- Non-linear Kalman filter
- The Cross-Entropy Method
- Bayesian filtering
