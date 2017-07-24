-  Differentiated Softmax - http://www.aclweb.org/anthology/P16-1186 

An interesting method to scale up training large neural nets is Differentiated Softmax (D-Softmax). 
I found this method interesting because of two reasons. First, the intuition make senses: Frequent words allow us to fit
more parameters to them, while rare words only allow to fit a few. Different words require a different number of parameters, 
so does the output layer. Second, this reminds me an interesting work of Variable Computation in Recurrent Neural Networks - https://arxiv.org/abs/1611.06188
(If you have read it yet, you can take a look at my notes on the paper https://github.com/hoangcuong2011/Good-Papers/blob/master/Variable%20Computation%20in%20Recurrent%20Neural%20Networks.md).
Let us consider sequential data such as audio. There are time periods where we don't hear anything (i.e. silence). 
It makes sense to create a model that does much less computation in those cases. The technique to handle this is more fancy :
we create a network that aims to do only one thing: predict how much computation we should does given an input. The technique in D-Softmax is far simpler, though.

Specifically, let us assume we have three bins of frequencies (A, B, and C). Each word belongs to each of these bins. All words
in a bin have the same embedding size (d_A, d_B and d_C). With D-softmax our network is structured in this way: each word in D-softmax is represented as a vector with the size of d_A + d_B + d_C. The vector is very sparse. For example, if a word belongs to bin A, then except the first d_A elements, the rest elements in the vector are zero. If a word belongs to bin A, the first d_A elements and the last d_C elements are zero. Finally, if a word belongs to bin C, only the last d_C elements are non-zero.
The weight matrix is also much larger, but are super sparse (See figure 1).

To me D-Softmax is a nice idea to know. It is, however, not clear from the paper: How to bin words based on their frequency and how to determine embedding size (d_A, d_B and d_C)

------------------------------


Updated (24th July 2017): I understand that it is not really optimal  in the original version because each word cluster uses a disjoint subset of the hidden representation. But how to fix that? The paper (https://arxiv.org/abs/1609.04309) suggests a modification that substantially improves D-softmax. The description is totally unclear, though!
