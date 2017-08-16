- *Additive Gaussian Processes* - http://hannes.nickisch.org/papers/conferences/duvenaud11gpadditive.pdf

A simple and interesting paper to read. GPs are powerful, but the expressiveness of the model heavily depends on kernel functions.
The most common kernel function is squared-exponential kernel. This kernel is powerful in the sense that it is the multivariate squared-exponential kernel:

    k(x, x') = sigma^2 \prod_{i=1}^{D}k(x_i, x'_i)
             = sigma^2 exp (-\sum_{1}^{D} 1/{2l_d^2} (x_d - x'_d)^2)

Here, D represents the total number of dimensions.

The problem with a GP model with this kernel function is that:
The interaction between all dimensions, though important, is difficult to generalize. I don't really get this, though.
Even more importantly, the interacton is not expressive enough because sometimes, we mainly care about other simpler
interactions such as:

    k_1(x, x') = sigma_1^2 \sum_1^{D}k(x_i, x_i') (this is basically GAM)
    k_2(x, x') = sigma_2^2 \sum_{i=1}^{D}\sum_{j=i+1}^{D}k_i(x_i, x'_i)k_{j}(x_j, x'_j)

and so on.
Finally, the models based on the kernel function may be susceptible to the curse of dimensionality. This is because the kernel with locality cannot capture non-local structure.
I don't get this point, though.

This paper suggests that a GP model should have a combination of all of these interactions. Two things may come to your mind
in the first place:

1. How to learn sigma? Fortunately, it is possible to learn them automatically by maximizing marginal likelihood of training data.
Of course overfitting might happen and experiments reveal this is indeed the case.

2. How to compute a combination of all of these interactions efficiently? The authors show that it is possible to use Newton-Girard formulae
to do so, with time complexity of O(D^2).

Experiments do not show the additive GP are significantlly better than the standard Squared-exponential kernel GP, though. But I think
the approach is still very promising in the sense that it helps do better for harder problems.

Overall, it is a very nice work to read, even though there are several important claims I don't really understand thoroughlly (minor notes: the paper is a bit oversold ...)
