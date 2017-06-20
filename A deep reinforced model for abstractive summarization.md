- A deep reinforced model for abstractive summarization - https://arxiv.org/pdf/1705.04304.pdf

A very nice paper to read. Since there are several good reviews for the paper (e.g. https://einstein.ai/research/your-tldr-by-an-ai-a-deep-reinforced-model-for-abstractive-summarization, 
http://www.shortscience.org/paper?bibtexKey=journals%2Fcorr%2F1705.04304), I don't go into detail here. There are some important take-home messages:

1. The paper aims to address an interesting task: abstractive summarization. Such a summarization system generates new phrases, possibly rephrases and uses
words that are not in the original text. Contrast to abstractive summarization, extractive summarization creates summaries by copying parts of the input. The two types of
problems reminds me of question answering task. The easier task is to answer a question by simply pointing to a specific part of the input (memory networks are the best framework to 
address the challenge, to the best of my limited knowledge). The harder task should be answering a question by reasoning, but
I don't have good background of sota models for that yet.

2. Like lots of other NLP problems, seq2seq are currently sota models. The problem with current seq2seq plus attention mechanism
is that it often generates unatural summaries consisiting of repeated phrases. This is not a surprising result, especially
as we can see in other NLP problems such as Machine Translation (Modeling Coverage for Neural Machine Translation, Context Gates for Neural Machine Translation, Guided Alignment Training for Topic-Aware Neural Machine Translation).
The author proposes a new attention mechanism to address the problem.

3. One one hand, I think some of the ideas proposed in the paper are very smart. On the other hand, I don't think I like
some solutions proposed in this work. Specificially, to prevent the model from using the same parts of the input on different decoding
steps, the authors propose the so called intra-temporal attention. The name is fancy, yet the idea is quite straightforward: we need to
normalize  the attention weights so that we penalize input tokens that have obtained high attention scores in the past decoding
steps. Equation 3 is an ``implementation" of the idea, which I found a bit ad-hoc. But basically I get their idea.
Having intra-tempora attention by itself is not enough to create good abstractive summaries, and the work proposes an additional 
mechanism: intra-decoder attention. Again, the name sounds fancy, yet the idea is quite straightforward: we have an attention score
between two hidden states at decoding (see Equations 6 and 7). Besides proposed attention mechanisms, I really like the idea of using a switching function that decides whether to use token generation or the pointer, 
but I am not sure the idea is proposed in the work, or it is already published somewhere.

4. Training is also an interesting part. Teacher forcing algorithm is naturally the most straightforward method to train the model. However, this could be problematic because of exposure bias (see this very good paper https://arxiv.org/abs/1506.03099). More importantly,
recall that the model does not have to produce an an exact word-by-word summary as in the ground-truth. It is therefore necessary to
learn a maximize a specific discrete metric (e.g. ROUGHE) instead. You can imagine how reinforcement learning come into place now, but I think WGAN can be also a good option. I even expect it is easier to train the model with WGAN and it and may give more robust result. The work also proposes to use
mixed training objective function, but it is just a hack, nothing new here.

That is all. The experiments, however, are a bit weak: It does not convince how intra-temporal and intra-decoder attention help.
The result is just that okay they, when putting together, are helpful. Also, training intra-attention with maximum likelihood seems does not help much, and sometimes it even give worse results. Experiments are not performed regarding to switching function, which I found a bit disappointed. The model gives SOTA and that is awesome! But the work can be much stronger by doing more detailed analysis.

Overall, this is a very nice paper. Yet it can be improved by many ways (having more experiments and better equations (?)). 
