

more refer:

https://towardsdatascience.com/a-conceptual-explanation-of-bayesian-model-based-hyperparameter-optimization-for-machine-learning-b8172278050f and its reference (such as: http://proceedings.mlr.press/v28/bergstra13.pdf)

https://www.aclweb.org/anthology/D15-1251



prerequisite: 

https://app.sigopt.com/static/pdf/SigOpt_Bayesian_Optimization_Primer.pdf

https://papers.nips.cc/paper/4522-practical-bayesian-optimization-of-machine-learning-algorithms.pdf





### Question

+ What's the assumptions and constraints ? 

  Does it can be used in any model (model agnostic ) ?

  Assumption: each hyper-parameters are independent to each other.   

  

+ why the TPE approach outperformed the GP approach ?

  

+ when the SMBO algorithm fails ?

  1) a bad choice of  surrogate function $p(y|x)$.

  2) it extracts structure in $\cal{H}$ that leads only to a local optimum.

  

+ The assumption is conflict with the sense ?

  assumption - `many elements of hyper-parameter assignment(x) are known to be irrelevant given particular values of other elements`

  sense - `Configuration spaces are tree-structured in the **sense** that some leaf variables (e.g. the number of hidden units in the 2nd layer of a DBN) are only well-defined when node variables (e.g. a discrete choice of how many layers to use) take particular values.`

  

+ How to decide each hyper-parameters groups belongs for GP ? 

  

+ **How to setting the threshold for Expected improvement?**

  Did it need some initial steps with random choice hyperparamters for decide the threshold ?

  Did the threshold $y^*​$ always update and how ?

  What's correlation $y^*$ with $f(x^*)$ ?

  

+ How to explain the process of the hyper-parameters optimization ?

  workflow

  



### explanation

First explanation:

---

怎么对超参数优化问题建模？

y = f(x) 

其中，x为超参数，$x \in \cal{X}$，$\cal{X}$为超参数的configuration space. y为超参数下损失函数的取值，f为损失函数。

此时，超参数优化问题就定义为在configuration space下对损失函数的最优化。

那么问题来了：

1）configuration space长什么样？

2）怎么计算损失函数？

3）什么时候是最优，即如何评估？

好，那就来看看具体怎么解决这些问题。

1）两点：第一，通常将configuration space看成图结构（超参数之间相互依赖），这里将其简化，看成树结构（当前子节点仅依赖于父节点，简化了超参数之间的依赖关系）。第二，将configuration space定义为一个生成过程，用于生成有效的超参数。

这个生成过程是怎样生成的呢？

随机搜索方法，只是从这个生成过程（先验分布）中，抽取超参数并验证，再去抽取下一组超参数。

超参数优化算法，则是在已有的超参数及损失函数值的前提下，抽取下一个有效的超参数。

GP - 对每组超参数定义先验分布，如uniform, log-uniform, quantized log-uniform, and categorical variables.

TPE - 也定义了先验分布，并做了转变，如uniform $\rightarrow$ truncated Gaussian mixture, log-uniform $\rightarrow$ exponentiated
truncated Gaussian mixture, categorical $\rightarrow$ re-weighted categorical。通过历史观测的超参数$x$及其损失函数值与阈值的大小，对历史观测的超参数$x$进行非参数密度估计，从而实现对$p(x|y)$的建模。

2）从当前的configuration space拿到一组超参数，直接用真实的损失函数计算成本太高，所以采用GP和TPE两种策略进行优化，即找到一个surrogate函数来代替损失函数。

根据历史观测的超参数$x$及其对应损失函数值$f(x)$，可以构成$\cal{H}$，这里就利用GP和TPE两种策略对$\cal{H}$建模，来近似真实的损失函数。

GP - 判别式模型，直接建模$p(y|x)$；

TPE - 生成式模型，对$(x,y)$联合建模，即建模x的生成过程$p(x|y)$.

3）Expected Improvement

怎么去优化Expected Improvement，它长什么样（landscape）？

GP - ？

TPE - ？

---



Second explanation:

---

https://towardsdatascience.com/a-conceptual-explanation-of-bayesian-model-based-hyperparameter-optimization-for-machine-learning-b8172278050f

新的理解：

$p(y|x)$ 称之为损失函数的surrogate！

其中$x$为超参数，$y$为该超参数下$f(x)$的取值，$f(x)$为损失函数

surrogate函数相比损失函数更易于优化，贝叶斯方法就通过选择在surrogate函数上表现最好的超参数，作为下一组超参数在真实损失函数上验证。

设想一下，如果surrogate函数可以近似真实的损失函数，那么就可以利用surrogate函数选择表现好的超参数，这个超参数同样可以在真实的损失函数取得很好的结果。这里通过使surrogate函数最大或最小来确定超参数。

Bayesian Optimization的基本步骤：

1. **Build a surrogate probability model of the objective function**
2. **Find the hyperparameters that perform best on the surrogate**
3. **Apply these hyperparameters to the true objective function**
4. **Update the surrogate model incorporating the new results**
5. **Repeat steps 2–4 until max iterations or time is reached**

Sequential Model-Based Optimization的基本步骤：

1. **A domain of hyperparameters over which to search**
2. **An objective function which takes in hyperparameters and outputs a score that we want to minimize (or maximize)**
3. **The surrogate model of the objective function**
4. **A criteria, called a selection function, for evaluating which hyperparameters to choose next from the surrogate model**
5. **A history consisting of (score, hyperparameter) pairs used by the algorithm to update the surrogate model**



$S(x,M_{t-1})$ - 基于$x$的参数空间及上一步的概率模型$M_{t-1}$，优化Expected Improvement，从而选择下一组最优的$x^*$。

$f(x^*)$ - 基于选择的最优$x^*$，利用真实的损失函数评估。

$M_t$ - 基于历史观测的$x$及其对应的函数值$f(x)$建立的概率模型$p(y|x)$，可以利用GP/TPE两种策略建模。



下一步，就是怎么优化Expected Improvement？

GP - ...

TPE - 根据$p(x|y)$的密度函数与Expected Improvement之间的关系，发现只要从$l(x)$中抽取超参数就可以不断最大化Expected Improvement，从而确定下一组最优的超参数。



SMBO的优点 - 每次选择最优参数，从而减少迭代次数，并且每次的提升最大。

------



### summary

+ data distribution -> $p(y|x)$ (such as network structure) -> parameter search

  1) Random search is competitive with the manual optimization of deep belief networks (DBNs).

  2) Automatic sequential optimization outperforms both manual and random search.

+ 



### problem definition

loss function - ...

configuration space - the configuration space is described by a graph-structured generative process

Hyper-parameter optimization is the problem of optimizing **<u>a loss function</u>** over <u>a graph-structured configuration space</u>.

In this work we restrict ourselves to <u>tree-structured configuration spaces</u>. Configuration spaces are tree-structured in the **sense** that some leaf variables (e.g. the number of hidden units in the 2nd layer of a DBN) are only well-defined when node variables (e.g. a discrete choice of how many layers to use) take particular values. Not only must a hyper-parameter optimization algorithm optimize over variables which are discrete, ordinal, and continuous, but it must simultaneously choose which variables to optimize.

we define a configuration space by <u>a generative process</u> for drawing valid samples. <br>$\rightarrow​$ Random search is the algorithm of <u>drawing</u> hyper-parameter assignments from that process and evaluating them.<br>$\rightarrow​$ Optimization algorithms work by identifying hyper-parameter assignments that could have been <u>drawn</u>, and that appear promising <u>on the basis of</u> the loss function’s value at other points.





### objective





### Architecture

Sequential Model-Based Optimization (SMBO)

（根据每次给定的超参数，重新训练模型并验证该组参数是否最优，当数据量大时，这种方式成本太高。SMBO采用替代模型来评估，并且考虑历史观测值（最优参数）选择下一次迭代的最优参数）

$x​$ - hyper-parameters

$y​$ - loss function’s value

$f$ - loss function of the model

$M​$ - the surrogate function $p(y|x)​$ in different step ?

$S​$ - Expected Improvement ?

$\cal{X}$ - configuration space

Sequential optimization algorithms work by leveraging structure in observed $(x, y)$ pairs in $\cal{H}$, $\cal{H} = (x_i, f(x_i))^{n}_{i=1}$.



![SMBO](https://github.com/bifeng/daily_book_notes/raw/master/resource/SMBO.png)



![SMBO](https://github.com/bifeng/daily_book_notes/raw/master/resource/smbo2.png)

​		This picture borrowed from Bayesian Optimization of Text Representations



#### surrogate

Two novel strategies for approximating $f​$ by modeling $\cal{H}​$: a hierarchical Gaussian Process and a tree-structured Parzen estimator.



#### criterion

The algorithms in this work optimize the criterion of **Expected Improvement (EI)** [10]. Other criteria have been suggested, such as Probability of Improvement and Expected Improvement [10], minimizing the Conditional Entropy of the Minimizer [11], and the bandit-based criterion described in [12].

We chose to use the EI criterion in our work because it is intuitive, and has been shown to work well in a variety of settings.

Expected improvement is the expectation under some model M of f : $\cal{X} \rightarrow \mathbb{R}^\N$ that f(x) will exceed (negatively) some **threshold** $y^*​$:
$$
EI_{y^{*}}(x) = \int^{\infty}_{-\infty} max(y^* - y,0) p_M(y|x)dy
$$
 $y^*$ is a threshold value of the objective function, $x$ is the proposed set of hyperparameters, $y$ is the actual value of the objective function using hyperparameters $x$ ($y$是一个变量，不是一个数值), and $p(y|x)$ is the surrogate probability model expressing the probability of $y$ given $x$. -- **the aim is to maximize the Expected Improvement with respect to x.** This means finding the best hyperparameters under the surrogate function $p(y|x)$.



### GP

the Gaussian-process based approach modeled $p(y|x)​$ directly.



$y^*$ - 基于历史观测$\cal{H}$，$f$函数的最优值，其中$f$为GP建模.



#### Optimizing EI in the GP

EI functions are usually optimized with an exhaustive grid search over the input space, or a Latin Hypercube search in higher dimensions.

The authors of [16] on the **landscape** of EI to design an evolutionary algorithm with mixture search, specifically aimed at optimizing EI, that is shown to outperform exhaustive search for a given budget in EI evaluations.



on the discrete part of our input space (categorical and discrete hyper-parameters) --> use the Estimation of Distribution (EDA,[17]) approach to sample candidate points according to binomial distributions.

on the continuous part of our input space (continuous hyper-parameters) --> use the Covariance Matrix Adaptation - Evolution Strategy (CMA-ES, [18]). CMA-ES is a state-of-the-art gradient-free evolutionary algorithm for optimization on continuous domains, which has been shown to outperform the Gaussian search EDA.



Use multiple GPs for each group of hyper-parameters: <br>we remark that all hyper-parameters are not relevant for each point. For example, a DBN with only one hidden layer does not have parameters associated to a second or third layer. <u>Thus it is not enough to place one GP over the entire space of hyper-parameters</u>. We chose to group the hyper-parameters by common use in a tree-like fashion and place different independent GPs over each group. As an example, for DBNs, this means placing one GP over common hyper-parameters, including categorical parameters that indicate what are the conditional groups to consider, three GPs on the parameters corresponding to each of the three layers, and a few 1-dimensional GPs over individual conditional hyper-parameters, like ZCA energy.



Runtime:<br>The runtime of each iteration of the GP approach scales cubically in $|\cal{H}|$ and linearly in the number of variables being optimized.

### TPE

the Tree-structured Parzen Estimator Approach modeled $p(x|y)$ and $p(y)​$.

The tree-structured Parzen estimator (TPE) models $p(x|y)​$ by transforming the generative process of configuration space, replacing <u>the distributions of the configuration prior</u> with <u>non-parametric densities</u>.

The TPE algorithm makes the following replacements in the configuation space: uniform $\rightarrow$ truncated Gaussian mixture, log-uniform $\rightarrow$ exponentiated truncated Gaussian mixture, categorical $\rightarrow$ re-weighted categorical.

（TPE对$p(x|y)$定义了两种密度函数。并不是所有的历史观测都是有用的，所以对于历史观测进行划分，优于阈值(threshold)的历史观测拟合第一个密度函数，剩余的历史观测拟合另一个密度函数）

Bayesian reasoning: $p(y|x) = \frac{p(x|y)p(y)}{p(x)}$.
$$
p(x|y) =
\begin{cases}
l(x) \ \ \  if\ y < y^*  \\
g(x) \ \ \  if\ y \geq y^*
\end{cases}
$$

Whereas the GP-based approach favoured quite an aggressive $y^*$ (typically less than the best observed loss), the TPE algorithm depends on a $y^*$ that is larger than the best observed f(x) so that some points can be used to form $l(x)$. The TPE algorithm chooses $y^*$ to be some quantile $\gamma$ of the observed $y$ values, so that $p(y < y^*) = \gamma$, but no specific model for p(y) is necessary.

这里讲了，TPE算法怎么选择$y^*​$, 即从历史观测$y​$中取$\gamma​$分位数。注意，$\gamma​$是一个常数，但是$y^*​$是一个随历史观测分布发生变化的变量。

#### Optimizing EI in the TPE

The models $l(x)​$ and $g(x)​$ are **hierarchical processes** involving discrete-valued and continuous valued variables.
$$
EI_{y^*}(x) = \frac{\gamma y^* l(x) - l(x) \int^{y^*}_{-\infty} p(y)dy}{\gamma l(x) + (1-\gamma)g(x)} \propto (\gamma + \frac{g(x)}{l(x)}(1-\gamma))^{-1}
$$

每次从参数空间中选择更优的超参数，并用代入上式$EI$评估（SMBO算法的第3步），这一部分比较耗时，但相比真实的损失函数评估超参数（SMBO算法的第4步）而言，成本更低。

上式也表明，为了最大化$EI​$，我们期望更高概率从$l(x)​$中抽取超参数$x​$，更低概率从$g(x)​$中抽取超参数$x​$.

This last expression shows that to maximize improvement we would like points $x$ with high probability under $l(x)$
and low probability under $g(x)$. **The tree-structured form** of $l$ and $g$ makes it easy to draw many candidates according to $l$ and evaluate them according to $g(x)/l(x)$. On each iteration, the algorithm returns the candidate $x^*$ with the greatest $EI$.

Runtime:<br>the runtime of each iteration of the TPE algorithm can scale linearly in $|\cal{H}|$ and linearly in the number of variables (dimensions) being optimized.











