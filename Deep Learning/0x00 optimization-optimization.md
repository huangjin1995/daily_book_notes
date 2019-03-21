cs231n





### optimization

#### first order optimization

(1) Use gradient form linear approximation
(2) Step to minimize the approximation

first-order Taylor expansion:





#### second order optimization

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

##### Quasi-Newton methods (BGFS most popular)

instead of inverting the Hessian (O(n^3)), approximate inverse Hessian with rank 1 updates over time (O(n^2) each).



##### L-BFGS  (Limited memory BFGS)

Does not form/store the full inverse Hessian.

- Usually works very well in full batch, deterministic mode i.e. if you have a single, deterministic f(x) then L-BFGS will probably work very nicely
- Does not transfer very well to mini-batch setting. Gives bad results. Adapting L-BFGS to large-scale, stochastic setting is an active area of research.







