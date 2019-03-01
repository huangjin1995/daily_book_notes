https://github.com/wzhe06/Reco-papers



### Challenge

+ position bias

  推荐系统实际上是“猜你喜欢”，但是因为“喜欢”太难衡量，所以我们经常用“用户点击”来代替“喜欢”来构建训练集。

  但是，“点击”信号与真正“喜欢”之间还是有较大的距离。比如，用户点击的可能他并不喜欢，只是排序比较靠前；用户未点击的，用户未必不喜欢，只是因为位置太靠后，压根没有曝光的机会。这种由位置造成的“点击”与“喜欢”之间的偏差，就是position bias，可能会带偏模型。

  + solution for supervised learning

    如果使用了历史ctr作为特征，而替换成使用coec（归一化点击率）作为特征。

    另外常见的作法是，在训练时，将position作为参数直接入模型参与训练，来解释y值中由位置引入的贡献。

    但是，在预测时，我们肯定不知道position是多少，因此都赋成0，(假设所有物料都放在第一位)，再打分，然后再根据打分排序。

  + solution for unsupervised learning

  

  