cs231n



## Regularization

Training: Add some kind of randomness

$y=f_w(x,z)$

Testing: Average out randomness (sometimes approximate)

$y=f(x)=E_z[f(x,z)]=\int p(z)f(x,z)dz ​$



### Add term to loss

L2/L1 regularization

Elastic net (L1+L2)



### Dropout

Intuition:

1. Forces the network to have a redundant representation;
   Prevents co-adaptation of features

2. Dropout is training a large ensemble of models (that share parameters).
   Each binary mask is one model



Train time: * p

In each forward pass, randomly set some neurons to zero
Probability of dropping is a hyperparameter; 0.5 is common



Test time: *p

Dropout makes our output random!

Integral equation: ?

Using a local approximate the integral.

At test time, multiply by dropout probability. (Why?)



Inverted dropout

Train time: *1/p

Test time: test time is unchanged!

Reduce the test time for the multiply.



Q: Which layers use dropout?

It's common in fully connected layers, sometimes in convolutional layers (drop entire feature maps randomly, or drop out entire channels).

Q: What happens to the gradient during training with dropout?

We only end up propagating the gradients through the nodes that were not droppped. This has the consequence that it takes longer to train because at each steps, you're only updating some subparts of the network, but you might have a better generalization after it's converged.

### Batch Norm

Training:

Normalize using stats from random minibatches



Testing: 

Use fixed stats to normalize



### Data Augmentation

Get creative for your problem!
Random mix/combinations of :
- translation
- rotation
- stretching
- shearing,
- lens distortions, … (go crazy)



Image Data Augmentation:

+ Horizontal Flips

+ Random crops and scales

  Training: sample random crops / scales

  Testing: average a fixed set of crops

+ Color Jitter
  Simple: Randomize contrast and brightness

  

+ More Complex:

  Apply PCA to all [R, G, B] pixels in training set

  Sample a “color offset” along principal component directions

  Add offset to all pixels of a training image





### Summary

+ If you training with batch norm, sometimes you don't use drop out at all.
+ 



















