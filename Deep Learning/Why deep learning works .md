https://zhuanlan.zhihu.com/p/45695998

https://zhuanlan.zhihu.com/p/23454281



refer:<br>[【深度学习系列】用PaddlePaddle和Tensorflow实现经典CNN网络GoogLeNet](https://mp.weixin.qq.com/s/AfbwFw9_hgdZvG974sbT3A) 



### Question

+ Why the deep neural networks (such as AlexNet (2012)) is so successful ?

+ Why the deep neural networks (such as AlexNet (2012)) is not facing the overfitting problem ?

  神经网络参数量这么大，居然没有过拟合？要是传统方法，早就过拟合了。这种方式是解决了维数灾难问题，还是绕过了这个问题？



### assumption

#### distribution

神经网络的特定结构和数据分布有某种契合性？如何定量地给出这些因素在最终效果中所占的比重？



#### sparse

Using sparse to improve the generalization (change the fully connection or convolution to the sparse connection).

当整个特征空间是非线性甚至不连续时：

- 学好局部空间的特征集更能提升性能，类似于Maxout网络中使用多个局部线性函数的组合来拟合非线性函数的思想；
- 假设整个特征空间由N个不连续局部特征空间集合组成，任意一个样本会被映射到这N个空间中并激活/不激活相应特征维度，如果用C1表示某类样本被激活的特征维度集合，用C2表示另一类样本的特征维度集合，当数据量不够大时，要想增加特征区分度并很好的区分两类样本，就要降低C1和C2的重合度（比如可用Jaccard距离衡量），即缩小C1和C2的大小，意味着相应的特征维度集会变稀疏。

GoogleNet的作者，也是基于网络结构的稀疏性兼顾计算机体系结构适于稠密矩阵的高性能计算，设计了Inception的结构。





