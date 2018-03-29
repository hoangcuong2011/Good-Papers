- Distant Supervision for Relation Extraction via Piecewise Convolutional Neural Networks - http://www.emnlp2015.org/proceedings/EMNLP/pdf/EMNLP203.pdf

This is a very good paper, showing how we can improve relation extraction using distant supervision by two things. First, instead of
extracting features manually (which could be wrong due to the error derived from existing NLP tools), we just need to use neural networks to extract them automatically. Second, instead of making an assumption
that the relation between two entities that are found in a KB always directly applies to the (unlabeled) text, this paper focuses 
on improving this as sometimes it is not the case that it is true.

Let us first focus on the second issue. The way the authors address the problem is to rely on multi-instance learning. It sounds fancy but
in fact it is very simple. We first put all sentences that have the same pair of entities with an exact relation type to a bag.
Multiple instance is a learning paradigm that addresses the classification problem in the specific context: if at least
one example in a bag is positive, than the bag is labeled positive. Otherwise if none of the examples in the bag is positive, than we
label the bag as negative. Here, instead of using the information relating to all instances in a bag to train the model, we rather use only
the instance that we believe they are truly correct. This makes sense that at least one of the instances in a bag should
refer to the relation type it is refered in KB. It, however, does not make much sense that we use only information regarding to 
such an instance and ignore the rest of other instances. Despite this, they show improvements by doing so.

To address the second issue, the authors adapt convolutional archiecture to automatically learn relevant features without complicated NLP preprocessing. Specifically,
given an input sentence each input word token is transformed into a vector by looking up pre-trained word embeddings. They also use position features to specify entity pairs, which are also transformed
into vectors. In the end, each sentence is transformed into a matrix wiht size s times d, where s is the sentence length and
d is total size of word and position embedings. The next step is to apply convolution layers into the matrix. This can be done by taking the dot product of a weight
matrix w with size filtersize times d, where d, as mentioned before is the total size of word and position embedings.In the end,
this results in a sequence of vector with fixed length (the specific length depends on the way we do zero-padding). Let us assume
we use n filters, and this results in a matrix with size n times fixed length.

The next step is to do max-pooling and then apply a non-linear function at the output. The author modifies the max-pooling a bit. First,
they segment each sequence of vector (that is an output of applying each convolution filter) into three different segments (see Figure 3).
They do max-pooling on the segments separately. This results in an output vector of length n * 3, where n is the number of filters.
They call such a technique as piecewise max pooling. I am not so sure how they split the segments, though. Perhaps they rely on the position
of entities in the sentence.

Finally, the output will be transformed by applying a softmax layer. First, it will be transformed though a linear operation:

o = W output + b, 
b is a biased vector, W is a matrix with size n * 3 times M, where M is the number of relation types. This should be followed by a softmax function.
Dropout is applied in the layer.

