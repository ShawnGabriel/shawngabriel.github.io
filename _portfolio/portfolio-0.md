---
title: "Stable Diffusion From Scratch"
excerpt: "<img src='/images/DeepView.jpg'><br/><br/>
<strong>2nd Place of UBC DSCI x DarkVision Computer Vision Hackathon<strong>
<br/>"
collection: portfolio
---

We model our data as a big joint distribution. Then, we learn the parameters through neural networks. Goal: learn the complex distribution so we can generate new data.

## The Math
Forward Process 'q': Markov chain of noisification which is a series of Gaussians that add noise. Overall, the forward process involves parameters used in our mean and variance are already known to us, as we initially start with our original image which we add noise little by little until it becomes fully noisified.

Reverse Process 'p': On the other hand, the parameters used for the mean and variance are unknown. The mean is calculated by neural networks and the variance is parameterized by. So, we start off with something noisy, then we would want the next image to be less noisy.

A lower bound for the quantity Theta is called the Evidence Lower Bound (ELBO). If we maximize the lower bound, it will maximize the likelihood of our data. We do this trhough training a network called ϵ_θ that given a noisy image at time stamp t and the time stamp when the noise was added (also t), it could predict how much noise is in the noisified image. If we do gradient descent on the loss function, we will maximize the ELBO and the likelihood of our data.

#### How can we create images that match our specific requirements?
Starting from the pure noise, we introduce a signal called a prompt/context which influences the model on how to remove the noise so the output move towards what we want. There's a reason as to why we don't want a prompt during the training of our model. It makes the model a conditioned model, where it's only capable of denoisifying images related to our prompt. On the other hand, an unconditioned model is where there is no prompt at all. The use of both a conditioned and an unconditioned model is called **classifier guidance**.

#### How to condition the reverse process?
If we instead replace the prompt with a zero, we would make the model both a conditioned and an unconditioned model, telling it to denoisfy whatever is present on the image on its own; this is called **classifier-free guidance**.
output = w * (output_conditioned - output_unconditioned) + output_unconditioned
where w is a weight that indicates how much we want the model to pay attention to the conditioning signal (prompt). The higher this value, the more our output will resemble our prompt.

#### CLIP (Contrastive Language-Image Pre-training)
A model built by OpenAI that allowed to connect text with images. So in the CLIP, we only utilize text embeddings for Stable Diffusion, as a conditioning signal for our model to denoise the image into what we want.

### VAE (Variational Autencoder)
We use this to compress the data, as we are not learning the distribution p(x) of our data set of images, but rather, a latent version of it. Hence, the name Stable Diffusion/Latent Diffusion. A Diffusion model is a model that progressively corrupts the data by adding noise and learns to reverse this process to generate new data from pure noise. A traditional autoencoder doesn't give semantic relationships between the data encoded and its vector representations.

Instead of a vector as per the traditional autoencoder, VAE encodes the data into two vectors representing the mean and the variance of a probability distribution that defines a latent space. That way, when training is initially started, a random initialization is chosen, but through the reconstruction loss and KL divergence, it will correct the data to which most represents our original data AND is able to generate new samples that have some resemblance to the original data.

It samples through the reparameterization trick, where the initialization of z involves epsilon, an additional variable that introduces stochasticity. This allows our model to perform backpropagation and update its weights. Note, the updated weights are the μ and σ, not ε. It is shown as:
z = μ + σ ⊙ ε

Last thing I would like to address, how does the encoder compress the whole image into the normal distribution in the first place?
It does that by capturing meaningful features of the image, which is segmented into separate latent dimensions. Each dimension will then hold a distinctive feature of the image, such as lighting, smile, head tilt, etc. After initializing the categories of the latent dimensions, training occurs through random initializations of epsilon and the parameters mu and sigma are updated according to the reconstruction loss and KL divergence.

More of my insights [here](https://shawngabriel.github.io)!
