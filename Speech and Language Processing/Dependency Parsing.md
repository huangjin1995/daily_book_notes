more refer:<br>[Dependency Parsing - Introduction Christopher Manning](http://spark-public.s3.amazonaws.com/nlp/slides/Parsing-Dependency.pdf) 

refer:<br>[NLP 笔记 - Dependency Parsing and Treebank](http://www.shuang0420.com/2017/03/09/NLP%20%E7%AC%94%E8%AE%B0%20-%20Dependency%20Parsing%20and%20Treebank/)



A dependency tree is a tree structure composed of the input words and satisfies a few constraints:
– Single-head
– Connected
– Acyclic



#### Application

It reveals the dependency <u>relationships</u> between words, especially the distance dependency.



+ semantic role labeling
+ relation extraction, question answering



#### Methods

Dependency Parsing 主要解决 linking 和 shifting 的问题，通常可以用机器学习分类器来解决。

- Dynamic programming (CFG with heads + CKY)
  和 lexicalized PCFG parsing 类似
  时间复杂度：O(n^5)
  Eisner (1996) 提出一种 O(n^3) 的算法, 在结束的时候再产生 items with heads 而不是在中间产生

- Graph algorithms
  McDonald et al.’s (2005) MSTParser(Maximum Spanning Tree), 单独用 ML 分类器来给 dependencies 算分

- Constraint Satisfaction
  Karlsson (1990), etc. 建立所有 links, 然后删掉不符合 hard constraints 的 link

- “Deterministic parsing”
  Nivre et al. (2008): MaltParser, Greedy choice of aKachments guided by ML classifiers

- MaltParser

  ...



#### Features

- Bilexical affinities
  issues→the is plausible
- Dependency distance
  mostly short links
- Intervening material
  Dependencies rarely span intervening verbs or punctuation
- Valency of heads
  How many dependents on which side are usual for a head?
- Some lexical word links are more common



#### Dataset

[The Prague Dependency Treebanks](https://ufal.mff.cuni.cz/pdt2.0/): Extremely high quality

[The Google Universal Dependency Treebanks](http://universaldependencies.org/) 



#### Tools

[Tregex](http://nlp.stanford.edu/software/tregex-faq.shtml)
[T-Regex operators](http://nlp.stanford.edu/manning/courses/ling289/Tregex.html)
[T-surgeon](http://nlp.stanford.edu/nlp/javadoc/javanlp/edu/stanford/nlp/trees/tregex/tsurgeon/Tsurgeon.html)



#### Papers

+ A Fundamental Algorithm for Dependency Parsing [paper](http://www.covingtoninnovations.com/mc/dgpacmcorr.pdf) 

**graph-based dependency parser**

- Bernd Bohnet. 2010. *Very High Accuracy and Fast Dependency Parsing is not a Contradiction*. The 23rd International Conference on Computational Linguistics (COLING 2010), Beijing, China. 

**transition-based dependency parser**:

- Bernd Bohnet and Joakim Nivre. 2012 *A Transition-Based System for Joint Part-of-Speech Tagging and Labeled Non-Projective Dependency Parsing.* EMNLP-CoNLL, pages 1455-1465 [pdf| bib]

- Bernd Bohnet and Jonas Kuhn. 2012. *The Best of BothWorlds -- A Graph-based Completion Model for Transition-based Parsers.* Proceedings of the 13th Conference of the European Chapter of the Association for Computational Linguistics (EACL), pages 77--87 [pdf|bib]





