http://cs231n.github.io/optimization-1/



### visualizing the loss function

在高维的参数空间中，寻找最优权重，很难获得直观的迭代寻优过程，怎么样进行可视化呢？

可视化方法：

利用损失函数的分段线性特性，实现可视化，并提供了理论支持。



### optimization

#### strategy 1 random search

求解最优权重太难了（analytical solution），而在一个特定权重上去优化以获得更好的权重，这个问题相对简单。

核心思想：迭代优化

> Our strategy will be to start with random weights and iteratively refine them over time to get lower loss

#### strategy 2 random local search

we will start out with a random W, generate random perturbations δW to it and if the loss at the perturbed W+δW is lower, we will perform an update. 



#### strategy 3 gradient descent





### computing the gradient



#### Computing the gradient numerically with finite differences

numerical gradient: slow, approximate but easy way

the numerical gradient has complexity linear in the number of parameters.



#### Computing the gradient analytically with Calculus 

analytic gradient: fast, exact but more error-prone way that requires calculus

application:<br>**gradient check**: Unlike the numerical gradient it can be more error prone to implement, which is why in practice it is very common to compute the analytic gradient and compare it to the numerical gradient to check the correctness of your implementation.





