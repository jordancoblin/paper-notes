# Understanding Variational Autoencoders (VAEs)

VAEs are a type of deep generative model that have become popular in recent years (alongside GANs).

**Autoencoder**: maps input data to "latent" representation (usually more compact, i.e. lower # of dimensions) via encoder. And then back to a representation with the original # of dimensions via the decoder.
Trained by minimizing the "reconstruction loss" between the result of decoder and original input.

**Attempt #1** at generating new data using this model: sample some point from the latent space and run this through the decoder.
Issues:
- The point that we sampled may have no meaningul output when fed through the decoder. (I.e. may be trained on shapes, but output is nothing resembling a shape).

**Regularization to the Rescue**
Can regularize the latent space, such that it also holds some properties that are useful for data generation. These properties are:
a) **Continuity**: Points that are close together in latent space also produce similar outputs.
b) **Completenes**: All points in the latent space produce some "meaningful" output.
c) Avoid overfitting of input data.

**Variational Autoencoders**: encoder now maps to _distributions_ over the latent space instead of points. Points are then sampled from this distribution and fed into the decoder to compute reconstruction error.

<img width="720" alt="image" src="https://user-images.githubusercontent.com/7538750/192180890-ee95f606-52ef-438f-93c4-b848cb3383f8.png">

Encoding input as probability distributions allows us to naturally express regularization: distributions are enforced to be close to a standard normal distribution.
The regularization term is expressed as the KL-divergence between the latent distribution and a standard Gaussian.

To achieve continuity and completeness, regularize the covariance matrix and mean of the distributions returned by the encoder.

Creates a "gradient" over the information encoded in the latent space.

**Variational Inference**: technique to approximate complex distributions. Select from a hypothesis class of parameterized distributions (e.g. family of Gaussians, whose parameters are mean and covariance) the best approximation of target distribution.
The best element in the hypothesis class is the one that minimizes the error (usually KL-divergence) between approximation and target, and can be found by gradient descent over parameters.


## Questions
- What does it mean for the encoder to produce distributions, exactly? Every input gives some different distribution? What is the structure of such a latent representation?
- Which part of regularization achieves which property?
