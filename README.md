# Good-Papers

- Variational Inference with Normalizing Flows: One of the best papers I read recently! A very good note can be found here
https://casmls.github.io/general/2016/09/25/normalizing-flows.html

An open question, as described in the reference note: ``whether the proposed normalizing flows is a universal approximator of all the distributions when the number of layers go to infinity."
Two technical questions: Do we still need to assume P(z_0) as a Gaussian distribution? Why is the model not scalable regarding to high-dimensional latent space?

- MADE: Masked Autoencoder for Distribution Estimation: An inspiring work! It shows how autoencoder can be used for density estimation. Of course doing that is non-trivial as a conventional autoencoder can simply memorize all the data given large enough units in hidden layers, implying it cannot be used for the task. The paper addresses this problem by structuring the network so that its output represents conditional probabilities of a dimension given the others. They proposed masked autoencoder to do so.

Question: This is a very nice framework, but how to make it work with real value?
