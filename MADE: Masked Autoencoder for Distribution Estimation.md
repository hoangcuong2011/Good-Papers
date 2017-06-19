- MADE: Masked Autoencoder for Distribution Estimation: https://arxiv.org/abs/1502.03509

An inspiring work! It shows how autoencoder can be used for density estimation. Of course doing that is non-trivial as a conventional autoencoder can simply memorize all the data given large enough units in hidden layers, implying it cannot be used for the task. The paper addresses this problem by structuring the network so that its output represents conditional probabilities of a dimension given the others. They proposed masked autoencoder to do so.

Question: This is a very nice framework, but how to make it work with real value?

