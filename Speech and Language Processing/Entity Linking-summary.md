## methods

### end to end

将实体链指任务，放在实体识别上，即在实体识别中新增实体的类型标签。



### two stage model

#### embedding

1）训练多义词实体向量，计算实体相似度

2）

#### text match

文本匹配：计算当前实体的文本与候选实体的文本匹配程度

#### text classify

文本分类：根据候选实体的类型及其文本训练分类模型，计算当前实体的文本所指类型。

#### text rank

文本排序

##### Non-collective approaches

Non-collective approaches, which resolve one mention at each time relying on prior popularity, context similarity, and other local features with supervised models.

##### Collective approaches

Collective approaches, which disambiguate a set of relevant mentions simultaneously by leveraging the global topical
coherence between entities through graph-based approaches.





##### features for ranking

![features_for_ranking](https://github.com/bifeng/daily_book_notes/raw/master/resource/features_for_ranking.png)

refer - "Information Extraction and Knowledge Base Population", Invited course for the 10th Russian Summer School in Information Retrieval, 2016. [200 slides](http://nlp.cs.rpi.edu/ie2016.pptx) or [300 slides](http://nlp.cs.rpi.edu/ie2016_long.pptx).









