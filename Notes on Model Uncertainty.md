Notes on Model Uncertainty (Regarding to Bayesian Deep Learning)

1. Edward = TensorFlow + Random Variables + Inference Algorithms

2. Deep neural networks: many parameters; very prone to overfitting; require large data sets

3. Optimising any neural network with dropout is equivalent to a form of approximate Bayesian inference

4. A network trained with dropout already is a Bayesian Neural Network!

5. "typical training of neural networks requires lots of labeled data to control the risk of overfitting. And the problem becomes harder when it comes to real world regression tasks. These tasks often have smaller training data to use, and the high-frequency characteristics of these data often makes neural networks easier to get trapped in overfitting." http://zhusuan.readthedocs.io/en/latest/bayesian_nn.html

6. "In BNN, the approximate distribution is usually further simplified by factorizing it into independent distributions for each weight layers (mean field approximation). This approximation creates larger bias and can be problematic in the deep neural network." https://becominghuman.ai/learning-note-dropout-in-recurrent-networks-part-1-57a9c19a2307
