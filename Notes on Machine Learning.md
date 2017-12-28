Good Notes on Machine Learning in general

1. Edward = TensorFlow + Random Variables + Inference Algorithms

2. Deep neural networks: many parameters; very prone to overfitting; require large data sets

3. Optimising any neural network with dropout is equivalent to a form of approximate Bayesian inference

4. A network trained with dropout already is a Bayesian Neural Network!

5. "typical training of neural networks requires lots of labeled data to control the risk of overfitting. And the problem becomes harder when it comes to real world regression tasks. These tasks often have smaller training data to use, and the high-frequency characteristics of these data often makes neural networks easier to get trapped in overfitting." http://zhusuan.readthedocs.io/en/latest/bayesian_nn.html

6. "In BNN, the approximate distribution is usually further simplified by factorizing it into independent distributions for each weight layers (mean field approximation). This approximation creates larger bias and can be problematic in the deep neural network." https://becominghuman.ai/learning-note-dropout-in-recurrent-networks-part-1-57a9c19a2307

7. "Uncertainty in predictions: As we will see below, the Bayesian Neural Network informs us about the uncertainty in its predictions. I think uncertainty is an underappreciated concept in Machine Learning as it’s clearly important for real-world applications. But it could also be useful in training. For example, we could train the model specifically on samples it is most uncertain about" - http://docs.pymc.io/notebooks/bayesian_neural_network_advi.html

8. "Training neural networks has a general problem that the parameters can be stuck in a local minimum, which limits the model performance. Therefore, in the training process, we hope the model parameters have the ability to jump out of the local minimum area when stuck at it and search in a bigger space to find the global minimum" - http://zhusuan.readthedocs.io/en/latest/bayesian_nn.html

9. "This might seem silly for such a small expression, but one of the key ideas in Tensorflow is deferred execution: it's very cheap to build a large and complex expression, and when you want to evaluate it, the back-end (to which you connect with a Session) is able to schedule its execution more efficiently (e.g. executing independent parts in parallel and using GPUs)." - https://stackoverflow.com/questions/33633370/how-to-print-the-value-of-a-tensor-object-in-tensorflow

10. "Standard deep learning tools for regression and classification do not capture model uncertainty. In classification,
predictive probabilities obtained at the end of the pipeline (the softmax output) are often erroneously interpreted as model confidence." https://arxiv.org/pdf/1506.02142.pdf

11. "It has long been known that infinitely wide (single hidden layer) NNs with distributions placed over their weights
converge to Gaussian processes (Neal, 1995; Williams, 1997). This known relation is through a limit argument that
does not allow us to translate properties from the Gaussian process to finite NNs easily." http://proceedings.mlr.press/v48/gal16.pdf

12. "The most commonly used automatic differentiation packages in machine learning, Theano (Bastien et al., 2012), Torch (Collobert et al., 2002) and TensorFlow(Abadi et al., 2016) require learning a new syntax in which to express operations, each acting as a compiler for a restricted mini-language" https://www.cs.toronto.edu/~duvenaud/papers/blackbox.pdf

13. Typically the kl divergence also lacks a closed form. Instead we maximize the evidence lower bound
(elbo), a proxy to the kl divergence - https://www.cs.princeton.edu/~rajeshr/papers/KRGB_nips2015.pdf

14. "In machine learning, one is always trying to optimize some kind of loss function. Traditionally, this is something like cross entropy or mean squared error. Sadly though, for some use cases, this is not the loss you want your final model to be good at. Take anything in the space of image generation, for example. To demonstrate a common error case, consider a model trying to generate a sharp edge. If a model is uncertain as to where exactly this edge should be, it will try to minimize the loss function to the best of its ability, instead of making a guess like a human would do. If this loss is mean squared error (or really any loss in pixel space) the model will output a blurry line — effectively averaging among all possible predictions. This blurry prediction has a lower loss value than a sharp random guess.

This is not what we want in a generative model. Ideally, we want to fool a human looking at the image. Sadly, human decisions can’t simply be plunked into a neural network, so we need some kind of proxy — preferably one that we can take the gradient of. The idea behind adversarial training is to turn this proxy into another neural network so that you essentially have an entire neural network as a loss function. The question then becomes how to train and work with these “adversarial” neural networks."

https://indico.io/blog/iclr-2016-takeaways/

15. "Variational inference is a powerful tool for approximate posterior inference. The idea is to posit a family of distributions over the latent variables and then find the member of that family closest to the posterior. Originally developed in the 1990s (Hinton & Van Camp, 1993; Waterhouse et al.,
1996; Jordan et al., 1999), variational inference has enjoyed renewed interest around developing
scalable optimization for large datasets (Hoffman et al., 2013), deriving generic strategies for easily
fitting many models (Ranganath et al., 2014), and applying neural networks as a flexible parametric
family of approximations (Kingma & Welling, 2014; Rezende et al., 2014). This research has been
particularly successful for computing with deep Bayesian models (Neal, 1990; Ranganath et al.,
2015a), which require inference of a complex posterior distribution (Hinton et al., 2006)."
https://arxiv.org/pdf/1511.06499.pdf

16. "The neural network used in the encoder (variational distribution) does not lead to any richer approximating distribution. It is a way to amortize inference such that the number of parameters does not grow with the size of the data (an incredible feat, but not one for expressivity!) (Stuhlmüller et al., 2013)". This is better explained from the perspective of variational inference than auto-encoders. For example, suppose we have a model with latent variables that are Gaussian a priori (as in VAEs). We may choose a fully factorized Gaussian as the variational distribution, where each latent variable is rendered independent. The inference network takes data as input and outputs the local variational parameters relevant to each data point. The optimal inference network outputs the set of Gaussian parameters which maximizes the variational objective. This means a variational auto-encoder with a perfect inference network can only do as well as a fully factorized Gaussian with no inference network. - http://dustintran.com/blog/variational-auto-encoders-do-not-train-complex-generative-models

17. "I do agree with the post main points, however I find one thing usually often overlooked by people who state that having an inference network can not be more powerful than having a separate variational parameters per data point. This is true theoretically, however there is one important fact. Consider the space of all possible separate hyperparameter per data point and the space of the inference network parameters. Theoretically, this says that in the first space there is a point, for which the ELBO of the dataset is higher than any point in the second space. However, there is no mention of how easy it is to obtain this set of parameters. And that is where I think is the key. The parameter space of the NN is IMHO a much easier space for optimizing the ELBO than the original space. The reason is simple - structure and similarity. By tieing up of the parameters of the network, it imposes a smoothness on the mapping between input data and variational parameters. This means that similar inputs lead to similar variational distribution. This in terms makes the optimization much easier than in the first case, especially in the stochastic setting. Additionally, I do not believe that we as humans and people interested in AI want something to be as expressive as non-parameterics, as that lacks a lot of exploitable structure in the world." - https://www.reddit.com/r/MachineLearning/comments/4ph8cq/variational_autoencoders_do_not_train_complex/

18. "In practice, we are usually interested in predicting ratings for new user/movie pairs rather than in estimating model parameters. This view suggests taking a Bayesian approach to the problem which involves integrating out the model parameters." https://www.cs.toronto.edu/~amnih/papers/bpmf.pdf

19. Supervised learning models still outperform all unsupervised models. This may be explained because
"supervised approaches have clear objectives that can be directly optimized". Meanwhile, "unsupervised approaches rely on proxy tasks such as reconstruction, density estimation, or generation, which do not directly encourage useful
representations for specific tasks." https://arxiv.org/pdf/1704.01444.pdf

20. "We use the customary definition of domain in machine translation: a domain is defined by a corpus from a specific source, and may differ from other domains in topic, genre, style, level of formality, etc" - http://www.aclweb.org/anthology/W/W17/W17-3204.pdf

21. "Note that the output of the NMT system is often quite fluent (e.g., Take heed of your own souls.)
but completely unrelated to the input, while the SMT output betrays its difficulties with coping with the out-of-domain input by leaving some words untranslated (e.g., Schaue by dich around.). This is of particular concern when MT is used for information gisting — the user will be mislead by hallucinated content in the NMT output." http://www.aclweb.org/anthology/W/W17/W17-3204.pdf

22. "Typical cross entropy training procedures for these models do not directly consider the behaviour of the final decoding method. As a result, for cross-entropy trained models, beam decoding can sometimes yield reduced test performance when compared with greedy decoding. We hypothesize that the under-performance of beam search in certain scenarios can be resolved by using a better designed training objective." - https://arxiv.org/pdf/1708.00111.pdf

23. "It has been found that decision trees have the potential advantage of computational scalability, handling data of mixed types, handling missing values, and dealing with irrelevant inputs [34]. However, decision trees has the limitations of low prediction accuracy and high variance [35]." - Twenty Years of Mixture of Experts

24. "Neural networks compute point estimates. Neural networks make overly confident decisions about the correct class, prediction or action. Neural networks are prone to overfitting.* -http://rpubs.com/arowan/bayesian_deep_learning

25. "Probabilistic Machine Learning: Aim: Use probability theory to express all forms of uncertainty. Uncertainty estimates needed in forecasting, decision making, learning from limited and noisy data. AI Safety: medicine, engineering, finance, etc.
The probabilistic approach provides a way to reason about uncertainty and learn from data" -http://rpubs.com/arowan/bayesian_deep_learning 

26. "Bayesian Neural Networks
A Bayesian neural network is a neural network with a prior distribution on the weights
- Accounts for uncertainty in weights
- Propagates this into uncertainty about predictions
- More robust against overfitting: randomly sampling over network weights as a cheap form of model averaging
- Can infer network hyperparameters by marginalising them out of the posterior distribution" -http://rpubs.com/arowan/bayesian_deep_learning 

27. "It is believed that for many problems including learning deep nets, almost all local minimum have very similar function value to the global optimum, and hence finding a local minimum is good enough. However, it is NP-hard to even find a local minimum. In the rest of the post, we will first see that getting stuck at saddle points is a very realistic possibility since most natural objective functions have exponentially many saddle points. We will then discuss how optimization algorithms can try to escape from saddle points." and "Finally, we prove that recovering the global minimum becomes harder as the network size increases and that it is in practice irrelevant as global minimum often leads to overfitting." http://www.offconvex.org/2016/03/22/saddlepoints/ and https://arxiv.org/abs/1412.0233

28. "However, several researchers experimenting with larger networks and SGD had noticed that, while multilayer nets do have many local minima, the result of multiple experiments consistently give very similar performance. This suggests that, while local minima are numerous, they are relatively easy to find, and they are all more or less equivalent in terms of performance
on the test set."  https://arxiv.org/abs/1412.0233


29. "For large-size networks, most local minima are equivalent and yield similar performance on a test set. The probability of finding a “bad” (high value) local minimum is non-zero for small-size networks and decreases quickly with network size. Struggling to find the global minimum on the training set (as opposed to one of the many good local ones) is not useful in practice and may lead to overfitting." https://arxiv.org/abs/1412.0233


30. "Unfortunately, it was shown in 1992 that training a very simple neural network is indeed NP-hard (Blum & Rivest, 1992). In the past, such theoretical concerns in optimization played a major role in shrinking the field of deep learning. That is, many researchers instead favored classical machining learning models (with or without a kernel approach) that require only convex optimization. While the recent great practical successes have revived the field, we do not yet know what makes optimization in deep learning tractable in theory." https://papers.nips.cc/paper/6112-deep-learning-without-poor-local-minima.pdf

31. " A classic paper in optimisation is ‘No Free Lunch Theorems for Optimization’ which tells us that no general-purpose optimisation algorithm can dominate all others. So to get the best performance, we need to match our optimisation technique to the characteristics of the problem at hand"  https://blog.acolyer.org/2017/01/04/learning-to-learn-by-gradient-descent-by-gradient-descent/

