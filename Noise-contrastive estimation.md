- Noise-contrastive estimation: A new estimation principle for unnormalized statistical models - http://proceedings.mlr.press/v9/gutmann10a/gutmann10a.pdf
and A fast and simple algorithm for training neural probabilistic language models - https://www.cs.toronto.edu/~amnih/papers/ncelm.pdf

Noise-contrastive estimation is a classic technique to efficiently train neural language models. It is not SOTA by any means as of
July 2017 (It has been often observed to produce less competitive performance, though). But it is worthy to have a good understanding
of the method.

Recall that for NNLMs, we need to compute an extremely expensive softmax function for every history: P(w|history) = exp(g(w_t,history))/all_word exp(g(w',history))

How to fix the problem? Here is the part that NCE comes into place. It reduces the problem to that of binary classification: discriminating between samples from the data distribution P(w|history) and samples from a known noise distribution P_{noise}(w). These two problems are totally unrelated to each other at first sights, but there is indeed a strong link between them as we will see later.

Specifically, let us assume that noise samples are k times more frequent than data samples: w is sampled from the mixture

1/(k+1) P(w|history) + k/(k+1) P_{noise}(w)

Let us use a variable D to denote which sample types each word is sampled from (D=1 implies the word samples from data distribution and D=0 implies the word samples from noise distribution). Recall that P(D, w|history) = p(w|history)*p(D|w, histor), we have

P(D|w, history) = P(D, w|history)/p(w|history)

Note that P(D=1, w|history) = 1/(k+1) P(w|history) and P(D=0, w|history) = k/(k+1) P_{noise}(w). We therefore have:


P(D=1|w, history) = 1/(k+1) P(w|history)/(1/(k+1) P(w|history)+k/(k+1) P_{noise}(w)) = P(w|history)/(P(w|history)+k P_{noise}(w))

P(D=0|w, history) = k P_{noise}(w)/(P(w|history)+k P_{noise}(w))






