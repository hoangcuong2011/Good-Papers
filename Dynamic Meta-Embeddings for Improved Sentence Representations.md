Dynamic Meta-Embeddings for Improved Sentence Representations 

Idea: Combing pre-trained embedding resources into a single one vector. Of course I don't mean concat them together.

Two steps:

1. Projecting all embeddings into a common space (which is 250 dimension from the paper) by learned linear functions.

2. Do a combination of the embedding together with attention mechanism.

They also use another version which is what they call contextualized dynamic meta-embeddings. After perfomming step 1, we put the embedding
of words in a sentence into a bidirection LSTM. After that we do a combination of the hidden vector from LSTM instead of the word embedding themselves.

It is, however, not so clear to me is that they have the same LSTM for all meta-embeddings or they have mutliple LSTMs.

Results: convincing improvements.

