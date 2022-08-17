# World Models

https://arxiv.org/pdf/1803.10122.pdf

Three components:

- Vision (**V**): uses variational auto-encoder to learn a compressed representation of observation space.
- Memory (**M**): predictive model - i.e. models transition function $ P(z_t+1 | a_t, z_t, h_t) $, outputs a probability density function (since many envs are stochastic). 
