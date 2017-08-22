- Asynchronous stochastic gradient descent

Somehow I missed the very recent trend in using asynchronous SGD in model training instead of synchronous SGD. The main goal of this 
writing is simply showing several resources that I found helpful to understand asynchronous SGD.

1. http://engineering.skymind.io/distributed-deep-learning-part-1-an-introduction-to-distributed-training-of-neural-networks (Highly recommend)
A general introduction to ASGD methods in general.
2. Large Scale Distributed Deep Networks - http://www.cs.toronto.edu/~ranzato/publications/DistBeliefNIPS2012_withAppendix.pdf
A somewhat naive ASGD method.
3. HOGWILD!: A Lock-Free Approach to Parallelizing Stochastic Gradient Descent - https://arxiv.org/abs/1106.5730
A classic paper that ignites trend in using ASGD in model training.
