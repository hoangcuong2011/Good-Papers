- *Gaussian Processes for Classification* - Chapter 3 of the book Gaussian Processes for Machine Learning http://www.gaussianprocess.org/gpml/chapters/RW3.pdf

Gaussian Processes are pretty powerful models for regression. Yet it is not quite straightfoward to extend the models to work
with classification. I found this chapter is not easy to understand, but I learnt quite a lot from it. I will try to
summarize its most crucial points here.

Let us turn our attention to binary classification: we need to classify each new input to 1 or 0. 
The straightforward way is to perform regression where the output values is 1 or 0. Specifically, given an input x, we can assume
a latent function over x as follows:

    f(x) = N(mean, variance).

It means that what we need to do is construct a Gaussian distribution in which sampling from the distribution gives us only values around +1 and -1? I don't think
this is a right approach to do.

We can also perform regression where the ouput values is P(y=1|x) or P(Y=-1|x) instead. I don't know whether it is a right approach to
try, but we at least stuck with the problem of constructing a Gaussian distribution that generating data is within range 0 and 1.
Even if we can do that in a nice way, I don't see how we can train such a model?

Okay in practice those are not the cases. Here is the way people do, which involves two steps:

    1. Evaluate a latent function f that models how the likelihood of one class versus the other over an input.
    
    2. Squash the output onto [0, 1] using an additional function (e.g. sigmoid, probit)

At this point, I guess it is hard to imagine how to train the model, since we do not obsere values of latent function f. The authors claim: the purpose of f is soly to allow a convenient formulation of the model, and f will be integrated out during training/prediction. Specifically, inference is divided into two steps for each new input x*. First we need to compute P(f*|x, y, x*) where <x, y> is training dataset.

    P(f*|x, y, x*) = integral df p(f*|x, x*, f)p(f|x, y)
    
Second we need to compute this function

    P(y* = 1|x, y, x*) = integral df* prior(f*)P(f*|x, y, x*)
Here prior(f*) is the value of squashing the output onto [0, 1]. It is however not trivial at all to compute P(f*|x, y, x*) (because p(f|x, y) is not a Gaussian distribution, i.e. y is only +1, -1 and therefore it is not the case) and P(y* = 1|x, y, x*) (because prior(f*) is not a Gaussian distribution).
