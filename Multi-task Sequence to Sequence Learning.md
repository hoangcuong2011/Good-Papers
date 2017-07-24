- Multi-task Sequence to Sequence Learning - https://arxiv.org/abs/1511.06114

seq2seq constitutes an encoder, a decoder and attention mechanism. The paper addresses an interesting aspect: can we
build one decoder and multiple decoders? Can we build multiple encoders and one decoder? Finally, can we build multiple encoder and decoders?

I am particularly interested in the first question: Can we build one encoder and multiple decoders that work for different tasks.
In the paper, the authors experiment with three tasks: Machine translation, parsing and autoencoder. Learning in this case is
rather straightforward: The model is optimize for each task given a fixed number of parameter updates. When switching between tasks,
we select randomly a new task with a certain probability. Very surprisingly, adding a very small number of parsing mini-batches, we can improve the translation quality produced by a large-scale NMT system substantially.
Adding a larger number of parsing mini-batches might hurt the performance, though!

Why does multi-task seq2seq learning achieve such an interesting result??? I still have no clue, though! Note that the baseline in the paper does not have attention mechanism.
