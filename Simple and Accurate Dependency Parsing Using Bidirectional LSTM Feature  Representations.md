- Simple and Accurate Dependency Parsing Using Bidirectional LSTM Feature Representations - https://arxiv.org/abs/1603.04351

This is a very good paper that focuses on feature representation for dependency. I personally learn a lot from this work. And in this note I 
would like to copy some text I found interesting from the paper. It is a well-written paper, solid experiments and provides convincing results.


- Modern approaches to dependency parsing can be broadly categorized into graph-based and transition-based parsers.
- Graph-based parsers (McDonald, 2006) treat parsing as a search-based structured prediction problem in which the goal is
learning a scoring function over dependency trees such that the correct tree is scored above all other trees.

- Transition-based parsers (Nivre, 2004; Nivre, 2008) treat parsing as a sequence of actions that produce a parse tree, and
a classifier is trained to score the possible actions at each stage of the process and guide the parsing process. 

- Perhaps the simplest graph-based parsers are arc-factored (first order) models  in which the scoring function 
for a tree decomposes over the individual arcs of the tree.  More elaborate models look at larger (overlapping) parts, 
requiring more sophisticated inference and training algorithms.

- The basic transition-based parsers work in a greedy manner, performing a series of locally-optimal decisions, and boast
very fast parsing speeds.  More advanced transition-based parsers introduce some search into the process using a beam
(Zhang and Clark, 2008) or dynamic programming.


- Regardless of the details of the parsing framework being used, a crucial step in parser design is choosing the right feature 
function for the underlying statistical model.  Recent work attempt to alleviate parts of the feature function design problem
by moving from linear to non-linear models, enabling the modeler to focus on a small set of “core” features and leaving
it up to the machine-learning machinery to come up with good feature combinations. However, the need to carefully define a
set of core features remains. 

- The BiLSTM excels at representing elements in a sequence (i.e., words) together with their contexts, capturing the element
and an ``infinite" window around it. We represent each word by its BiLSTM encoding, and use a concatenation of a minimal set
of such BiLSTM encodings as our feature function, which is then passed to a non-linear scoring function (multi-layer
perceptron).

- Traditionally, state-of-the-art parsers rely on linear models over hand-crafted feature functions. The feature functions 
look at core components (e.g. ``word on top of stack", ``leftmost child of the second-to-top word on the stack", ``distance
between the head and the modifier words"), and are comprised of several templates, where each template instantiates a
binary indicator function over a conjunction of core elements (resulting in features of the form ``word on top of stack
is X and leftmost child is Y and . . . ").

- Examples of good feature functions are the feature-set proposed by Zhang and Nivre (2011) for transition-based parsing
(including roughly 20 core components and 72 feature templates), and the featureset proposed by McDonald et al. (2005) for
graph-based parsing, with the paper listing 18 templates for a first-order parser, while the first order feature extractor in
the actual implementation’s code (MSTParser2 ) includes roughly a hundred feature templates.

- Coming up with a good feature-set for a parser is a hard and time consuming task, and many researchers attempt to reduce
the required manual effort. The recent popularity of neural networks prompted a move from templates of sparse, binary 
indicator features to dense core feature encodings fed into non-linear classifiers. Chen and Manning (2014) encode each 
core feature of a greedy transition-based parser as a dense low-dimensional vector, and the vectors are then concatenated 
and fed into a nonlinear classifier (multi-layer perceptron) which can potentially capture arbitrary feature combinations.
Weiss et al. (2015) showed further gains using the same approach coupled with a somewhat improved set of core features, 
a more involved network architecture with skip-layers, beam search-decoding, and careful hyper-parameter tuning.

- The above works tackle the effort in hand-crafting effective feature combinations. A different line of work attacks the
feature-engineering problem by suggesting novel neural-network architectures for encoding the parser state, including
intermediatelybuilt subtrees, as vectors which are then fed to nonlinear classifiers.

- Work by Vinyals et al. (2015) employs a sequence-to-sequence with attention architecture for constituency parsing. Each
token in the input sentence is encoded in a deep-BiLSTM representation, and then the tokens are fed as input to a deepLSTM 
that predicts a sequence of bracketing actions based on the already predicted bracketing as well as the encoded BiLSTM 
vectors. A trainable attention mechanism is used to guide the parser to relevant BiLSTM vectors at each stage. This
architecture shares with ours the use of BiLSTM encoding and end-to-end training. The sequence of bracketing actions can be
interpreted as a sequence of Shift and Reduce operations of a transition-based parser.

- Recurrent neural networks (RNNs) are statistical learners for modeling sequential data. The RNN model provides a 
framework for conditioning on the entire history x1:i without resorting to the Markov assumption which is traditionally
used for modeling sequences.	

- The recurrent neural network (RNN) abstraction is a parameterized function RNNθ(x1:n) mapping a sequence of n input
vectors x1:n, xi ∈ R din to a sequence of n output vectors h1:n, hi ∈ R dout. Each output vector hi is conditioned on all 
the input vectors x1:i , and can be thought of as a summary of the prefix x1:i of x1:n.

- BiRNN Training During training, the encoded vectors vi are fed into further network layers, until at some point a 
prediction is made, and a loss is incurred. The back-propagation algorithm is used to compute the gradients of all the
parameters in the network (including the BiRNN parameters) with respect to the loss, and an optimizer is used to update
the parameters according to the gradients. The training procedure causes the BiRNN function to extract from the input
sequence x1:n the relevant information for the task at hand.

- Our feature function φ is then a concatenation of a small number of BiLSTM vectors. The exact feature function is 
parser dependent and will be discussed when discussing the corresponding parsers. The resulting feature vectors are 
then scored using a non-linear function, namely a multi-layer perceptron with one hidden layer (MLP).

- Transition-based Parser: The transition-based parsing framework assumes a transition system, an abstract machine that
processes sentences and produces parse trees. The transition system has a set of configurations and a set of transitions 
which are applied to configurations. When parsing a sentence, the system is initialized to an initial configuration based 
on the input sentence, and transitions are repeatedly applied to this configuration. After a finite number of transitions,
the system arrives at a terminal configuration, and a parse tree is read off the terminal configuration. 

- In a greedy parser, a classifier is used to choose the transition to take in each configuration, based on features extracted from the configuration itself.
Given a sentence s, the parser is initialized with the configuration c (line 2). Then, a feature function φ(c) represents the configuration c as a vector, which is fed to a scoring function SCORE assigning scores to (configuration,transition) pairs. SCORE scores the possible transitions t, and the highest scoring transition tˆis chosen (line 4). The transition tˆ is applied to the configuration, resulting in a new parser configuration. The process ends when reaching a final configuration, from which the resulting parse tree is read and returned
Transition systems differ by the way they define configurations, and by the particular set of transitions available to them. A parser is determined by the choice of a transition system, a feature function φ and a scoring function SCORE. The feature function φ(c) is typically complex. Our feature function is the concatenated BiLSTM vectors of the top 3 items on the stack and the first item on the buffer. I.e.,  This feature function is rather minimal: it takes into account the BiLSTM representations of s1, s0 and b0, which are the items affected by the possible transitions being scored, as well as one extra stack context s2
The training objective is to set the score of correct transitions above the scores of incorrect transitions. We use a margin-based objective, aiming to maximize the margin between the highest scoring correct action and the highest scoring incorrect action. The hinge loss at each parsing configuration c is defined as:

 
