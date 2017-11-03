- Black Box Variational Inference  - https://arxiv.org/pdf/1401.0118.pdf

This is a very important paper in Variational Inference. We all know how useful VI is: it is scalable to big data, even though
there is a trade off with accuracy. But thing pulls us back is how tedious it is to derive VI. It is very difficult to do so, and also
it is very time-consuming/model-specific.

Black box Variational Inference (BBVI) solves the problem in an elegant way. Recall that minimizing KL-divergece between the true posterior distribution
and the approximate distribution is equavalant to maximizing ELBO. In BBVI, parameters are learned directly by maximizing ELBO.
This seems impossible, but in fact it is. We indeed can compute noisy unbiased gradients of the ELBO with Monte Carlo samples 
from the variational distribution (Equation 3). Equation 3 does not come intuitively. The proof in the extra materials provide in details
how we can come up with Eq. 3

While Eq. 3 reveals a door to optimize ELBO much easier. The optimization only requires computing gradients of the variational approximating family. However, there is still a difficulty with sampling. MC gives us very high variance
that is "too large too be useful". The authors propose two ways to reduce the problem, with Rao-Blackwellization and smart Control Variates.
I am aware of those techniques, but not really in-depth though!

While the work is very nice, a problem with BBVI is that the variance in sampling still very high! (See this https://arxiv.org/pdf/1603.00788.pdf) How to address this challenge? Reparameterization and amortization come to rescue! 
(See this tutorial from David Blei https://www.youtube.com/watch?v=Dv86zdWjJKQ)


Some notes:
- A very good introduction to BBVI: http://keyonvafa.com/logistic-regression-bbvi/
