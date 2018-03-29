- Modeling Relation Paths for Representation Learning of Knowledge Bases - http://www.aclweb.org/anthology/D15-1082

This is a very good paper, showing that we can improve representation learning of knowledge base using relation paths instead of taking direct relations between entities. A similar idea
is also developed in this work https://arxiv.org/pdf/1506.01094.pdf.

At a high level, involving relation paths in training raises three difficulties:

1. we need to handle an explosive number of possible paths to train.
 
2. we need to handle the realiablity of paths. Some path makes senses: A was born in city B, B is a city of country C -> The nationality of A is C.
Meanwhile, some path does not make any sense: A is a friend of B, B works with C -> It is unlikely that A has anything to do with C.

3. relation path representation: how to create a new representation from two representations.

In order to see how the paper addresses the challenges, let me first presensent how they score relation between two 
certain entities h and t that are linked in a knowledge base.
The energy function is computed as follows:

E = E(h, r, t) + E(h, P, t):

where E(h, P, t) is a sume of all possible paths that comes from h to t:

E(h, P, t) is proportional to sum all p in paths P: R(p|h, t)E(h, p, t)

where R(p|h, t) denotes the reliability of the path, which is what we need to specifiy in (2) and E(h, p, t) is computed based on
a relation path representation in (3).

The authors address (1) in an intuitive way: we restrict the length of the graph, and we restrict the path with reliablity that
is over a certain threshold. The way they address (2) is not so clear to me. Specificially, let us assume we are given a path:
S_0 -> r1 -> S_1 -> r2 -> ... -> r_i -> S_i -> ...

At a node S_i: we compute R(path| S_0, S_i) as:

R(S_i)= \sum_{all predecessors of S_i with relation type r_i} R(predecessors)/Normalization

where Normalization = count all successors of node with relation type r_i.

What I don't get is the intuition. Does it mean that a path that has high reliablity in the case that: its predecessors do not
have many successors with the same relation type? It is also not clear to me regarding to the update: do parameters always converge?

Regarding to 3, the authors address the technical question by investing different composition operation regarding
to the embeddings of relation type (ADD, MULTIPLICATION or an RNN). None of these approaches out-perform the others in their experiments, though.







