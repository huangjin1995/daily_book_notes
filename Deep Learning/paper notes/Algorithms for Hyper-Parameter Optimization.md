### Question

+ What's the assumptions and constraints ? 

  Does it can be used in any model (model agnostic ) ?

  Assumption: each hyper-parameters are independent to each other.   

+ How to evaluate each hyper-paramters choice?

  

+ why the TPE approach outperformed the GP approach ?

  

+ when the SMBO algorithm fails ?

  1) a bad choice of  $p(y|x)$.

  2) it extracts structure in $\cal{H}​$ that leads only to a local optimum.



### summary

+ data distribution -> $p(y|x)$ (such as network structure) -> parameter search

  1) Random search is competitive with the manual optimization of deep belief networks (DBNs).

  2) Automatic sequential optimization outperforms both manual and random search.

+ 



### problem definition

Hyper-parameter optimization is the problem of optimizing a loss function over <u>a graph-structured configuration space</u>.

In this work we restrict ourselves to <u>tree-structured configuration spaces</u>. Configuration
spaces are tree-structured in the sense that some leaf variables (e.g. the number of hidden
units in the 2nd layer of a DBN) are only well-defined when node variables (e.g. a discrete choice of
how many layers to use) take particular values. Not only must a hyper-parameter optimization algorithm
optimize over variables which are discrete, ordinal, and continuous, but it must simultaneously
choose which variables to optimize.



### objective





### Architecture

Sequential Model-Based Optimization (SMBO)

（根据每次给定的超参数，重新训练模型并验证该组参数是否最优，当数据量大时，这种方式成本太高。SMBO采用替代模型来评估，并且考虑历史观测值（最优参数）选择下一次迭代的最优参数）

Sequential optimization algorithms work by leveraging structure in observed $(x, y)$ pairs.

it extracts structure in $\cal{H}​$ 



![SMBO](https://github.com/bifeng/daily_book_notes/raw/master/resource/SMBO.png)



#### surrogate

Two novel strategies for approximating $f$ by modeling $\cal{H}$: a hierarchical Gaussian Process and a tree-structured Parzen estimator.



#### criterion

The algorithms in this work optimize the criterion of **Expected Improvement (EI)** [10]. Other criteria have been suggested, such as Probability of Improvement and Expected Improvement [10], minimizing the Conditional Entropy of the Minimizer [11], and the bandit-based criterion described in [12].

We chose to use the EI criterion in our work because it is intuitive, and has been shown to work well in a variety of settings.



### GP



### TPE





