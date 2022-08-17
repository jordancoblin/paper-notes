# World Models

https://arxiv.org/pdf/1803.10122.pdf

Three components:

- Vision (**V**): uses variational auto-encoder to learn a compressed representation of observation space.
- Memory (**M**): predictive model - i.e. models transition function $P(z_{t+1} | a_t, z_t, h_t)$ where $h_t$ is hidden state at time $t$, outputs a probability density function (since many envs are stochastic). Use Mixture Density Network output layer to approximate P as a mixture of Gaussian distribution (MDN-RNN).  
- Controller (**C**): control agent. Uses a simple linear layer, such that most of the complexity lives in **M** and **V**. $a_t = W_c [z_t h_t] + b_c$

<img width="452" alt="image" src="https://user-images.githubusercontent.com/7538750/185034977-aca81f81-8cba-4caf-bb49-1835560bc6f0.png">

Training:
- Collect a set of 10,000 rollouts using random policy.
- Train V using these rollouts by minimizing loss between input vector and output vector reconstructed from $z_t$.
- Pass inputs through V to obtain latent input vectors $z_t$, and train M.

Can also use this model for planning/"hallucinating" experience.
