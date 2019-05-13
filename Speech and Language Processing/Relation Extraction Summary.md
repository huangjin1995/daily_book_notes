## Question

+ **View the relation classify as tagging problem ?**
+ How to use multi-task/joint learning in named entity recognition and relation extraction ?

- <u>how to reduce redundancy in joint learning ?</u>

  Most joint learning method is detect all the entities first, then the final decision is obtained via exhaustively enumerating the combinations between detected entity mentions and relation types.

  redundant information, such as entity redundancy - entity which complete useless, relation redundancy - entity which has part relation.(完全没有关系的实体，只有部分关系的实体（该实体只与某些实体存在关系，与其它实体不存在关系）)

  Example:

  The $[$United States$]_{E-loc}$ President $[$Trump$]_{E-per}$ will visit the $[$Apple Inc$]_{E-Org}$ .

  

  Solution:

  threshold - filter 

  additional label - us "NA" label for no relation type

  attention - use attention to select the most effect entities or relations. Selective attention for inter sentence attention (句子之间-sentence level attention). Self-attention/copy mechanism for intra sentence attention (句子内部-entity level attention).

  ​	多个句子共用一对实体，应用selective attention，选择合适的句子预测实体对关系的概率

  ​	一个句子的多对实体，应用self attention，或者应用selective attention（转化为多个相同句子不同实体对关系的向量表示），确定各实体对关系的概率（multi-label）

  

- how to reduce noisy for distant supervised dataset ?

  Solution:

  Multi-instance learning - 从训练集中抽取取置信度高的训练样例训练模型

  Attention - 利用Attention模型对数据进行全方位的权重计算，从而得到全面而不失“选择”的训练数据

  ...

  

  select correct sample form the noisy data 

  separate the correct sample from noisy data, and use the noisy data as negative example

  ...

  

- how to decide/discriminate the no-relation in sentence ? (the classifier will also need to be able to label an example as no-relation)

  Similar to Unlinkable Mention Prediction of Entity Linking.

  method 1 - threshold (manual setting or as a parameter to learn in rank)

  method 2 - a filter classifier (binary)

  method 3 - combined (add no-relation as candidate relation in rank)

- how to select/generate the proper negative samples ?

- Intra-sentence relation extraction vs. inter-sentences (cross-sentences) relation extraction ?

+ Relation detection first or entity recognition first ?

  

  some papers:

  Extracting contextualized complex biological events with rich graph based feature sets, Bj¨orne, J.; Heimonen, J.; Ginter, F.; Airola, A.; Pahikkala, T.; and Salakoski, T. 2011. Computational Intelligence.

  Identifying relations for open information extraction, Fader, A.; Soderland, S.; and Etzioni, O. EMNLP 2011.

  A Hierarchical Framework for Relation Extraction with Reinforcement Learning, Ryuichi Takanobu, Tianyang Zhang, Jiexi Liu, Minlie Huang,  AAAI 19 [arxiv](https://arxiv.org/abs/1811.03925) | [code](https://github.com/truthless11/HRL-RE)  - joint learning

  some code:

  https://github.com/baidu/information-extraction - two stage: first stage, a p-classification model is a multi-label classification which employs a stacked Bi-LSTM with max-pooling network, to identify the predicate involved in the given sentence; second stage, a so-labeling model is a deep Bi-LSTM-CRF network is adopted with BIEO tagging scheme in the so-labeling model to label the element of subject and object mention, given the predicate which is distinguished in the p-classification model.(多标签分类问题，针对一个句子，预测该句子的多个谓语(predicate，即关系类型)；序列标注问题，针对一个句子及其一个谓语，预测该句子的主语(subject)和宾语(object)，其中谓语以embedding方式作为特征输入。注意，词向量是以one-hot encoding方式基于模型训练的词向量。) 

  

  

+ overlapping relation extraction problem ?

  **(这个问题是否重要，是否值得独立建模？)**

  solution:

  1. one sentence just focus one pair of entities, so if the sentence contain multiple relation, then you need replicate the sentence. (one sentence one label)

  Downside - 

  First, it will introduce the sentence independent hypotheses, which is not true!

  Second, for multiple relation share the common entity, you will lose the information for this entity connection with other entities.

  Third, for prediction new sentence, you should provide lots of entity pairs of this sentence, which is redundancy.

  Last but not least, create lots of training example which contain some redundancy.

  2. multi-label learning (one sentence multi-label)

  

  some papers:

  

  1. Knowledge based weak supervision for information extraction of overlapping relations, Raphael Hoffmann, Congle Zhang, Xiao Ling, Luke Zettlemoyer, and Daniel S Weld. ACLHLT 2011, [paper](http://raphaelhoffmann.com/publications/acl2011.pdf) [Slides](http://raphaelhoffmann.com/publications/acl2011-slides.pptx) [Source Code](http://www.cs.washington.edu/ai/raphaelh/mr). :star::star::star:

  2. A Walk-based Model on Entity Graphs for Relation Extraction, Fenia Christopoulou, Makoto Miwa, Sophia Ananiadou, ACL 2018, [arxiv](https://arxiv.org/abs/1902.07023v1) 

     treats multiple pairs in a sentence simultaneously and considers interactions among them...

  3. Extracting Relational Facts by an End-to-End Neural Model with Copy Mechanism, Xiangrong Zeng, Daojian Zeng, Shizhu He, Kang Liu, Jun Zhao, ACL 2018 [code](https://github.com/xiangrongzeng/copy_re) 

     Classify overlapping entity with three triplet overlap degree, including Normal, EntityPairOverlap and SingleEntiyOverlap.

     seq2seq learning with copy mechanism - one entity is allowed to be copied several times when it needs to participate in different triplets.

     Joint learning - the entities and relations could be jointly extracted

     Dataset: New York Times Corpus/WebNLG

     缺点：没有针对各类overlapping type进行ablation analysis！！！This method strongly relies on the training data, and cannot extract multi-word entity mentions.

  4. A Hierarchical Framework for Relation Extraction with Reinforcement Learning, Ryuichi Takanobu, Tianyang Zhang, Jiexi Liu, Minlie Huang,  AAAI 19 [arxiv](https://arxiv.org/abs/1811.03925) | [code](https://github.com/truthless11/HRL-RE) 

     classify overlapping relations into two types: Type I: two triples share only one entity within a sentence, Type II: two triples share two entities (both head and tail entities) within a sentence.

     a hierarchical reinforcement learning (HRL) framework - 1) a high-level RL process that detects a relation indicator in a sentence; 2) a low-level RL process that identifies the associated entities for the corresponding relation.

     joint extraction - a “relation”-first, “argument”-second approach. <u>we first detect a relation indicator and then extract the corresponding entities as the argument of a relation</u>. 

     ​	**relation indicator**, is the position in a sentence when sufficient information has been mentioned to identify
     a semantic relation. Different from relation trigger (i.e., explicit relation mention), relation indicators can be verbs
     (e.g. die of), nouns (e.g. his father), or even prepositions (e.g. from/by), other symbols such as comma and period.

     ​	**relation triggers**, which refer to a phrase that explicitly expresses the occurrence of a relation in a sentence, and then determine their arguments to reduce the task complexity. But there are many cases where no relation trigger appears in a sentence so that such relations cannot be captured.

     Dataset: New York Times Corpus

     缺点：没有分析该模型的不足之处 (bad cases analysis).

  

  



## methods



两种思路：

1. 设计特定的模型以适配数据

2. 转换数据以适配特定的模型



### hand-written patterns

1. Some entities contain the relation.

    For example: 

   `"text": "山东仙坛股份有限公司成立于2001年，注册资金1"`

   `{"predicate": "总部地点", "object_type": "地点", "subject_type": "企业", "object": "山东", "subject": "山东仙坛股份有限公司"}` 

2. Relation triggers (lexical)

   For example:

   `"text": "家庭生活王建国的夫人为东南大学建筑学院教授、博士生导师，中国建筑史专家陈薇教授"`

   `{"predicate": "妻子", "object_type": "人物", "subject_type": "人物", "object": "陈薇", "subject": "王建国"}`

3. Type constraint: entities type constraint to the relation type

   特定的实体对类型组合，才构成某种关系类型。

   For example: `subject_type` and `object_type` constraint to `predicate`.

   ```
   {"object_type": "地点", "predicate": "出生地", "subject_type": "人物"}
   {"object_type": "Date", "predicate": "出生日期", "subject_type": "人物"}
   {"object_type": "Number", "predicate": "身高", "subject_type": "人物"}
   {"object_type": "Text", "predicate": "民族", "subject_type": "人物"}
   {"object_type": "学校", "predicate": "毕业院校", "subject_type": "人物"}
   ...
   ```

   

4. Domain constraint

   一个句子或一段文本，只会同时出现某类`subject_type`。

   

   

   







### supervised



#### Architecture

![relation_extraction_supervised_learning](https://github.com/bifeng/daily_book_notes/raw/master/resource/relation_extraction_supervised_learning.png)

Step one is to find pairs of named entities (usually in the same sentence).

Step two, **a filtering classifier** is trained to make a binary decision as to whether a given pair of named entities are related (by any relation). **Positive examples** are extracted directly from all relations in the annotated corpus, and **negative examples** are generated from within-sentence entity pairs that are not annotated with a relation.

Step three, **a final classifier** is trained to assign a label to the relations that were found by step 2.

The use of the filtering classifier can speed up the final classification and also allows the use of distinct feature-sets appropriate for each task. For each of the two classifiers, we can use any of the standard classification techniques (logistic regression, neural network, SVM, etc.)



#### feature-based

Let’s consider features for classifying the relationship between American Airlines (Mention 1, or M1) and Tim Wagner (Mention 2, M2) from this sentence:

**American Airlines**, a unit of AMR, immediately matched the move, spokesman **Tim Wagner** said

Useful **word features** include

+ The headwords of M1 and M2 and their concatenation
  Airlines Wagner Airlines-Wagner
+ Bag-of-words and bigrams in M1 and M2
  American, Airlines, Tim, Wagner, American Airlines, Tim Wagner
+ Words or bigrams in particular positions (neighboring words)
  M2: -1 spokesman
  M2: +1 said
+ Bag of words or bigrams between M1 and M2:
  a, AMR, of, immediately, matched, move, spokesman, the, unit
+ Stemmed versions of the same

Embeddings can be used to represent words in any of these features. 

Useful **named entity features** include

+ Named-entity types and their concatenation
  (M1: ORG, M2: PER, M1M2: ORG-PER)
+ Entity Level of M1 and M2 (from the set NAME, NOMINAL, PRONOUN)
  M1: NAME [it or he would be PRONOUN]
  M2: NAME [the company would be NOMINAL]
+ Number of entities between the arguments (in this case 1, for AMR)

The **syntactic structure features** of a sentence can also signal relationships among its entities. Syntax is often featured by using strings representing syntactic paths: the (dependency or constituency) path traversed through the tree in getting from one entity to the other.

+ Base syntactic chunk sequence from M1 to M2
  NP NP PP VP NP NP
+ Constituent paths between M1 and M2
  NP $\uparrow$ NP $\uparrow$ S $\uparrow$ S $\downarrow$ NP
+ Dependency-tree paths
  Airlines $\leftarrow_{subj}$ matched $\leftarrow_{comp}$ said $\rightarrow_{subj}​$ Wagner



It is also able to use very rich features that are conjunctions of these individual features.

we would learn rich **conjunction features** like this one:
M1 = ORG & M2 = PER & nextword=“said”& path= NP $\uparrow$ NP $\uparrow$ S $\uparrow$ S $\downarrow$ NP





#### neural-based

##### architecture

One option is to use a similar architecture as we saw for named entity tagging: a bi-LSTM model with word embeddings as inputs and a single softmax classification of the sentence output as a 1-of-N relation label. Because <u>relations often hold between entities that are far part in a sentence (or across sentences)</u>, it may be possible to get higher performance from algorithms like convolutional nets (dos Santos et al., 2015) or chain or tree LSTMS (Miwa and Bansal 2016, Peng
et al. 2017).

##### representation

句子中实体关系的向量表示方法：

1. 



### semi-supervised 

#### bootstrapping 



#### distant supervision

![relation_extraction_distant_supervision](https://github.com/bifeng/daily_book_notes/raw/master/resource/relation_extraction_distant_supervision.png)



The distant supervision method combines the advantages of bootstrapping with supervised learning.

Instead of just a handful of seeds, distant supervision uses a large database to acquire a huge number of seed examples, creates lots of noisy pattern features from all these examples and then combines them in a supervised
classifier.

First, uses a large database to acquire a huge number of seed examples - Wikipedia-based databases like DBPedia or Freebase have tens of thousands of examples of many relations.

Second, run named entity taggers on large amounts of text - used articles from Wikipedia—and extract all sentences
that have two named entities that match the tuple.

Training instances can now be extracted from this data, one training instance for each identical tuple <relation, entity1, entity2>.

Third, apply feature-based or neural classification.



### unsupervised



### Joint/Multitask training

NER + RE













