https://github.com/sebastianruder/NLP-progress/blob/master/english/entity_linking.md



### methods



+ 端到端模型

  1. 将实体链指任务，放在实体识别上，即在实体识别中新增实体的类型标签。

  

+ 两阶段模型

  1. 词向量：

     1）训练多义词实体向量，计算实体相似度

     2）

  2. 文本匹配：计算当前实体的文本与候选实体的文本匹配程度

  3. 文本分类：根据候选实体的类型及其文本训练分类模型，计算当前实体的文本所指类型。

  4. 

