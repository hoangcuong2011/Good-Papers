- *Probabilistic Matrix Factorization* (https://www.cs.toronto.edu/~amnih/papers/pmf.pdf)


A classic paper on collaborate filtering, which aims to infer user preferences for items, 
given a very large yet incomplete collection of user preferences.

The task involves with very large datasets (e.g. Netflix), and there are a lot of infrequent users in the data.
This makes it difficult. The authors propose a solution that is basically a probabilistic extension of SVD, and
can reduce to SVD in the limit of prior variances going to infinity.

To understand the paper, recall the matrix factorization from the non-probabilistic view. To predict the rating given by user
i to move j, we simply compute the dot product between the corresponding features vectors:

R_{ij} = sum_{k} U_{ik}V_{jk}
for all possible latent factors k. We learned both of matrices by minimizing squared error.

Here, probabilistic matrix factorization is a simple probabilistic linear model with Gaussian observation noise. Specifically,

P(R_{ij}| U_i, V_j, delta^2) = N(R_{ij}|U_i, V_j, delta^2)

Here, the user and movie feature vectors are given zero-mean spherical Gaussian priors as well:

P(U| sigma_{U}^2) = prod_{i=1}^{N}N(U_i| 0, delta_U^2I)

P(V| sigma_{V}^2) = prod_{i=1}^{N}N(V_i| 0, delta_V^2I)

The model is learned with MAP learning with fixed hyperparameters. This is equivalent to minimizing sum-of-squared-errors with
quadratic regularization terms, where the ratio delta^2/delta_U^2 and delta^2/delta_V^2 is fixed. Find a local minimum by performing gradient descent in
U and V .

It is however not easy to learn suitable ratios. One simple way is to perform grid searching. This is, however, very expensive.
The way the authors address the problem is to introduce priors for the hyperparameters and maximize the log-posterior of the
model over both parameters and hyperparameters. This seems like very important.

The last thing we need to take care is that there are a lot of infrequent users. The authors reduce the problem
by introducing a latent similarity constraint matrix that shared between all users. The idea makes sense to me, even though I don't know
how they end up with Eq 7 (i.e. it is a bit ad hoc to me).

Overall I really like the paper, and, it is ver nice to know that a nice technique (probabilistic matrix factorization) can address
a very practical problem (collaborating filtering).
