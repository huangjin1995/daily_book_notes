#### 1.3 Matching and Ranking

Learning to match is in fact feature learning for learning to rank, from the viewpoint of machine learning.

### Semantic Matching in Search

#### 2.1 Mathematical View

+ Supervised Learning

  Intuition: Query q is generated according to probability distribution P(q), document d is generated according to conditional probability distribution P(d|q), and response r is generated according to conditional probability distribution P(r|q, d).
  This corresponds to the following fact. Queries are submitted to the search system independently, documents are retrieved with the query words given a query, and the relevance can be approximately determined given a pair of query and document.



  Suppose that training data $(q_1,d_1,r_1), (q_2,d_2,r_2), \dots, (q_N,d_N,r_N)$ is given. Each sample is a triple representing query $q$, document $d$, and response $r$. The goal of learning to match is to learn a model represented by the conditional probability:
  $$
  P(r|q,d)
  $$
  Click through data collected at a search engine can be used as the training data.



  Click-through data is noisy. One common method for data cleaning is threshold
  cut-off. More research on the problem is surely necessary.

  Daxin Jiang, Jian Pei, and Hang Li. Mining search and browse logs for web search: A survey. ACM Trans. Intell. Syst. Technol., 4(4):57:1–57:37, October 2013.



  The challenges of the learning task include the large scale of problem and the sparseness of training data.

+ Unsupervised Learning

  Intuition: Given a query, we retrieve documents and calculate the conditional probabilities (matching scores) of documents with respect to the query, represented as P(d|q), and then rank the documents according to the conditional probabilities P(d|q).
  $$
  P(d|q) \propto P(d) P(q|d)
  $$
  where $P(d)$ denotes the prior probability of document $d$. 



  The matching degree between query $q$ and document $d$ can be represented by the conditional probability:
  $$
  P(q|d)
  $$




  The challenges for this learning task also lie in the large scale of problem and the sparseness of training data.

#### 2.2 System View

![architecture](https://github.com/bifeng/daily_book_notes/raw/master/resource/architecture_web_search_engine.png)

![query_understanding](https://github.com/bifeng/daily_book_notes/raw/master/resource/query_understanding.png)

![document_understanding](https://github.com/bifeng/daily_book_notes/raw/master/resource/document_understanding.png)

![query_document_matching](https://github.com/bifeng/daily_book_notes/raw/master/resource/query_document_matching.png)



### Question

+ Why not just training matching model use ranking object?
+ How to combine the matching model and the ranking model and avoid overfitting?
+ 