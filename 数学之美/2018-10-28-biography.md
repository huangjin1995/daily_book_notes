天气：阴  
阅读时间：19日-下午  


## chapter 7
+ 弗里德里克·贾里尼克(Frederek Jelinek, 1932.11.18-2010.9.14)[1]  
学派 - 诺威格(Peter Norvig)[2]/费尔南多·皮耶尔(Fernando Pereira)[3]

    费尔南多·皮耶尔(Fernando Pereira)  
弟子 - Ryan Mcdonald[4]


+ 成就  
1). 在贾里尼克之前，科学家们把语音识别问题当作人工智能和模式匹配问题。而贾里尼克把它当成通信问题，并用两个隐含马尔可夫模型（声学模型和语言模型）把语音识别概括得清清楚楚。  
这个框架结构至今仍对语音和语言处理影响深远，它不仅从根本上使得语音识别有实用的可能，而且奠定了今天自然语言处理的基础。  
2). 贾里尼克和波尔(L. Bahl)、库克(J. Cocke)以及拉维夫(J. Raviv)的另一大贡献是BCJR算法，这是今天数字通信中应用最广的两个算法之一（另一个是维特比算法）。  

+ 境界  
一个人想要在自己的领域做到世界一流，他的周围必须有非常多的一流人物。
在学术上，最大的帮助是提高学术境界，告诉的最多是"什么方法不好"。

> Notes:
> "什么方法不好"，是从一生的经验教训中得到的，可以节省很多无用功的时间。

> reference:  
[1] http://www.clsp.jhu.edu/people/jelinek/promoce.html  
    http://googleresearch.blogspot.com/2010/09/remembering-fred-jelinek.html  
[2] http://www.norvig.com/  
[3] https://sites.google.com/site/fernandopereira/  
[4] https://ryanmcd.github.io/




天气：晴  
阅读时间：22日-晚


# chapter 13
+ 阿米特‧辛格尔（Amit Singhal）[1]

+ 简单的哲学  
  一直坚持寻找简单有效的解决方案，主要原因在于容易解释每一个步骤和方法背后的道理，便于出现问题时查错，也容易找到改进的目标。    
  譬如，通常对一类搜索有改进的方法，会对另一类搜索产生负面的影响。此时，就需要找出这个方法产生负面影响的原因和场景，并且避免它的发生。  
  
  简单而有效的解决方案，源于对搜索问题各个细节的仔细研究、深思熟虑、去伪存真的结果，也源于每天坚持分析一些搜索结果不好的例子。
  
  一个好的算法应该像AK-47冲锋枪那样：简单、有效、可靠性好而且容易读懂（易操作）。  
  
  先帮助用户解决80%的问题，再慢慢解决剩下的20%问题，是在工业界成功的秘诀之一（Growth Hack）-如果一开始就追求大而全的解决方案，之后长时间不能完成，最好不了了之，这是做事情的方法不对。


+ 简单的思想实现复杂的系统
思想简单 - ...  
使用简单 - 只需不断积累语料，可以不断提高模型的精度  
1). 隐含马尔可夫模型  
语音识别系统-SPHINX系统  
2). 有限状态机  
Google Now

> Notes:  
> 简单方法，之所以可行，某种程度上也在于大量数据的支撑。

> reference:  
[1] https://en.wikipedia.org/wiki/Amit_Singhal  




天气：晴  
阅读时间：27日-白天  


## chapter 22
+ 米奇·马库斯（Mitch Marcus）  
米奇·马库斯（Mitch Marcus）[1]  
弟子 - 迈克尔·柯林斯（Michael Collins）[2]、艾里克·布莱尔（Eric Brill）、大卫·雅让斯基（David Yarowsky）[3]、拉纳帕提（Adwait Ratnaparkhi）、Jason Eisner[4]

    迈克尔·柯林斯（Michael Collins）  
弟子 - Percy Liang[5]、Terry Koo[6]、Luke Zettlemoyer[7]  

    Jason Eisner  
弟子 - Noah Smith[8]  

+ 迈克尔·柯林斯  
追求完美 -  
1). 写了一个以他的名字命名的、在相当长一段时间内世界上最好的文法分析器（Sentence Parser）  
2). 博士论文堪称自然语言处理领域的范文，介绍了所有事情的来龙去脉，任何具备一点计算机和自然语言处理知识的人，都可以轻而易举地读懂他复杂的方法（在特征提取上做了深入的研究！）  

+ 艾里克·布莱尔  
简单才美-  
1). 基于变换规则的机器学习方法（Transformation Rule Based Machine learning）  
应用场景 - 词性标注、语音识别  

    示例：拼音转汉字
a - 寻找每个拼音对应最常见的汉字  
b - 根据上下文，列举所有同音字的替换规则 - “去伪存真”  
c - 将所有规则应用到事先标识好的语料，挑出有用的，删掉无用的 - “去粗取精”  
d - 重复b、c两步，直至找不出有用的为止  


+ Summary  
Michael Collins/Jason Eisner对NLP结构学习领域贡献极大  
David Yarowsky早年研究词义消歧，是著名的yarowsky algorithm的作者，后来做了很多跨语言学习的开创性工作  


> reference:  
[1] https://www.cis.upenn.edu/~mitch/  
[2] http://www.cs.columbia.edu/~mcollins/  
[3] http://www.cs.jhu.edu/~yarowsky/  
[4] http://www.cs.jhu.edu/~jason/  
[5] https://cs.stanford.edu/~pliang/  
[6] http://people.csail.mit.edu/maestro/  
[7] https://www.cs.washington.edu/people/faculty/lsz/  
[8] https://homes.cs.washington.edu/~nasmith/  
