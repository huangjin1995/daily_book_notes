(Just read the introduction and conclusion of this paper)

A Sensitivity Analysis of (and Practitioners’ Guide to) Convolutional Neural Networks for Sentence Classification

a sensitivity analysis of <u>one-layer CNNs</u> to explore the effect of architecture components on model performance.



Motivation:

we selected this simple one-layer CNN in light of observed strong empirical performance, which <u>positions</u> it as a new standard baseline model.



#### Summary

+ This is a good ablation analysis.
+ It's assumption that the design of multi-layer CNNs' inter structure is less important to these parameters. That's wrong! Think about the ResNet.
+ The advice for practitioner are applicable only to datasets comprising sentences with similar properties to the those considered in this work. So, which datasets is more correlation with your task?

#### Conclusion

+ word vector representation or one-hot vectors

  if one has a sufficiently large amount of training data, the latter maybe a good shoot.

+ filter region size

  The filter region size can have a large effect on performance, and should be tuned.

+ feature maps number

  The number of feature maps can also play an important role in the performance.

+ pooling strategies

  1-max pooling uniformly outperforms other pooling strategies (local max pooling, global k-max pooling, local average pooling).

+ regularization

  Regularization has relatively little effect on the performance of the model (dropout rate, l2-norms).

##### Advice for practitioner

+ start from baseline configuration and using the fine-tuning of word2vec or GloVe, or one-hot vectors for large training dataset size.

| Description         | Values          |
| ------------------- | --------------- |
| input word vectors  | Google word2vec |
| filter region size  | (3,4,5)         |
| feature maps        | 100             |
| activation function | ReLU            |
| pooling             | 1-max pooling   |
| dropout rate        | 0.5             |
| l2 norm constraint  | 3               |

‘feature maps’ refers to the number of feature maps for each filter region size.

+ Line-search over the single filter region size to find the ‘best’ single region size. A reasonable range might be 1~10. But it's correlate with the sentence (average) length. 

  Once this ‘best’ region size is identified, it may be worth exploring combining multiple filters using regions sizes near this single best size, given that empirically multiple ‘good’ region sizes always outperformed using only the single best region size.

+ Alter the number of feature maps for each filter region size from 100 to 600, and when this is being explored, use a small dropout rate (0.0-0.5) and a large max norm constraint. Also pay attention whether the best value found is near the border of the range (Bengio, 2012). If the best value is near 600, it may be worth trying larger values.

+ Consider different activation functions if possible: ReLU and tanh are the best overall candidates. And it might also be worth trying no activation function at all for our one-layer CNN.

+ Use 1-max pooling; it does not seem necessary to expend resources evaluating alternative strategies.

+ Regarding regularization: When increasing the number of feature maps begins to reduce performance, try imposing stronger regularization, e.g., a dropout out rate larger than 0.5.





