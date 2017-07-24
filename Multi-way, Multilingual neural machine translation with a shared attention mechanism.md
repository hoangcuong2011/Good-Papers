- Multi-way, Multilingual neural machine translation with a shared attention mechanism http://www.aclweb.org/anthology/N16-1101

This paper addresses an interesting problem: how to build a multi-way, multilingual NMT. 
Having a seq2seq that handles multilingual tasks is somewhat trivial. The tricky part is about attention mechanism. Given one source language and multiple target languages, it is trivial to build
different NMT with separate attention mechanisms. But it is not the case with multiple (let's say N) source and (let's say M) target languages at the same time. Doing so is quite expensive, and more importantly, having different attention mechanisms makes it less likely for the model to benefit from having multilingual translation. 

But how to build a NMT with a single shared attention mechanism? The way the authors did is quite straightforward! Given N source and M target languages, we creat N encoders and M decoders. There is nothing fancy with N encoders (i.e. bidirectional recurret network). One thing should be noted, though: the dimensionality of context vectors can be different, which requires a linear transformation into a common dimensional space (Eq. 9).

The most tricky part is about decoder and attention mechanism. The paper doesn't describe those parts clear though. The decoder is a conditional recurrent language model. At each time step t', it updates its hidden state by:

z_t' = non_linear_transformation (z_{t'-1}, y_{t'-1}, c_{t'})

here, z is hidden state, y is target symbol and c is time-dependent context vector.

Thing should be noted here: for each decoder the weight for non_linear_transform is learned for all N encoders. Training the model requires a set of bilingual corpora, not a set of multi-way parallel corpora (which make sense).

Why should we notice about this? The model parameters are shared from all language pairs and not pair-specific. I don't believe it works all the time. Perhaps it depends on the training strategy. For instance, let us assume we have a very large English-French corpora, but we have a very small English-Vietnamese bilingual data. Doing so (training E-F first, and then E-V) might hurt English-French NMT, but significantly improve English-Vietnamese NMT. Meanwhile, training E-V first, and then E-F might improve translation performance for both language pairs. All of these are just my hypotheses, though (i.e. no verification).


Back to our decoder. Two things are important: how to feed its input and how to create time-dependent context vector?
Feeding its input is straightforward, but note that the authors applied a transformer to transform the last context vector h from an encoder. Ironically, the authors use h_0 instead of h_{T} where T is the length of the input).
