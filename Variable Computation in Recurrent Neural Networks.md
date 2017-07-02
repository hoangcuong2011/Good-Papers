- Variable Computation in Recurrent Neural Networks - https://arxiv.org/abs/1611.06188

The paper addresses on an interesting problem that I never thought about it before. Consider sequential data such as audio. There are time
periods where we don't hear anything (i.e. silence). Consider another case such as video. There are time periods where
we don't see much changes (i.e. You especially see this in Indian movies.haha).  It is natural to come up a question: how to create a model that do much less
computation in those cases? 

Recall that in RNN, the bulk of computation comes from matrix multiplications:
h_t = tanh(U h_t{-1} + V x_t) (1)

with D-dimensional matrices U and V.

The key idea is to have an additional network with less number of parameters:
m_t = tanh(u h_t{-1} + v x_t) (2)

Here, u and v are D-dimensional vectors. The network output gives us a real number representing a computation budget m_t.
In the end, we need to perform a *partial* update of the first [m_t D] dimensions of its hidden state in Equation (1). The idea
is quite straightforward, I think!

However, 
this way the model require making a hard choice of number of diemnsions to be updated, making the model non-differentiable. In the paper the authors
approximate the hard choice by using a gate function to apply a soft mask. Even with that training (with backprop) is still
difficult, and the work exploits other tricks to improve training.

In general, I like the paper. I believe the idea is novel. Even the improvement is not that significant as in other work (e.g. https://github.com/hoangcuong2011/Good-Papers/blob/master/Outrageously%20Large%20Neural%20Networks:%20The%20Sparsely-Gated%20Mixture-of-Experts%20Layer.md)
This paper provides another way to increase network size while keeping the same budget of computation cost.
