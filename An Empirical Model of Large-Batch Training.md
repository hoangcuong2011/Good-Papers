An Empirical Model of Large-Batch Training https://arxiv.org/pdf/1812.06162.pdf


When the batch size is very small, the approximation will have very high variance, and the resulting gradient
update will be mostly noise. Applying a bunch of these SGD updates successively will average out the
variance and push us overall in the right direction, but the individual updates to the parameters won’t be very
helpful, and we could have done almost as well by aggregating these updates in parallel and applying them
all at once (in other words, by using a larger batch size). For an illustrative comparison between large and
small batch training, see Figure 2.




By contrast, when the batch size is very large, the batch gradient will almost exactly match the true gradient,
and correspondingly two randomly sampled batches will have almost the same gradient. As a result, doubling
the batch size will barely improve the update – we will use twice as much computation for little gain.



These results show that at fixed values of the loss, the noise scale
does not depend significantly on model size.





https://www.reddit.com/r/MachineLearning/comments/8e9x8g/r_180407612_revisiting_small_batch_training_for/

