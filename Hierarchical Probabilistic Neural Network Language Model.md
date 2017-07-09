- Hierarchical Probabilistic Neural Network Language Model http://www.iro.umontreal.ca/~lisa/pointeurs/hierarchical-nnlm-aistats05.pdf

This is a classic paper, showing how to speed up NN Language Model. The technique is not SOTA by any means as of 2017, but it is very interesting to study.

Recall that for NN LM we need to compute an extremely expensive softmax function:
exp(g(w_t,history))/all_word exp(g(w',history))

The paper shows how to approximate the softmax function while speeding up the computation. How? First recall that once we have a deterministic mapping between each point x and a class C(x), we can compute P(w|history) in a different way as follows:
P(w|history) = p(w|history, C(w))p(C(w)|history).

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




The current paper pushes the idea to the limit. Let us assume we have a hierarchical tree where at the bottom, each word belongs to a specific class. Going up higher, each class belongs to a higher-level class. An illustration can be found here https://i.stack.imgur.com/OPq7K.gif. For convenience, let us simply assume the depth of the tree is just only 2. Let us use C_1(.) to denote the class function at leaf, and C_2(.) to denote the class function  at the top level. We can reduce the computation from O(|sqrt(V)) to even lower.

P(w|history) = p(w|history, C_1(w))p(C_1(w)|history) = p(w, C_2(C_1(w))|history, C_1(w))p(C_1(w),C_2(C_1(w))|history)

= p(w| history, C_1(w), C_2(C_1(w))) p(C_2(C_1(w))|history, C_1(w)) p(C_2(C_1(w))|history,C_1(w))p(C_2(C_1(w))|history)



------------------------ not done yet, to be continued later --------------------
