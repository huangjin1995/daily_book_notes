[Must-read papers on neural relation extraction](https://github.com/thunlp/NREPapers)

https://github.com/thunlp/OpenNRE

https://zhuanlan.zhihu.com/p/44772023 summary

http://shomy.top/2018/02/28/relation-extraction/ paper notes



https://mp.weixin.qq.com/s/qw9i24goTsVgdk1qW6ie9A 首先对关系抽取的各种主流技术进行概述，而后结合业务中的选择与应用，重点介绍了基于DeepDive的方法，并详述它在神马知识图谱数据构建工作中的应用进展。



#### distant supervision

+ Distant supervision for relation extraction without labeled data, Mike Mintz, Steven Bills, Rion Snow, **Dan Jurafsky**, 2009 ACL, [paper](http://stanford.edu/~jurafsky/mintz.pdf) 

  <details><summary>Assumption</summary>
      The intuition of distant supervision is that any sentence that contains a pair of entities that participate in a known Freebase relation is likely to express that relation in some way.
  </details>
  

+ 

##### training/testing

training:

1. 使用NET（named entity tagger）标注。
2. 对在freebase中出现的实体对提取特征（从所有出现该实体对的句子中），构造训练数据。
3. Multi-class logistic regression classifier

论文中采用的NET标注工具为斯坦福的NRT标注器，再生成训练集的过程中，我们首先对大量文本句子进行命名实体标注，如果一个句子中含有两个实体，且这两个实体在Freebase（KB）中是一个关系对，那么从句子中提取特征，将关系作为类别，直到该类别中不再有新的句子加入，我们从该类别中的所有句子提取特征向量并且合并成一个更大的特征向量，从而训练出Multiclass logistic regression classifier。

testing:

1. 使用NET（named entity tagger）标注。
2. 在句子中出现的每对实体都被考虑做为一个潜在的关系实例，作为测试数据。
3. 使用训练好的模型对实体对进行分类。

 在测试阶段，先对句子中的命名实体进行标注，抽取其中的命名实体对和特征。如果多个句子的命名实体对一样，则将它们的特征合并在同一个特征向量中。然后利用逻辑回归分类器，对关系名称进行识别。这种方法的好处是可以综合文本中的多处，对一个实体对进行关系判断。

例如：<Steven Spielberg, Saving Private Ryan >---film-director

我们单看以下的第一个句子和第二个句子，都不能判断出Steven Spielberg和Saving Private Ryan之间存在film-director关系，但是把两个句子结合起来我们就能做到了。

 [Steven Spielberg]’s film [Saving Private Ryan] is loosely based on the brothers’ story.

 Allison co-produced the Academy Award winning [Saving Private Ryan], directed by [Steven Spielberg]... 

##### Multi-instance learning

周志华 - 

- [Multi-instance learning](http://cs.nju.edu.cn/zhouzh/zhouzh.files/publication/publication_toc.htm#Multi-Instance%20Learning)
- [多示例学习](https://wenku.baidu.com/view/a66fab43f12d2af90242e6da.html) 
- 



##### Attention 



##### Joint Learning



##### summary

过滤或降低噪声数据的方法：

Multi-instance learning - 从训练集中抽取取置信度高的训练样例训练模型

Attention - 利用Attention模型对数据进行全方位的权重计算，从而得到全面而不失“选择”的训练数据

Joint Learning - 对于错误传播放大的问题近期更有“joint learning”方法的提出，将命名实体识别和关系抽取两部并为一步走



