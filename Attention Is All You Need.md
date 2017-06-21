Attention Is All You Need - https://arxiv.org/abs/1706.03762

An interesting paper. It is however a bit technical to follow, and I think it would be easier to read once we already
take a look at the following relevant work:
- Wavenet/Bytenet https://arxiv.org/abs/1609.03499 and https://arxiv.org/abs/1610.10099
- ConvS2S https://arxiv.org/abs/1705.03122
- Attention in general: https://arxiv.org/pdf/1703.03906.pdf (the link would help you quickly understand section 3.2)
- Intra-attention: https://arxiv.org/pdf/1705.04304.pdf

In the last 2 years, we have seen how seq2seq models achieve SOTA performance in many NLP applications. Yet in the last couple of months,
there is a trend of improving seq2seq in a significant way. Most papers focus on two most important aspects.

First, seq2seq encodes an input into a fixed-size vector. We humans don't translate in that way. More importantly, 
both short and long input sentences are encoded into a size-fixed vector regardless their length. This does not sound right.
Second, seq2seq is slow. The computation is sequential and this must need to change. Both problems are challenging,
but from a research point of view, the first one is more interesting to work on.

The most important contribution of the paper is to propose a new model architecture that helps
us get rid of recurrence. Following the recent trend (eg. see BYTENET, WAVENET, CONVS2S), in their model, decoder is stacked directly on top of encoder.
Note that the encoder itself has multiple layers, so does the decoder. 
Different to previous work, each layer has two sub-layers: the first is an attention mechanism, 
the second is position-wise fully connected 
FFN. This reminds me of ConvS2S. In ConvS2S the attention model is equipped with ``a sense of
order by embedding the position of input elements". But the way ConvS2S is built is different: The embedding of
position of input elements and the input elements themselves are combined to obtain input representations. Here we have two
different type NNs for the two types of information respectively. BTW in BYTENET we don't have position-wise FFN, but we have dilated convolutions. 

Let us go into detail about attention. The attention mechanism proposed in the paper is pretty novel, in the sense that the attention is multi-head self-attention mechanism.
It is a bit vague, however, to understand whether the real merit comes from "multi-head" part, or the "self-attention"
part. We will get into there later. 

Let me first explain what is self-attention. Basically,
one of the main problems with current seq2seq plus attention mechanism is that it often generates unatural output text 
(consisiting of repeated phrases). This is because the original attention (https://arxiv.org/abs/1409.0473) is not strong enough: 
seq2seq could use the same parts of the input on different decoding steps, and it could also repeat generating target texts.
They way people addressed the problem (at least from the related work https://arxiv.org/pdf/1705.04304.pdf)
is to normalize attention weights (computed by the ``original" attention mechanism). In this way we explicitly penalize input
tokens that have obtained high attention scores in the past decoding steps. 
Unfortunately, I don't see any point how the attention mechanism proposed in the paper explicitly addresses the problem. 
The only thing they mentioned is that they masked out (setting to -infinity) all values in the input of the softmax which corresponds to illegal connections". 
But I don't think that is strong enough, at least I still don't know how that fixes the problem of using the same parts of
the input on different decoding steps. I guess by explicitly having a position-wise FFN would fix that problem.

Besides self-attention mechanism, the paper also proposes multi-head attention. Instead of performing a single attention function
with d-dimension, we performed *h* parallel attention functions with d/h-dimension. The output vectors are then concantenated (see Figure 2).
I thought this idea is all about speed. But Table 3 in the experiment reveals that this helps improve the accuracy (h=1 and h=8), abeit not much.
Why is that? The author claims: "multi-head attention allows the model to jointly attend to information from different representation
subspaces at different locations." This is great, but I think it should be elaborated more. As a side note, increasing
h from 8 to 16 and 32 does not help. Hmm ....

Position-wise FFNs are also an interesting topic to discuss. The network is simply two linera transformations with a ReLU activation in between,
and there is nothing fancy here. The interesting thing is about how to add positional encodings to the input embeddings.
A natural way is to embed the absolute position of input elements, as done in CONVS2S. The second way is to use ``sine and cosine functions of different frequencies".
The ``sinusoidal" version is quite complicated, while giving similar performance to the absolute position version. But more importantly,
it may allow the model to produce better translation on longer sentences at test time (longer than the sentences in the training data) (i.e. sinusoidal allows the model to extrapolate to longer sequence lengths).
I feel this is particularly interesting, perhaps because not only it is nice, but also because I am a fan of pointer networks, which address a similar problem).
Unfortunately, the experiments don't elaborate this point in detail.

That is all! Several tricks have been done, of course to make it work, but basically those are the main important take-home messages from the paper:
new architecture, where attention is all we need to get a very strong result. (Note that FFNs can be interpreted as attention mechanism, as in the appendix).

This is a very good paper. I enjoyed reading it a lot! But I think it is written a bit rush:

- The paper is too technical and not easy to follow. 
- The experiments are quite weak. Well, they give SOTA result (+2 bleu score) and that is awesome! But we already know
how amazing Google fellows are! The paper itself would be much stronger if the paper clarifies several important things, to name a few:
1. Does having separate position-wise FFNs help? (comparing to ConvS2S).
2. The paper got a significantly improvement over ConvS2S, but where does the improvement come from? It is not clear from the work.
I believe the source of improvement should mainly come from of self-attention. This is the thing ConvS2S doesn't have.
Multi-head attention might be a reason, but it should not be a key factor here. 
3. How sinusoidal helps translate long sentences.
4. I am not really clear about the scaling factor in Equation 1. With my limited knowledge, I think it is new, but I don't see
any experiment that elaborates that point...


