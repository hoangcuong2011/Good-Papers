- Depthwise Separable Convolutions for Neural Machine Translation - https://arxiv.org/abs/1706.03059

An interesting paper to read. This can be seen as an "Xception"-like (https://arxiv.org/abs/1610.02357) architecture 
to NLP in general. Understanding Xception requires background of Google's Inception (https://arxiv.org/abs/1409.4842). 

At a high-level, Xception is similar to an extreme version of Inception modul where 1x1 conv is performed over all the input channels,
and convolutions with larger receptive field (e.g. 3x3, or 5x5) performed *independently* over *each of output channels*.
See this picture http://i.imgur.com/kylzfIQ.png). For convenience, let us refer 1x1 conv as pointwise conv, and a larger receptive
field conv as depthwise conv.

This extreme version may give a better performance than the "original" Inception-like
architecture: having multiple different "paths" of convolutions on *all the input channels". Each path 
can be started with a 1x1 or pooling convolution, followed directly
by a larger receptive field (e.g. 3x3, or 5x5) convolution (see this http://i.imgur.com/jwYhi8t.png).

The intuition that the extreme version is a better version is because different paths are believed to be sufficiently decoupled 
in Inception. So we explit force that in the extreme version.  

Note that Xception is slightly different than the extreme version: it has multiple different paths of convolutions over
each of input channels. Each path starts with a depthwise conv, followed directly by a pointwise convolution. Let us refer
this specific structure as of a depthwise separable convolution. In Image classification, it gives better results than Inception, 
while having less model's parameters. Amusingly, we should not put any activation after depthwise conv in Xception.
The absence of any non-linearity gives faster convergence and better performance. I found this particularly interesting (it is
strange, isn't it?). But I still cannot figure why?

Now back to the paper. The main contribution of the paper is to specifically apply Xception-like architecture to NMT. The system is
fairly easy to follow once you know what depthwise separable convolution is

At a high-level,
Table 2 gives us all take-home messages (Table 3 is nice, but it is simply to show off, I think.):
1. Depthwise separable convolution helps improves the accuracy, while reducing significantly number of model's parameters.
2. Depthwise separable convolution allows us experiment with convolutions with large receptive field. This is important. While
the number of parameteres does not increase much, the final performance is generally better.
3. As it is possible to work with large receptive field conv, we can forget about dialations. OK this is a bit too optimistics,
but with small-scale dilations (i.e. 1-2-4-8) as in the paper, the need for dilation can be completely removed.

The authors also experiment with super-separable convs, but the improvement is rather marginal.

Overall, this is a very nice paper to read. I think depthwise separable convolution will be widely used in future.  This is particularly the case as ConvSeq is getting more and more attentions.

