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













