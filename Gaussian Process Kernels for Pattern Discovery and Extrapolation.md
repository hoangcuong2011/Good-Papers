- *Gaussian Process Kernels for Pattern Discovery and Extrapolation* - https://arxiv.org/abs/1302.4245

A very beautiful paper to read! The thing GPs are excellent at is regression. Yet it is still difficult
to discover patterns and do extrapolation with standard kernels such as RBF. Those are simply not expressive enough!

The paper proposes a new kernel type that helps do so, while inference remains simple and analytic. Experiments described in
section 4.4 say everything: the new one can learn very complex oscillatory pattern while others cannot. How is that possible?


The root of all the beauties lie in Theorem 3.1 (Bochner), which shows that a function is a covariance function of a weakly stationary mean square if and only if it can be represented as in Eq. 6. (See this for a more detailed explanation of the theorem http://www.gaussianprocess.org/gpml/chapters/RW4.pdf)

The consequence is that there are a dual form between a kernel function (k) and its spectral density or power spectrum of k (S) as in Eqs. 7 and 8. This leads to a very important thing: The expressiveness of a kernel function can be represented by looking at the spectral density.

Coming ack to the traditional RBF kernel. Plugging the kernal to Eq. 8 leads to the fact that the density is a Gaussian distribution centered on the origin (I indeed don't get the word origin here). The authors suppose that it should be better to use a complex form of spectral density: A mixture of Gassians. Their argument is that such a mixture, given a large number of components, can approximate arbitrary distribution (see this for a reference http://www.dsp.utoronto.ca/~kostas/Publications2008/pub/bch3.pdf). I am not so sure about this as this is the first time I heard this thing. If it is true (and I understand correctly), this is very nice!

Having a mixture of Gaussians as the form of spectral density leads to a very nice form of kernel function (Eq. 12). The thing I am not so sure is that how hard it is to optimize the hyperparameters with the new kernel, as we ineed have more parameters here. The authors mentioned they use nonlinear conjugate gradients to do so, but admitted it is not really stable (?) in the Supplementary.
