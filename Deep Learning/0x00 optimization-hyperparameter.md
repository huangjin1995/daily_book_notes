refer: CS231n

http://cs231n.github.io/neural-networks-3/

[Chapter 4. Hyperparameter Tuning](https://www.oreilly.com/library/view/evaluating-machine-learning/9781492048756/ch04.html) 

#### what are hyperparamters ?

*model parameter* - which is learned during the training phase. “Training a model” involves using an optimization procedure to determine the best model parameter that “fits” the data.

*hyperparameters* - sometimes also knowns as “nuisance parameters.” These are values that must be specified outside of the training procedure.

#### What do hyperparameters do?

A regularization hyperparameter controls the **capacity** of the model, i.e., how flexible the model is, how many degrees of freedom it has in fitting the data. Proper control of model capacity can prevent overfitting.

Another type of hyperparameter comes from the training process itself (controls the **convergence** of the model ?). Training a machine learning model often involves optimizing a loss function (the training metric). A number of mathematical optimization techniques may be employed, some of them having parameters of their own. For instance, stochastic gradient descent optimization requires a learning rate or a learning schedule. Some optimization methods require a convergence threshold. Random forests and boosted decision trees require knowing the number of total trees (though this could also be classified as a type of regularization hyperparameter). These also need to be set to reasonable values in order for the training process to find a good model.

#### Cross-validation strategy

coarse -> fine cross-validation in stages

+ First stage: only a few epochs to get rough idea of what params work
+ Second stage: longer running time, finer search … (repeat as necessary)

Tip 1: detecting explosions in the solver
If the cost is ever > 3 * original cost, break out early

Tip 2: parameter space:<br>It’s best to optimize in log space (the learning rate is multiplying your gradient update (multiplicative effect), so it makes more sense to consider a range of learning rates that are multiplied or divided by some value, rather than uniformly sampled.) ! Such as, <br>`regularize = 10 ** uniform(-5,5)`<br>` learning_rate = 10 ** uniform(-3,-6)`

Tip 3: **Careful with best values on border**. <br>It is important to double check that the best learning rate is not at the edge of this interval. For example, `learning_rate = 10 ** uniform(-6, 1)`, the border value is `10**-6=1e-06` and `10**1=10`.























