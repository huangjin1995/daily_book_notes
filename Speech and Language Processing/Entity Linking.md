https://github.com/sebastianruder/NLP-progress/blob/master/english/entity_linking.md







### challenge

+ for long tail and newly emerging <u>entities</u> that have few or no links associated with them.

+ how to decide/discriminate the unlinkable entity in sentence ?

  Unlinkable Mention Prediction of Entity Linking.

  method 1 - threshold (manual setting or as a parameter to learn in rank)

  method 2 - a filter classifier (binary)

  method 3 - combined (add Unlinkable as candidate in rank)

+ Short text entity linking vs. Long text entity linking



### Tools

+ YODIE: Yet another Open Data Information Extraction system [site](https://gate.ac.uk/applications/yodie.html)



### Competition

+ the TAC-KBP track

  http://www.nist.gov/tac/about/index.html

  The Knowledge Base Population (KBP) track conducted as part of NIST Text Analysis Conference (TAC) is an international entity linking competition held every year since 2009. Entity linking is regarded as one of the two subtasks in this track.

+ Making Sense of Microposts 2016 - Named Entity rEcognition and Linking (NEEL) Challenge [site](http://microposts2016.seas.upenn.edu/challenge.html) 

  Overview of the EVALITA 2016 Named Entity rEcognition and Linking in Italian Tweets (NEEL-IT) Task [site](http://giusepperizzo.github.io/publications/Basile_Rizzo-2016neelit.pdf) 

+ NLP&CC 2013 - 中文微博实体链接 [site](http://tcci.ccf.org.cn/conference/2013/pages/page04_eva.html) 

+ 





### Conference

+ [Entity Linking and Retrieval Tutorial](https://github.com/ejmeij/entity-linking-and-retrieval-tutorial) 2014
+ 



### STOA

+ https://github.com/sebastianruder/NLP-progress/blob/master/chinese/chinese.md#entity-linking
+ https://github.com/sebastianruder/NLP-progress/blob/master/english/entity_linking.md
+ https://paperswithcode.com/task/entity-linking



### Scholars

+ [heng ji](http://nlp.cs.rpi.edu/hengji.html) 

+ 

  



### Literature review

+ [Entity Discovery and Linking and Wikification Reading List](http://nlp.cs.rpi.edu/kbp/2018/elreading.html)
+ "Information Extraction and Knowledge Base Population", Invited course for the 10th Russian Summer School in Information Retrieval, 2016. [200 slides](http://nlp.cs.rpi.edu/ie2016.pptx) or [300 slides](http://nlp.cs.rpi.edu/ie2016_long.pptx).
+ Entity Linking with a Knowledge Base: Issues, Techniques, and Solutions, Wei Shen, Jianyong Wang, and Jiawei Han 2015, [paper](http://dbgroup.cs.tsinghua.edu.cn/wangjy/papers/TKDE14-entitylinking.pdf) :star::star::star:



### paper

+ DeepType: Multilingual Entity Linking by Neural Type System Evolution, Jonathan Raiman, Olivier Raiman, AAAI 2018  [arxiv](https://arxiv.org/pdf/1802.01021.pdf) 

+ Neural Cross-Lingual Entity Linking, Avirup Sil, Gourab Kundu, Radu Florian, Wael Hamza, AAAI18, [arxiv](https://arxiv.org/abs/1712.01813) 

  细粒度上下文表示-只取mention所在句子的左边n个词和右边n个词

  句子级别上下文表示-取mention所在的整个句子

+ Analysis of Named Entity Recognition and Linking for Tweets, Leon Derczynski, Diana Maynard, Giuseppe Rizzo, Marieke van Erp, Genevieve Gorrell, Raphaël Troncy, Johann Petrak, Kalina Bontcheva, 2015, [arxiv](https://arxiv.org/abs/1410.7182) :star::star::star:

  

+ Joint Learning of the Embedding of Words and Entities for Named Entity Disambiguation, Ikuya Yamada, Hiroyuki Shindo, Hideaki Takeda, Yoshiyasu Takefuji, CoNLL 2016 [arxiv](https://arxiv.org/abs/1601.01343) :star:

  从词向量角度

+ Toward Socially-Infused Information Extraction: Embedding Authors, Mentions, and Entities, Yi Yang, Ming-Wei Chang, Jacob Eisenstein, EMNLP 2016, [arxiv](https://arxiv.org/abs/1609.08084v1) 

  For the task of entity linking in Twitter, Yang et al. (2016) employ the bilinear scoring function to learning the vector embedding of the entities, mentions, and context.

  

+ Collaborative Ranking: A Case Study on Entity Linking, Zheng Chen, Heng Ji, emnlp 2011 [arxiv](https://www.aclweb.org/anthology/D11-1071) 

  从文本排序角度



