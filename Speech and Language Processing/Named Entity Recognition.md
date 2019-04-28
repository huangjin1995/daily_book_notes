refer:<br>[面向新闻媒体的命名实体识别技术](https://mp.weixin.qq.com/s/onAU0jJpFMXY80aRGB6vIA) 



### literature review

+ A Survey on Deep Learning for Named Entity Recognition, Jing Li, Aixin Sun, Jianglei Han, Chenliang Li, 2018.12, [arxiv](https://arxiv.org/abs/1812.09449) 
+ A Survey on Recent Advances in Named Entity Recognition from Deep Learning models, Vikas Yadav, Steven Bethard, 2018, [paper](https://www.aclweb.org/anthology/C18-1182) 
+ A survey of named entity recognition and classification, David Nadeau, Satoshi Sekine, 2007, [paper](https://nlp.cs.nyu.edu/sekine/papers/li07.pdf)  :star::star::star::star:



### Challenge

- 自动识别未登录词从而发现新词

- 兼容领域词库从而实现多领域自动适配

  

- 嵌套的实体类型？

  一个实体类型的长词，包含另一个实体类型的短词

  

- 一个实体属于多种类型？

  

- 如何识别大量的实体类型？

  示例：文本中存在上百种类型的实体，如何识别？

  1）训练多个单类型的实体识别器

  对于同一个实体，如果其类型也相同，但实体所指不相同，则在训练该类型的实体识别器时，需要新增标签进行区分。

  2）数据增广

  新增弱标注数据，扩大训练集

  

- how to recognize long tail of less well-known entities ?

  



### STOA

+ https://nlpprogress.com/english/named_entity_recognition.html
+ 



### tools

+ http://alchemy.cs.washington.edu/
+ ProbCog: A Toolbox for Statistical Relational Learning and Reasoning [code](https://github.com/opcode81/ProbCog) 
+ 



### Method

#### rule and dictionary based



#### machine learning based



#### deep learning based

#### Combined

1. 字符级别的 Bi-LSTM + CRF

   1）分词+实体

   每个字处于词的不同位置作为序列中的一种状态（常见的位置状态有：B（词的开头）、E（词的结尾）、M（词的中间）、S（单个字组成的词）），每种实体类型也是一种状态（常见的实体类型有：人名（PER），机构名（ORG），其他词性（NO）），则实体词的类型联合字在词中的位置，构成了4*3=12种序列状态。

   2）分词+词性

   ...

   3）分词+词性+实体

   ...

   优缺点：

   字符级别，可以避免OOV问题。

   缺点在于它无法利用词性等信息，而这些信息有利于实体的识别。

   

2. 实体词典+规则

   规则主要包括：书名号中的电影名、带分隔符的外国人名等特殊格式。

   

### data anotation

+ a. 使用已有的开源NER对文章粒度的长文本进行预处理，提取各类实体词，<u>人工结合文章语境，对实体词进行添加和删除</u>。将所标注的实体词放回文章，生成新的训练集进入到NER算法模型，这样可以达到比大部分开源NER更好的效果。
+ b. 使用类似boosting的数据采样方案，基于a中标注数据分组产生多个NER模型，对段落粒度的文本进行扫描。如果标注结果不一致，则认为该样本存在较低的置信度，把该段文本投入到逐字逐句的标注流程，进一步提升数据集的准确率。











