How Does Batch Normalization Help Optimization?

https://arxiv.org/abs/1805.11604



refer: CS231n

https://www.zhihu.com/question/300940578





#### BatchNorm

You want unit gaussian activations?

1. Compute the empirical mean and variance independently for each dimension.
2. Normalize

Usually inserted after Fully Connected or Convolutional layers, and before nonlinearity.



It's **not clear** that we necessarily want a unit gaussian input to a tanh layer.



Advantages:

- Improves gradient flow through the network
- Allows higher learning rates
- Reduces the strong dependence on initialization
- Acts as a form of regularization in a funny way, and slightly reduces the need for dropout, maybe



Note: 

It could learn the identity mapping, but in practice it doesn't, but you still get this batch normalization effect.

At test time BatchNorm layer functions differently: The mean/std are not computed
based on the batch. Instead, a single fixed empirical mean of activations during training is used. (e.g. can be estimated during training with running averages)



#### InstanceNorm



#### LayerNorm



#### GroupNorm



