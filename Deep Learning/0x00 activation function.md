https://en.wikipedia.org/wiki/Activation_function

refer: Deep Learning Book



#### Sigmoid

$$
\phi(a) = \frac{1}{1+e^{-a}}
$$

Disadvantages:

It is more prone to discarding information due to saturation both in forward propagation and in back propagation.



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

It is easier optimization with stochastic gradient descent than sigmoid.

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
max(0,a) + \alpha_i min(0,a), a < 0
\end{cases}
$$
Leaky ReLU fixes $\alpha_i$ to a small value like 0.01. Parametric ReLU or PReLU treats $\alpha_i$ as a learnable parameter.



Disadvantage:  The zero-gradient problem - They cannot learn via gradient-based methods on examples for which their activation is zero.

Solution:

1. initializing the biases to a small positive number, but it's still possible for a rectified linear unit to learn to de-activate and then never be activated again.

2. maxout units

3. the leaky ReLU or parametric ReLU




##### question

why it's effect?



#### Maxout

It generalizes the rectifier but introduces multiple weight vectors $w_i$ (called filters) for each hidden unit.
$$
h_i = max_i(b_i + w_i \cdot x)
$$




Advantage: ...Specifically, if the features captured by $n$ different linear filters can be summarized without losing information by taking the max over each group of $k$ features, then the next layer can get by with $k$ times fewer weights. Because each unit is driven by multiple filters, maxout units have some redundancy that helps them to resis forgetting how to perform tasks that they were trained on in the past.



Due to the greater number of weight vectors, maxout units typically need extra regularization such as dropout.







