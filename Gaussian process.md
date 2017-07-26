Gaussian process
Gaussian Process is a very interesting model that models uncertainty. Several sources can be referred as a very basic introduction
of the topic:
- http://cs229.stanford.edu/section/cs229-gaussian_processes.pdf (I highly recommend this)
- http://katbailey.github.io/post/gaussian-processes-for-dummies/

Even with thoses references, it is still quite difficult to start learning the topic. I guess this happens for lots of
people. Here I want to give a very informal introduction to the topic. I am interested in the topic, but I am not knowledgable
by anymeans. Despite that, my viewpoint is from a dummy and I hope my introduction will be helpful for beginner.

So what is GP? You can think GP as distribution over functions. It sounds fancy at first sights, but the concept is indeed
very straightforward. You can imagine you have a set of points:
[1, 2, 3, 4, 5]
You have a set of functions f, in which each specific function f transforms the set of points to another space:
[f(1), f(2), f(3), f(4), f(5)].

Why do we need a set of functions instead of a specific and useful function? Think about this: in practice we may want
to perform a regression, but there doesn't exist any specific function that you defined in advance, e.g. y = ax+b, that perfectly
matches the data) (See this: http://katbailey.github.io/images/bad_least_squares.png). Because we cannot define such a function,
it makes senses to find a set of functions f. (???)


Let us assume we have N different functions: f_1, f_2, ..., f_N. Can we define a distribution over functions? GP assume that
each sample can be sampled from a multivariate Gaussian distribution with mean U and covariate matrix K.

The size of U is N, and the size of K is NxN. Not all arbitrary matrices K gives us valid Gaussian Processes: each covariate matrix needs
to be positive semidefinite, i.e. x^T K x >= 0 for all vector x with size N. But how to check a matrix is positive semidefinite?
I don't see much articles about this, perhaps it is not easy to do so.



