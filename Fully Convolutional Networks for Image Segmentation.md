- Fully Convolutional Networks for Image Segmentation: https://people.eecs.berkeley.edu/~jonlong/long_shelhamer_fcn.pdf
It took me for a while to understand the paper, mainly because my lack of relevant background. The paper addresses one of the most difficult problems in AI: image segmentation (a.k.a. pixel-label labeling, dense prediction problem). Perhaps, its most important idea is to propose an end-to-end learning of a simple deconvolution to approach the problem. The deconvolution is implemented as bilinear interpolation, but it can be implemented as a deconvolution network that is composed of
deconvolution and unpooling layers (see this http://www.cv-foundation.org/openaccess/content_iccv_2015/papers/Noh_Learning_Deconvolution_Network_ICCV_2015_paper.pdf)

There are several things I don't quite get yet, mainly with my very limited background:
First and most importantly, I wonder whether the final layers of the encoder have to be with the size of 1x1xdepth? I don't think it has to be that way (e.g. see https://arxiv.org/pdf/1511.00561.pdf), but I am not so sure why it is so common with the architecture (e.g. see http://www.cv-foundation.org/openaccess/content_iccv_2015/papers/Noh_Learning_Deconvolution_Network_ICCV_2015_paper.pdf)
Second, I don't really have background of bilinear interpolation, and to me a decoder makes more sense than that technique. Why do the authors use it instead?
Third, I don't see why the encoder has to be a fully convolutional network. To me having several fully-connected layers at the end would be still fine (or could be even better abeit there are tons of more parameters).
Finally, applying Dilated Convolutions seems to be a very good idea to help image segmentation  (see this https://arxiv.org/abs/1511.07122). I admit I don't get this point though, but I believe this is just a matter of time and I need to think a bit more about it.



It is very pleased to know how people addressed this very hard problem with autoencoder-decoder. Nonetheless, I was wondering instead of using an encoder-decoder, are there other types of models that can produce such a heat map for each image?
