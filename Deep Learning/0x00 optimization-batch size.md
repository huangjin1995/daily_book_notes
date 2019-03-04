refer:<br>[怎么选取训练神经网络时的Batch size?](https://www.zhihu.com/question/61607442) 



### batch size

The size of the mini-batch is a hyperparameter but it is not very common to cross-validate it. It is usually based on memory constraints (if any), or set to some value, e.g. 32, 64 or 128. <u>We use powers of 2 in practice because many vectorized operation implementations work faster when their inputs are sized in powers of 2.</u> 



[https://danluu.com/3c-conflict/](https://link.zhihu.com/?target=https%3A//danluu.com/3c-conflict/) 这个详细说了CPU为什么讨厌16，32...。



#### why it is important?

Intuition:<br>考虑极端情况，当batch size为1时，它会带来很大的噪声/方差，所以不会在某个点停留太久，容易跳出局部最优点或鞍点，而当batch size为N（全部样本）时，它的方差很小，所以对梯度的估计比较稳定，却容易陷入局部最优点或鞍点。



Theory:





#### 一阶优化/二阶优化

对于二阶优化算法（共轭梯度法、L-BFGS等）而言，噪声带来的收益会大大降低，因此batch size尽可能大。



#### how to choose batch size?

1. noise

当感觉训练时噪音不够时，比如收敛碰到鞍点或者局部最小值时，调小batch size。（很少会碰到）
当感觉训练时噪音太大时，调大batch size到喂饱硬件（这也很少做），再不行就调小learning rate，也可以直接调小learning rate。

2. 

《Deep Learning》一书，建议使用逐步增加的batch size来兼并两者的优点。

3. ..

   常见的带learning rate下降的sgd。开始时依赖batch带来的噪音快速下降，接下来使用较低的learning rate消除这些噪音寻求稳定收敛。一般而言只要batch不太大，样本里的噪音总是够用的。





### summary

+ batch size 本质是引入多大的噪声

  batch size 越小，噪声越大，反之，噪声越小

+ 



### Question

+ 

