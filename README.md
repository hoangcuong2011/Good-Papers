# Good-Papers

- Variational Inference with Normalizing Flows: One of the best papers I read recently! A very good note can be found here
https://casmls.github.io/general/2016/09/25/normalizing-flows.html

An open question, as described in the reference note: ``whether the proposed normalizing flows is a universal approximator of all the distributions when the number of layers go to infinity."
A technical question: Do we still need to assume P(z_0) as a Gaussian distribution?

- MADE: Masked Autoencoder for Distribution Estimation: An inspiring work! It shows how autoencoder can be used for density estimation. Of course doing that is non-trivial as a conventional autoencoder can simply memorize all the data given large enough hidden units, implying it cannot generate any new meaningful images (?). The paper addresses this problem by structuring the network so that its output represents conditional probabilities of a dimension given the others. They proposed masked autoencoder to do so.
