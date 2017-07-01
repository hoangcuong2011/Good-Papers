- A Clockwork RNN - http://proceedings.mlr.press/v32/koutnik14.pdf

An interesting paper. It is challenge to train RNN to learn long-term dependencies. The paper proposes a simple modification to RNN that
learns the different dynamic time-scales inherent in complex signals efficiently.

The take-home message is that for a certain tasks (e.g. Spoken Word Classification), we should create our RNN in the way that

The neurons in the hidden layer are partitioned into K different modules. Each of the modules is assigned a clock period T. At
each time step t, only the output of modules i that satisify t mode period T_i are active. In this way, the clockwork RNN not only has significantly
less parameters, but also could significantly improves the performance, due to a better fitting to dynamic time-scales inherent in complex
signals. In the implementation, matrix weights are block-upper triangular matrix.

While the idea makes sense, I consider it as a specific tool to address a specific problem (modeling dynamic time-scales inherent in complex
signals). When it comes to Spoken word classificaiton, CW-RNN outperforms LSTM, but for other problems such as Online Handwriting
Recognition, LSTM outperforms CW-RNN substantially.
