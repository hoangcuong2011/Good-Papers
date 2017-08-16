- Kernel Interpolation for Scalable Structured Gaussian Processes (KISS-GP) - http://proceedings.mlr.press/v37/wilson15.pdf


A very interesting yet challenging paper to read. GPs are limited to its computational complexity (O(N^3)). Common techniques
that address the difficulty are inducing point methods. Yet it is far to say these methods totally ease the challenge, to say the least.
Previous work only brings the complexity down to only (O(NM^2)). It is still practically too much, and also very importantly, 
increasing the number of pseudo inputs (M) significantly improves the performance.

Meanwhile, structure exploiting approaches such as Kronecker and Toeplitz methods have orthognal advantages to inducing point methods.

The problem is Kronecker methods require that inputs are on a multidimensional lattice, which makes them inapplicable to most datasets. Toeplitz methods are similarly restrictive,
requiring that the data are on regularly spaced 1D grid.

The paper takes advantages of both different approaches in a very smart way: They propose an inducing point method
that learns pseudo inputs with a specific constraint: they are on a multidimensoinal lattice. Sound trivial idea to implement, right? Actually 
it is not at all. Let me explain in detail how they implement the idea.

First, recall that inducing point methods use an alternative kernel:

  K_{x, U} K_{U, U}^-1 K_{U, x}

for a set of m inducing points (a.k.a. pseudo inputs) U. The inversion of K_{U, U} takes O(m^3) which is very expensive. 

But if we assume inducing points are multidimensional inputs on a Cartesian grid, the inversion can be performed easily. But one thing I don't get
from the paper is how to put that grid constraist to the selection of pseudo inputs, though. Remember that such a selection
is performed automatically through maximizing marginal likelihood, but doing so with having such a constraint is not
straightforward to me.

The another problem now is to try to ease the dominant O(m^2n) computations that are associated with K_{x, U}. The key idea is to perform approximation: let us assume we need to estimate k(x_i, u_j), we then find two pseudo points in U (let's say u_a and u_b) that are closest to x_i. We
can then form:

  k(x_i, uj) = w_i k(u_a, u_j) + (1-w_i) k(u_b, u_j)

In this end, we form K_{x, U} = W K_{U, U}

Here, W is a very sparse n * m matrix. I am not so sure how to create such a matrix, though. It is pretty unclear in the paper. I guess for every point x_j, it took us O(log m) to determine two relevant pseudo inputs u_a and u_b. Hence creating
such a matrix costs O(n log m)???

It is, still not so clear to me how it costs O(n+m^2) computations and storage, though.


------- to be continued ----------------------
