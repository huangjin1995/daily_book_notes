refer: Deep Learning book

... it can easily be generalized to arbitrary families of parametrized functions (for which computing a gradient is meaningful) and their corresponding computational graph ...

The basic idea of the back-propagation algorithm is that the partial derivative of the cost $J$ with respect to parameters $\theta$ can be decomposed recursively by taking into consideration the composition of functions that relate $\theta$ to $J$, via intermediate quantities that mediate that influence, e.g., the activations of hidden units in a deep neural network.

