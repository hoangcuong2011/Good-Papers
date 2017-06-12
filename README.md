# Good-Papers

- Variational Inference with Normalizing Flows: One of the best papers I read recently! A very good note can be found here
https://casmls.github.io/general/2016/09/25/normalizing-flows.html

An open question, as described in the reference note: ``whether the proposed normalizing flows is a universal approximator of all the distributions when the number of layers go to infinity."
Two technical questions: Do we still need to assume P(z_0) as a Gaussian distribution? Why is the model not scalable regarding to high-dimensional latent space?

- MADE: Masked Autoencoder for Distribution Estimation: An inspiring work! It shows how autoencoder can be used for density estimation. Of course doing that is non-trivial as a conventional autoencoder can simply memorize all the data given large enough units in hidden layers, implying it cannot be used for the task. The paper addresses this problem by structuring the network so that its output represents conditional probabilities of a dimension given the others. They proposed masked autoencoder to do so.

Question: This is a very nice framework, but how to make it work with real value?

- Improving Variational Inference with Inverse Autoregressive Flow: An interesting paper. It combines two successful approaches in deep generative models recently: normalizing flow and autoregressive models. While the idea of normalizing flow is powerful, the authors claimed they are not scalable (but why?). Their intuition is that Gaussian autoregressive functions can scale well to high-dimensional latent space. The idea of using autogressive models is seems a very good idea (e.g. see MADE, PixelCNN). The authors show that such functions can also turn into invertible non-linear transformations of the input. It therefore makes sense to use inverse Gaussian autoregressive functions as new flow. They show that their model achieve SOTA. A direct comparision between normalizing flow and inverse autoregressive flow is not performed, though!

It is quite surprising (at least to me) that applying many steps of conditional gaussian distributions can model arbitrary complex distribution. Why is that the case? I was wondering because in Normalizing Flows are designed to get rid of simple Gaussian distributions.

- Density estimation using Real NVP: A thought-provoking paper. Working with probabilistic generative models involve sampling (sample x given p(x)), inference (compute p(z|x) = p(z)p(x|z)/p(x) with latent (continuous) variables z) and exact likelihood computation (p(x) = int_{z}p(x|z)p(z)d(z). The paper proposes an interesting inversion models that address all the problems in a nice way. What I mean a nice way here is: exact sampling, easy to do inferenec and the likelihood can be computed easily. There seems no way of having such a model. But the author proves we can by exploiting bijective functions that map between each point of data (x) and a value of latent continous variable. The space of the variable must be easy to sample (e.g. a Gaussian: z ~ N(mean, variance)). Since we expoloiting bijective functions, it would be easy to find an inverse function of the bijective function so that given a point x, we can easily compute z (inference). Finally, the likelihood can be computed directly from the densitity function of z (it only involves additional computation regarding to the determinant of the Jocobian matrix with respect to the inverse function and x). Obviously, the bijective function must have a super rich representation to model arbitrary distribution, it must be easy and efficient to compute the Jacobian matrix (and the determinant of the matrix). The function they proposed relied on affine coupling layers. Relying on the idea everything can be done in a very neat way!

Question: how to train the model (maximize the likelhood of the data?) not sure I am missing something but they didn't describe that?

