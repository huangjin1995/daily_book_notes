天气：阴  
阅读时间：早班车<br>记录时间:  25-晨

Semantic Role Labeling - slp2 - chapter 20.9/ slp3 - chapter 18



more refer:<br>https://web.stanford.edu/~jurafsky/slp3/slides/22_SRL.pdf



### Semantic Role Labeling



#### What's SRL?

Who      did what      to whom    when and where

Agent    Predicate    Theme      Time          Location

​	Semantic roles are representations that express the abstract role that arguments of a predicate can take in the event; these can be very specific, like the BUYER, abstract like the AGENT, or super-abstract (the PROTO-AGENT). These roles can both represent general semantic properties of the arguments and also express their likely relationship to the syntactic role of the argument in the sentence.

#### Why we need the SRL?

​	Semantic roles is to act as a shallow meaning representation that can let us make simple inferences that aren’t possible from the pure surface string of words (字面意义), or even from the parse tree (句法分析). It's useful in dealing with complications like **diathesis alternations**. <br>(Many verbs allow their thematic roles to be realized in various syntactic positions, these multiple argument structure realizations are called verb alternations or diathesis alternations)



#### What's the difficulty of SRL?

It's very difficult to come up with a standard set of roles, and equally difficult to produce a formal definition of roles like AGENT, THEME, or INSTRUMENT.

1. Role like AGENT or THEME often need to fragment into many specific roles.
2. Can not reason about and generalize across semantic roles with finite discrete lists of roles.
3. It's difficult to formally define the thematic roles.

These problems have led to alternative semantic role models that use either many fewer or many more roles.

The first of these options is to define generalized semantic roles that abstract over the specific thematic roles. For example, PROTO-AGENT and PROTO-PATIENT are generalized roles that express roughly agent-like and roughly patient-like meanings. These roles are defined, not by necessary and sufficient conditions, but rather by a set of heuristic features that accompany more agent-like or more patient-like meanings.

The second direction is instead to define semantic roles that are specific to a particular verb or a particular group of semantically related verbs or nouns.

**PropBank** uses both proto-roles and verb-specific semantic roles. **FrameNet** uses semantic roles that are specific to a general semantic idea called a frame.

#### Methods (How)

##### classification problem

语义角色标注大致分为四个步骤：

1. 将问题给出的句子进行句法分析得到句法树。并对句法树进行剪枝，去掉不可能成为语义角色的标注单元。

2. 使用分类器给选出的候选论元。

3. 对论元进行分类，类别为所有的语义角色标签。有些系统中也将2、3步骤合为一步，也就是将非语义角色也作为一个分类标签，在本文中就是使用的这种方法。

4. 后处理。在此步骤中，常常做一些强制的一致性限制。

可以看出，语义角色标注的核心就是对论元进行语义标签的分类。语义角色标注的不同方法，其实就是针对这个问题设计不同的更加高效的分类器。

##### sequence labeling problem



#### Application

##### Question Answering

+ Using Semantic Roles to Improve Question Answering, EMNLP 2007, [paper](http://www.aclweb.org/anthology/D07-1002)

  method: view semantic role assignment as an optimization problem in a bipartite
  graph and answer extraction as an instance of graph matching.

  data: the TREC datasets

+ QASR: Spoken Question Answering Using Semantic Role Labeling, [paper](http://www.cs.columbia.edu/~sstoyanchev/papers/Stenchikova_Tur_QASR_ASRU05-demo.pdf)



##### Machine Translation

Shallow semantics might act as a useful **intermediate language** in machine translation.



#### Example

谓词相同，语义不变的情况

Example: SRL语义标注结果一致<br>昨天 ， 张三 用球拍打了李四 。<br>李四 昨天被 张三 用球拍 打了 。<br>昨天 ，用一个球拍，张三 把 李四 打了。

谓词改变但语义不变的情况

Example: SRL语义标注结果不一致<br>“豪华汽车制造商去年销售了1214辆汽车。”<br>“豪华汽车制造商去年汽车的出售量是1214辆。”

谓词时态改变但语义改变的情况

Example: SRL语义标注结果一致<br>“豪华汽车制造商将要销售大量汽车。”<br>“豪华汽车制造商已销售了大量汽车。”

### Tutorials

- Semantic Role Labeling Tutorial at [NAACL 2013](http://naacl2013.naacl.org/) [site](http://ivan-titov.org/teaching/srl-tutorial-naacl13/) 
- [CoNLL-2005 Shared Task: Semantic Role Labeling](http://www.lsi.upc.es/~srlconll/)
- [Illinois Semantic Role Labeler](http://cogcomp.cs.illinois.edu/page/software_view/SRL) state of the art semantic role labeling system [Demo](http://cogcomp.cs.illinois.edu/page/demo_view/SRL), uses PropBank.
- [Preposition SRL](https://github.com/CogComp/cogcomp-nlp/tree/master/prepsrl): Identifies semantic relations expressed by prepositions
- [Shalmaneser](http://www.coli.uni-saarland.de/projects/salsa/shal/) is another state of the art system for assigning semantic predicates and roles.

1. [Mate tools](http://code.google.com/p/mate-tools/) (which I'm currently using), uses Propbank style
2. [BioKIT](http://nlp.comp.nus.edu.sg/software) - SRL for biomedical text
3. [SEMAFOR](http://www.ark.cs.cmu.edu/SEMAFOR/) - the parser (MST) requires 8GB of RAM
4. [Propbank-Nombank frames](http://nlp.cs.lth.se/software/semantic_parsing:_propbank_nombank_frames/) and [The LTH System for Frame-Semantic Structure Extraction ](http://nlp.cs.lth.se/software/semantic_parsing:_framenet_frames/)may be related to Mate tools
5. [ClearNLP](http://clearnlp.wikispaces.com/)
6. [CogCompNLP pipeline](https://github.com/CogComp/cogcomp-nlp/tree/master/pipeline): multiple versions of SRL (verb, preposition, comma, noun)

http://sourceforge.net/projects/swirl-parser/

https://blog.csdn.net/ilovewindseed/article/details/8841365

http://www.kenvanharen.com/2012/11/comparison-of-semantic-role-labelers.html

https://github.com/talnsoftware/deepsyntacticparsing/wiki

### Paper



 中文语义角色标注的特征工程, 2007 [paper](http://ir.hit.edu.cn/~car/papers/chinese_srl_jocip.pdf)



+ Deep Semantic Role Labeling with Self-Attention AAAI 2018 [arxiv](https://arxiv.org/abs/1712.01586) | [code](https://github.com/XMUNLP/Tagger) 

- Encoding Sentences with Graph Convolutional Networks for Semantic Role Labeling EMNLP 2017 [paper](https://arxiv.org/abs/1703.04826) | [code](https://github.com/diegma/neural-dep-srl)

- A Simple and Accurate Syntax-Agnostic Neural Model for Dependency-based Semantic Role Labeling CoNLL 2017 [paper](https://arxiv.org/abs/1701.02593)  | [code](https://github.com/diegma/neural-dep-srl)

- Deep Semantic Role Labeling: What works and what's next, ACL 2017 [paper](https://homes.cs.washington.edu/~luheng/files/acl2017_hllz.pdf) | [code](https://github.com/luheng/deep_srl) 

- Chinese LTP - A Unified Architecture for Semantic Role Labeling and Relation Classification, Coling 2016 [paper](http://ir.hit.edu.cn/~car/papers/coling16guo-2.pdf) 

- Anders Björkelund, Love Hafdell, and Pierre Nugues. *Multilingual semantic role labeling.* In Proceedings of The Thirteenth Conference on Computational Natural Language Learning (CoNLL-2009), pages 43--48, Boulder, June 4--5 2009.

- Automatic Labeling of Semantic Roles, Daniel Gildea and Daniel Jurafsky. 2000 [paper](https://www.cs.rochester.edu/~gildea/gildea-cl02.pdf) 

- 

### Question

+ what's the difference of ... and **CCG** SRL?