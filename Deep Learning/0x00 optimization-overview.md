https://en.wikipedia.org/wiki/Hyperparameter_optimization

[Chapter 4. Hyperparameter Tuning](https://www.oreilly.com/library/view/evaluating-machine-learning/9781492048756/ch04.html) 



## manual



## grid search



## random search

Random search wasn’t taken very seriously before. This is because it doesn’t search over all the grid points, so it cannot possibly beat the optimum found by grid search. But then along came Bergstra and Bengio. They showed that, in surprisingly many instances, random search performs about as well as grid search. All in all, trying 60 random points sampled from the grid seems to be good enough.

In hindsight, there is a simple probabilistic explanation for the result: for any distribution over a sample space with a finite maximum, the maximum of 60 random observations lies within the top 5% of the true maximum, with 95% probability. That may sound complicated, but it’s not. Imagine the 5% interval around the true maximum. Now imagine that we sample points from this space and see if any of them land within that maximum. Each random draw has a 5% chance of landing in that interval; if we draw *n* points independently, then the probability that all of them miss the desired interval is $(1 – 0.05)^n​$. So the probability that at least one of them succeeds in hitting the interval is 1 minus that quantity. We want at least a 0.95 probability of success. To figure out the number of draws we need, just solve for *n* in the following equation:

$1 – (1 – 0.05)^n > 0.95​$

We get *n* >= 60.

The moral of the story is: *<u>if at least 5% of the points on the grid yield a close-to-optimal solution</u>, then random search with 60 trials will find that region with high probability*. The condition of the if-statement is very important. It can be satisfied if either the close-to-optimal region is large, or if somehow there is a high concentration of grid points in that region. The former is more likely, because a good machine learning model should not be overly sensitive to the hyperparameters, i.e., the close-to-optimal region is large.

## bayesian model-based optimization

https://towardsdatascience.com/a-conceptual-explanation-of-bayesian-model-based-hyperparameter-optimization-for-machine-learning-b8172278050f



## evolutionary optimization



## gradient-based optimization

refer: CS231n

### first order optimization

(1) Use gradient form linear approximation
(2) Step to minimize the approximation

first-order Taylor expansion:





### second order optimization

(1) Use gradient and Hessian to form quadratic approximation
(2) Step to the minima of the approximation

second-order Taylor expansion:



Solving for the critical point we obtain the Newton parameter update:



Q: What is nice about this update?

There is no hyperparameters! No learning rate!

Q2: Why is this bad for deep learning?

Hessian has O(N^2) elements
Inverting takes O(N^3)
N = (Tens or Hundreds of) Millions

#### Quasi-Newton methods (BGFS most popular)

instead of inverting the Hessian (O(n^3)), approximate inverse Hessian with rank 1 updates over time (O(n^2) each).



#### L-BFGS  (Limited memory BFGS)

Does not form/store the full inverse Hessian.

- Usually works very well in full batch, deterministic mode i.e. if you have a single, deterministic f(x) then L-BFGS will probably work very nicely
- Does not transfer very well to mini-batch setting. Gives bad results. Adapting L-BFGS to large-scale, stochastic setting is an active area of research.















