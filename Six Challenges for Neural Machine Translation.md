- Six Challenges for Neural Machine Translation - http://www.aclweb.org/anthology/W/W17/W17-3204.pdf

An interesting paper written by one of the fathers of Statistical Machine Translation. The paper is very easy to follow,
and should be considered as a must read for MT researchers. I list out several challenges here:

1. "NMT systems have lower quality out of domain, to the point that they completely sacrifice adequacy for the sake of fluency."
The paper shows that in some cases, NMT outputs are very fluent but completely not related to the input (quite funny indeed!)

2. "NMT systems have a steeper learning curve with respect to the amount of training data, resulting in worse quality in low-resource
settings, but better performance in highresource settings." - It only works well with large data!

3. Translating with low-frequency words - It is better than SMT, but there is still a large room for improvements.

4. NMT systems have lower translation quality on very long sentences. SMT performs better with such much long inputs.

5. "The attention model for NMT does not always fulfill the role of a word alignment model, but may in fact dramatically diverge."
I found this observation extremely interesting.

6. "Beam search decoding only improves translation quality for narrow beams and deteriorates when exposed to a larger search space."
I was not really surprised this this finding, though. I also observed similar phenomenon with SMT.

7. " NMT systems are much less interpretable" - Well, everybody agrees with this. "The answer to the question of why the training data leads these systems to decide on
specific word choices during decoding is buried in large matrices of real-numbered values."

An enjoy read!
