https://en.wikipedia.org/wiki/Activation_function



#### Sigmoid

$$
\phi(a) = \frac{1}{1+e^{-a}}
$$



#### Softmax

$$
\phi(a) = softmax(a) = \frac{e^{a_i}}{\sum_j e^{a_i}}
$$

$\sum_i \phi_i(a)=1$ and $\phi_i(a) > 0$.





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

##### question

why it's effect?



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







