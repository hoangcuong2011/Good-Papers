- Zero-Resource Translation with Multi-Lingual Neural Machine Translation - https://arxiv.org/pdf/1606.04164.pdf

This paper investigates how to apply multi-lingual neural machine translation to zero-resource translation. Both the topics are pretty 
cool. Multi-lingual NMT translates between multiple languages using single shared attention mechanism (http://www.aclweb.org/anthology/N16-1101) (See this
for a review https://github.com/hoangcuong2011/Good-Papers/blob/master/Multi-way%2C%20Multilingual%20neural%20machine%20translation%20with%20a%20shared%20attention%20mechanism.md).
Zero-resource translation concerns with the case where there does not exist any direct parallel examples between a source-target language pair. 
In the context of SMT, zero-resource translation has been addressed by pivot-based translation, but the performance is not that
great.

The paper has a review of Multi-lingual NMT. Let us assume we are given N source and M target languages, and we will create N encoders and M decoders. There is nothing fancy with N encoders (i.e. bidirectional recurret network). The most tricky part is about decoder and attention mechanism. The decoder is a conditional recurrent language model. At each time step t', it updates its hidden state by:

z_t' = non_linear_transformation (z_{t'-1}, y_{t'-1}, c_{t'})

here, z is hidden state, y is target symbol and c is time-dependent context vector. Non_linear_transformation can be LSTM, GRU.

Time-dependent context vector at each time step is nothing different than traditional attention mechanism. The main difference is the way we compute the score (Eq. 2): We have a shared transformation (representing by a matrix): all decoders use this matrix given a specific source language. We aso have a shared transformation (representing by another matrix): each decoder uses the same matrix for all source languages.



There are several strategies we can exploit. One to one translation: one source sentence and one target sentence. Many to one translation: many source sentences, one target sentence. The tricky part, of course, is how to train many to one translation.
In the work, the authors propose two different approaches, namely early average and late average. With early average, we take the average of different time-dependent context vector. We also feed input to decoder as the average of encoders' outputs.
With late average, we simply take the average of output prediction (p(y_{t} = w| y_{<t}) = sum of all languages p(y_{t} = w| y_{<t}, language X) ). The second strategy can be thought of as ensemble with respect to multiple source languages.

In experiments, many to one strategy indeed helps build much better NMT system. However, doing so with single NMT systems also helps a lot (Table 3).

Now let us come back to our zero-shot translation problem. A strategy to deal with the problem is one to one translation. This turns out does not work at all.
