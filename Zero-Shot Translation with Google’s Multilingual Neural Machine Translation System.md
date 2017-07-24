- Zero-Shot Translation with Google’s Multilingual Neural Machine Translation System https://arxiv.org/abs/1611.04558 (also see this https://research.googleblog.com/2016/11/zero-shot-translation-with-googles.html)

This paper addresses an important problem: let us assume we are given N source and M target languages. 
How to build a single NMT system that works well with all translation pairs. This problem has never been attemped before. 
A very close study I am aware of is this paper: Zero-Resource Translation with Multi-Lingual Neural Machine Translation (See this for a review https://github.com/hoangcuong2011/Good-Papers/blob/master/Zero-Resource%20Translation%20with%20Multi-Lingual%20Neural%20Machine%20Translation.md). Yet
in that paper, they build N encoders and M decoders, with a shared attention mechanism. Here our goal is totally different
as you can imagine: we want to build only one single model that works for all N * M pairs.

Thing should be noted, however: If we build N encoders and M decoders and a shared attention mechanism, 
we then expect a significant improvement over translation accuracy. However, if we try to build a single model only, it is 
indeed no way to achieve that I believe. So the goal should be realistic: we try to get as much competitive to single
NMT systems as possible. The paper is somewhat over-sell at this point. Other than that this work is awesome!

So how do the authors create a single NMT model that works for all language pairs? The only difference is that in the input
we have an additional signal: the code of target output. Let me make it clear by showing an example. In traditional single NMT,
we are given an input (let's say Spanish) and the system translates into a target sentence (let's say English). For instance:

How are you -> abcxyz.

In this system, the input is modified to "<es> input" to indicate Spanish is the target language:

<es> how are you -> abcxyz.

I indeed don't see why they don't have another token to mark the language of input, though!

Training the model is fairly straightfoward. We concatenate all the data and then we just do training! One can adjust for the relative ratio of the language data as well.
This however does not help much.

In experiments, given many inputs and one target, multilingual NMT increases the performance compared to single NMT systems. The improvement
is marginal though. Given one input and many outputs, multilingual NMT gets worse/slightly worse in most cases.
Finally, given multiple inputs and outputs, multilingual NMT gets worse in all cases.

The very interesting aspect of the paper is to investigate how well the multilingual NMT produces zero-shot translation.
For instance, let us assume we have data for English-Spanish and English-Portugese. How is translation Spanis-Portugese quality the system produces?
The result is quite decent, even though it is much worse from bridging two NMT systems: One from Spanish to English and one from English to Portugese.

Overall I really like the paper. Experiment results are very interesting. Claims are really over-hyped, though.

