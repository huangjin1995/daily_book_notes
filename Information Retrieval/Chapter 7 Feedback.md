https://en.wikipedia.org/wiki/Relevance_feedback

Feedback takes the results of a user’s actions or previous search results to improve retrieval results.



### Feedback

#### relevance feedback

The first form of feedback is **relevance feedback**, we use <u>explicit relevance judgements</u>, which <u>require some user effort</u>, but this method is the most reliable.



#### pseudo relevance feedback

There is another form of feedback called **pseudo relevance feedback**, or **blind feedback**. In this case, we <u>don’t have to involve users</u> since we simply ==assume== that the top k ranked documents are relevant. Let’s say we assume the top k = 10 documents are relevant. Then, we will use these documents to learn and to improve the query (Do Query Expansion). Unfortunately, pseudo relevance feedback is not completely reliable; we have to arbitrarily set a **cutoff** and hope that the ranking function is good enough to get at least some useful documents.<br>(Below the cutoff is the negative feedback documents, above the cutoff is the positive feedback documents)

But it is not without the dangers of an automatic process. For example, if the query is about copper mines and the top several documents are all about mines in Chile, then there may be query drift in the direction of documents on Chile. In addition, if the words added to the original query are unrelated to the query topic, the quality of the retrieval is likely to be degraded, especially in Web search, where web documents often cover multiple different topics.

The procedure is:

1. Take the results returned by initial query as relevant results (only top k with k being between 10 and 50 in most experiments).
2. Select top 20-30 (indicative number) terms from these documents using for instance [tf-idf](https://en.wikipedia.org/wiki/Tf-idf) weights.
3. Do Query Expansion, add these terms to query, and then match the returned documents for this query and finally return the most relevant documents.



#### implicit feedback

There is also another feedback method called **implicit feedback**. In this case, we <u>still involve users</u>, but we don’t have to explicitly ask them to make judgements. Instead, we are going to observe how the users interact with the search results by observing their <u>clickthroughs</u> (<u>implicit relevance judgements</u>). If a user clicked on one document and skipped another, this gives a clue about whether a document is useful or not. We can even ==assume== that we’re going to use only the snippet here in a document that is displayed on the search engine results page (the text that’s actually seen by the user). We can ==assume== this displayed text is probably relevant or interesting to the user since they clicked on it. This is the idea behind implicit feedback.



### Feedback in Models

####  the Vector Space Model



#### the Language Models





### Summary

+ 

### Question

+ What kinds of the users relevance judgements or feedback can be used to improve future rankings?

+ 

+ 