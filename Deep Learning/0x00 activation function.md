https://en.wikipedia.org/wiki/Activation_function

refer: Deep Learning Book, CS231n, http://cs231n.github.io/neural-networks-1/



#### Sigmoid

$$
\phi(a) = \frac{1}{1+e^{-a}}
$$

Advantages:

+ Squashes numbers to range [0,1].

+ Historically popular since they have nice interpretation as a saturating “firing rate” of a neuron.

Disadvantages:

+ Saturated neurons “kill” the gradients. It is more prone to discarding information due to **saturation** both in forward propagation and in back propagation. (What happens when x = -10 or x = 10?)

+ Sigmoid outputs are not zero-centered. (Consider what happens when the input to a neuron (x) is always positive...What can we say about the gradients on w? Always all positive or all negative :(. This could introduce undesirable zig-zagging dynamics in the gradient updates for the weights. However, notice that once these gradients are added up across a batch of data the final update for the weights can have variable signs, somewhat mitigating this issue.) <u>This is also why you want zero-mean data ! (It's only helps at the first layer of your network.)</u> 

+ exp() is a bit compute expensive.

#### Softmax

$$
\phi(a) = softmax(a) = \frac{e^{a_i}}{\sum_j e^{a_i}}
$$

$\sum_i \phi_i(a)=1$ and $\phi_i(a) > 0$.





#### tanh

$$
\phi(a) = \tanh(a)
$$

Connection to sigmoid:
$$
\tanh(x) = 2 \times sigmoid(2x) - 1
$$



Advantage:

+ It is easier optimization with stochastic gradient descent than sigmoid.

+ Squashes numbers to range [-1,1]

+ zero centered (nice)

Disadvantage:

+ still kills gradients when saturated :(

##### question

why it's effect?

### Piecewise linear units

Piecewise linear units, such as absolute value rectifiers and rectified linear units.

Advantage: <br>propagate information easier<br>optimization easier<br>regularize easier<br>



#### ReLU

ReLU:  rectified linear unit (ReLU) or Rectifier or positive part
$$
\phi (a) = max(0,a)
$$
also written $\phi(a)=(a)^+$.

Variants:
$$
\phi(a) = 
\begin{cases}
a,  \ a \geq 0\\
max(0,a) + \alpha_i min(0,a), \ a < 0
\end{cases}
$$
Leaky ReLU fixes $\alpha_i$ to a small value like 0.01. Parametric ReLU or PReLU treats $\alpha_i$ as a learnable parameter.



Advantage:

- Does not saturate (in +region)
- Very computationally efficient
- Converges much faster than sigmoid/tanh in practice (e.g. 6x)
- Actually more biologically plausible than sigmoid

Disadvantage:  

+ Not zero-centered output.
+ Dead ReLU (in -region). The zero-gradient problem - They cannot learn via gradient-based methods on examples for which their activation is zero.

Solution:

1. initializing the biases to a small positive number (e.g. 0.01), but it's still possible for a rectified linear unit to learn to de-activate and then never be activated again.

2. maxout units

3. the leaky ReLU or parametric ReLU




##### question

why it's effect?



#### Leaky ReLU

$$
\phi (a) = max(0.01 \cdot a,a)
$$

Advantage:

- Does not saturate
- Computationally efficient
- Converges much faster than
  sigmoid/tanh in practice! (e.g. 6x)
- will not “die”.

Disadvantage:



#### Parametric ReLU

Parametric ReLU or PReLU
$$
\phi (a) = max(\alpha_i \cdot a,a)
$$


#### Exponential Linear Units (ELU)

$$
\phi(a) = 
\begin{cases}
a,  \ a > 0\\
\alpha_i \cdot (exp(a) - 1),\ a \leq 0
\end{cases}
$$

Advantage:

- All benefits of ReLU
- Closer to zero mean outputs
- Negative saturation regime compared with Leaky ReLU adds some robustness to noise 

Disadvantage:

+ Computation requires exp()



#### Maxout

It generalizes the rectifier but introduces multiple weight vectors $w_i$ (called filters) for each hidden unit.
$$
h_i = max_i(b_i + w_i \cdot x)
$$



Advantage: 

- Does not have the basic form of dot product -> nonlinearity
- Generalizes ReLU and Leaky ReLU
- Linear Regime! Does not saturate! Does not die!

+ ...Specifically, if the features captured by $n$ different linear filters can be summarized without losing information by taking the max over each group of $k$ features, then the next layer can get by with $k$ times fewer weights. Because each unit is driven by multiple filters, maxout units have some redundancy that helps them to resis forgetting how to perform tasks that they were trained on in the past.

Disadvantage:

+ doubles the number of parameters/neuron :(. Due to the greater number of weight vectors, maxout units typically need extra regularization such as dropout.



### Summary

TLDR: In practice:
- Use ReLU. Be careful with your learning rates
- Try out Leaky ReLU / Maxout / ELU
- Try out tanh but don’t expect much
- Don’t use sigmoid





