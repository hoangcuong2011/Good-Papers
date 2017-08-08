- *Gaussian Processes for Classification* - Chapter 3 of the book Gaussian Processes for Machine Learning http://www.gaussianprocess.org/gpml/chapters/RW3.pdf

Gaussian Processes are pretty powerful models for regression. Yet it is not quite straightfoward to extend the models to work
with classification. I found this chapter is not easy to understand, but I learnt quite a lot from it. I will try to
summarize its most crucial points here.

Let us turn our attention to binary classification: we need to classify each new input to +1 or -1. 
The straightforward way is to perform regression where the output values is +1 or -1. Specifically, given an input x, we can assume
a latent function over x as follows:

    f(x) = N(mean, variance).

It means that what we need to do is to construct a Gaussian distribution in which sampling from the distribution gives us only values around +1 and -1? I don't think
this is a right approach to do.

We can also perform regression where the ouput values is P(y=1|x) or P(Y=-1|x) instead. I don't know whether it is a right approach to
try, but we at least stuck with the problem of constructing a Gaussian distribution that generating data is within range 0 and 1.Even if we can do that, I don't see how we can train such a model?

Okay in practice those are not the approaches people try. Here is the best way to date, which involves two steps:

    1. Evaluate a latent function f that models how the likelihood of one class versus the other over an input.
    
    2. Squash the output onto [0, 1] using an additional function (e.g. sigmoid, probit)

It can be somewhat similar to the regression approach I just mentioned, but it is indeed very different. At this point, I guess it is hard to imagine how to train the model, since we do not observe values of latent function f. The authors claim: the purpose of f is soly to allow a convenient formulation of the model, and f will be integrated out during training/prediction. 

Inference is divided into two steps for each new input x*. First we need to compute P(f*|x, y, x*) where <x, y> is training dataset.

    P(f*|x, y, x*) = integral df p(f*|x, x*, f)p(f|x, y)
    
Second we need to compute this function

    P(y* = 1|x, y, x*) = integral df* prior(f*)P(f*|x, y, x*)
    
Here prior(f*) is the value of squashing the output onto [0, 1]. 

It is not trivial at all to compute P(f*|x, y, x*) (because p(f|x, y) is not a Gaussian distribution, i.e. y is only +1, -1 and therefore it is not the case) and P(y* = 1|x, y, x*) (because prior(f*) is not a Gaussian distribution).

The perhaps only way to address the problem is using approximation. We first focus on computing P(f*|x, y, x*), which is difficult because of p(f|x, y). We can easy the difficulty if p(f|x, y) is approximated by a normal distribution, so that the integral can be intractable to compute (see this https://github.com/hoangcuong2011/Good-Papers/blob/master/Gaussian%20CheatSheet.md). Laplace's method comes into place now (see this for an introduction https://github.com/hoangcuong2011/Good-Papers/blob/master/Gaussian%20CheatSheet.md). Let us assume f^ as the solution of

    f^ = argmax_f p(f|x, y)
   
Using Laplace's method, 

    p(f|x, y) \approximate N(f|f^, A^-1) where A s the negative second order derivative of ln p(f|x, y) at f^.

The challenge now is finding f^. This is indeed not trivial at all. See the chapter for a reference. The method in the chapter only works with some nice squashing form (i.e. sigmoid and probit only), though.


P(y* = 1|x, y, x*) is also very challenging to compute because prior(f*) is not a Gaussian distribution. The first step to address the problem is to decompose P(y* = 1|x, y, x*) into two components as follows:

    P(y* = 1|x, y, x*) = \integral_{}^{}df* P(y*=1| f*)P(f*|x, y, x*)
