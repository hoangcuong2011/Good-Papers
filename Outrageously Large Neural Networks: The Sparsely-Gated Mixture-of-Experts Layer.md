- Outrageously Large Neural Networks: The Sparsely-Gated Mixture-of-Experts Layer - https://openreview.net/pdf?id=B1ckMDqlg

A very interesting paper to read. Giving sufficiently large datasets, large-scale NNs with larger number of parameters NNs can provide
better performance (see this greate video by Andrew Ng https://www.youtube.com/watch?v=LcfLo7YP8O4). It is, however, very
expensive to scale the size of neural nets, even with Google.

A simple and elegant idea to address the problem is to apply A Mixture of Experts (MoE). 
Here the experts can be simply feed-forward (sub)-networks, but can be more complex NNs. 
Having thousands of experts demands a massive amount computational resources. 
However, using a gate network that decides only a few of the experts active on a per-example basis can solve the problem
(Sparsely-Gated Network). This idea, surprisingly, is very challenging to implement.
There are several difficulties in the implementation:

1. The shrinking batch problem: let us assume we are given a batch of a specific number, let say, n, examples to train
the network. Let us assume our gating network chooses k among K experts, then each expert receives only a batch of k/K*n, which is pretty small.
Increasing the batch size is difficult, due to limited memory.
2. The network bandwidth: I don't really get how hard it is, though.
3. Balancing expert utilization: This is very difficult. A few experts may get all the credits while the rest are useless.

The paper addresses all these major technical challenges. Experiments show that SOTA models, once
integrated with the gate network can beat SOTA results with significantly less computation.

I think this is an important paper, and it is very pleased to read it. Also, I believe 
having the Sparsely-Gated Mixture-of-Experts Layer will be a must in SOTA NN systems.

As a side note, it is quite hard to figure out how to train the gate network with backpropagation. I thought using
top-K gating implying an argmax operator, which is therefore not possible to apply backprop? 
Also I believe implementing the model requires very high engineering skills.
