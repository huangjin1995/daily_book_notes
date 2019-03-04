实际与理论相反的事实



1. 为什么batch size不是越大越好？

2. categorical column with hash bucket？

   we are forcing the different input values to a smaller set of categories. This means that two probably unrelated inputs will be mapped to the same category, and consequently mean the same thing to the neural network. 

   it turns out that hashing often works well in practice. That's because hash categories provide the model with some separation. The model can use additional features to further separate it from each other.

   [hashed_column](https://www.tensorflow.org/guide/feature_columns#hashed_column)

3. After column crossed, still include the original (uncrossed) features?

   when creating feature crosses, you typically still should include the original (uncrossed) features in your model. The independent latitude and longitude features help the model distinguish between examples where a hash collision has occurred in the crossed feature.

   [crossed_column](https://www.tensorflow.org/guide/feature_columns#crossed_column)

   









