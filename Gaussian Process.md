Gaussian Process
Gaussian Process is a very interesting model that models uncertainty. Besides the classic book Gaussian Processes for Machine Learning (http://www.gaussianprocess.org/gpml/), several sources can be referred as a very basic introduction
of the topic:
- http://cs229.stanford.edu/section/cs229-gaussian_processes.pdf (I highly recommend this)
- http://katbailey.github.io/post/gaussian-processes-for-dummies/

Even with those references, it is still quite difficult to start learning the topic. I guess this happens for lots of
people. Here I want to give a very informal introduction to the topic. I am interested in the topic, but I am not knowledgable
by anymeans. Despite that, my viewpoint is from a dummy and I hope it will be helpful for beginner.

So what is GP? You can think GP as distribution over functions. It sounds fancy at first sights, but the concept is indeed
straightforward. You can imagine you have a set of points:
[x_1 = 1, x_2 = 2, x_3 = 3, x_4 = 4, x_5 = 5]
You have a set of functions f, in which each specific function f transforms the set of points to another space:
[f(1), f(2), f(3), f(4), f(5)].

Why do we need a set of functions instead of a specific and useful function? Think about this: in practice we may want
to perform a regression, but there doesn't exist any specific function that you defined in advance, e.g. y = ax+b, that perfectly
matches the data) (See this: http://katbailey.github.io/images/bad_least_squares.png). Because we cannot define such a function,
it makes senses to find a set of functions f. (???)


Let us assume we have N different functions: f_1, f_2, ..., f_N. Can we define a distribution over functions? GP assume that
the function's outputs can be sampled from a multivariate Gaussian distribution with mean U and covariate matrix K in which each element ij in the matrix is defined by a specific kernel function k(x_i, x_j).

The size of U is N, and the size of K is NxN. Not all arbitrary matrices K gives us valid Gaussian Processes: each covariate matrix needs
to be positive semidefinite, i.e. x^T K x >= 0 for all vector x with size N. But how to check a matrix is positive semidefinite?
I don't see many articles about this, perhaps it is not easy to do so. Also we normally don't have to do much in practice because kernel functions are well studied (well-studied valid kernel functions can be referred to this link: http://www.cs.toronto.edu/~duvenaud/cookbook/index.html).
Perhaps squared exponential kernel (k(x, x') = exp(-0.5 * (x - x') ^ 2) is the most common one.

What is the key here? I believe the key idea is the output of the function at points to be similar if the kernel function
at those points to be similar. Now you know why people usually say: "A GP defines a prior over functions". Prior means the
way we define the kernel function.

To have a better understanding, let me show some code https://github.com/hoangcuong2011/GPs. Let us assume we have 40 points

import numpy as np
import matplotlib.pyplot as pl

n = 40
Xtest = np.linspace(0, 10, n).reshape(-1,1)

Our kernel function is squared exponential kernel:

def SquaredExponentialKernel(a, b):
	sqdist = (np.sum(a, 1) - b)**2
	return np.exp(-.5 * sqdist)

With that kernel function, our covariate matrix is as follows:

K_ss = SquaredExponentialKernel(Xtest, Xtest)

Let us assume we want to draws 100 functions over these points. All we need to do is to sample 100 vectors from 
a multivariate Gaussian distribution with mean [0, ....., 0] and covariate matrix K_ss. The code is as follows: 

dataPoints = 100
L = np.linalg.cholesky(K_ss + 1e-15*np.eye(n))
f_prior = np.dot(L, np.random.normal(size=(n,dataPoints)))

pl.plot(Xtest, f_prior)
pl.axis([0, 10, -5, 5])
pl.title('Samples from the GP prior')
pl.show()


Note that the code involves Get Cholesky decomposition (see this https://en.wikipedia.org/wiki/Multivariate_normal_distribution to know why)






----------------- far from finished yet -----------------------
