- **Cross-Sentence N-ary Relation Extraction with Graph LSTMs** https://arxiv.org/abs/1708.03743

This is a good paper that describes how we can extract a more than binary relationship between entities (e.g. ternary and n-ary in general).

The problem itself is hard, and it is even harder given that we need to extract such relationships using cross-sentence extraction.
This is because in a single sentence, such a relationship is barely existed. One can design a model with hand-craft features but the supervision signal for n-ary relations is gonna be sparse. The paper
approaches the problem by learning a continuous representation for words and entities. Specificially, we use a neural network that learns a contextual representation
for each word. For the entities in question, their contextual representations are concatenated and become the input the the relation classifiers.
Note that for a multi-word entity, we can simply use the average of its word representations, but better solution might help.

What kind of neural networks that: learn a continuous representation of words given sequence of text and can be incorporated luingistics analysses such as syntatic and discourse dependiences?
The paper proposes to propose what they call graph LSTM. Instead of having a single connection in hidden states representing two adjacent words, there can be
multiple connections depends on the structure of graph (e.g. dependency graph). 

The idea is intuitive, but raises difficulty in training. Training the network with
backpropagation can suffere for oscilliation or failure to converge. However, as the authors observe that dependencies such
as coreference and discourse relations are generally sparse, the backbone of a document graph consists of the linear chain and dependency
tree is. Backpropgation can be done efficient by applying asyncronous updates. Specifically,  they partition the document graph into two directed
acyclic graphs: an one contains the left-to-right forwardpointing (and linear chain)
dependencies. The other DAG covers the right-to-left backward-pointing dependencies (and linear chain). While I get the idea,
I don't really get the details here though. 

The another difficulty is that each hidden state may have multiple forward connections (In other words, a hidden state may have
several precedents). In order to make it works we need some modifications regarding to the forget gate in LSTM. The best solution proposed
in the paper is straightforward: each connection should have its own typed weight matrix. But this would brings much more parameters to train the model.

Experiments reveal several interesting findings to me. First, Graph LSTMs are better than BiLSTMs, but the improvement is not that substantial. Perhaps, syntactic parsing is less accurate in the biomedical domain and this causes the observation. Interestingly, LSTMs significantly outperformed CNN in the cross-sentence setting, verifying the importance
in capturing long-distance dependencies by LSTMs.



