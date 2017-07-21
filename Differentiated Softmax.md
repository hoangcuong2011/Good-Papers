-  Differentiated Softmax - http://www.aclweb.org/anthology/P16-1186

An interesting method to scale up training large neural nets is Differentiated Softmax (D-Softmax). 
I found this method interesting because of two reasons. First, the intuition make senses: Frequent words allow us to fit
more parameters to them, while rare words only allow to fit a few. Different words require a different number of parameters, 
so does the output layer. Second, this reminds me an interesting work of Variable Computation in Recurrent Neural Networks - https://arxiv.org/abs/1611.06188
(If you have read it yet, you can take a look at my notes on the paper https://github.com/hoangcuong2011/Good-Papers/blob/master/Variable%20Computation%20in%20Recurrent%20Neural%20Networks.md).
Let us consider sequential data such as audio. There are time periods where we don't hear anything (i.e. silence). 
It makes sense to create a model that does much less computation in those cases. The technique to handle this is more fancy :
we create a network that aims to do only one thing: predict how much computation we should does given an input.
The technique in D-Softmax is far simpler
