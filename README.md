# Some good papers I like

*Papers with detailed notes*

- Variational Inference with Normalizing Flows: https://arxiv.org/abs/1505.05770
- MADE: Masked Autoencoder for Distribution Estimation: https://arxiv.org/abs/1502.03509
- Improving Variational Inference with Inverse Autoregressive Flow: https://arxiv.org/abs/1606.04934
- Density estimation using Real NVP: https://arxiv.org/abs/1605.08803
- Wasserstein GAN: https://arxiv.org/abs/1701.07875 
- ImageNet Classification with Deep Convolutional Neural Networks https://papers.nips.cc/paper/4824-imagenet-classification-with-deep-convolutional-neural-networks:
- Fully Convolutional Networks for Image Segmentation: https://people.eecs.berkeley.edu/~jonlong/long_shelhamer_fcn.pdf
- Convolutional Sequence to Sequence Learning - https://arxiv.org/pdf/1705.03122.pdf
- WaveNet: A Generative Model for Raw Audio - https://arxiv.org/abs/1609.03499
- A Deep Reinforced Model for Abstractive Summarization - https://arxiv.org/pdf/1705.04304.pdf
- Attention Is All You Need - https://arxiv.org/abs/1706.03762
- Depthwise Separable Convolutions for Neural Machine Translation - https://arxiv.org/abs/1706.03059
- Outrageously Large Neural Networks: The Sparsely-Gated Mixture-of-Experts Layer - https://openreview.net/pdf?id=B1ckMDqlg
- One Model To Learn Them All - https://arxiv.org/abs/1706.05137
- Incorporating Copying Mechanism in Sequence-to-Sequence Learning - http://www.aclweb.org/anthology/P16-1154


*Papers with quick notes* 
- *Bagging by Design (on the Suboptimality of Bagging)* - https://www.aaai.org/ocs/index.php/AAAI/AAAI14/paper/view/8406 - Take-home message: a nice study, proposing a provably optimal subsampling *design-bagging* method. The proposed one outperforms the original bagging method convincingly (both theoretical and experimental aspects).
- *On Multiplicative Integration with Recurrent Neural Networks* - https://arxiv.org/abs/1606.06630 - Take-home message: we can modify the additive integration with multiplicative integration in RNN. The goal is to make transition (i.e. gradient state over state) tighter to inputs.
- *Importance weighted autoencoders* - https://arxiv.org/abs/1509.00519 - Take-home message: A nice paper, showing that training with weighted sample always better (a clear explanatio from the paper). Also, one can tighten the bound simply by drawing more samples in the Monte Carlo objective.
- *Adversarial Autoencoders* - https://arxiv.org/abs/1511.05644 - Take-home message: Instead of using KL divergence as in Variational autoencoders, we should rather optimize JS divergence. This makes sense as JS could better than KL in inference.
- *On Large-Batch Training for Deep Learning: Generalization Gap and Sharp Minima* - https://arxiv.org/abs/1609.04836 Take-home message: Very good paper, explaing why SGD with small-batch size is so useful: an optimizer should aim for flat minima (maxima) instead of sharp minima(maxima). Small batch size helps achieve this because there is lots of noisy gradients in training.
- *Deep Exponential Families: https://arxiv.org/abs/1411.2581* - Take-home message: Stacking multiple exponential models (up to 3 layers) can improve the performance. Inference is much harder, though. I personally like this work a lot!
- *Semi-Supervised Learning with Deep Generative Models* - https://arxiv.org/abs/1406.5298 - Take-home message: a classic on semi-supervised learning with deep generative models, using stochastic variational inference for training. The model may not work as well as ladder networks, yet it is classic and has broad applications.
- *Exponential Family Embeddings* - https://arxiv.org/abs/1608.00778 - Take-home message: A very cool work, showing how to
generalize word2vec to other very interesting models (e.g. items in a bucket). Also, instead of using exp as in the original model, the paper shows other possibilities including posson, gaussian, bernoulil. I personally like this work a lot!
- *Hierarchical Variational Models* - https://arxiv.org/abs/1511.02386 - Take-home message: Showing how to increase the richness of q function by using a hierarchical model with global paramter. The model itself is equivalent to Auxiliary Deep Generative Models (https://arxiv.org/abs/1602.05473)
- *The Marginal Value of Adaptive Gradient Methods in Machine Learning* - https://arxiv.org/abs/1705.08292 - Take home message: Adagrad/Adam and other adaptive methods are awesome, but if we tune SGD properly, we could do *much* better.
- *Markov Chain Monte Carlo and Variational Inference: Bridging the Gap* - https://arxiv.org/abs/1410.6460 - Take-home message: The paper proposes a very nice idea how to improve MCMC using variational inference (by exploiting the likelihood to see whether the chain converges and to estimate the parameter for tuning MCMC). Meanwhile it also can help variational inference using MCMC, but how? This is the point I don't really quite get!
- *Categorical Variational Autoencoders using Gumbel-Softmax* - https://arxiv.org/abs/1611.01144 - Take-home message: How to convert discrite variable into an approximate form that fits into reparameterization tricks (using Gumbel-Softmax function).
- *Context Gates for Neural Machine Translation* - https://arxiv.org/abs/1608.06043 - Take-home message: The paper shows that in seq2seq we should control how a word is generated. A content word should generated based on inputs, while a 
common word should be generated based on the context of target words. The paper proposes a gate network that integrate the information into seq2seq in a nice way.
