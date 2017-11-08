- Learning to Generate Reviews and Discovering Sentiment - https://arxiv.org/pdf/1704.01444.pdf

I found this paper interesting because of three things. First, the topic is about sentiment analysis, which I get quite interested recently.
Second, several things from the paper are new to me. Finally, I like the way the authors make a very good story from their experiments.

Specifically, the work is about unsupervised representation learning. URL is very promising since unlabeled data are
every where. Unsupervised learning is also very useful in the sense that its outputs should complement
supervised learning (e.g. pre-trained word vectors are very helpful in NLP).

But to date, supervised learning models still outperform unsupervised models. This may be explained because
"supervised approaches have clear objectives that can be directly optimized". Meanwhile, "unsupervised approaches rely on proxy tasks such as reconstruction, density estimation, or generation, which do not directly encourage useful
representations for specific tasks." The paper exploits other perspectives: distributional issue and the limited capacity of current unsuperivsed
representation learning models. Specificially, "Current generic distributed sentence representations may be very lossy - good at capturing the
gist, but poor with the precise semantic or syntactic details which are critical for applications."

The paper investigates these things by first attempting to learn an unsupervised representation by training byte (character) level language modelling.
Then it tries to use the outputs to train a sentiment analysis classifier. The authors trained their model on a very large dataset (Amazon review dataset) (the training took 1 month!)


Given a new text (paragraph, article or whatever), we simply perform some preprocessings and then feed the text into the LSTM.
Here is the interesting thing: we then get the outputs of all the output units (there are 4,096 units) and consider them as
a feature vector representing the string read by the model. We turned the model into a sentiment classifier by taking a linear combination of these units, learning the weights of the combination via the available supervised data.
This is new to me, indeed.

What is next?  By inspecting the
relative contributions of features, they discovered a single unit within the LSTM that directly corresponds to sentiment.
This is very surprising, as remember that the LSTM model is trained only to predict the next character in text.

But why???? It is indeed an open question why the model recovers the concept of sentiment in such a precise, disentangled, interpretable,
and manipulable way. It is pitty that the authors don't digg into details to have an answer!

Overall I like the paper and like their interesting findings. But I think the paper should be improved in some ways:

- I don't think the story written in the paper is really coherent.

- The findings are interesting but a more deeper investigations on why they are the case would satisfy readers more.


