- *The Human Kernel* - http://papers.nips.cc/paper/5765-the-human-kernel

A very interesting paper to read! I don't think it provides any novel techniques as claimed in the paper, but I think it is
a very good work that helps us understand better how GP extrapolates beyond data and how human can do that.

Things that should be clear in the first place: extrapolation is difficult. I am not so sure how well other models (e.g. Neural networks) can handle the challenge. For GPs, I have to say it is extremely non-trivial. Experiments in the paper reveal that too.

I should also note about RBF: small length scale implies two things. First, the curve we draw from a GP with the kernel function would be not so smooth. Second, the complexity of the GP model is very large (if we draw a curve from a GP with a kernel funtion with a very large value, the curve should almost look like a line.



But the goal of the paper is not really to try to compare the performance of GPs with humans. More specificially,
let us assume we have a GP with a specific kernel (e.g. RBF or spectral mixture (see this https://github.com/hoangcuong2011/Good-Papers/blob/master/Gaussian%20Process%20Kernels%20for%20Pattern%20Discovery%20and%20Extrapolation.md)). The authors
try two different way to learn the parameters:

1. maximizing the marginal likelihood of the training data (note that we only have a set of training data, so let us
call the data as a single "realisation").
2. maximixing the marginal likelihood of the human-extrapolation-annotated data. Note that there are multiple people who did
the job, and the authors assume their prediction data (from each person) is sampled from a certain distribution. This is fundamentally different to the first approach regarding to the training philosophy. Yet regarding to the training technique it is quite straightforward: the marginal likelihood of the data is simply a product of the marginal likelihood of prediction data from each person.

What the authors learnt from their experiments is that:

- (2) is extremely helpful. (1) is quite inaccurate. This is what Figure 1 is all about. This is also what Firgure 3 o and 3p are about. This raises to me an interesting question: Should I split the training data to multiple subsets and learn model parameters under these multiple realisations?

- Humans have a strong prior bias for smooth functions (i.e. heavy-tailed correlation). I believe this is what Figure 2(g) is about. But I might be wrong.

- RBF is very inaccurate. We should use a GP with a spectral mixture kernel, even though such a model is far from perfect.


The next bunch of experiments are about Human Occam's razor. Several conclusions are made from experiments:

- Maximixing marginal likelihood of training data causes underfitting. I found this really surprising. Should we penalize harder the complexty terms in the formula??? I think we should do so to learn more accurate parameters. But I am not so sure why the authors do not state that explicitly.

- Even more surprising, humans prefer an even much simpler solution. As a side note, humans agree with the GP marignal likelihood about the best fit.
