- SoundNet - Learning Representations from Unlabeled Video - https://arxiv.org/abs/1610.09001

The paper aims to address the problem of acoustic scene classification. The task is difficult with respect to limited training data. The paper addresses the difficulty by leveraging large amounts of two-million unlabeled videos. 

The rational of the approach is that: (1) each video contains sound data, and (2) there exists good enough techniques that 
recognize scenes and objectives in images and videos  with good accuracy (take a look at Places365 CNNs http://places2.csail.mit.edu/download.html,
the video scene detection framework that was used in the paper). In the end, we can use Places365 to detect sences and objectives from our videos in the first place, and then learn acoustic representation 
of the sound in the videos using the detected sences and objectives as the training data. The acoustic representation will be used as features for training classifiers, using a small amount of labeled sound data.


Technically, SoundNet is implemented in very straightforward way (Figure 1). We have two (sub)
deep networks. The first one processes videos, and the second one processes waveforms. The outputs of the two subnetworks 
(the *distribution of categories*) should be similar given each pair of video/waveform. 
The authors use KL-divergence to implement the idea. Other options can be tried (e.g. l2), of course. It is quite surprising that l2 provides a substantially worse than KL-divergence.

Experiments validate the soundness of the approach. Using the two-million unlabeled videos, Soundnet outperforms significantly other SOTA baselines.

In general, I like the paper. It is simple and nice to read. Exploiting the natural synchronization between vision and sound seems a neat idea, but I am not sure whether this study is the first one that proposes the idea.

The paper itself raises a question to me, however. That is, I am not so sure whether we should have a shared representations
between both videos and waveforms, or we should have separate representations that we should try to (indirectly) align them, somehow, as shown in the paper.


