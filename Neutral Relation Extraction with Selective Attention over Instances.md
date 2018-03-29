- *Neutral Relation Extraction with Selective Attention over Instances* (http://www.aclweb.org/anthology/P16-1200): 



An interesting paper shows how to improve relation extraction with selective attention model. 

Specifically, a key to relation extraction using distance learning is to assume that what a pair of entities in a given 
(unlabeled) text refers to exactly the relation type that is described in a knowledge base. This is obviously not correct 
and a good way to fix the problem is to use multiple-instance learning 
(see this https://github.com/hoangcuong2011/Good-Papers/blob/master/Distant%20Supervision%20for%20Relation%20Extraction%20via%20Piecewise%20Convolutional%20Neural%20Networks.md).

But the solution is rather unsatisfied and the paper proposes a better solution.  They propose a selective attention model for
learning how well each pair of entities refers to a specific relation type r. First, let us assume we have a bag S of 
all sentences x_i that contain a specific pair of entities. Our goal is to have a sort of vector like this to train the model:

S = sum_{all vectors x_i} alpha_i x_i.

The key here is how to learn alpha_i? It should be something like this:

alpha_i proportional to  x_i M r

where M is a specific matrix regarding to a specific relation type. The size of M should be a times b where
a is the fixed length of embedding r and b is the fixed length of sentence embeddings.

Of course we should have a softmax transformation of output x_i M r. And that is it. The method strikes me at how simple it is and how it can address a quite hard problem.
