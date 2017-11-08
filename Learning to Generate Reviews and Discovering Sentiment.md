- Learning to Generate Reviews and Discovering Sentiment - https://arxiv.org/pdf/1704.01444.pdf

I am not an expert by any means. So I simply put my comments on the paper here, and hope someone would correct me if I was wrong at some points.

I found this paper interesting because of two things. First, several things from the paper are new to me. Second, I like the way the authors make a very good story from their experiments.

Unsupervised representation learning is very promising since unlabeled data are every where. But to date, supervised learning models still outperform unsupervised models. This may be explained because "supervised approaches have clear objectives that can be directly optimized". Meanwhile, "unsupervised approaches rely on proxy tasks such as reconstruction, density estimation, or generation, which do not directly encourage useful representations for specific tasks." The paper exploits other perspectives: distributional issue and the limited capacity of current unsupervised representation learning models. Specifically, "current generic distributed sentence representations may be very lossy - good at capturing the gist, but poor with the precise semantic or syntactic details which are critical for applications." This combines with the limited capacity may be the root of devil, and the authors investigate into details this point.

How? The authors first attempts to learn an unsupervised representation by training byte (character) level language modelling. Then we can use the outputs to train a sentiment analysis classifier. The authors trained their model on a very large dataset (Amazon review dataset) (the training took 1 month!)

Given a new text (paragraph, article or whatever), we simply perform some pre-processing and then feed the text into the mLSTM. Here is the interesting thing: we then get the outputs of all the output units (there are 4,096 units) and consider them as a feature vector representing the string read by the model. We turned the model into a sentiment classifier by taking a linear combination of these units, learning the weights of the combination via the available supervised data. This is new to me, indeed.

What is next? By inspecting the relative contributions of features, they discovered a single unit within the LSTM that directly corresponds to sentiment. This is a very surprising finding, as remember that the mLSTM model is trained only to predict the next character in text.

But why is it the case? It is indeed an open question why the model recovers the concept of sentiment in such a precise way. It is pity, however, that the authors don't dig into details to have a satisfied answer!

Overall I like the paper and like their interesting findings. This is a very cool work!

But I think the paper could be significantly improved in two ways:

- I don't think the story written in the paper is really coherent.

- The findings are interesting but a deeper investigation would satisfy readers more. So far everything is still as "I read a very cool paper which shows that there exists a neural sentiment neuron by simply training language modeling, but I don't know why!". 
