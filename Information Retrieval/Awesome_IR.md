https://en.wikipedia.org/wiki/Information_retrieval

https://en.wikipedia.org/wiki/Learning_to_rank

Hang Li, Learning to Rank, Encyclopedia of Machine Learning and Data Mining, 729-734, 2017. ([pdf](http://www.hangli-hl.com/uploads/3/4/4/6/34465961/learning_to_rank.pdf))

Modern Information Retrieval: A Brief Overview, 2001 [paper](http://singhal.info/ieee2001.pdf)

### conference

+ SIGIR  Special Interest Group on Information Retrieval, 国际信息检
  索大会
+ TREC Text REtrieval Conference, 国际文本检索大会 

  [Tracks](https://en.wikipedia.org/wiki/Text_Retrieval_Conference)
+ WSDM

### scholars

+ 翟成祥 [illinois](http://czhai.cs.illinois.edu/) 语言模型
+ 杨益銘 [CMU](http://www.cs.cmu.edu/~yiming/) 文本分类
+ 刘铁岩 [自述](http://www.cnblogs.com/blessw/archive/2010/03/27/1698636.html) | [microsoft](https://www.microsoft.com/en-us/research/people/tyliu/) 排序学习-listwise approach to learning to rank



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
+ Microsoft [site](https://www.microsoft.com/en-us/research/project/mslr/) 

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

