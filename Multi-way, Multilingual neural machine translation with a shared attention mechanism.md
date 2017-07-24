- Multi-way, Multilingual neural machine translation with a shared attention mechanism http://www.aclweb.org/anthology/N16-1101

This paper addresses an interesting problem: how to build a multi-way, multilingual NMT. 
Having a seq2seq that handles multilingual tasks is somewhat trivial. The tricky part is about attention mechanism. Given one source language and multiple target languages, it is trivial to build
different NMT with separate attention mechanisms [1]. But it is not the case with multiple (let's say N) source and (let's say M) target languages at the same time. Doing so is quite expensive, and more importantly, having different attention mechanisms makes it less likely for the model to benefit from having multilingual translation. But how to build a NMT with a single shared attention mechanism? Actually it is very straightforward to do so. I will explain it now.

First let us be more specific: given N source and M target languages, we creat N encoders and M decoders. There is nothing fancy with N encoders (i.e. bidirectional recurret network). One thing should be noted, though: the dimensionality of context vectors can be different, which requires a linear transformation into a common dimensional space (Eq. 9).

The most tricky part is about decoder and attention mechanism. The paper doesn't describe those parts clear though. The decoder is a conditional recurrent language model. At each time step t', it updates its hidden state by:

z_t' = non_linear_transformation (z_{t'-1}, y_{t'-1}, c_{t'})

here, z is hidden state, y is target symbol and c is time-dependent context vector.

Thing should be noted here: for each decoder the weight for non_linear_transform is learned for all N encoders. Training the model requires a set of bilingual corpora, not a set of multi-way parallel corpora (which make sense).

Why should we notice about this? The model parameters are shared from all language pairs and not pair-specific. I don't think it works all the time. Perhaps it depends on the training strategy. For instance, let us assume we have a very large English-French corpora, but we have a very small English-Vietnamese bilingual data. Doing so (training E-F first, and then E-V) might hurt English-French NMT, but significantly improve English-Vietnamese NMT. Meanwhile, training E-V first, and then E-F might improve translation performance for both language pairs. All of these are just my hypotheses, though (i.e. no verification).


Back to our decoder. Two things are important: how to feed its input and how to create time-dependent context vector?
Feeding its input is straightforward, but note that the authors applied a transformer to transform the last context vector h from an encoder. Ironically, the authors use h_0 instead of h_{T} where T is the length of the input).

Now let us move to the attention. The paper doesn't describe the part clear though. I refer the reader to
Eq. 1, 2 in this paper: https://arxiv.org/pdf/1606.04164.pdf There is indeed nothing fancy: time-dependent context vector at each time step is nothing different than traditional attention mechanism (except we have a transformation with matrix U in Eq. 1). The main difference is the way we compute the score (Eq. 2): We have a shared transformation (representing by a matrix): all decoders use this matrix given a specific source language. We aso have a shared transformation (representing by another matrix): each decoder uses the same matrix for all source languages.


Experiments reveal how the multi-way, multilingual NMT helps build better translation compared to single NMT, which is not surprising at all though. The thing the authors should compare, to me, is to build a NMT as in [1] that trains with one source language and multiple target languages. I don't think the proposed system is better than that one.

Overall I really like this paper, even though the paper is not written so well at some point.


[1]: Multi-Task Learning for Multiple Language Translation, Daxiang Dong, Hua Wu, Wei He, Dianhai Yu and Haifeng Wang, ACL 2015.
