- Sparse Gaussian Processes using Pseudo-inputs - https://papers.nips.cc/paper/2857-sparse-gaussian-processes-using-pseudo-inputs

Gaussian Processes is a very interesting/beautiful model (see this https://github.com/hoangcuong2011/Good-Papers/blob/master/Gaussian%20Process.md).
A problem with GPs is that it requires a complexity of O(N^3) to train. This paper proposes a new solution that has only O(M^2N) training cost. How? I found the idea is very smart, and to understand it let us first reexamine the way we made prediction with GPs.

For simplicity, let us assume a noise-free GP model that is trained on a data set of N input vectors X with dimension D and corresponding real valued target vector Y, i.e. our underlying latent function f can be sampled from the following distribution:

    f sample from N(zero-mean vector, cov matrix K with size N)

During training, we only need to find a *small* number of hyperparameters that control the smootheness of the Gaussian distribution. Let us assume we are using ARD kernel function with two types of parameters:

    K(x_n, x_{n'}) = c exp[ -.5 * sum_{d=1}^{D} b_d (x_n^d - x_{n'}^d)^2 ]

Here we have D+1 parameters: c and D b_ds.

During test time, we can made predict to a new data point x* by sampling a value from the following distribution:

    y* sample from N(u*, SIGMA*), where

    u* = K(x*,X)^T K(X,X)^-1 Y

    SIGMA* = K(x*, x*) - K(x*, X)K(X, X)^-1 K(X, x*)^T
    
Two things are important here. First, during training we may select a small subset to learn model parameters, I guess.
But during test time, it is more complicate: we need to compute the inversion of the covariance matrix K(X, X)^-1. Once the inversion is computed, prediction is O(N^2) for both the ppredictive mean and predictive variance per new test point.

The way the authors fix the problem is quite elegant: we first find a very small subset XX, YY with size M of training data that represents all the training data: i.e., we assume each training data point is sampled from the following distribution

    y sample from N(u, SIGMA), where

    u = K(x,XX)^T K(XX,XX)^-1 YY

    SIGMA = K(x, x) - K(x, XX)K(XX, XX)^-1 K(XX, x)^T

If we find a subset that explains the real data well, we can drastically decrease training cost: the inversion of the convariance matrix takes
only O(M^3).  Once the inversion is computed, prediction is O(NM^2) for predictive mean, but still O(N^2M) for predictive variance (NN * NM * MM * MN -> O(N^2M)). The way the authors circumvent this difficulty is to assume the training data is generated independently. This means that our SIGMA matrix is diagonal. There are only N elements in the predictive variance we need to compute, and the complexity is thus N (11 * 1M * MM * M1) = NM^2. It is very smart to do so, even though I believe 
it hurts the accuracy.

