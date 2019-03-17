Fixup Initialization: Residual Learning Without Normalization

http://export.arxiv.org/abs/1901.09321



refer: CS231n, http://cs231n.github.io/neural-networks-2/



### Question

what happens when W=0 init is used?

all the neurons will do the same thing



### initialization

- First idea: Small random numbers
  (gaussian with zero mean and 1e-2 standard deviation)

  Works ~okay for small networks, but <u>problems with deeper networks</u>. 

  For example: tanh activation function

  1) `w=np.random.randn(in,out) * 0.01`, all activations in deeper layer collapse to zero.

  2) `w=np.random.randn(in,out) * 1.0`, almost all neurons completely saturated, either -1 and 1. Gradients will be all zero.

  Weight too small or too large is not a good choice. 

- Xavier initialization [Glorot et al., 2010]

  `w = np.random.randn(in,out)/np.sqrt(in)`

  Reasonable initialization. (Mathematical derivation assumes linear activations)

  Works for tanh activation function, but when using the ReLU nonlinearity it breaks.

- He et al., 2015

  `w = np.random.randn(in,out)/np.sqrt(in/2)`



### Debug  Strategy

+ Check the activation statistics. (What do the gradients look like?)



+ 









