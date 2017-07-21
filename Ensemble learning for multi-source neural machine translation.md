- Ensemble learning for multi-source neural machine translation - http://www.aclweb.org/anthology/C/C16/C16-1133.pdf

This paper addresses an interesting problem: How to ensemble multi-source NMT. It has been observed that combining multiple systems 
often improves performance substantially. For SMT, system combination is technicaly challenging, yet for NMT it is quite straightforward
to combine multiple NMTs. A common method is uniform weighting of the output layers: distributions over the target 
vocabulary produced by different trained instances of the same NMT architecture for the same language pair. Different instances
of NMTs can be produced by different parameter initializations, or paramater snapshots from different training epochs. Another way is
to use different equivalent source sentences in different languages to translate into the same target language.

The goal of this paper is to investigate the best way to combine individual predictors into an ensemble.

-------------------- not done yet ---------------
