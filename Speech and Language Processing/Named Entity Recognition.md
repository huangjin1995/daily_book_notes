refer:<br>[面向新闻媒体的命名实体识别技术](https://mp.weixin.qq.com/s/onAU0jJpFMXY80aRGB6vIA) 



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

  



### literature review

+ A Survey on Deep Learning for Named Entity Recognition, Jing Li, Aixin Sun, Jianglei Han, Chenliang Li, 2018.12, [arxiv](https://arxiv.org/abs/1812.09449) 
+ A Survey on Recent Advances in Named Entity Recognition from Deep Learning models, Vikas Yadav, Steven Bethard, 2018, [paper](https://www.aclweb.org/anthology/C18-1182) 
+ A survey of named entity recognition and classification, David Nadeau, Satoshi Sekine, 2007, [paper](https://nlp.cs.nyu.edu/sekine/papers/li07.pdf)  :star::star::star::star:

### Paper

+ Neural architectures for named entity recognition, Guillaume Lample, Miguel Ballesteros, Sandeep Subramanian, Kazuya Kawakami, and Chris Dyer. NAACL 2016. [arxiv](https://arxiv.org/abs/1603.01360) :star::star::star::star:

  a CRF layers to decode the tag sequence

+ Ashish Vaswani, Yonatan Bisk, Kenji Sagae, and Ryan Musa. 2016. Supertagging with lstms. In Proceedings
  of the NAACL international conference. pages 232–237.

  a LSTM layers to decode the tag sequence

+ Arzoo Katiyar and Claire Cardie. 2016. Investigating lstms for joint extraction of opinion entities and relations.
  In Proceedings of the 54th ACL international conference.

  a LSTM layers to decode the tag sequence



### STOA

+ https://nlpprogress.com/english/named_entity_recognition.html
+ 



### tools

+ http://alchemy.cs.washington.edu/
+ ProbCog: A Toolbox for Statistical Relational Learning and Reasoning [code](https://github.com/opcode81/ProbCog) 
+ 









