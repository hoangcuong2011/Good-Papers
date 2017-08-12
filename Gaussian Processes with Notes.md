- Gaussian Processes with Notes

Gaussian Processes are pretty models. In this article I refer several important claims:

**Short notes**
- GPs are limited in their ability to learn non-stationary functions (e.g., a function with sudden jumps). http://www2.ift.ulaval.ca/~chaib/publications/Yali-AISTAS16.pdf (the best explanation of non-stationary functions I ever seen) 
- A GP is an MLP with infinite units in the hidden layer, source: Neal 1996
- Gaussian processes provide flexible, non-parametric, probabilistic approaches to function estimation. However, their tractability comes at a price: they can only represent a restricted class of
functions. Indeed, even though sophisticated definitions and combinations of covariance functions can lead to powerful models (Durrande et al., 2011; Gönen & Alpaydin, 2011; Hensman et al.,
2013; Duvenaud et al., 2013; Wilson & Adams, 2013), the assumption about joint normal distribution of instantiations of the latent function remains; this limits the applicability of the models. One
line of recent research to address this limitation focused on function composition (Snelson et al., 2004; Calandra et al., 2014). Inspired by deep neural networks, a deep Gaussian process instead
employs process composition (Lawrence & Moore, 2007; Damianou et al., 2011; Lázaro-Gredilla, 2012; Damianou & Lawrence, 2013; Hensman & Lawrence, 2014), source: https://arxiv.org/abs/1511.06455


-----------------------------------------------------------------------------
**Longer notes**

- Depending on kernel function, GP Regression is equivalent to: 

**Linear Regression**, 

**Polynomial Regression**, 

**Splines**,

**Kalman Filters**,

**Generalized Additive Models**. 

We can use gradients of model evidence to learn which model best explains the data; no need for cross-validation!!!

source: https://www.cs.toronto.edu/~duvenaud/papers/uw_additive_gp_slides.pdf

- Useful properties of Gaussian processes, source: https://www.cs.toronto.edu/~duvenaud/thesis.pdf

**Analytic inference**. Given a kernel function and some observations, the predictive posterior distribution can be computed exactly in closed form. This is a rare property for nonparametric models to have.

**Expressivity**. Through the choice of covariance function, we can express a wide range of modeling assumptions

**Model selection**. A side benefit of being able to integrate over all hypotheses is that we can compute the marginal likelihood of the data given a model. This gives us a principled way of comparing different models.

**Closed-form predictive distribution**. The predictive distribution of a GP at a set of test points is simply a multivariate Gaussian distribution. This means that GPs can easily be composed with other models or decision procedures.

**Easy to analyze**. It may seem unsatisfying to restrict ourselves to a limited model class, as opposed to trying to do inference in the set of all computable functions. However, simple models can be used as well-understood building blocks 
for constructing more interesting models.

- Limitations of Gaussian processes, source: https://www.cs.toronto.edu/~duvenaud/thesis.pdf

**Slow inference**. This problem can be addressed by approximate inference schemes, though.

**Light tails of the predictive distribution**. The predictive distribution of a standard GP model is Gaussian. We may sometimes with to use non-Gaussian predictive likelihoods, for example in order to be robust to outliers, or to perform classification. Using non-Gaussian likelihoods requires approximate inference. Fortunately, mature software packages exist (Hensman et al., 2014b; Rasmussen and Nickisch, 2010; Vanhatalo et al., 2013) which can automatically perform approximate inference for a wide variety of non-Gaussian likelihoods, and also implement sparse approximations.

**The need to choose a kernel**. The flexibility of GP models raises the question of which kernel to use for a given problem. Choosing a useful kernel is equivalent to learning a useful representation of the input.
