refer:<br>Text Data Management and Analysis-A Practical Introduction to Information Retrieval and Text Mining, 2016 - Chapter 9 Search Engine Evaluation

###### Cranfield Evaluation Methodology (1960s)

It’s a methodology that has been very useful not only for search engine evaluation, but also for evaluating virtually all kinds of empirical tasks.

The basic idea of this approach is to build reusable test collections and define measures using these collections. Using these test collections, we will define measures that allow us to quantify the performance of a system or algorithm.

That is, we have the same criteria, same corpus, and same relevance judgments to compare the different algorithms.

###### Practical Issues in Evaluation

1. For documents and queries, they must represent real queries and real documents that users interact with. In order to evaluate a high-recall retrieval task, we must ensure there exist many relevant documents for each query. If a query has only one relevant document in the collection, then it’s not very informative to compare different methods using such a query because there is not much room to see a difference.
2. For relevance judgments (labeling), if we can’t afford judging all the documents in
   the collection, which subset should we judge? The solution here is **pooling**. This
   is a strategy that has been used in many cases to solve this problem. First, choose
   a diverse set of ranking methods; these are different types of retrieval systems.We
   hope these methods can help us nominate likely relevant documents. The goal is
   to pick out the relevant documents so the users can make judgements on them.
   That way, we would have each system return the top $k$ documents according to its
   ranking function. The $k$ value can vary between systems, but the point is to ask them to suggest the most likely relevant documents. We then simply combine all these top $k​$ sets to form a pool of documents for human assessors to judge. T<u>he remaining unjudged documents are assumed to be non-relevant and the human annotators do not need to spend time and effort manually judging them</u>. If the pool is large enough, this ==assumption== is perfectly fine. That means if your system participates in contributing to the pool then it’s unlikely that it will be penalized since the top-ranked documents have all been judged. However, this is problematic for evaluating a new system that may not have contributed to the pool, since the documents it returns may not have been judged and are assumed to be non-relevant.
3. For compare of two systems, we need to use many queries to avoid jumping
   to an incorrect conclusion that one system is better than another. Then using statistical significance test to quantify the difference.
4. It’s also challenging to correlate the evaluation measures with the perceived utility of users. We have to consider carefully what the users care about and then design measures to capture their <u>preferences</u>.
5. Some other evaluation strategies such as A-B testing. this is where an evaluating system would mix the results of two methods randomly, showing the mix of results to users. A-B testing can also be used to compare two different retrieval interfaces.

