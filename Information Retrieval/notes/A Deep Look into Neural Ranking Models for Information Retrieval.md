more refer:

- A Review on Deep Learning Techniques Applied to Answer Selection, COLING 2018 [paper](https://aclweb.org/anthology/C18-1181) 

  Three neural network architectures: siamese architecture, attentive architecture, compare-aggregate architecture.

- Deep Learning for Matching in Search and Recommendation

- https://github.com/NTMC-Community/awaresome-neural-models-for-semantic-match

  

refer:

[如何匹配两段文本的语义？](https://mp.weixin.qq.com/s/F9ZV4jV3UiVuKVz1aqgv9w) 



### Application

#### Ad-hoc retrieval



#### Question Answering

Question-answering (QA) attempts to automatically answer questions posed by users in natural languages based on some information resources. The questions could be from a closed or open domain, while the information resources could vary from structured data (e.g., knowledge base) to unstructured data (e.g., documents or Web pages). There have been a variety of task formats for QA, including <u>multiple-choice selection, answer passage/sentence retrieval, answer span locating, and answer synthesizing from multiple sources</u>. 

（In this survey, we focus on answer passage/sentence retrieval as it can be viewed as a typical IR problem.）

**vocabulary mismatch is still a basic problem in QA.**

Benchmark data sets: <br>TREC QA [53], WikiQA [37], WebAP [57, 58], **InsuranceQA**[59], WikiPassageQA [56] and MS MARCO [36].

#### Community Question Answering

Community question answering (CQA) aims to find answers to users' questions based on existing QA resources in CQA websites, such as Quora, Yahoo! Answers, Stack Overflow, and Zhihu. 

As a retrieval task, CQA can be further divided into two categories. The first is to directly retrieval answers from the answer pool, which is similar to the above QA task with some additional user behavioral data (e.g., upvotes/downvotes).(问题与答案匹配-只关注答案及用户行为) The second is to retrieve similar questions from the question pool, based on the assumption that answers to similar question could answer new questions. (问题与问题匹配-只关注问题)

(Unless otherwise noted, we will refer to the second task format as CQA.)

**vocabulary mismatch is still a challenging problem as both questions are short and there exist different expressions for the same intent.**

Benchmark data sets: <br>The Quora Dataset, Yahoo! Answers Dataset [25] and SemEval-2017 Task3 [64]. The recent proposed datasets include CQADupStack8 [65], ComQA9 [66] and LinkSO [67].

#### Paraphrase Identification



#### Natural Language Inference



#### Automatic Conversation

Automatic conversation (AC) aims to create an automatic human-computer dialog process for the purpose of <u>question answering, task completion, and social chat (i.e., chit-chat)</u>. In general, AC could be formulated either as an IR problem that aims to rank/select a proper response from a dialog repository or a generation problem that aims to generate an appropriate response with respect to the input utterance. 

（In this paper, we restrict AC to the social chat task with the IR formulation. This could be
further divided into single-turn conversation or multi-turn conversation.）

**vocabulary mismatch is no longer the central challenge in AC. Instead, it is critical to model correspondence/coherence and avoid general trivial responses.**

Benchmark data sets: <br>Ubuntu Dialog Corpus (UDC) [75, 77, 78], **Sina Weibo dataset** [74, 26, 79, 80], MSDialog [81, 30, 82] and **the "campaign" NTCIR STC** [83].

### Model Architecture



#### Symmetric vs. Asymmetric Architectures

**underlying assumptions**

**design principles**

**learning strategies**

##### Symmetric matching

Note here symmetric structure means that the inputs s and t can exchange their positions in the input layer without affecting the final output.

+ siamese networks

  Representative models include DSSM [13], CLSM [47] and LSTMRNN[48].

+ symmetric interaction networks

  Representative models include DeepMatch [14], Arc-II [17], MatchPyramid [18] and Match-SRNN [69].

+ compare-aggregate networks

  BiMPM...



##### Asymmetric matching

Note here asymmetric structure means if we change the position of the inputs s and t in the input layer, we will obtain totally different output.

Ad-hoc retrieval: Three major strategies used in the asymmetric architecture to handle the heterogeneity between the query and the document, namely query split, document split, and joint split.

![asymmetric_architecture](https://github.com/bifeng/daily_book_notes/raw/master/resource/asymmetric_architecture.png)

+ Query split is based on the assumption that most queries in ad-hoc retrieval are keyword based, so that we can split the query into terms to match against the document.

  A typical model based on this strategy is DRMM

+ Document split is based on the assumption that a long document could be partially relevant to a query under the scope hypothesis, so that we split the document to capture ne-grained interaction signals rather than treat it as a whole.

  A representative model based on this strategy is HiNT

+ Joint split, by its name, uses both assumptions of query split and document split. 

  A typical model based on this strategy is DeepRank.




Question Answering:  Three major strategies used in the asymmetric architecture to handle the heterogeneity between the question and the answering, namely attention, compare, aggregation, ....

+ Attention

  One-way Attention, which typically leverages the question representation to obtain the attention over candidate answer words in order the enhance the answer representation.

  For example, IARNN [86] and CompAgg [87] get the attentive answer representation sequence that weighted by the question sentence representation.

+ Compare

  

+ Aggregation

  



Community Question Answering: ...



Automatic Conversation: ...



#### Modular

##### Representation vs. Interaction

**underlying assumptions**

**design principles**

**learning strategies**

![representation_interaction_architectures](https://github.com/bifeng/daily_book_notes/raw/master/resource/representation_interaction_architectures.png)

###### Representation (global matching)

The underlying assumption of this type of architecture is that **relevance depends on compositional meaning of the input texts**.

Representation methods include fully-connected networks (DSSM), convolutional networks (Arc-I, CNTN, CLSM) and recurrent networks (LSTM-RNN, MV-LSTM).

Notes:

Representation-focused better fits tasks with the global matching requirement. This architecture is also more suitable for tasks with short input texts (since it is often difficult to obtain good high-level representations of long texts).

Moreover, models in this category are efficient for online computation, since one can pre-calculate representations of the texts offline.

###### Interaction (local matching)

The underlying assumption of this type of architecture is that **relevance is in essence about the relation between the input texts**, so it would be more effective to directly learn from interactions rather than from individual representations.

Interaction methods include non-parametric, parametric.

Non-parametric interaction functions are functions that reflect the closeness or distance between inputs without learnable parameters. In this category, some are defined over each pair of input word vectors, such as binary indicator function [18, 33], cosine similarity function [18, 61, 33], dot-product function [18, 33, 34] and radial-basis function [18]. The others are defined between a word vector and a set of word vectors, e.g. the matching histogram mapping in DRMM [21] and the kernel pooling layer in K-NRM [85].

Parametric interaction functions are adopted to learn the similarity/distance function from data. For example, Arc-II [17] uses 1D convolutional layer for the interaction between two phrases. Match-SRNN [69] introduces the neural tensor layer to model complex interactions between input words. In general, parametric interaction functions are adopted when there is sufficient training data since they bring the model flexibility at the expense of larger model complexity.

**Three most used interaction methods, always combined as a pipeline:**

+ **Attention**

  ...

+ **Comparison**

  ...

+ **Aggregation**

  ...

BiMPM

IARNN [86] and CompAgg [87] 

decomposable attention model - Parikh et al., EMNLP ‘16



Notes:

Interaction-focus better fits tasks that call for specific matching patterns (e.g., exact word matching) and diverse matching requirement [21], e.g., ad-hoc retrieval. This architecture also better fit tasks with heterogeneous inputs, e.g., ad-hoc retrieval and QA, since it circumvents the difficulty of encoding long texts. 

Unfortunately, models in this category are not efficient for online computation, since the interaction function cannot be pre-calculated.

##### Single-granularity vs. Multi-granularity

**underlying assumptions**

**design principles**

**learning strategies**

+ Single-granularity

  The underlying assumption of the single-granularity architecture is that **relevance can be evaluated based on the high level features** extracted from the single-form text inputs.

  Many neural ranking models fall in this category, with either symmetric (e.g., DSSM and MatchPyramid) or asymmetric (e.g., DRMM and HiNT) architectures, either representation-focused (e.g., ARC-I and MVLSTM) or interaction-focused (e.g., K-NRM and Match-SRNN).

+ Multi-granularity

  The underlying assumption of the multigranularity architecture is that **relevance estimation requires multiple granularities of features**, either from different-level feature abstraction or based on different
  types of language units of the inputs.

  There two basic types of multi-granularity, namely vertical multi-granularity and horizontal multi-granularity.

  ![multi-granularity_architectures](https://github.com/bifeng/daily_book_notes/raw/master/resource/multi-granularity_architectures.png)

  + Vertical multi-granularity takes advantage of the hierarchical nature of deep networks so that the evaluation function g could leverage different level abstraction of features for relevance estimation.

    For example, MultigranCNN, MACM.

  + Horizontal multi-granularity is based on the assumption that language has intrinsic structures (e.g., from words to phrases/n-grams or sentences), and we shall consider different types of language units as inputs, apply certain single-granularity architectures over each input form, and aggregate all the granularity for better relevance estimation. 

    For example, Conv-KNRM, MIX.

  With multi-granularity features extracted, models in this category are expected to better fit tasks that require fine-grained matching signals for relevance computation, e.g., ad-hoc retrieval [84] and QA [92]. However, the enhanced model capability is often reached at the expense of larger model complexity.

  



##### Deep vs. Wide

**underlying assumptions**

**design principles**

**learning strategies**



##### Nonlinear vs. Linear

**underlying assumptions**

**design principles**

**learning strategies**



##### Factorization vs. non-factorization

**underlying assumptions**

**design principles**

**learning strategies**



#### Ablation analysis

模型消融分析，可以从**模型组件**及**数据分布**两个方面分析模型架构的有效性！



##### Summary

1) Asymmetric的text不能交换位置，Symmetric可以交换位置。

2) Asymmetric的text长短不一，导致各自的embedding空间差异较大；Symmetric的长短差异较小。

3) 对于Asymmetric不好解决的问题，则转化为Symmetric。

4) Attention在Asymmetric中的效果较Symmetric中更为显著。

5）...

6）...





### Model Comparison

#### Empirical Comparison on Ad-hoc Retrieval

Overview of previously published results on ad hoc retrieval datasets. The citation in each row denotes the original paper where the method is proposed. The superscripts 1-5 denote that the results are cited from [21],[33],[34],[84], [28] respectively. The subscripts denote the model architecture belongs to (S)ymmetric or (A)symmetric/(R)epresentation-focused or (I)nteraction-focused or (H)ybrid/Singe-(G)ranularity or (Multi-granularity. The back slash symbols denote that there are no published results for the specic model on the specic data set in the related literature.

![empirical_comparison_on_ad_hoc_retrieval](https://github.com/bifeng/daily_book_notes/raw/master/resource/empirical_comparison_on_ad_hoc_retrieval.png)

#### Empirical Comparison on QA (TREC QA/WikiQA/Yahoo! Answers)

Overview of previously published results on QA benchmark data sets. The citation in each row denotes the original paper where the method is proposed. The superscripts 1-10 denote that the results are cited from [37], [69], [61], [86], [88], [121], [87], [122], [120], [92] respectively. The subscripts denote the model architecture belongs to (S)ymmetric or (A)symmetric/(R)epresentation-focused or (I)nteraction-focused or
(H)ybrid/Single-(G)ranularity or (M)ulti-granularity. The back slash symbols denote that there are no published results for the specic model on the specic data set in the related literature.

![empirical_comparison_on_qa](https://github.com/bifeng/daily_book_notes/raw/master/resource/empirical_comparison_on_qa.png)



https://paperswithcode.com/sota/question-answering-on-wikiqa

| Rank | Method                                                       | MAP   | MRR   | Paper Title                                                  | Year | Paper                                                        | Code                                                         |
| ---- | ------------------------------------------------------------ | ----- | ----- | ------------------------------------------------------------ | ---- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| 1    | [HyperQA](https://paperswithcode.com/paper/hyperbolic-representation-learning-for-fast) | 0.712 | 0.727 | [Hyperbolic Representation Learning for Fast and Efficient Neural Question Answering](https://paperswithcode.com/paper/hyperbolic-representation-learning-for-fast) | 2017 | [paper](https://paperswithcode.com/paper/hyperbolic-representation-learning-for-fast) | [code](https://paperswithcode.com/paper/hyperbolic-representation-learning-for-fast#code) |
|      |                                                              |       |       |                                                              |      |                                                              |                                                              |



#### Empirical Comparison on QA (TREC QA)

https://aclweb.org/aclwiki/Question_Answering_(State_of_the_art)

#### Empirical Comparison on PI (MSRP)

https://aclweb.org/aclwiki/Paraphrase_Identification_(State_of_the_art)

#### Empirical Comparison on NLI (SNLI)

https://nlp.stanford.edu/projects/snli/



https://paperswithcode.com/sota/natural-language-inference-on-snli

| Rank | Method                                                       | % Test Accuracy | % Train Accuracy | Parameters | Paper Title                                                  | Year | Paper | Code |
| ---- | ------------------------------------------------------------ | --------------- | ---------------- | ---------- | ------------------------------------------------------------ | ---- | ----- | ---- |
| 1    | [MT-DNN](https://paperswithcode.com/paper/multi-task-deep-neural-networks-for-natural) | 91.1            | 96.8             | 110m       | [Multi-Task Deep Neural Networks for Natural Language Understanding](https://paperswithcode.com/paper/multi-task-deep-neural-networks-for-natural) | 2019 |       |      |
| 2    | [Densely-Connected Recurrent and Co-Attentive Network Ensemble](https://paperswithcode.com/paper/semantic-sentence-matching-with-densely) | 90.1            | 95.0             | 53.3m      | [Semantic Sentence Matching with Densely-connected Recurrent and Co-attentive Information](https://paperswithcode.com/paper/semantic-sentence-matching-with-densely) | 2018 |       |      |
| 3    | [Fine-Tuned LM-Pretrained Transformer](https://paperswithcode.com/paper/improving-language-understanding-by) | 89.9            | 96.6             | 85m        | [Improving Language Understanding by Generative Pre-Training](https://paperswithcode.com/paper/improving-language-understanding-by) | 2018 |       |      |
| 4    | [300D DMAN Ensemble](https://paperswithcode.com/paper/discourse-marker-augmented-network-with) | 89.6            | 96.1             | 79m        | [Discourse Marker Augmented Network with Reinforcement Learning for Natural Language Inference](https://paperswithcode.com/paper/discourse-marker-augmented-network-with) | 2018 |       |      |
| 5    | [150D Multiway Attention Network Ensemble](https://paperswithcode.com/paper/multiway-attention-networks-for-modeling) | 89.4            | 95.5             | 58m        | [Multiway Attention Networks for Modeling Sentence Pairs](https://paperswithcode.com/paper/multiway-attention-networks-for-modeling) | 2018 |       |      |
| 6    | [450D DR-BiLSTM Ensemble](https://paperswithcode.com/paper/dr-bilstm-dependent-reading-bidirectional) | 89.3            | 94.8             | 45m        | [DR-BiLSTM: Dependent Reading Bidirectional LSTM for Natural Language Inference](https://paperswithcode.com/paper/dr-bilstm-dependent-reading-bidirectional) | 2018 |       |      |
| 7    | [300D CAFE Ensemble](https://paperswithcode.com/paper/compare-compress-and-propagate-enhancing) | 89.3            | 92.5             | 17.5m      | [Compare, Compress and Propagate: Enhancing Neural Architectures with Alignment Factorization for Natural Language Inference](https://paperswithcode.com/paper/compare-compress-and-propagate-enhancing) | 2017 |       |      |
| 8    | [ESIM + ELMo Ensemble](https://paperswithcode.com/paper/deep-contextualized-word-representations) | 89.3            | 92.1             | 40m        | [Deep contextualized word representations](https://paperswithcode.com/paper/deep-contextualized-word-representations) | 2018 |       |      |
| 9    | [KIM Ensemble](https://paperswithcode.com/paper/neural-natural-language-inference-models) | 89.1            | 93.6             | 43m        | [Neural Natural Language Inference Models Enhanced with External Knowledge](https://paperswithcode.com/paper/neural-natural-language-inference-models) | 2017 |       |      |
| 10   | [SLRC](https://paperswithcode.com/paper/i-know-what-you-want-semantic-learning-for) | 89.1            | 89.1             | 6.1m       | [I Know What You Want: Semantic Learning for Text Comprehension](https://paperswithcode.com/paper/i-know-what-you-want-semantic-learning-for) | 2018 |       |      |
| 11   | [Densely-Connected Recurrent and Co-Attentive Network](https://paperswithcode.com/paper/semantic-sentence-matching-with-densely) | 88.9            | 93.1             | 6.7m       | [Semantic Sentence Matching with Densely-connected Recurrent and Co-attentive Information](https://paperswithcode.com/paper/semantic-sentence-matching-with-densely) | 2018 |       |      |
| 12   | [448D Densely Interactive Inference Network (DIIN, code) Ensemble](https://paperswithcode.com/paper/natural-language-inference-over-interaction-1) | 88.9            | 92.3             | 17m        | [Natural Language Inference over Interaction Space](https://paperswithcode.com/paper/natural-language-inference-over-interaction-1) | 2017 |       |      |
| 13   | [300D DMAN](https://paperswithcode.com/paper/discourse-marker-augmented-network-with) | 88.8            | 95.4             | 9.2m       | [Discourse Marker Augmented Network with Reinforcement Learning for Natural Language Inference](https://paperswithcode.com/paper/discourse-marker-augmented-network-with) | 2018 |       |      |
| 14   | [BiMPM Ensemble](https://paperswithcode.com/paper/bilateral-multi-perspective-matching-for) | 88.8            | 93.2             | 6.4m       | [Bilateral Multi-Perspective Matching for Natural Language Sentences](https://paperswithcode.com/paper/bilateral-multi-perspective-matching-for) | 2017 |       |      |
| 15   | [ESIM + ELMo](https://paperswithcode.com/paper/deep-contextualized-word-representations) | 88.7            | 91.6             | 8.0m       | [Deep contextualized word representations](https://paperswithcode.com/paper/deep-contextualized-word-representations) | 2018 |       |      |
| 16   | [KIM](https://paperswithcode.com/paper/neural-natural-language-inference-models) | 88.6            | 94.1             | 4.3m       | [Neural Natural Language Inference Models Enhanced with External Knowledge](https://paperswithcode.com/paper/neural-natural-language-inference-models) | 2017 |       |      |
| 17   | [600D ESIM + 300D Syntactic TreeLSTM](https://paperswithcode.com/paper/enhanced-lstm-for-natural-language-inference) | 88.6            | 93.5             | 7.7m       | [Enhanced LSTM for Natural Language Inference](https://paperswithcode.com/paper/enhanced-lstm-for-natural-language-inference) | 2016 |       |      |

#### Empirical Comparison on QA (InsuranceQA)

a training set, a validation set, two test sets

The questions are much shorter than answers. The average length of questions is 7, and the average length of answers is 94.

|                                          | Top-1 Accuracy v1 | Top-1 Accuracy v2 |
| ---------------------------------------- | ----------------- | ----------------- |
| QA-LSTM with attention (avg pooling) [1] | 68.4              |                   |
| SUBMULT+NN[2]                            | 77.0              |                   |
|                                          |                   |                   |
|                                          |                   |                   |
|                                          |                   |                   |
|                                          |                   |                   |
|                                          |                   |                   |

v1: version1 dataset, v2: version2 dataset

Applying Deep Learning to Answer Selection: A Study and An Open Task, Minwei Feng, Bing Xiang, Michael R. Glass, Lidan Wang, Bowen Zhou ASRU 2015 [arxiv](https://arxiv.org/abs/1508.01585) | [english dataset](https://github.com/shuzi/insuranceQA) | [chinese dataset](https://github.com/Samurais/insuranceqa-corpus-zh) 

[1] LSTM-based Deep Learning Models for Non-factoid Answer Selection, Ming Tan, Cicero dos Santos, Bing Xiang, Bowen Zhou ICLR 2016 [arxiv](https://arxiv.org/abs/1511.04108) 

[2] is CompAgg[87]

### Reference



BiMPM: Bilateral Multi-Perspective Matching for Natural Language Sentences, Zhiguo Wang, Wael Hamza, Radu Florian, IJCAI 2017 [arxiv](https://arxiv.org/abs/1702.03814) | [code](https://github.com/zhiguowang/BiMPM) 



 