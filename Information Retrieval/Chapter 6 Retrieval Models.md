

There are various different kinds of retrieval models which fall into different categories.

First, one family of the models are based on the similarity idea. Basically, we ==assume== that if a document is more similar to the query than another document is, we would say the first document is more relevant than the second one. So in this case, the ranking function is defined as the similarity between the query and the document. One well-known example of this case is the vector space model.

The second set of models are called probabilistic retrieval models. In this family of models, we follow a very different strategy. We ==assume== that queries and documents are all observations from random variables, and we ==assume== there is a binary random variable called R (with a value of either 1 or 0) to indicate whether a document is relevant to a query. We then define the score of a document with respect to a query as the probability that this random variable R is equal to 1 given a particular document and query. There are different cases of such a general idea. One is the classic probabilistic model, which dates back to work done in the 1960s and 1970s, another is the language modeling approach, and yet another is the divergence-from-randomness model.

## similarity

### vector space model





## probabilistic 

### classic probabilistic model



### language modeling



### divergence-from-randomness model





