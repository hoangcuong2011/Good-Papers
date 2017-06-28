- SoundNet - Learning Representations from Unlabeled Video - https://arxiv.org/abs/1610.09001

The paper aims to address a problem of acoustic scene classification. The task is difficult with respect to limited training data.

The paper addresses the problem by leveraging large amounts of two-million unlabeled videos. 
The rational of the method is that: (1) each video contains sound data, and (2) there exists good enough techniques that 
recognize scenes and objectives in images and videos  with good accuracy (take a look at Places365 CNNs http://places2.csail.mit.edu/download.html,
the video scene detection framework that was used in the paper). In the end, we can use Places365 to detect sences and objectives from our videos in the first place, and then learn acoustic representation 
of the sound in the videos using the detected sences and objectives as the training data. The acoustic representation will be used as features for training classifiers, using a small amount of labeled sound data.

Exploiting the natural synchronization between vision and sound seems a neat idea, but I am not sure whether this study
is the first one that proposes the idea.

Technically, SoundNet is implemented in very straightforward way (Figure 1). We have two
deep networks. The first one processes videos, and the second one processes waveforms. The outputs of the two subnetworks 
(the *distribution of categories*) should be similar given each pair of video/waveform. 
The authors use KL-divergence to implement the idea. Other options can be tried (e.g. l2). Surprisingly, l2 provides
a substantially worse than KL-divergence.

Experiments validate the soundness of the approach. Using the two-million unlabeled videos, Soundnet outperforms significantly other SOTA baselines.





