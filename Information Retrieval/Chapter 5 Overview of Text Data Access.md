### 5.3 Text Retrieval



### 5.5 Document Selection vs. Document Ranking

In general, we may ==assume== that there exists a subset of documents in the collection, i.e., $R(q) ⊂ C$, which are relevant to the user’s query $q$; that is, they
are relevant documents or documents useful to the user who typed in the query.
Naturally, this relevant set depends on the query $q$. However, which documents are relevant is generally unknown; the user’s query is only a “hint” at which documents should be in the set $R(q)$.Thus, the best a computer can do is to return an approximation of $R(q)$, which we will denote by $R^\prime(q)$.

Now, how can a computer compute $R^\prime(q)$? At a high level, there are two alternative strategies: document selection vs. document ranking.

In document selection, we will implement a binary classifier to classify a document as either relevant or non-relevant with respect to a particular query. <u>Using such a strategy</u>, the system must estimate the **absolute relevance**, i.e., whether a document is relevant or not.

In document ranking, we will implement a ranking function and rank all the documents in descending values of this ranking function and let the user decide a **cutoff**. A user would then browse the ranked list and stop whenever they consider it appropriate. <u>Using this strategy</u>, the system only needs to estimate the **relative relevance** of documents: which documents are more likely relevant.

Since estimation of relative relevance is intuitively easier than that of absolute relevance, we can expect it to be easier to implement the ranking strategy. Indeed, ranking is generally preferred to document selection for multiple reasons.<br>	First, due to the difficulty for a user to prescribe the exact criteria for selecting relevant documents, the binary classifier is unlikely accurate. Often the query is either over-constrained (result in no relevant documents) or under-constrained (result in too many relevant documents). Even if the classifier can
be accurate, a user would still benefit from prioritization of the matched relevant
documents for examination since a user can only examine one document at a time and some relevant documents maybe more useful than others (relevance is a matter of degree). For all these reasons, ranking documents appropriately becomes a main technical challenge in designing an effective text retrieval system.





