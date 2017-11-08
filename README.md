# Some good papers I like
**Basic Background**
- Gradient regarding to algebra (TODO list)
- Gaussian CheatSheet
- Kronecker-Factored Approximations (TODO list)
- Asynchronous stochastic gradient descent

**Topics with detailed notes**
- *Expectation Propagation*
- *Gaussian processes*
- *Gaussian Processes with Notes*


**Papers with detailed notes**

- *Six Challenges for Neural Machine Translation*: http://www.aclweb.org/anthology/W/W17/W17-3204.pdf
- *Learning to Generate Reviews and Discovering Sentiment*: https://arxiv.org/pdf/1704.01444.pdf
- *Black Box Variational Inference*: https://arxiv.org/pdf/1401.0118.pdf
- Stochastic Variational Deep Kernel Learning (i.e. *Deep Kernel Learning for Multi-task Classification*) - https://arxiv.org/pdf/1611.00336.pdf
- *The Human Kernel* - http://papers.nips.cc/paper/5765-the-human-kernel
- *Additive Gaussian Processes* - http://hannes.nickisch.org/papers/conferences/duvenaud11gpadditive.pdf
- *Kernel Interpolation for Scalable Structured Gaussian Processes (KISS-GP)* - http://proceedings.mlr.press/v37/wilson15.pdf
- *Gaussian Process Kernels for Pattern Discovery and Extrapolation* - https://arxiv.org/abs/1302.4245
- *Adversarial Examples, Uncertainty, and Transfer Testing Robustness in Gaussian Process Hybrid Deep Networks* - https://arxiv.org/pdf/1707.02476.pdf
- *Gaussian Processes for Classification* - Chapter 3 of the book Gaussian Processes for Machine Learning http://www.gaussianprocess.org/gpml/chapters/RW3.pdf
- *Sparse Gaussian Processes using Pseudo-inputs* - https://papers.nips.cc/paper/2857-sparse-gaussian-processes-using-pseudo-inputs
- *Multi-task Sequence to Sequence Learning* - https://arxiv.org/abs/1511.06114
- *Zero-Resource Translation with Multi-Lingual Neural Machine Translation* - https://arxiv.org/pdf/1606.04164.pdf
- *Multi-way, Multilingual neural machine translation with a shared attention mechanism* - http://www.aclweb.org/anthology/N16-1101
- *Differentiated Softmax* - http://www.aclweb.org/anthology/P16-1186
- *Noise-contrastive estimation:  A new estimation principle for
unnormalized statistical models* http://proceedings.mlr.press/v9/gutmann10a/gutmann10a.pdf
- *Hierarchical Probabilistic Neural Network Language Model* - http://www.iro.umontreal.ca/~lisa/pointeurs/hierarchical-nnlm-aistats05.pdf
- *Variational Inference with Normalizing Flows*: https://arxiv.org/abs/1505.05770
- *MADE: Masked Autoencoder for Distribution Estimation*: https://arxiv.org/abs/1502.03509
- *Improving Variational Inference with Inverse Autoregressive Flow*: https://arxiv.org/abs/1606.04934
- *Density estimation using Real NVP*: https://arxiv.org/abs/1605.08803
- *Wasserstein GAN*: https://arxiv.org/abs/1701.07875 
- *ImageNet Classification with Deep Convolutional Neural Networks*: https://papers.nips.cc/paper/4824-imagenet-classification-with-deep-convolutional-neural-networks:
- *Fully Convolutional Networks for Image Segmentation*: https://people.eecs.berkeley.edu/~jonlong/long_shelhamer_fcn.pdf
- *Convolutional Sequence to Sequence Learning*: https://arxiv.org/pdf/1705.03122.pdf
- *WaveNet: A Generative Model for Raw Audio*: https://arxiv.org/abs/1609.03499
- *A Deep Reinforced Model for Abstractive Summarization*: https://arxiv.org/pdf/1705.04304.pdf
- *Attention Is All You Need*: https://arxiv.org/abs/1706.03762
- *Depthwise Separable Convolutions for Neural Machine Translation*: https://arxiv.org/abs/1706.03059
- *Outrageously Large Neural Networks: The Sparsely-Gated Mixture-of-Experts Layer*: https://openreview.net/pdf?id=B1ckMDqlg
- *One Model To Learn Them All*: https://arxiv.org/abs/1706.05137
- *Incorporating Copying Mechanism in Sequence-to-Sequence Learning*: http://www.aclweb.org/anthology/P16-1154
- *SoundNet - Learning Representations from Unlabeled Video*: https://arxiv.org/abs/1610.09001
- *Improving Neural Language Models with a Continuous Cache*: https://openreview.net/pdf?id=B184E5qee
- *A Clockwork RNN*: http://proceedings.mlr.press/v32/koutnik14.pdf
- *Variable Computation in Recurrent Neural Networks*: https://arxiv.org/abs/1611.06188
- *Probabilistic Matrix Factorization*: https://www.cs.toronto.edu/~amnih/papers/pmf.pdf



**Papers with quick notes**

- *The Variational Gaussian Process* (https://arxiv.org/abs/1511.06499) - I don't think I fully understand the idea of using GPs in Variational Inference. But the paper really gives me a better understanding of the general picture of Variational Inference with hierarchical latent variables. That is, having a variational distribution that is also a hierarchical Bayesian model is very difficult to train, and the paper provides a cutting edge method to do so. I recommend readers to take a look at these slides (http://mlg.postech.ac.kr/~readinglist/slides/20160822.pdf). I personally learn a lot from it.
- *Natural Gradient*  (http://andymiller.github.io/2016/10/02/natural_gradient_bbvi.html): I heard about Natural gradient concept for a while, but I never really captured it until this paper. It is a very beautiful idea and I encourage people to take a look at this tutorial to have a better understanding of the concept!
- *Progressive growing of GANs for improved quality, stability and variation* (http://research.nvidia.com/sites/default/files/pubs/2017-10_Progressive-Growing-of/karras2017gan-paper.pdf)
The paper shows how to improve GANs with a better training scheme. Recall the main problem with GAN is it is very difficult to train: the gradients tend to be useless if the training and generated distributions do not have substantial overlap (i.e. too easy to tell apart). Among various tweaks they did to address this problem, the most important one is to gradually improve the size of both generator and discriminator networks. Starting from a low resolution, the authors add new layers that model increasingly more fine-grained details as training progresses. I am not really familiar with GANs in practice, but resulting images the improve model produces is really impressive. Those are perhaps the best ones to date.

- *Multi-Task Bayesian Optimization* (https://papers.nips.cc/paper/5086-multi-task-bayesian-optimization.pdf) - Another classic paper. The authors investigate how to transfer the knowledge gained from previous optimizations to a new and related task. This turns out pretty straightforward to do so under Multi-task GPs. They also investigate how to perform Bayesian optimization using knowledge gained from related yet easier to optimize tasks. This idea makes sense to me and it is not surprising to see how useful it is in their topic modeling case study. I was, however, not so clear about the part of optimizing an average function over multiple tasks.

- *Practical Bayesian Optimization of Machine Learning Algorithms* (https://arxiv.org/pdf/1206.2944.pdf) - A very very good paper. I was aware of this work but I couldn't manage  to take a look at it (well it is not easy to follow if we don't have sufficient background). Basically given a set of hyperparameters, the paper tries to address the search in a better way: Instead of trying all possible values as in exhaustive grid search, they deploy a proxy-optimization search that helps us look for promising points. The results are very promising, as the model is able to learn good hyperparameters much quicker than using exhaustive grid search. I strongly recommend to take a look at this paper to have a taste of how GPs can be used to solve a really difficult problem of hyperparameters optimization.

- *Deep Neural Networks as Gaussian Processes* (https://arxiv.org/abs/1711.00165) - It has been long known how a GP corresponds to a neural network with *single* hidden layer. Yet it is not clear how it is with *deep* neural networks. This work delineates the correspondence between *deep* neural networks and Gaussian Processes. Specificially, the work provides an equation of covariance matrix that corresponds to each non-linear function used in deep neural networks. For RELU, it is easy to compute the equivalent covariance matrix, but for other certain non-linear functions, it seems like it is not trivial to do so. They provide an algorithm to compute covariance matrix, which is quite difficult to follow. Bayesian inference also helps the model learn where it gives good prediction and where it does not. Figure 2 is really impressive/interesting to me.
Overall I think the paper is very interesting/important.

- *What Uncertainties Do We Need in Bayesian Deep Learning for Computer Vision?* The paper studies the benefits of modeling uncertainty in Bayesian deep learning models for vision tasks. They define two types of uncertainty: aleatoric uncertainty that captures noise inherent and epistemic uncertaint which accounts for uncertainty in the model. They propose a BNN models that captures all these things, and show how this helps visition tasks. Some of the techniques are too involved too me, but overall I enjoyed reading the paper.

- *Dropout as a Bayesian Approximation: Representing Model Uncertainty in Deep Learning* (https://arxiv.org/abs/1506.02142): Take-home message: This paper is quite thought-provoking. It reveals the connection between dropout training as performing approximate Bayesian learning in a deep Gaussian Processes model. It also suggests a way to get model uncertainty (MCDropout), which is important in practice. This is because predictive mean and predictive uncertainty should provide more stable performance especially when the model is run on the wild (i.e. the test data is compleletely different to the training data). The mathematics is really involved though.

- *Hogwild: A Lock-Free Approach to Parallelizing Stochastic Gradient Descent* (http://machinelearning.wustl.edu/mlpapers/paper_files/NIPS2011_0485.pdf): Take-home message: The paper ignites the trend in using asynchronous SGD instead of synchronous SGD. Assuming we are performing updates over very sparse parameters, we can perform asynchronous SGD without any needs of locking mechanism regarding to synchronizing model parameters. The mathematical proofs for the result are difficult to understand though. As a side note, the method does not fit to training NNs because NN model parameters are not that sparse.
- *Deep Kernel Learning* (https://arxiv.org/abs/1511.02222) and *Stochastic Variational Deep Kernel Learning* (http://papers.nips.cc/paper/6425-stochastic-variational-deep-kernel-learning) and *Learning Scalable Deep Kernels with Recurrent Structure* (https://arxiv.org/abs/1610.08936) - Take-home message: The studies contribute a hybridge architecture between GPs and (Deep) Neural Networks. The combination makes sense, and experiment results show promising results. Training the model is end-to-end and scalable (The scalability is mainly due previous work of Andrew Wilson et. al., though, not in those studies per say). I found the research line very inspiring. Yet the papers are really technical to follow.
- *Assessing Approximations for Gaussian Process Classification* (http://papers.nips.cc/paper/2903-assessing-approximations-for-gaussian-process-classification.pdf) and its longer version *Assessing Approximate Inference for
Binary Gaussian Process Classification* (http://www.jmlr.org/papers/volume6/kuss05a/kuss05a.pdf) - Take-home message: GP classification models are intractable to train. There are three main choices to ease the intractability: using Laplace's method, Expectation Propagation and MCMC. MCMC works best but it is too expensive. Laplace's method is simple but the paper suggests that it is *very* inaccurate. EP works surprisingly well.
- *Sequential Inference for Deep Gaussian Process* (http://www2.ift.ulaval.ca/~chaib/publications/Yali-AISTAS16.pdf) and Training and Inference for Deep Gaussian Processes (Undergrad thesis - http://keyonvafa.com/deep-gaussian-processes/) - Take-home message: Deep GPs are powerful models, yet difficult to train/inference due to computation intractability. The papers address the problem by using sampling mechanisms. The techniques are very straightforward. The first paper totally eases computational cost by using an active set instead of the full dataset. The size of active set has a quite significant impact to the performance, though. As a side note, the performance really depends on parameter initialization (The second paper). The first paper really shows the benefits of having deep GP models, even though a deep GP model does not work well with MNIST classification (the accuracy is quite low, around 94%-95%). The first paper is really good and deserves more attention.
- *Efficient softmax approximation for GPUs* - https://arxiv.org/abs/1609.04309 - Take-home message: Providing a systematic comparison between various methods for speeding up training NLMs with large vocabulary. The paper also proposes an one that pretty fits to GPUs. Their method is very technical to follow, though. The proposed one works best. Meanwhile, their modification to Differentiated Softmax works pretty well. But it is totally unclear to me how they modify D-Softmax.
- *Strategies for Training Large Vocabulary Neural Language Models* - http://www.aclweb.org/anthology/P16-1186 - Take-home message: Providing a systematic comparison between various methods for speeding up training neural language models with large vocabulary. Hierarchical softmax works best for large dataset (very surprising), differentied softmax works well for small-scale dataset (but the speed up factor is not so high). NCE works very bad, and Self-normalization works OK. Good notes on the paper can be also found here https://github.com/dennybritz/deeplearning-papernotes/blob/master/notes/strategies-for-training-large-vocab-lm.md
- *See, hear, and read: deep aligned representations* - https://arxiv.org/abs/1706.00932: The paper proposes a nice *Cross-Modal Networks* to approach the challenge of learning discriminative representations shared across modalities. Given inputs as different types (image, sound, text), the model produces a *common representation* shared across modalilities. The
common representation can bring huge benefits. For instance, let us assume we have pairs of images and sound (from videos).
Let us also assume we have pairs of images and text (from caption datasets). Such a common representation can map between sound and text using images as a bridge (pretty cool!). It is however unclear from the paper how the cross-model networks are designed/implemented. Lots of technical details are missing, and it is very hard to walk through the paper.
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
