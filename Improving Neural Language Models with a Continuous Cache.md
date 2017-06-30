- Improving Neural Language Models with a Continuous Cache - https://openreview.net/pdf?id=B184E5qee

A common phenomenon in natural language is about repetition and recency effects of words: many words, especially content words, are repeated in close context.

Accounting for the phenomenon is fairly simple, using a cache-based adaptive model (A cache-based
natural language model for speech recognition - http://ieeexplore.ieee.org/document/56193/). Specificially,
what we need to do is to simply build a LM model using the elements stored in a fixed-size cache to estimate model parameters.
The size of the cache should be really small, and the LM built on the cache is normally a unigram LM.

How can we implement the idea in Neural Language Models? This is what the paper is about.
At time step t, the proposed cache-based NLM computes a distribution over words given the history based on the current
hidden state, and the stored hidden representations of previous words:
P_cache(word |hidden representations h_1, ..., h_{t}) 
proportional to sum_{i=1)^{t-1} delta(word, previous word i)exp(\theta * h_t * h_k)

The observation of using h_k as key and h_t as query vector is a nice one. I also like the fact that the model uses dot product to learn similarity between two vectors, abeit I am sure the idea is already proposed elsewhere for decades. Note that theta is a hyperparameter, tuned on a validation set.

In experiments, the cache size is small (can be up to 10K), which is similar to the normal cache size developed with traditional language models.
Results are convincing.

While the model is nice, I believe we can improve the model by having an additional weight matrix W as follows

P_cache(word |hidden representations h_1, ..., h_{t}) 
proportional to sum_{i=1)^{t-1} delta(word, previous word i)exp(\theta * h_t * *W* * h_k)

The weight can be learned by using backprop. In this case training the model can be harder, but I expect we can have
better performance.

Finally, I also think having decay factor can help, as the idea is proved by previous work (e.g. see this paper ftp://mi.eng.cam.ac.uk/pub/reports/auto-pdf/clarkson_icassp97.pdf)

