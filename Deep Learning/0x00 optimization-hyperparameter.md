refer: CS231n

http://cs231n.github.io/neural-networks-3/



#### Cross-validation strategy

coarse -> fine cross-validation in stages

+ First stage: only a few epochs to get rough idea of what params work
+ Second stage: longer running time, finer search … (repeat as necessary)

Tip 1: detecting explosions in the solver
If the cost is ever > 3 * original cost, break out early

Tip 2: parameter space:<br>It’s best to optimize in log space (the learning rate is multiplying your gradient update (multiplicative effect), so it makes more sense to consider a range of learning rates that are multiplied or divided by some value, rather than uniformly sampled.) ! Such as, <br>`regularize = 10 ** uniform(-5,5)`<br>` learning_rate = 10 ** uniform(-3,-6)`

Tip 3: **Careful with best values on border**. <br>It is important to double check that the best learning rate is not at the edge of this interval. For example, `learning_rate = 10 ** uniform(-6, 1)`, the border value is `10**-6=1e-06` and `10**1=10`.

#### Random Search vs. Grid Search

As argued by Bergstra and Bengio in [Random Search for Hyper-Parameter Optimization](http://www.jmlr.org/papers/volume13/bergstra12a/bergstra12a.pdf), “randomly chosen trials are more efficient for hyper-parameter optimization than trials on a grid”. 





















