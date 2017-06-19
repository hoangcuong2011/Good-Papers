- Convolutional Sequence to Sequence Learning - https://arxiv.org/pdf/1705.03122.pdf:
A new paper from FAIR, describing a new NMT architecture that uses CNNs instead of RNNs.

RNNs are the first citizens when it comes to sequence to sequence learning, but they have two main drawbacks. 

First, reading thorough an input sentence into into a fixed-size vector before generating the output based on the vector
seems problematic. First, we don't translate in that way. Second, both shorter and longer input sentences are encoded into
a size-fixed  vector regardless their length. This does not sound right. Attention mechanism can help but I think we can do 
better by using a more relevant NMT model in the first place. 

Second, RNNs are sequential models, which means it is hard (or even impossible?) to parallel.

CNNs seems a better matching to the problem. The paper is quite technical, so I suggest readers
should take a look at the figure in the first place to have a better high-level view of the model 
https://code.facebook.com/posts/1978007565818999/a-novel-approach-to-neural-machine-translation/

It is not possible to capture arbitrary long relationships
(in principle, RNNs do): each convolutional layer has a fixed-size receptive field. But we can stack multiple 
convolutional layers on top of each other increases the context size. Arguably, as the input sentence is processed 
hierarchically, and it is easier to capture complex relationships in the data. Hierarchical structure also helps
learning easier since the number of non-linearities is significantly reduced compared to a chain rule. Perhaps this 
is the reason why the authors claim CNNs do not suffer from vanishing gradient as in their related 
work https://arxiv.org/abs/1612.08083

It is quite nice that experiment results show that increasing the number of convolutional layeres improves the performance significantly.
This however happens only on the encoder, but not on the decoder (I still cannot figure out why it is the case yet).

Multi-step attention is also interesting. The special thing here is that each decoder layer has a separate attention 
mechanism. Equation 1 can look a bit complicated but if you take a look at the figure in the link above, everything should
be much easier to follow. I however can imagine such a multi-hoe attention mechanism should be very hard to train, and it
would be very surprising if we can train the model without good parameter initialization tricks.

Overall I really like the paper. Having a different yet strong model for translation is obviously great. I however have a bit concern whether it replaces sequence-to-sequence model or not. It is also not clear to me how function words are generated during the translation. But of course the model is quite basic (even though it is very technical), and there is lots of space we can improve.
