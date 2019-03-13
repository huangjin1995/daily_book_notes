more refer:

Automatic differentiation in machine learning: a survey [arxiv](https://arxiv.org/abs/1502.05767) (last revised 5 Feb 2018)

refer: <br>Deep Learning book<br>[Calculus on Computational Graphs: Backpropagation](http://colah.github.io/posts/2015-08-Backprop/)



### Backpropagation

... it can easily be generalized to arbitrary families of parametrized functions (for which computing a gradient is meaningful) and their corresponding computational graph ...

The basic idea of the back-propagation algorithm is that the partial derivative of the cost $J$ with respect to parameters $\theta$ can be decomposed recursively by taking into consideration the composition of functions that relate $\theta$ to $J​$, via intermediate quantities that mediate that influence, e.g., the activations of hidden units in a deep neural network.

### Automatic differentiation 

Automatic differentiation of a function with $d$ inputs and $m$ outputs can be done either by carrying derivatives forward, known as forward mode computation, or carrying them backwards, known as backward mode computation. 

The former is more efficient when $n < m$ and latter is more efficient when $d > m$. (<u>How to understand it</u>?)



Motivation: For [multivariate chain rule](https://en.wikipedia.org/wiki/Chain_rule#Higher_dimensions),  we can use “sum over paths” rule, but it’s very easy to get a combinatorial explosion in the number of possible paths.

The backpropagation algorithm is efficient because it employs **a dynamic programming strategy** to reuse rather than re-compute partial sums associated with the gradients on intermediate nodes.

Example:

![chain-def-greek](https://github.com/bifeng/daily_book_notes/raw/master/resource/chain-def-greek.png)

In the above diagram, there are three paths from $X​$ to $Y​$, and a further three paths from $Y​$ to $Z​$. If we want to get the derivative $\frac{\partial Z}{\partial X}​$ by summing over all paths, we need to sum over $3 * 3 = 9​$ paths:
$$
\frac{\partial Z}{\partial X} = \alpha\delta + \alpha\epsilon + \alpha\zeta + \beta\delta + \beta\epsilon + \beta\zeta + \gamma\delta + \gamma\epsilon + \gamma\zeta
$$
The above only has nine paths, but it would be easy to have the number of paths to grow exponentially as the graph becomes more complicated.

Instead of just naively summing over the paths, it would be much better to factor them:
$$
\frac{\partial Z}{\partial X} = (\alpha + \beta + \gamma)(\delta + \epsilon + \zeta)
$$
This is where “forward-mode differentiation” and “reverse-mode differentiation” come in. They’re algorithms for efficiently computing the sum by factoring the paths. Instead of summing over all of the paths explicitly, they compute the same sum more efficiently by merging paths back together at every node.

#### forward-mode differentiation

![chain-forward-greek](https://github.com/bifeng/daily_book_notes/raw/master/resource/chain-forward-greek.png)



#### reverse-mode differentiation

![chain-backward-greek](https://github.com/bifeng/daily_book_notes/raw/master/resource/chain-backward-greek.png)



#### Summary

The reverse-mode gives the derivatives of one output with respect to all inputs. If a function with a million inputs and one output, and we want to calculate the derivatives of the cost with respect to millions, or even tens of millions of parameters, for use in [gradient descent](https://en.wikipedia.org/wiki/Gradient_descent). So, reverse-mode differentiation, called backpropagation in the context of neural networks, gives us a massive speed up!

The forward-mode gives us the derivatives of all outputs with respect to one input. If one has a function with lots of outputs, forward-mode differentiation can be much, much, much faster.





