[科研笔记：系统不能太精巧，正如人不能太聪明](http://blog.sciencenet.cn/home.php?mod=space&uid=362400&do=blog&id=721678)

[科普随笔：NLP主流最大的偏见，规则系统的手工性](http://blog.sciencenet.cn/blog-362400-701815.html)

[科普随笔：NLP主流成见之二，所谓规则系统的移植性太差](http://blog.sciencenet.cn/blog-362400-703502.html)

摘录语言学派和规律的大致对应关系（《认知能力与语言学理论》石毓智 89页，96页）：
演绎规律：经典数学和力学等     ----------------转换生成语言学
统计规律：遗传学、气象学等     -----------------语料库语言学
功能或目的规律：生物学、生命科学等  ---------功能语言学
发生规律：植物学、化学等            ----------语法化理论

### 计算语言学家

​	计算语言学家主要是根据自然语言的种种复杂现象，怎样设计语言处理的架构和流程，怎样突破规则系统的框架与其他语言处理包括机器学习进行协调，怎样平衡语言条件的宽窄，怎样与QA（质量检测）协调确保系统开发的健康，怎样保证语言学家团队编制规则的操作规范以确保系统的可持续性（data driven，unit testing，regression testing，code review，maintenability，baselines，等等等等），怎样根据语言开发需求对于现有形式框架的限制提出扩展要求，以及怎样保证复杂系统的鲁棒性等等。一个领头的计算语言学家就是一个系统的架构师，系统的成败绝不仅仅在于语言规则的编制及其堆积，更多的决定于系统架构的合理性。

​	架构合理指的是用语言学分析支持信息抽取的体系：一个不依赖领域的语言分析器作为基础；一个语言分析支持的依赖于领域的信息抽取器。只有后者才有移植性问题，前者是基本不随领域而变的（领域专业词典可以象用户词典那样外挂，语言学词典与规则内核可基本保持不变）。分析器做得越深入，抽取器就越简化，移植性则越强，因为快速开发领域抽取器的逻辑条件增强了。在深度分析（deep parsing）的逻辑语义基础上做抽取移植效果最佳。

### 规则系统

#### 什么是规则系统？

【立委科普：NLP 联络图 （之一）】

http://blog.sciencenet.cn/blog-362400-629730.html

???

在 *NLP* 领域，与机器学习平行的传统方法还有语言学家（*linguist*）或知识工程师（*knowledge engineer*）手工编制的语言规则（*Linguistic rules*, or *hand-crafted rules*），这些规则的集合称计算文法（*Computational grammar*），由计算文法支持（or 编译）的系统叫做规则系统（*Rule system*）。

#### 如何设计一个好的规则系统？

​	如果规则系统的架构和分析完全没有深度，只允许编写表层模式（surface patterns）的规则，直接连接输入与输出，用脚后跟想也可以得出移植性差的结论，因为表层规则依赖于任务，任务一换，辛辛苦苦编制调试出来的规则就没有再利用的可能。

​	对于浅层的NLP（Natural Language Processing）任务，譬如标注产生式合成词（productive compouds）、词性（Part of Speech tagging）、专名标注（Named Entity tagging）、日期、数量单位、邮递地址等（以机器学习为辅），而对于最常见的NLP应用，信息抽取、舆情抽取等，语言学家需要究竟背后的深层结构及其概括和推理。

​	规则系统可以设计成一个规则层级体系（rule hierarchy），独立于领域和应用方向的语言学规则组件（parsers）以及在语言学之上的针对领域和应用的信息抽取规则子系统。结果是，在转移应用目标时候，底层的语言学组件基本保持不变，而只需要重新编写不同的信息抽取规则而已。实践证明，对于规则系统，真正的知识瓶颈在语言学组件的构建上，而信息抽取本身花费不多。这是因为前者需要应对自然语言变化多端的表达方式，把它逻辑化，而后者是建立在逻辑形式（logical form）上的规则，一条等价于底层规则的几百上千条。

#### 示例

【立委科普：如何自动识别同一个意思千变万化的表达？】

http://blog.sciencenet.cn/home.php?mod=space&uid=362400&do=blog&id=1019639

???

### 系统不能太精巧

#### Anything involving more than 3 levels of dependency is too delicate

​	Countless lessons learned over the years in the NLP system development show that a robust real life system should not be too sophisticated just as man should not be too smart.  As a rule of thumb,  anything involving more than 3 levels of dependency is too delicate.  You can "make" it work today, but it will break some day.  One recent lesson was my effort to handle Chinese **long distance negation** and **satire in question forms**: it seemed to work, but in the end, it created more problems than it solved. Stay simple, stay foolish.<br>	以否定式为例，初始的规则是不考虑否定式的，大约有七成现象不涉及否定式（如：*iPhone 5 有问题*）。把否定带入是第一层（如：*iPhone 5 没有问题*），这时候应该涵盖约九成有关现象了。如果进一步考虑 double negation 的处理（如：*iPhone 5 并非没有问题*），算是第二层，那该到九成以上了。再进一步去对付远距离否定（如：*我不认为 iPhone 5 没有问题*；*iPhone 5 没有问题，是不可能的*），这就到第三层了。第三层人力还勉强可为，虽然已经很危险了。如果你还不知足藏拙适可而止，还要把系统进一步复杂化去对付远距离否定与反问句交互等复杂现象（如：*谁不认为 iPhone 5 没有问题*？），你开始越过红线，忘乎所以了。弄巧成拙，聪明反被聪明误，就是为你预备的警句。

+ 



