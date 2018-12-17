句子压缩，在不改变或尽可能最小改变原句语义的情况下，使用句法知识消除不太重要的词或短语，将句子缩短。(speech and language processing, 2ed, chapter 23, bibliography)

#### 规则方法

1. 句法树（深层）

   首先使用句法分析得到句法树，其次通过裁剪规则删除多余的子树，最后评估规则裁剪出来的句法子树是否能够表述原句的基本意思。

2. 语义角色标注（浅层）

   语义角色标注是一种浅层的语义分析技术。SRL is figure out who did what do whom. 通过提取谓词-论元构建简单的句子。

3. Use a sequence labeling model to compress sentences


Sentence compression based PT(Polarity-target) pair extraction
– Simplify the extraction rules
– Improve the parsing accuracy 



Sentence Compression for Aspect-Based Sentiment Analysis, 2015 [paper](http://ir.hit.edu.cn/~car/papers/ieee2015-2.pdf)



难点：<br>结果无法量化，自动评测形成闭环！



