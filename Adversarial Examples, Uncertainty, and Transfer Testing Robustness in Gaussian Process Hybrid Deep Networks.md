- **Adversarial Examples, Uncertainty, and Transfer Testing Robustness in Gaussian Process Hybrid Deep Networks** - https://arxiv.org/pdf/1707.02476.pdf

Deep neural networks do not capture their own uncertainties. GPs can improve DNNs regarding to this aspect. 
GPs are powerful models by themselves. The problem with them is that simple kernels such as the RBF
kernel, are not expressive enough (this is not surprisingly as there are only two types of parameters for a normal kernel functions).
DNNs can help GPs regarding to this aspect.

The general idea is to put GPs at the top of a DNN. This paper thoroughly investigates
how good such an architecture is. Here is the result:

- **Classification**

*MNIST*: putting GPs on top of a DNN is very helpful, especially when we have small datasets to train.

*CIFAIR-10*: putting GPs on top of a DNN is not that helpful, quite disappointed with this.

- **Robustness to adversiarial examples**

It seems doing so quite helpful.

- **Domain Adaptation**

I like the experiments: they train different models on MNIST, and test on completely different datasets.
Unfortunately, it seems like doing so does not help improve DA. The remarkably thing is that the log likelihood of the DNN-GP model is close to log (0.1) (a uniform predictor on a ten classs problem) for hard cases, while a DNN cannot provide this thing. I found this interesting but I need more time to digest this.

Overall I think this is a nice work to know, even though I have several questions:

- It is not clear to me how the model can be trained end-to-end? I am gonna digging in this.
- It is still not clear to me it should be a must to put GPs on top of a DNN (I need more time to think about this carefully). Meanwhile it is pretty clear that DNN really helps GPs.






