- Exponentiated Gradient (EG) (see this paper: https://users.soe.ucsc.edu/~manfred/pubs/J36.pdf)

Recently I am quite interested in Exponentiated Gradient (EG). Here is what I have learned:

- Learning model parameters without any constraints is a well-study, and (stochastic) Gradient Descent is a popular choice.

- The problem becomes complicate when we are given some additional constraints. One of the most common constraints is the simplex constrain (i.e. the sum of all weights is to 1).
In this case, Exponentiated Gradient comes into place to help. So it is basically that: "EG algorithms are gradient-based methods that
maintain simplex constraints" (see http://www.cs.columbia.edu/~mcollins/papers/ibm2convex.pdf)

- The modification regarding to EG compared to GD is rather simple:
Let us assume we have to learn a vector w. At iteration t+1, 

    w_{t+1} = w_t + learning_rate * gradient respect to w at time t
Meanwhile we rather use a new update For EG:

    w_{t+1, i} = w_{t, i}r_{t, i}/Normalization Constant
where

    r_{t, i} = exponential (learning rate * gradient respect to w_i at time t)
As we can see, the weights of the EG algorithm are positive and sum to 1

- "In spite of the non-differentiability of the objective function, subgradient methods still have strong convergence guarantees when combined with EG updates (e.g., the convergence proofs in (Beck and Teboulle, 2003) go through with minor modifications; see also
(Bertsekas, 1999))." (see http://www.cs.columbia.edu/~mcollins/papers/ibm2convex.pdf)


- The algorithm has solid theoretical underpinnings! But these things are really hard to follow though (see http://hunch.net/?p=286#comments)
