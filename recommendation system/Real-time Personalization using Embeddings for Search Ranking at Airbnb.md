Real-time Personalization using Embeddings for Search Ranking at Airbnb, Mihajlo Grbovic (Airbnb); Haibin Cheng (Airbnb), KDD 2018, Best Paper 

Mihajlo Grbovic(Airbnb) talk in Recsys 2017 [slides]()



refer:<br>[从KDD 2018 Best Paper看Airbnb实时搜索排序中的Embedding技巧](https://zhuanlan.zhihu.com/p/55149901)<br>[Airbnb如何解决Embedding的数据稀疏问题？](https://zhuanlan.zhihu.com/p/57313656)





### Contribution

+ real time personalization

  由于在这些embedding相关的feature中，我们加入了“最近点击listing的相似度”，“最后点击listing的相似度”这类特征，由于这类特征的存在，用户在点击浏览的过程中就可以得到实时的反馈，搜索结果也是实时地根据用户的点击行为而改变，所以这无疑是一个real time个性化系统。

+ 





### Architecture



基于embedding得到不同的user-listing pair feature，然后输入搜索排序模型，得到最终的排序结果。



### embedding

how to construct the listing (短租房) and user(租客) embedding?

文章通过两种方式生成了两种不同的embedding分别capture用户的short term和long term的兴趣。

1. **一是通过click session数据生成listing的embedding**，生成这个embedding的目的是为了进行listing的相似推荐，以及对用户进行session内的实时个性化推荐。
2. **二是通过booking session生成user-type和listing-type的embedding**，目的是捕捉不同user-type的long term喜好。由于booking signal过于稀疏，Airbnb对同属性的user和listing进行了聚合，形成了user-type和listing-type这两个embedding的对象。

#### embedding based on click

该部分两个要点：

1. clicked listing数据清洗

   Airbnb主要利用click session数据中的clicked listings进行embedding。

   其中，click session指的是一个用户的一次搜索过程，clicked listings即为点击的listing序列，这个序列需要满足两个条件，一个是只有停留时间超过30s的listing page才被算作序列中的一个数据点，二是如果用户超过30分钟没有动作，那么这个序列会断掉，不再是一个序列。一是清洗噪声点和负反馈信号，二是避免非相关序列的产生。

   然后，把这个clicked listings组成的sequence当作一个“句子”样本，开始embedding的过程。

2. embedding目标函数

   正样本很自然的取自click session sliding window里的两个listing，负样本则是在确定central listing后随机从语料库（这里就是listing的集合）中选取一个listing作为负样本。

   

   针对其业务特点，在目标函数中新增以下样本：

   正样本：把booking的信息引入embedding。这样直观上可以使Airbnb的搜索列表更倾向于推荐之前booking成功session中的listing。从这个motivation出发，Airbnb把click session分成两类，最终产生booking行为的叫booked session，没有的称做exploratory session。

   负样本：为了更好的发现同一市场（marketplace）内部listing的差异性，Airbnb加入了另一组negative sample，就是在central listing同一市场的listing集合中进行随机抽样，获得一组新的negative samples。



cold start problem:<br>简言之，如果有new listing缺失embedding vector，就找附近的3个同样类型、相似价格的listing embedding进行平均得到。



embedding效果：<br>embedding不仅encode了price，listing-type等信息，甚至连listing的风格信息都能抓住，说明即使我们不利用图片信息，也能从用户的click session中挖掘出相似风格的listing。

#### question

+ 一个session中，点击的listings总体而言应该比较少，这样如何训练呢？

+ listing的id还是listing的内容作为输入？

  

+ 为什么Airbnb objective中正负样本的正负号正好跟word2vec objective的正负号正好相反？

+ Airbnb加入booked listing作为global context，为什么在objective中不加sigma加和符号？

+ 这里我们其实只得到了listing的embedding，如果是你，你会怎样在real time search ranking过程中使用得到的listing embedding？

+ 

  

#### embedding based on booking

为了捕捉用户的长期偏好，Airbnb在这里使用了booking session序列，比如用户在过去1年依次book过5个listing，即为一个booking listing序列。

但是该会遇到非常棘手的数据稀疏问题，表现在以下三点：

1. book行为的总体数量本身就远远小于click的行为，所以booking session集合的大小是远远小于click session的；

2. 单一用户的book行为很少，大量用户在过去一年甚至只book过一个房源，这导致很多booking session sequence的长度为1；

3. 大部分listing被book的次数也少的可怜，大家知道w2v要训练出较稳定有意义的embedding，item最少需要出现5-10次，但大量listing的book次数少于5次，根本无法得到有效的embedding。

Airbnb如何解决如此严重的数据稀疏问题，训练出有意义的user embedding和listing embedding呢？他们给出的答案是**基于某些属性规则做相似user和相似listing的聚合**。

聚合之后，获得user type和listing type。一种直观的生成新的booking listing序列的方式是这样，直接把user type当作原来的user id，生成一个由listing type组成的booking session。这种方法能够解决数据稀疏性的问题，却无法直接得到user type embedding。为了让user type embedding和listing type embedding在同一个vector space中生成，airbnb采用了一种比较“反直觉”的方式。

针对某一user id按时间排序的booking listing序列，$(l_1,l_2,\dots,l_M)$，我们用（user_type, listing_type）组成的元组替换，因此，sequence变成了
$$
((u_{type1},l_{type1}),(u_{type2},l_{type2}),\dots,(u_{typeM},l_{typeM}))
$$
​	其中，$l_{type1}$指的就是listing l1对应的listing type，$u_{type1}$指的是该user在book listing l1时的user type，由于某一user的user_type会随着时间变化，所以$u_{type1}$与$u_{type2}​$ 不一定相同。

​	由于我们用一个（user type，listing type）的元组替换掉了原来的listing，如何确定central item就成为了一个核心问题。针对该问题，文章的原话是这么说的：

> instead of listing l , the center item that needs to be updated is either user_type (ut) or listing_type (lt) depending on which one is caught in the sliding window.



embedding目标函数<br>

负样本：为了引入“房主拒绝”（reject）这个action，airbnb又在objective中加入了reject这样一个negative signal。

#### question

+ 为了使user type和listing type在一个vector space中，airbnb到底是怎么处理booking session的？

+ airbnb是如何进行query embedding，使其能够捕捉到推荐地点的语义信息的？
+ 







