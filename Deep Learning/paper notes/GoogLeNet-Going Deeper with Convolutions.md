### motivation

The most straightforward way of improving the performance of deep neural networks is by increasing their size. This includes both increasing the depth – the number of levels of the network and its width – the number of units at each level.

However this simple solution comes with two major drawbacks.

First, Bigger size typically means a larger number of parameters, which makes the enlarged network more prone to <u>overfitting</u>, especially if the number of labeled examples in the training set is limited.

Second, uniformly increased network size is the dramatically increased use of computational resources. If the added capacity is used inefficiently (for example, if most weights end up to be close to zero), then a lot of computation is wasted.

The fundamental way of solving both issues would be by ultimately moving from fully connected to <u>sparsely connected architectures</u>, even inside the convolutions....Their main result states that if the probability distribution of
the data-set is representable by a large, very sparse deep neural network, then the optimal network topology can be constructed layer by layer by analyzing the correlation statistics of the activations of the last layer and clustering neurons with highly correlated outputs....

On the downside, todays <u>computing infrastructures</u> are very inefficient when it comes to numerical calculation on non-uniform sparse data structures. ... Also, non-uniform sparse models require more sophisticated engineering and computing infrastructure. Most current vision oriented machine learning systems utilize sparsity in the spatial domain just by the virtue of employing convolutions. However, convolutions are implemented as collections of dense connections
to the patches in the earlier layer....

This raises the question whether there is any hope for a next, intermediate step: <u>an architecture that makes use of the extra sparsity, even at filter level, as suggested by the theory, but exploits our current hardware by utilizing computations on dense matrices.</u> The vast literature on sparse matrix computations (e.g. [3]) suggests that clustering sparse matrices into relatively dense submatrices tends to give state of the art practical performance for sparse matrix multiplication.

<u>The Inception architecture</u> started out as a case study of the first author for assessing the hypothetical output of a sophisticated network **topology** construction algorithm that tries to <u>approximate a **sparse** structure implied by [2] for vision networks and covering the hypothesized outcome by **dense**, readily available components</u>. Despite being a highly speculative undertaking, only after two iterations on the exact choice of topology, we could already see modest gains against the reference architecture based on [12].

...The most convincing proof would be if an automated system would create network **topologies** resulting in similar gains in other domains using the same algorithm but with very differently looking global architecture....

### Architecture

The main idea of the Inception architecture is based on finding out how an optimal local sparse structure in a convolutional vision network can be approximated and covered by readily available dense components.

