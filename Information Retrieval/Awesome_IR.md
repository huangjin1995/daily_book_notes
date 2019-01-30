https://en.wikipedia.org/wiki/Information_retrieval

https://en.wikipedia.org/wiki/Learning_to_rank

Hang Li, Learning to Rank, Encyclopedia of Machine Learning and Data Mining, 729-734, 2017. ([pdf](http://www.hangli-hl.com/uploads/3/4/4/6/34465961/learning_to_rank.pdf))

### conference

+ SIGIR  Special Interest Group on Information Retrieval, 国际信息检
  索大会
+ TREC Text REtrieval Conference, 国际文本检索大会 

  [Tracks](https://en.wikipedia.org/wiki/Text_Retrieval_Conference)
+ WSDM

### scholars

+ [Salton](http://link.zhihu.com/?target=http%3A//www.cs.cornell.edu/Info/Department/Annual96/Beginning/salton.html)（1927 - 1995）美国康奈尔大学：IR领域的奠基者，也因对**向量空间模型**（VSM）的贡献（ *In this model, both documents and queries are represented as vectors of term counts*）而被世人熟知，人称“*the Father of Information Retrieval*”

+ [Spark Jones](http://link.zhihu.com/?target=https%3A//www.cl.cam.ac.uk/misc/obituaries/sparck-jones/)（1935 - 2007）英国剑桥大学：NLP和IR的杰出先驱，同时也是**概率检索模型**（*Probabilistic model of retrieval*）的提出者之一。我们现在用的IDF term weighting就是她的贡献之一

+ [Stephen Robertson](http://www.staff.city.ac.uk/~sb317/) 微软英国剑桥研究院：概率检索模型的倡导者之一，并且开发了OKAPI检索系统

+ [W.B. Crofit](http://link.zhihu.com/?target=http%3A//ciir.cs.umass.edu/croft) 美国UMass CIIR：基于**统计语言建模IR模型**的提出者，并和CMU共同开发了Lemur工具（开源搜索引擎）

+ [Susan Dumais](http://link.zhihu.com/?target=http%3A//susandumais.com) 微软研究院：**隐形语义索引**LSI的提出者

+ [Thorsten Joachims](http://www.cs.cornell.edu/people/tj/) Cornell: Feedback

+ [聂建云](http://rali.iro.umontreal.ca/nie/jian-yun-nie-en/) Montreal：**跨語言檢索**、IR模型

  Université de Montréal

+ [翟成祥](http://czhai.cs.illinois.edu/) UIUC: 语言模型、IR模型、主題模型（Topic Model）

  University of Illinois at Urbana-Champaign

+ [杨益銘](http://www.cs.cmu.edu/~yiming/) CMU: 文本分类

+ [刘铁岩](https://www.microsoft.com/en-us/research/people/tyliu/)  [自述](http://www.cnblogs.com/blessw/archive/2010/03/27/1698636.html) Microsoft: 排序学习-listwise approach to learning to rank



### books

- Christopher D. Manning, Prabhakar Raghavan and Hinrich, 2008. Introduction to Information Retrieval, Cambridge University Press. [online-book](https://nlp.stanford.edu/IR-book/)

- Tie-Yan Liu. *Learning to Rank for Information Retrieval*, **Springer**, 2011.

- Semantic Matching in Search, by Hang Li and Jun Xu, Now Publisher, 2014 

  Hang Li, Semantic Matching in Search, SIGIR 2014 Workshop on Semantic Matching in Information Retrieval, Gold Coast, July 2014. ([slides](http://www.hangli-hl.com/uploads/3/4/4/6/34465961/semantic_matching_in_search.pdf))

  Hang Li, Jun Xu. Semantic Matching in Search. Foundations and Trends in Information Retrieval. Now Publishers, 2014. ([pdf](http://www.hangli-hl.com/uploads/3/4/4/6/34465961/ml_for_match-step2.pdf))



### datasets

+ LETOR (3.0, 4.0) - microsoft [site](https://www.microsoft.com/en-us/research/project/letor-learning-rank-information-retrieval/) 

+ Yandex [site](https://academy.yandex.ru/events/data_analysis/grant2009/) 

+ Yahoo! [site](https://webscope.sandbox.yahoo.com/catalog.php?datatype=c) 

  <details><summary>features</summary>
      1) Text match: The match score can be as simple as a count or can be more complex such as BM25. Counts can be
  the number of occurrences in the document, the number of missing query terms or the number of extra terms (i.e. not in the query). Some basic features are defined over the query terms, while some others are arithmetic functions (min, max, or average) of them. Finally, there are also proximity features which try to quantify how far in the document are the query terms (the closer the better).<br>
      2) Topical matching (topic level): This can for instance been done by classifying both the query and the document in a large topical taxonomy.<br>
      3) Click: For a given query and document, different click probabilities can be computed: probability of click, first click, last click, long dwell time click or only click. Also of interest is the probability of skip (not clicked, but a document below is).<br>
      4) Query<br>
      5) Document classifier<br>
      6) Document statistics<br>
      7) Web graph<br>
      8) External references<br>
      9) Time<br>
  </details>

+ Microsoft [site](https://www.microsoft.com/en-us/research/project/mslr/) 

  <details><summary>features</summary>
      1) Language Model: 	Language model approach for information retrieval (IR) with absolute discounting smoothing, Bayesian smoothing using Dirichlet priors or Jelinek-Mercer smoothing.<br>
      2) Click: click count, dwell time.<br>
      3) Quality: The score is outputted by a web page quality classifier.<br>
      4) Query<br>
      5) Document<br>
      6) Others
  </details>



Notes:<br>Proximity features, which are known to be powerful relevance signals improving
the mean average precision and ERR@20 by approximately 10% [Tao and Zhai
2007; Cummins and O’Riordan 2009; Boytsov and Belova 2010].-- [paper](https://trec.nist.gov/pubs/trec20/papers/srchvrs.web.update.pdf) 

### competition

- Yahoo! Learning to Rank Challenge

  Yahoo! Learning to Rank Challenge Overview, JMLR, 2011, [paper](http://proceedings.mlr.press/v14/chapelle11a/chapelle11a.pdf) 

  <details>
      <summary>notes </summary> 
   	1) regresson or decision tree?<br>
      The solutions to ranking problem are quite mature(?). All of them used decision trees and ensemble methods, and comparing the best solution of ensemble learning with the baseline of regression model (GBDT), the relevance gap is rather small.<br>
      The simple regression based and decision tree based:
      In general, the choice of the loss function is all the more critical as the class of function is small, resulting in underfitting; But when the class of functions is sufficiently large and underfitting is not an issue anymore, the choice of the loss function is of secondary importance.<br>
      For simple regression based model, gains can be obtained by designing a loss function specifically tuned for ranking.<br>
      For decision based model, the modeling complexity is large enough and squared loss optimization is sufficient.<br>
      2) transfer learning<br>
      The benefits from transfer learning seem limited(?).<br>

- 



### tools

+ RankSVM [site](http://www.cs.cornell.edu/people/tj/svm_light/svm_rank.html) 
+ 



### resources

+ Information on Information Retrieval (IR) books, courses, conferences and other resources, stanford, update to 2009, [site](https://nlp.stanford.edu/IR-book/information-retrieval.html) 
+ 信息检索学术资源整理 [site](https://zhuanlan.zhihu.com/p/32072517) 
+ 