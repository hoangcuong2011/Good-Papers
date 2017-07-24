- Multi-task Sequence to Sequence Learning - https://arxiv.org/abs/1511.06114

Seq2seq contains an encoder, a decoder. The paper addresses an interesting aspect: can we
build one decoder and multiple decoders? Can we build multiple encoders and one decoder? Finally, can we build multiple encoder and decoders? Note that the baseline in the paper does not have attention mechanism.

I am particularly interested in the first two questions. First, can we build one encoder and multiple decoders that work for different tasks.
In the paper, the authors experiment with three tasks: Machine translation, Parsing. Learning in this case is
rather straightforward: The model is optimized for each task given a fixed number of parameter updates. When switching between tasks,
we select randomly a new task with a certain probability. Very surprisingly, adding a very small number of parsing mini-batches, we can improve the translation quality produced by a large-scale NMT system significantly.
Adding a larger number of parsing mini-batches might hurt the performance, though! The story still goes in the same way with respect to parsing: translation can really help parsing!


Having many-to-one multi-task seq2seq is also interesting. In the paper, the authors investigate whether translation and image captioning can help each other. Technically, the framework contains multiple encoders (input text and image), and one decoder (English output). Very surprisingly, adding a very small number of image captioning mini-batches, we can improve the translation quality produced by a large-scale NMT system significantly, too.

Why does multi-task seq2seq learning achieve such an interesting result??? I have no clue, though! 
