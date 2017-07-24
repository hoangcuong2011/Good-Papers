- Hierarchical Probabilistic Neural Network Language Model http://www.iro.umontreal.ca/~lisa/pointeurs/hierarchical-nnlm-aistats05.pdf

This is a classic paper, showing how to speed up NN Language Model. The technique is not SOTA by any means as of 2017, but it is very interesting to study. I am personally aware of this study for a long time. I thought the idea is trivial to propose/understand. But it is indeed not trivial to me at all when I read up on it. I am curious how about you?

OK. Here is the thing. Recall that for NN LM we need to compute an extremely expensive softmax function for every history:
exp(g(w_t,history))/all_word exp(g(w',history))

The paper shows how to approximate the softmax function while speeding up the computation. How? First recall that once we have a deterministic mapping between each point x and a class C(x), we can compute P(w|history) in a different way as follows:

P(w|history) = p(w|history, C(w)) p(C(w)|history).

The hierarchical decomposition is proposed by Goodman in 2001 (https://arxiv.org/abs/cs/0108006). The nice thing about the composition is that it is much faster to compute. 
One one hand, p(C(w)|history) is much faster to compute.
On the other hand, p(w|history, C(w)) is also much faster to compute, because we only need to normalize all other words (w') that
are as in the same class as w. Why is that? Let us assume a word w'' does not belong to C(w). We have 


P(w''|history, C(w)) propto P(history, C(w)|w'')p(w'') = P(history|w'', C(w))p(C(w)|w'')p(w'')
since p(C(w)|w'') = 0, P(history, C(w)|w'')p(w'') would be 0 and P(w''|history, C(w)) would be 0.

As a result, we don't need to compute P(w''|history, C(w)) for all words w'' that do not belong to C(w). Let us assume we have sqrt(V) classes,
where each class contains sqrt(V) words, where V is the size of the vocab. The model can drastically reduce the computation from O(V) to (O|sqrt(V)|).

Of course there is no free lunch. Although any C(.) would yield correct probabilities, generalization
could be better for choices of word classes that "make sense". I however didn't have any experience with this before. I expect a comparison of different mapping functions would be a really interesting test.




The current paper pushes the idea to the limit. How?

I thought this is the way the authors did: Let us assume we have a hierarchical tree where at the bottom, each word belongs to a specific class. Going up higher, each class belongs to a higher-level class. An illustration can be found here https://i.stack.imgur.com/OPq7K.gif. For convenience, let us simply assume the depth of the tree is just only 2. Let us use C_1(.) to denote the class function at leaf, and C_2(.) to denote the class function  at the top level. We can reduce the computation from O(|sqrt(V)|) to even lower.

P(w|history) = p(w|history, C_1(w))p(C_1(w)|history) = p(w, C_2(C_1(w))|history, C_1(w))p(C_1(w),C_2(C_1(w))|history)

= p(w| history, C_1(w), C_2(C_1(w))) p(C_2(C_1(w))|history, C_1(w)) p(C_2(C_1(w))|history,C_1(w))p(C_2(C_1(w))|history)

While this way of decomposition is useful, it is very difficult to construct such a tree! Is it the way the authors did? Actually they did it in a totally different way!

First, let us assume we can represent a word as a binary vector with size m, i.e. there is a mapping
between w and a unique binary vector size m: [b_1(w), b_2(w), ..., b_m(w)]. In this way we have:

P(w|history) = P(b_1(w), b_2(w), ..., b_m(w)|history) = prod_{j=1}^{m} P(b_j(w)|b_1(w), ..., b_{j-1}(w), history)

In other words, each word enjoys a unique path from the root to itself. Let us assume such a tree as a balanced tree. The length of the path is the same as the heigh of the tree on average. In this way, the final probability (P(w|history)) is the continuous multiplication of probabilities regarding to steps in the path we travel from the root to leaf. Apparently, the time complexity decreases from O(|V|) to O(log(|V|)). 

But how expensive is it to compute the probability regarding to a specific step? For instance, let us assume we need to compute probabilities regarding to the very first step:
P(0|history) and P(1|history) (Note that P(0|history) + P(1|history) = 1).
If we think of the work of Goodman, we still need to count all the words in the vocab, and see which one starts with 0 or 1 to compute P(0|history) and P(1|history). Therefore I was very confusing that we do not speed up the computation at all. Actually I was wrong - there is nothing related to the work of Goodman at this point. That is, P(0|history) is the output of a network and the output is a simple non-linear function. One possible way can be: 

sigmoid(bias of Node + U*representation of Node + W * hidden layer)


Finally, how to build such a tree? In this work the authors rely on Wordnet. Experiments show that the method gains a remarkable speed up at more than 250 times, while achiving a competitive performance to the original model.

There is no doubt that the method is classic. Yet the paper can be more solid by having experiment with the model with random clusterings, clustering based on word frequency and other unsupervised clustering methods. The way the authors did experiments is using prior knowledge (Wordnet), which makes the comparison is unfair.


----------------------
Updated (21st July 2017): There is a work (Strategies for Training Large Vocabulary Neural Language Models - http://www.aclweb.org/anthology/P16-1186 ) that provides a comparison between different clustering methods (Table 4). Here is the result: random < frequency < k-means < weighted k-means. Note that k-means runs on the outputs produced by Hellinger PCA word embeddings.

Updated (24th July 2017): There is a work (Efficient softmax approximation for GPUs - https://arxiv.org/abs/1609.04309) that provides a comparison between frequency and Brown clustering. Not surprising, the result is as follows: Frequency < Brown clustering.
