- Noise-contrastive estimation: A new estimation principle for unnormalized statistical models - http://proceedings.mlr.press/v9/gutmann10a/gutmann10a.pdf
and A fast and simple algorithm for training neural probabilistic language models - https://www.cs.toronto.edu/~amnih/papers/ncelm.pdf

Noise-contrastive estimation is a classic technique to efficiently train neural language models. It is not SOTA by any means as of
July 2017 (I noticed it often produces less competitive performance compared to other methods, though). But it is worthy to have a good understanding
of the method. As a side note, there are several excellent tutorials about this topic (e.g. https://arxiv.org/pdf/1410.8251.pdf and http://ruder.io/word-embeddings-softmax/index.html)

Recall that for NNLMs, we need to compute an extremely expensive softmax function for every history: P(w|history) = exp(g(w_t,history))/all_word exp(g(w',history))

How to fix the problem? Here is the part that NCE comes into place. It reduces the problem to that of binary classification: discriminating between samples from the data distribution P(w|history) and samples from a known noise distribution P_{noise}(w). These two problems are totally unrelated to each other at first sights, but there is indeed a strong link between them as we will see later.

Specifically, let us assume that noise samples are k times more frequent than data samples: w is sampled from the mixture

1/(k+1) P(w|history) + k/(k+1) P_{noise}(w)

Let us use a variable D to denote which sample types each word is sampled from (D=1 implies the word samples from data distribution and D=0 implies the word samples from noise distribution). Recall that P(D, w|history) = p(w|history)*p(D|w, histor), we have

P(D|w, history) = P(D, w|history)/p(w|history)

Note that P(D=1, w|history) = 1/(k+1) P(w|history) and P(D=0, w|history) = k/(k+1) P_{noise}(w). We therefore have:


P(D=1|w, history) = 1/(k+1) P(w|history)/(1/(k+1) P(w|history)+k/(k+1) P_{noise}(w)) = P(w|history)/(P(w|history)+k P_{noise}(w))
and
P(D=0|w, history) = k P_{noise}(w)/(P(w|history)+k P_{noise}(w))

Did we make anything easier? Unfortunately, everything is still the same! Our goal is to reduce the problem to that of computing P(D=1|w, history) and P(D=0|w, history). Yet our equation still involves p(w|history), which is obviously too expensive to compute. 

Getting stuck at this point, I was wondering two questions:
1. Why does the author reduces the problem to binary classification? Is there any link between them?
2. How to move forward?

Now let me answer question 1. To train our binary classification, we simply maximze the expectation (Eq. 9) in Gutman paper. The Gradient of the objective results Eq 11. When k goes to infinity, the derivative of gradient leads to Eq. 12, which is nice because the gradient is zero only when the mode distribution matches the emprical distribution.


The next part is to answer question 2. How to sidestep the problem? Recall that:

P(w|history) = exp(g(w_t,history))/all_word exp(g(w',history))

NCE sidestep the problem by treating the normalzing constant as a learned parameter (i.e. instead of computing it directly, we try to induce it through inference). In other words, we assume:

P(w|history) = exp(g(w_t,history)) exp(log c_{history})),

here c_{history} can be understood as a learned parameter corresponding to the logarithm of the normalizing constant with respect to each history: c_{history} = all_word exp(g(w',history)). It can be learned during training. Two things surprised me with this trick: it actually works (why?), and second c_{history} closes to 1 in practice. Therefore, as reported by Mnih and Teh, fixing the normalizing constants to 1 instead of learning hem, did not affect the performance of resulting models. You might also wonder why the authors did not try to do the same trick to solve the original problem. The reason is that if we do that, the normalizing constants all_word exp(g(w',history)) can be reached close to zero to achieve large likelihood. Reducing the problem to binary classification, this is not the case (the sum of P(D=1|w, history) and P(D=0|w, history) does not go to arbitrarily large).

As a summary, let me recall what Chris Dyer wrote: NCE transfors the computationally expensive learning problem into a binary classification proxy problem that uses the same parameters but requires statistics that are easier to compute. This is pretty much what NCE is. The idea is pretty non-trivial, and a good one to know!



