### Question

+ What's the motivation for the bias objective ?



### Contribution

Introduce a novel tagging scheme for joint extract entities and relations. 

#### The Bias Objective

![joint_entity_relation_tag_loss](https://github.com/bifeng/daily_book_notes/raw/master/resource/joint_entity_relation_tag_loss.png)



It is biased towards relational labels to enhance links between entities, and get a relatively low ratio on the single entities (refer to those who cannot find their corresponding entities).



### Disadvantage

In this paper, we only consider the situation where an entity belongs to a triplet, and we leave identification of <u>overlapping relations</u> for future work.

we only use the NYT dataset.

论文作者主要考虑一个实体只属于一个三元组的情况.

（1）如果一个实体参与了多个关系类型不同三元组，这套标签就不能表达这个关系. 示例：`美国总统`川普，同时也是`川普公司`掌门人。这句话中有两个关系，也就是说川普这个实体是两个三元组的实体，而且这两个三元组关系类型不同，无法给川普打标签，或者说只能识别一个关系.

（2）也无法处理交叉关系. 示例：付笛声任静夫妇... 。该句子包含两种关系-`任静 付笛声 丈夫`与`付笛声 任静 妻子`.

（3）无法确定实体类型.



In the future work, we will replace the softmax function in the output layer with multiple classifier, so that a word can has multiple tags. In this way, a word can appear in multiple triplet results, which can solve the problem of overlapping relations.





