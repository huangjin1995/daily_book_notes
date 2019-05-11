## Question

+ **View the relation classify as tagging problem ?**
+ How to use multi-task/joint learning in named entity recognition and relation extraction ?

- <u>how to reduce redundancy in joint learning ?</u>

  redundant information, such as entity redundancy - entity which complete useless, relation redundancy - entity which has part relation.(完全没有关系的实体，只有部分关系的实体（该实体只与某些实体存在关系，与其它实体不存在关系）)

  Example:

  The $[$United States$]_{E-loc}$ President $[$Trump$]_{E-per}$ will visit the $[$Apple Inc$]_{E-Org}$ .

  

  Solution:

  threshold - filter 

  additional label - us "NA" label for no relation type

  attention - use attention to select the most effect entities or relations

  ???

  

- how to decide/discriminate the no-relation in sentence ? (the classifier will also need to be able to label an example as no-relation)

  Similar to Unlinkable Mention Prediction of Entity Linking.

  method 1 - threshold (manual setting or as a parameter to learn in rank)

  method 2 - a filter classifier (binary)

  method 3 - combined (add no-relation as candidate relation in rank)

- how to select/generate the proper negative samples ?

- Intra-sentence relation extraction vs. inter-sentences (cross-sentences) relation extraction ?







## methods



两种思路：

1. 设计特定的模型以适配数据

2. 转换数据以适配特定的模型



### hand-written patterns



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

One option is to use a similar architecture as we saw for named entity tagging: a bi-LSTM model with word embeddings as inputs and a single softmax classification of the sentence output as a 1-of-N relation label. Because <u>relations often hold between entities that are far part in a sentence (or across sentences)</u>, it may be possible to get higher performance from algorithms like convolutional nets (dos Santos et al., 2015) or chain or tree LSTMS (Miwa and Bansal 2016, Peng
et al. 2017).



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













