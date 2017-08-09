- **Gaussian Processes for Classification** - Chapter 3 of the book Gaussian Processes for Machine Learning http://www.gaussianprocess.org/gpml/chapters/RW3.pdf

Gaussian Processes are pretty powerful models for regression. Yet it is not quite straightfoward to extend the models to work
with classification. I found this chapter is not easy to understand, but I learnt quite a lot from it. I will try to
summarize its most crucial points regarding to the intuition here.

Let us turn our attention to binary classification: we need to classify each new input to +1 or -1. 
The straightforward way is to perform regression where the output values is +1 or -1. Specifically, given an input x, we can assume
a latent function over x as follows:

    f(x) = N(mean, variance).

It means that what we need to do is to construct a Gaussian distribution in which sampling from the distribution gives us only values around +1 and -1? I don't think
this is a right approach to do.

We can also perform regression where the ouput values is P(y=1|x) or P(Y=-1|x) instead. I don't know whether it is a right approach to
try, but we at least stuck with the problem of constructing a Gaussian distribution that generating data is within range 0 and 1. Even if we can do that, I don't see how we can train such a model?

Okay in practice those are not the approaches people try. Here is the best way to date, which involves two steps:

    1. Evaluate a latent function f that models how the likelihood of one class versus the other over an input.
    
    2. Squash the output onto [0, 1] using an additional function (e.g. sigmoid, probit)

It can be somewhat similar to the regression approach I just mentioned, but it is indeed very different. At this point, I guess it is hard to imagine how to train the model, since we do not observe values of latent function f. The authors claim: the purpose of f is soly to allow a convenient formulation of the model, and f will be integrated out during training/prediction. 

Inference is divided into two steps for each new input x*. First we need to compute P(f*|x, y, x*) where <x, y> is training dataset.

    P(f*|x, y, x*) = integral df p(f*|x, x*, f)p(f|x, y)
    
Second we need to compute this function

    P(y* = 1|x, y, x*) = integral df* prior(f*)P(f*|x, y, x*)
    
Here prior(f*) is the value of squashing the output onto [0, 1]. 

It is not trivial at all to compute P(f*|x, y, x*) (note p(f|x, y) is not a Gaussian distribution, i.e. y is only +1, -1 and therefore it is not the case) and P(y* = 1|x, y, x*) (note prior(f*) is not a Gaussian distribution).

**How to compute P(f*|x, y, x*) **

We first focus on computing P(f*|x, y, x*). The simplest approach is to use sampling (e.g. MCMC). This approach is extremely espensive, though. The another approach, which I found very smart is to approximate p(f|x, y) using a normal distribution.
The key insight here is that such an approximation "implies a Gaussian Process approximation to the posterior process, which gives rise to an approximate P(f*|x, y, x*)" (see these two papers for a reference: Assessing Approximations for Gaussian Process Classification (http://papers.nips.cc/paper/2903-assessing-approximations-for-gaussian-process-classification.pdf) and its longer version Assessing Approximate Inference for Binary Gaussian Process Classification (http://www.jmlr.org/papers/volume6/kuss05a/kuss05a.pdf)). But how to approximate p(f|x, y)? Laplace's method comes into place now (see this for an introduction https://github.com/hoangcuong2011/Good-Papers/blob/master/Gaussian%20CheatSheet.md).
Expectation Propagation can also be a solution. 

1. Laplace's method

Even if you know Laplace's method, I don't think it is straigtforward to apply it here. If we *blindedly" apply Laplace's method, let us assume f^ as the solution of

    f^ = argmax_f p(f|x, y)
   
With f^, p(f|x, y) can be computed as follows:

    p(f|x, y) \approx N(f|f^, A^-1) where A s the negative second order derivative of ln p(f|x, y) at f^.

Well, we got stuck at this point - we obviously cannot compute second order derivative of ln p(f|x, y).

So this is the way Laplace's method is actually applied. Notice that:

    p(f|x, y) = p(x, y, f)/p(x, y) = p(y|x, f)p(x, f)/p(x, y) = 
              = p(y|f)p(f|x)p(x)/(p(y|x)p(x)) = p(y|f)p(f|x)/p(y|x).

The denominator p(y|x) does not involve with f at all, let us focus the unnormalized log version of p(f|x, y) instead:

    unnormalize log p(f|x, y) = ln  p(y|f)  + ln  p(f|x)

Recall from GPs for regression, ln  p(f|x) has a very nice form:
    
    ln p(f|x) = -1/2(f^T K^-1 f + ln |K| + n ln 2 \pi

the first and second order derivatives of ln p(f|x) also has the nice for:
    
    (ln p(f|x))' = -K^{-1}f
    (ln p(f|x))'' = -K^{-1}

It is the right time to apply Laplace's method:

    p(f|x, y) \approx N(f|f^, (K^{-1}+(ln  p(y|f))'')^-1

The last is about finding f^. This is indeed not trivial at all. We know that (ln  p(y|f))' - K^{-1}f^ = 0, so

    f^ = K((ln  p(y|f^))')
    
To solve this problem, we can use Newton method. I haven't had any experience with using Newton method for this problem, though! As you can see, everything is fully non-trivial!

**How to compute P(y* = 1|x, y, x*)**

P(y* = 1|x, y, x*) is also very challenging to compute because prior(f*) is not a Gaussian distribution. The first step to address the problem is to decompose P(y* = 1|x, y, x*) into two components as follows:

    P(y* = 1|x, y, x*) = \integral_{}^{}df* P(y*=1| f*)P(f*|x, y, x*)

Even with that, it is still not trivial at all to compute P(y* = 1|x, y, x*). If  P(y*=1| f*) is a probit distribution, the integral can be solved analytically. If we use sigmoid, perhaps sampling is the only option.


---- to be continued ------
