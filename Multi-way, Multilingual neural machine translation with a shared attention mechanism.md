- Multi-way, Multilingual neural machine translation with a shared attention mechanism http://www.aclweb.org/anthology/N16-1101

This paper addresses an interesting problem: how to build a multi-way, multilingual NMT. 
Having a seq2seq that handles multilingual tasks is somewhat trivial. The tricky part is about attention mechanism. Given one source language and multiple target languages, it is trivial to build
different NMT with separate attention mechanisms. But it is not the case with multiple source and target languages at the same time. Doing so is quite expensive, and more importantly, having different attention mechanisms makes it less likely for the model to benefit from having multilingual translation. 

But how to build a NMT with a single shared attention mechanism?



