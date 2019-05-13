more refer:

Multi-Label Classification: An Overview, Grigorios Tsoumakas, Ioannis Katakis [paper](https://www.researchgate.net/profile/Grigorios_Tsoumakas/publication/273859036_Multi-Label_Classification_An_Overview/links/574575e308aea45ee8539026/Multi-Label-Classification-An-Overview.pdf) 

A Tutorial on Multi-Label Learning, EVA GIBAJA, SEBASTIAN VENTURA, [paper](https://www.researchgate.net/profile/Sebastian_Ventura/publication/270337594_A_Tutorial_on_Multi-Label_Learning/links/54bcd8460cf253b50e2d697b/A-Tutorial-on-Multi-Label-Learning.pdf) 

https://users.ics.aalto.fi/jesse/talks/Multilabel-Part01.pdf 

https://users.ics.aalto.fi/jesse/talks/Multilabel-Part02.pdf

[scikit-multilearn](https://github.com/scikit-multilearn/scikit-multilearn/fork) 



多标签学习算法分为两种思路：

1）改造数据适应算法 (problem transformation)

2）改造算法适应数据 (algorithm adaption)



![multi_label_learning](https://github.com/bifeng/daily_book_notes/raw/master/resource/multi_label_learning_methods.png)

### Problem Transformation (PT)

The first one (dubbed PT1) subjectively or randomly selects one of the multiple labels of each multi-label instance and discards the rest, while the second one (dubbed PT2) simply discards every multi-label instance from the multi-label data set. 

![PT1](https://github.com/bifeng/daily_book_notes/raw/master/resource/PT1.png)

![PT2](https://github.com/bifeng/daily_book_notes/raw/master/resource/PT2.png)

The third problem transformation method that we will mention (dubbed PT3), considers each different set of labels that exist in the multi-label data set as a single label. It so learns one single-label classifier H: X → P(L) , where P(L) is the power set of L. One of the negative aspects of PT3 is that it may lead to data sets with a large number of classes and few examples per class. 

![PT3](https://github.com/bifeng/daily_book_notes/raw/master/resource/PT3.png)

The most common problem transformation method (dubbed PT4) learns |L| binary classifiers $H_l: X →
{l, ¬l}$ , one for each different label $l$ in L. It transforms the original data set into |L| data sets $D_l$ that contain all examples of the original data set, labelled as l if the labels of the original example contained $l$ and as $¬l$ otherwise. It is the same solution used in order to deal with a single-label multiclass problem using a binary classifier. 

![PT4](https://github.com/bifeng/daily_book_notes/raw/master/resource/PT4.png)

A straightforward, yet undocumented, problem transformation method is the following (dubbed PT5): Firstly, it decomposes each example (x, Y) into |Y| examples $(x, l)$ for all $l ∈ Y$. Then it learns one single-label coverage-based classifier from the transformed data set. Distribution classifiers are those classifiers that can output a distribution of certainty degrees (or probabilities) for all labels in L. Finally it post-processes this distribution to output a set of labels. One simple way to achieve this is to output those labels for which the certainty degree is greater than a specific threshold (e.g. 0.5). A more complex way is to output those labels for which the certainty degree is greater than a percentage (e.g. 70%) of the highest certainty degree. 

![PT5](https://github.com/bifeng/daily_book_notes/raw/master/resource/PT5.png)

A problem transformation (dubbed PT6): Each example (x, Y) is decomposed into |L| examples $(x, l, Y[l])$, for all $l ∈ L$, where $Y[l] = 1$ if $l ∈ Y$, and $[l] = −1​$ otherwise. 

![PT6](https://github.com/bifeng/daily_book_notes/raw/master/resource/PT6.png)

#### Summary

PT3效果很好，PT4较好也应用比较广泛，PT6由于数据不平衡（如果标签密度太小会导致大量的-1）

...

### Algorithm Adaption







### multi-class vs multi-label vs multi-task

Multiclass classification means a classification task with more than two classes; e.g., classify a set of images of fruits which may be oranges, apples, or pears. Multiclass classification makes the assumption that each sample is assigned to one and only one label: a fruit can be either an apple or a pear but not both at the same time.

Multilabel classification assigns to each sample a set of target labels. This can be thought as predicting properties of a data-point that are not mutually exclusive, such as topics that are relevant for a document. A text might be about any of religion, politics, finance or education at the same time or none of these.

Multioutput-multiclass classification and multi-task classification means that a single estimator has to handle several joint classification tasks. This is a generalization of the multi-label classification task, where the set of classification problem is restricted to binary classification, and of the multi-class classification task. The output format is a 2d numpy array or sparse matrix.

The set of labels can be different for each output variable. For instance a sample could be assigned “pear” for an output variable that takes possible values in a finite set of species such as “pear”, “apple”, “orange” and “green” for a second output variable that takes possible values in a finite set of colors such as “green”, “red”, “orange”, “yellow”…

This means that any classifiers handling multi-output multiclass or multi-task classification task supports the multi-label classification task as a special case. Multi-task classification is similar to the multi-output classification task with different model formulations. For more information, see the relevant estimator documentation.

