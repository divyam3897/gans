## Introduction
Deep Convolutional GAN, or DCGAN uses convolutional layers in the generator and discriminator. Keras implementation of [Deep Convolutional Generative Adversarial Networks](http://arxiv.org/abs/1511.06434) which is a stabilize Generative Adversarial Networks.

## Architecture guidelines for stable Deep Convolutional GANs  
• Replace any pooling layers with strided convolutions (discriminator), allowing the network to learn
its own spatial downsampling and fractional-strided convolutions (generator), allowing it to learn its own
spatial upsampling.  
• Use batchnorm in both the generator and the discriminator: This stabilizes learning by normalizing the
input to each unit to have zero mean and unit variance. Directly applying batchnorm to all layers
however, resulted in sample oscillation and model instability. This was avoided by not applying
batchnorm to the generator output layer and the discriminator input layer.  
• Remove fully connected hidden layers for deeper architectures.  
• Use ReLU activation in generator for all layers except for the output, which uses Tanh. It was observed that using a bounded activation allowed the model to learn more quickly to saturate and cover the color space of the training distribution.  
• Use LeakyReLU activation in the discriminator for all layers. This was in contrast to the original GAN paper, which
used the maxout activation.  

![Architecture](dcgan.png)

## Results 
| | | |
|:-------------------------:|:-------------------------:|:-------------------------:|
|<img width="1604" alt="" src="https://github.com/divyam3897/gans/blob/master/dcgans/results/relu_generated_image.png">  Image generated with relu without batch norm |  <img width="1604" alt="" src="https://github.com/divyam3897/gans/blob/master/dcgans/results/generated_image_batch_norm_relu.png">Relu with batch norm|<img width="1604" alt="" src="https://github.com/divyam3897/gans/blob/master/dcgans/results/generated_200_epochs.png"> Tanh with 200 epochs, no batchnorm|
|<img width="1604" alt="" src="https://github.com/divyam3897/gans/blob/master/dcgans/results/no_batch_norm_disc_tanh.png"> Tanh with no batch norm in discriminator  |  <img width="1604" alt="" src="https://github.com/divyam3897/gans/blob/master/dcgans/results/gen_disc_tanh_bachnorm.png"> Tanh with batch norm in generator and discriminator|<img width="1604" alt="" src="https://github.com/divyam3897/gans/blob/master/dcgans/results/tanh_batch_noise_gen.png"> Gaussian noise in generator with tanh and batch norm|
