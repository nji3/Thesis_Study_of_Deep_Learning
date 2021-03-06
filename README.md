# Deep Learning Study Tutorial

## Optimization

<div align="center">
        <img src="https://github.com/nji3/Deep_Learning_Study_Tutorial/blob/master/readme_images/optim_gd.png" width="400px"</img> 
</div>

Gradient Descent is a very common scheme of optimization algorithms. It is very useful to find the global/local minimum of the loss function we used to do the training of the model. The most foundmental types of gradient descent methods are the batch gradient descent, mini-batch gradient descent and the stochastic gradient descent. The convergence of these optimization algorithms is proven years ago.

For the deep learning model, the stochastic gradient descent and the mini-batch gradient descent become very popular to train the loss function because they are functional as a kind of regularization to the model complexity. People now use very advanced optimization method based on the stochastiv gradient descent with an adaptive learning rate. Adam is one of the most used optimization algorithm in the deep learning field.

## Convolutional Neural Networks

<div align="center">
        <img src="https://github.com/nji3/Deep_Learning_Study_Tutorial/blob/master/readme_images/cnn_cs231n_nn_vs_cnn.jpeg" width="400px"</img> 
</div>

A convolutional neural network consists of an input and an output layer, as well as multiple hidden layers. The hidden layers of a CNN typically consist of convolutional layers, RELU layer i.e. activation function, pooling layers, fully connected layers and normalization layers.

<div align="center">
        <img src="https://github.com/nji3/Deep_Learning_Study_Tutorial/blob/master/readme_images/cnn_structure.png" width="400px"</img> 
</div>

The CNN model is designed to apply an cross-correlation operation (in Math) inspired by the convolution operation into the Nueral Networks' structure. We execute a convolution by sliding the filter over the input. At every location, a matrix multiplication is performed and sums the result onto the feature map. It could help extract the small features of the image rather than summarize the whole image together. More layers or more filters the model has, more specific the extracted features will be. For instance, rather than learn the whole human image together, CNN would extract the nose, eyes, mouth and etc. seperately. However, one disadvatage is that CNN could not extract/recgnize the specific location of the extracted features. Now, a Capsule Network presented by Hinton in 2017 is believed to improve this problem efficiently.

## Autoencoder and VAE(Variational Autoencoder)

### Autoencoder

<div align="center">
        <img src="https://github.com/nji3/Deep_Learning_Study_Tutorial/blob/master/readme_images/ae_structure.png" width="400px"</img> 
</div>

The Autoencoder model is a structure consists of one top-down model and a bottom up model. These two models are called encoder and the decoder. It will compress the information first and then release the information again. 

The basic idea is to use layers of neural networks to encode the original data (images or the sequences) into a low-dimensional vectors of values first. It's like a summarization of the high-dim data by the low-dim data. However, not like PCA, with the neural networks sturcture, the original data would be sent to a high dimensional space first and then to a very low dimensional space.

By using the ConvNet, the decoder layers would be called Deconv layers. It would reconstruct images simlar to the original images. The decoder part could be used as a image generator.

### Variational Autoencoder

<div align="center">
        <img src="https://github.com/nji3/Deep_Learning_Study_Tutorial/blob/master/readme_images/vae_structure.png" width="400px"</img> 
</div>

The VAE is a unsupervised learning method used to generate images similar to the training images. Not like the simple autoencoder model, the VAE tries to learn the distribution of the latent layer from the distribution of the training data and then use the laten layer distribution to learn an approximation distribution to the true distribution. There are several tricks used in the design of the VAE structure and we could explian it in a way of EM algorithm. I will write the detailed derivation later.

## Conditional Variational Autoencoder

Conditional Variational Autoencoder is based on the assumption of VAE with a improvement of introducing new conditioning parts for the probability density. We could look at the object functions for VAE and CVAE. The difference is very clear.

The VAE:

<div align="center">
        <img src="https://github.com/nji3/Deep_Learning_Study_Tutorial/blob/master/readme_images/VAE_object.png" width="600px"</img> 
</div>

The CVAE:

<div align="center">
        <img src="https://github.com/nji3/Deep_Learning_Study_Tutorial/blob/master/readme_images/CVAE_object.png" width="600px"</img> 
</div>

Now, the real latent variable is distributed under P(z|c), That is, it’s now a conditional probability distribution (CPD). Think about it like this: for each possible value of c, we would have a P(z). We could also use this form of thinking for the decoder.

This would give a chance to learn the distribution of specific groups of images. Like the hand writing digits seperated by labels, the human face images seperated by genders or even the image inpainting conditioning on the incomplete image.

## Generative Adversarial Network

<div align="center">
        <img src="https://github.com/nji3/Deep_Learning_Study_Tutorial/blob/master/readme_images/gan_schema.png" width="400px"</img> 
</div>

Not like the VAE, the GAN is a competition between the Generator and the Discriminator. VAE tries to learn a distribution that catches/averages all the modes of the original distribution. However, GAN just want to approximate one mode of the true distribution perfectly. This is one reason that GAN could generate better images. We would want to train the GAN model in seperated steps. First generator would genrate new images and the combined data of generated images and the true images are used to train the discriminator for a binary classification task. Then the discriminator will be frozen, and the generator will be trained in a way of generating fake images with labels saying that these images are real. By iterating these two steps, we could finally have very good fake images.

## Image Fill

I'm currently working on a thesis for filling incomplete images. It's generally a intuitive guide about how to use popular deep learning methods to accomplish the image impainting tasks. For real life images, it would be better to fill any random holes. Here for convinence, I would just use the images with missing patches in the center. Below is an example.

<div align="center">
        <img src="https://github.com/nji3/Deep_Learning_Study_Tutorial/blob/master/readme_images/car_incomp_exp.png" width="800px"</img> 
</div>

What's the application for this task? In real life, if something you don't want appears in the image, you could just wipe that part out and reconstruct it. This could be a simple example of why we want to do this task.
