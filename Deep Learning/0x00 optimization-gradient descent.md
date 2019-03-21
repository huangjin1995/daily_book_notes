http://cs231n.github.io/optimization-1/



### Gradient descent

缺点：理论上，利用所有样本进行计算可以使loss降到最小，然而，实际上很容易陷入局部最小值或鞍点。此外，每一次迭代的计算量也非常大。







### Mini-batch gradient descent

假设条件：mini-batch的数据分布近似于训练数据的分布

So, the gradient from a mini-batch is a good approximation of the gradient of the full objective. Therefore, much faster convergence can be achieved in practice by evaluating the mini-batch gradients to perform more frequent parameter updates.



### Stochastic gradient descent

(or also sometimes **on-line** gradient descent)

SGD technically refers to using a single example at a time to evaluate the gradient, you will hear people use the term SGD even when referring to mini-batch gradient descent (i.e. mentions of MGD for “Minibatch Gradient Descent”, or BGD for “Batch gradient descent” are rare to see), where it is usually assumed that mini-batches are used. 

优点：随机性，有利于跳出鞍点。

缺点：训练耗时，样本差异较大会使训练比较震荡





### Problems with SGD

1. What if loss changes quickly in one direction and slowly in another? What does gradient descent do?

This is referred to the loss function has high **condition number**: ratio of largest to smallest singular value of the Hessian matrix is large.

The gradient descent will Very slow progress along shallow dimension, jitter along steep direction (zigzagging behavior). This problem actually becomes much more common in <u>high dimensions</u>.

2. What if the loss function has a local minima or saddle point?

Zero gradient, gradient descent gets stuck. Saddle points much more common in <u>high dimension</u>.

3. What if the minibatches is just getting noisy estimate of the gradient at our current point (not the true information about the gradient) ?

Our gradients come from minibatches so they can be noisy, then vanilla SGD kind of meanders around the space and might actually take a long time to get towards the minima.

### Question

Why the zigzagging behavior will happen? (condition number)





### SGD + Momentum

... equations and graph illustration



Intuition: You can think of the velocity equation as a smooth moving average of you recent gradients with kind of a exponentially decaying weight on your gradients going back in time.



We step in the direction of our velocity vector rather than the direction of our raw gradient vector.

a weighted average of velocity and gradient, it helps overcome some noise in our gradient estimate.



+ How to deal with the problem of SGD by momentum?

When we pass that point of local minima (or saddle points), the point will still have velocity even if it doesn't have gradient (or gradient is very small).

high condition number problem - our velocity will just keep building up and will actually accelerate our descent across that less sensitive dimension...

minibatches noise problem - we're building up this velocity over time, the noise kind of gets averaged out in our gradient estimates...

#### Nesterov Momentum

... equations and graph illustration



Intuition: a weighted difference between our current velocity and our previous velocity. It's  incorporate some kind of error-correcting term.



Change of variables $\tilde{x}_t= x_t + \rho v_t ​$ and rearrange:



$\tilde{x}_{t+1} = \tilde{x}_t + v_{t+1} + \rho(v_{t+1} - v_t)​$



#### Question

why the original nesterov momentum is annoying? (usually we want update in terms of $x_t$)  **read the paper**

1 - the gradient of $x_t$ is unrelated to $\rho v_t$ terms ($\bigtriangledown f(x_t + \rho v_t)$) ? 

2 - tensorflow code ?

What if the minima call lies in very narrow basin (sharp minima), will the velocity just to skip right over that minima? 

1 - if you have a very sharp minima, that actually could be a minima that overfits more.

2 - if we collect more training data, maybe that very sensitive minima would actually disappear

So, with this intuition, we maybe want to land in very flat minima because those very flat minima are probably more robust and generalize better. 



### AdaGrad

... equations and graph illustration



Added element-wise scaling of the gradient based on the historical sum of squares in each dimension



+ How to deal with the problem of SGD by AdaGrad ?

Q: What happens with AdaGrad? (condition number)

For small gradient, we add the sum of the squares of the small gradient, we are going to be dividing by a small number, so we'll accelerate movement  

For large gradient, ... we slow down our progress

Q2: What happens to the step size over long time?

The steps actually get smaller and smaller. As you approach a minima, you want to slow down so you actually converge, but you might get stuck in a saddle point.

### RMSProp

Intuition:

a momentum over the squared gradients



### Adam

Intuition:

first moment - gradients (velocity) and bias correction

second moment - squared gradients and bias correction



Adam with beta1 = 0.9, beta2 = 0.999, and learning_rate = 1e-3 or 5e-4 is a great starting point for many models! 



+ How to deal with the problem of SGD by Adam ?

Q: What happens at first timestep?

If we initialized our second moment estimate was zero, then sometimes there is a very large step at the beginning. So, we need the bias correction. 





### AdaBound

Based on Luo et al. (2019). [Adaptive Gradient Methods with Dynamic Bound of Learning Rate](https://openreview.net/forum?id=Bkg3g2R9FX). In *Proc. of ICLR 2019*.

https://github.com/Luolc/AdaBound



