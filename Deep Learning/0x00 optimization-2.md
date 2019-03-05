http://cs231n.github.io/optimization-2/

**Motivation**: Understanding of this process and its subtleties is critical for you to understand, and effectively develop, design and debug Neural Networks.

#### gradient

Keep in mind what the derivatives tell you: They indicate the rate of change of a function with respect to that variable surrounding an infinitesimally small region near a particular point:
$$
\frac{df(x)}{dx} = \lim_{h \rightarrow 0} \frac{f(x+h)-f(x)}{h}
$$
A nice way to think about the expression above is that when *h* is very small, then the function is well-approximated by a straight line, and the derivative is its slope. In other words, the derivative on each variable tells you the sensitivity of the whole expression on its value. (This can be seen by rearranging the above equation ($f(x+h)=f(x) + h \frac{df(x)}{dx}​$))

> The derivative on each variable tells you the sensitivity of the whole expression on its value.

#### backpropagation

The **forward pass** computes values from inputs to output. The **backward pass** then performs backpropagation which starts at the end and recursively applies the chain rule to compute the gradients all the way to the inputs of the circuit. The gradients can be thought of as flowing backwards through the circuit.

#### Intuitive understanding of backpropagation

...

Backpropagation can thus be thought of as gates communicating to each other (through the gradient signal) whether they want their outputs to increase or decrease (and how strongly), so as to make the final output value higher.

...









#### Question

+ Backpropagation will happen into both `logits` and `labels` ?
+ 











