+ Tracks

  TREC QA tracks 

  Microblog tracks

  ...

### Application

#### Ad-hoc retrieval



#### Question Answering

Question-answering (QA) attempts to automatically answer questions posed by users in natural languages based on some information resources. The questions could be from a closed or open domain, while the information resources could vary from structured data (e.g., knowledge base) to unstructured data (e.g., documents or Web pages). There have been a variety of task formats for QA, including <u>multiple-choice selection, answer passage/sentence retrieval, answer span locating, and answer synthesizing from multiple sources</u>. 

（In this survey, we focus on answer passage/sentence retrieval as it can be viewed as a typical IR problem.）

**vocabulary mismatch is still a basic problem in QA.**

Benchmark data sets: <br>TREC QA [53], WikiQA [37], WebAP [57, 58], InsuranceQA[59], WikiPassageQA [56] and MS MARCO [36].

#### Community Question Answering

Community question answering (CQA) aims to find answers to users' questions based on existing QA resources in CQA websites, such as Quora, Yahoo! Answers, Stack Overflow, and Zhihu. 

As a retrieval task, CQA can be further divided into two categories. The first is to directly retrieval answers from the answer pool, which is similar to the above QA task with some additional user behavioral data (e.g., upvotes/downvotes).(问题与答案匹配-只关注答案及用户行为) The second is to retrieve similar questions from the question pool, based on the assumption that answers to similar question could answer new questions. (问题与问题匹配-只关注问题)

(Unless otherwise noted, we will refer to the second task format as CQA.)

**vocabulary mismatch is still a challenging problem as both questions are short and there exist different expressions for the same intent.**

Benchmark data sets: <br>The Quora Dataset, Yahoo! Answers Dataset [25] and SemEval-2017 Task3 [64]. The recent proposed datasets include CQADupStack8 [65], ComQA9 [66] and LinkSO [67].

#### Automatic Conversation

Automatic conversation (AC) aims to create an automatic human-computer dialog process for the purpose of <u>question answering, task completion, and social chat (i.e., chit-chat)</u>. In general, AC could be formulated either as an IR problem that aims to rank/select a proper response from a dialog repository or a generation problem that aims to generate an appropriate response with respect to the input utterance. 

（In this paper, we restrict AC to the social chat task with the IR formulation. This could be
further divided into single-turn conversation or multi-turn conversation.）

**vocabulary mismatch is no longer the central challenge in AC. Instead, it is critical to model correspondence/coherence and avoid general trivial responses.**

Benchmark data sets: <br>Ubuntu Dialog Corpus (UDC) [75, 77, 78], Sina Weibo dataset [74, 26, 79, 80], MSDialog [81, 30, 82] and the "campaign" NTCIR STC [83].

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

+ One-way Attention, which typically leverages the question representation to obtain the attention over candidate answer words in order the enhance the answer representation.

  For example, IARNN [86] and CompAgg [87] get the attentive answer representation sequence that weighted by the question sentence representation.



Question Answering: 



Community Question Answering: 



Automatic Conversation: 

#### Modular

##### Representation vs. Interaction

**underlying assumptions**

**design principles**

**learning strategies**

![representation_interaction_architectures](https://github.com/bifeng/daily_book_notes/raw/master/resource/representation_interaction_architectures.png)

+ Representation (global matching)

  The underlying assumption of this type of architecture is that **relevance depends on compositional meaning of the input texts**.

  Representation methods include fully-connected networks (DSSM), convolutional networks (Arc-I, CNTN, CLSM) and recurrent networks (LSTM-RNN, MV-LSTM).

  Notes:

  Representation-focused better fits tasks with the global matching requirement. This architecture is also more suitable for tasks with short input texts (since it is often difficult to obtain good high-level representations of long texts).

  Moreover, models in this category are efficient for online computation, since one can pre-calculate representations of the texts offline.

+ Interaction (local matching)

  The underlying assumption of this type of architecture is that **relevance is in essence about the relation between the input texts**, so it would be more effective to directly learn from interactions rather than from individual representations.

  Interaction methods include non-parametric, parametric.

  Non-parametric interaction functions are functions that reflect the closeness or distance between inputs without learnable parameters. In this category, some are defined over each pair of input word vectors, such as binary indicator function [18, 33], cosine similarity function [18, 61, 33], dot-product function [18, 33, 34] and radial-basis function [18]. The others are defined between a word vector and a set of word vectors, e.g. the matching histogram mapping in DRMM [21] and the kernel pooling layer in K-NRM [85].

  Parametric interaction functions are adopted to learn the similarity/distance function from data. For example, Arc-II [17] uses 1D convolutional layer for the interaction between two phrases. Match-SRNN [69] introduces the neural tensor layer to model complex interactions between input words. In general, parametric interaction functions are adopted when there is sufficient training data since they bring the model flexibility at the expense of larger model complexity.

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

只有少量涉及消融分析的论文，可以精读！



### Model Comparison

Overview of previously published results on QA benchmark data sets. The citation in each row denotes the original paper where the method is proposed. The superscripts 1-10 denote that the results are cited from [37], [69], [61], [86], [88], [121], [87], [122], [120], [92] respectively. The subscripts denote the model architecture belongs to (S)ymmetric or (A)symmetric/(R)epresentation-focused or (I)nteraction-focused or
(H)ybrid/Single-(G)ranularity or (M)ulti-granularity. The back slash symbols denote that there are no published results for the specic model on the specic data set in the related literature.

![empirical_comparison_on_qa](https://github.com/bifeng/daily_book_notes/raw/master/resource/empirical_comparison_on_qa.png)





