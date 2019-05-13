#### Challenge

Three task:

One pair entities correspond to only one sentence

One pair entities correspond to multiple sentences (distant supervised datasets)

Multiple pair entities correspond to only one sentence (overlapping relation extraction)

<u>It must consider the domain of relation type (data distribution unbalance problem).</u>



#### Resource

http://lietc.com/wiki/relation_extraction

https://github.com/roomylee/awesome-relation-extraction



#### Literature Review

A Review of Relation Extraction, Nguyen Bach, Sameer Badaskar, 2007 [paper](http://www.cs.cmu.edu/~nbach/papers/A-survey-on-Relation-Extraction.pdf) | [slide](http://www.cs.cmu.edu/~nbach/papers/A-survey-on-Relation-Extraction-Slides.pdf) 



[Must-read papers on neural relation extraction](https://github.com/thunlp/NREPapers) 



https://zhuanlan.zhihu.com/p/44772023 summary

https://www.cnblogs.com/theodoric008/p/7874373.html summary

http://shomy.top/2018/02/28/relation-extraction/ paper notes

https://mp.weixin.qq.com/s/qw9i24goTsVgdk1qW6ie9A 首先对关系抽取的各种主流技术进行概述，而后结合业务中的选择与应用，重点介绍了基于DeepDive的方法，并详述它在神马知识图谱数据构建工作中的应用进展。



#### Related tasks

+ attributes extraction

  OpenTag: Open Attribute Value Extraction from Product Profiles, Guineng Zheng, Subhabrata Mukherjee, Xin Luna Dong, Feifei Li, KDD 2018, [arxiv](https://arxiv.org/abs/1806.01264v1) (BiLSTM-CRF with Attention)

  Unsupervised Extraction of Attributes and Their Values from Product Description

  http://www.stokastik.in/attribute-extraction-from-e-commerce-product-description/

  http://www.stokastik.in/bilstm-crf-sequence-tagging-for-e-commerce-attribute-extraction/

+ 



#### STOA

https://nlpprogress.com/english/relationship_extraction.html

https://paperswithcode.com/task/relation-extraction

##### Dataset

+ Distantly Supervised Datasets

  (It mainly contain the multiple sentences share a pair of entities)

  

  New York Times Corpus

  This dataset consists of 1.18M sentences sampled from 294k 1987-2007 New York Times news articles. There are 24 valid relations in total.

  Give one pair of entity which share by multiple or one sentence, decide the relationship of entity pair in each sentence. In the original testing data set, there are 74,857 entity pairs that correspond to only one sentence, nearly 3/4 over all entity pairs.

  (Sebastian Riedel, Limin Yao, and Andrew McCallum. Modeling relations and their mentions without labeled text, 2010. In Proceedings of ECML PKDD.)

  

  Wiki-KBP

  the number of relation type in the test set is more than that of the train set

  

+ Supervised Datasets

  SemEval-2010 Task 8

  Given a sentence and two tagged nominals, to predict the relation between those nominals *and* the direction of the relation.

  

  TACRED (TAC KBP)

  

  BioInfer

  more than 50% of the data has overlapping relations

  

  WebNLG

  It is originally created for Natural Language Generation (NLG) task. This dataset contains 246 valid relations. In this dataset, a instance including a group of triplets and several standard sentences (written by human). Every standard sentence contains all triplets of this instance.

  (Claire Gardent, Anastasia Shimorina, Shashi Narayan, and Laura Perez-Beltrachini. 2017. Creating training
  corpora for nlg micro-planners. In Proceedings of ACL.)

  

+ Few-shot Datasets

  FewRel

  





#### Tools



https://github.com/thunlp/OpenNRE



Convolutional Neural Network for Relation Extraction:(ER-CNN, MLMI-CNN, MLMI-CONT)

https://github.com/may-/cnn-re-tf



#### paper

+ Improving Relation Extraction by Pre-trained Language Representations. Christoph Alt, Marc Hübner, Leonhard Hennig, AKBC 2019, [paper](https://openreview.net/pdf?id=BJgrxbqp67) | [code](https://github.com/DFKI-NLP/TRE) 



##### Multi-task Learning

+ A Hierarchical Multi-task Approach for Learning Embeddings from Semantic Tasks, Victor Sanh, Thomas Wolf, **Sebastian Ruder**, AAAI 2019, [arxiv](https://arxiv.org/abs/1811.06031) | [code](https://github.com/huggingface/hmtl) 

+ Multi-Task Transfer Learning for Weakly-Supervised Relation Extraction, Jing Jiang, 2009 [paper](https://www.aclweb.org/anthology/P09-1114) :star::star:

  



##### Joint Learning

Giannis Bekoulis, Johannes Deleu, Thomas Demeester, Chris Develder. Joint entity recognition and relation extraction as a multi-head selection problem. Expert Systems with Applications, Volume 114, Pages 34-45, 2018

Giannis Bekoulis, Johannes Deleu, Thomas Demeester, Chris Develder. Adversarial training for multi-context joint entity and relation extraction, In the Proceedings of the Conference on Empirical Methods in Natural Language Processing (EMNLP), 2018

[code](https://github.com/bekou/multihead_joint_entity_relation_extraction) 



End-to-End Relation Extraction using LSTMs on Sequences and Tree Structures, Makoto Miwa, Mohit Bansal, ACL2016, [arxiv](https://arxiv.org/pdf/1601.00770v2.pdf) :star::star::star: - It utilizes more linguistic resources (e.g., POS tags, chunks, syntactic parsing trees).



Joint Entity and Relation Extraction Based on A Hybrid Neural Network



A neural joint model for entity and relation extraction from biomedical text



Going out on a limb: Joint Extraction of Entity Mentions and Relations without Dependency Trees



Joint Extraction of Entities and Relations Based on a Novel Tagging Scheme, Suncong Zheng, Feng Wang, Hongyun Bao, Yuexing Hao, Peng Zhou, Bo Xu, ACL2017 outstanding paper, [arxiv](https://arxiv.org/abs/1706.05075) | [code](https://github.com/zsctju/triplets-extraction) :star:

CoType: Joint Extraction of Typed Entities and Relations with Knowledge Bases, Xiang Ren, Zeqiu Wu, Wenqi He, Meng Qu, Clare R. Voss, Heng Ji, Tarek F. Abdelzaher, Jiawei Han, WWW 2017, [arxiv](https://arxiv.org/abs/1610.08763) | [code](https://github.com/INK-USC/DS-RelationExtraction) 



##### Two-stage



Relation Classification via Convolutional Deep Neural Network, Daojian Zeng, Kang Liu, Siwei Lai, Guangyou Zhou and Jun Zhao, 2014 :star::star::star:



###### Attention

It can be used for the distant supervision dataset. - 利用Attention模型对数据进行全方位的权重计算，从而得到全面而不失“选择”的训练数据.

Neural Relation Extraction with Selective Attention over Instances, Yankai Lin, Shiqi Shen, Zhiyuan Liu, Huanbo Luan, Maosong Sun, ACL 2016, [paper](http://nlp.csai.tsinghua.edu.cn/~lzy/publications/acl2016_nre.pdf) | [OpenNRE](https://github.com/thunlp/OpenNRE) :star::star::star:

Cross-relation Cross-bag Attention for Distantly-supervised Relation Extraction, Yujin Yuan, Liyuan Liu, Siliang Tang, Zhongfei Zhang, Yueting Zhuang, Shiliang Pu, Fei Wu, Xiang Ren, AAAI 2019 [arxiv](https://arxiv.org/abs/1812.10604)



###### Multi-instance

Mainly for the distant supervision dataset. - 从训练集中抽取取置信度高的训练样例训练模型.

- Multi-instance Single-label

  For multi-sentence share a pair of entities, it assume that only one sentence is active for this entity pair (should have only one relation type). Hence, it will lose a large amount of rich information containing in those neglected sentences.

Modeling relations and their mentions without labeled text, Sebastian Riedel, Limin Yao, and Andrew McCallum. 2010 ECML-PKDD, :star::star::star:

Distant supervision for relation extraction via piecewise convolutional neural networks, Daojian Zeng, Kang Liu, Yubo Chen, and Jun Zhao.. In Proceedings of EMNLP. 2015.:star::star::star:



- Multi-instance Multi-label

  multi-sentence share a pair of entities should have multiple relation type

Knowledge based weak supervision for information extraction of overlapping relations, Raphael Hoffmann, Congle Zhang, Xiao Ling, Luke Zettlemoyer, and Daniel S Weld. ACLHLT 2011, [paper](http://raphaelhoffmann.com/publications/acl2011.pdf) [Slides](http://raphaelhoffmann.com/publications/acl2011-slides.pptx) [Source Code](http://www.cs.washington.edu/ai/raphaelh/mr). :star::star::star:

Multi-instance Multi-label Learning for Relation Extraction, Mihai Surdeanu, Julie Tibshirani, Ramesh Nallapati, **Christopher D. Manning**, EMNLP-CoNLL 2012 [paper](http://aclweb.org/anthology-new/D/D12/D12-1042.pdf) | [code](https://nlp.stanford.edu/software/mimlre.shtml):star::star::star:



###### Dependency Trees

Shortest dependency path (SDP) between entity pairs of dependency parse trees

RelEx—Relation extraction using dependency parse trees, Katrin Fundel  Robert Küffner  Ralf Zimmer, Bioinformatics 2007. :star::star::star:

Classifying relations via long short term memory networks along shortest dependency paths, Y. Xu, L. Mou, G. Li, Y. Chen, H. Peng, and Z. Jin, EMNLP 2015. 

Improved relation classification by deep recurrent neural networks with data augmentation, Y. Xu, R. Jia, L. Mou, G. Li, Y. Chen, Y. Lu, and Z. Jin, arXiv preprint arXiv:1601.03651, (2016).

Graph Convolution over Pruned Dependency Trees Improves Relation Extraction, Yuhao Zhang, Peng Qi, **Christopher D. Manning**, EMNLP 2018 [arxiv](https://arxiv.org/abs/1809.10185) | [code](https://github.com/qipeng/gcn-over-pruned-trees) 



###### Reinforcement Learning

Mainly for the distant supervision dataset.

Reinforcement Learning for Relation Classification from Noisy Data, Jun Feng, Minlie Huang, Li Zhao, Yang Yang, Xiaoyan Zhu, AAAI2018. [arxiv](https://arxiv.org/abs/1808.08013v1) | [code](https://github.com/unreliableXu/TensorFlow_RLRE) 

Robust Distant Supervision Relation Extraction via Deep Reinforcement Learning, Pengda Qin, Weiran Xu, William Yang Wang, [arxiv](https://arxiv.org/abs/1805.09927v1) - Unlike the removal operation in the previous studies, we redistribute them into the negative examples.



#### distant supervision

+ Distant supervision for relation extraction without labeled data, Mike Mintz, Steven Bills, Rion Snow, **Dan Jurafsky**, 2009 ACL, [paper](http://stanford.edu/~jurafsky/mintz.pdf) :star::star::star::star:

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







