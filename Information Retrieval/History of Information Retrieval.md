refer:<br>M. Sanderson and W. B. Croft. 2012. The history of information retrieval research. Proc. of the IEEE, 100(Centennial-Issue):1444–1451, 2012. [paper](http://ciir-publications.cs.umass.edu/getpdf.php?id=1066) 

### Early use of computers for IR

IR as a research discipline was starting to emerge at this time with two important developments: how to index documents and how to retrieve them.

--> Indexing – the move towards words

+ The classic approach was to use a hierarchical subject classification scheme, such as the Dewey Decimal system, which assigned numerical codes to collection items.
+ Alternatives were proposed, most notably Taube et al’s **Uniterm** system [16], which was essentially a proposal to index items by a list of keywords. <u>As simple an idea as this seems today, this was at the time a radical step.</u> 

--> Ranked retrieval

+ The style of search was to use Boolean retrieval. A query was a logical combination of terms (a synonym of word in IR literature), which resulted in a set of those documents that exactly matched the query.

+ A probabilistic approach were proposed by Luhn [19] proposed and Maron, Kuhns, and Ray [20], where each document in the collection was assigned a score indicating its relevance to a given query. The documents were then sorted and those at the top ranks were returned to the user. The researchers manually assigned keywords to a collection of 200 documents, weighting those assignments based on the importance of the keyword to the document. The scores assigned to the documents were based on a probabilistic approach. 

  In the same year as Maron et al’s work, Luhn suggested “that the frequency of word occurrence in an article furnishes a useful measurement of word significance” [21]; his approach later became known as **term frequency** weighting.


### 1960s

Gerard Salton, who formed and led a large IR group, first at Harvard University, then at Cornell. The group produced numerous technical reports (the ISR reports), establishing ideas and concepts that are still major areas of investigation today.

--> A view of the documents and queries represent as **vectors**, it first proposed by Switzer [23]. Later, the similarity between a document and query vector was suggested by Salton [24].

--> The introduction of **relevance feedback** [25].

--> Others<br>	The clustering of documents with similar content; the statistical association of terms with similar semantic meaning, increasing the number of documents matched with a query by expanding the query with lexical variations (so called stems) or with semantically associated words, ...

### 1970s

--> Luhn’s term frequency ($tf$) weights (based on the occurrence of words within a document), were complemented with Spärck Jones’s work on word occurrence across the documents of a collection (**inverse document frequency** ($idf$)). The idea of combining these two weights ($tf \cdot idf$) was quickly adopted.

--> Salton synthesised the outputs of his group’s work on vectors to produce the **vector space model** [33].

--> An alternative means of modelling IR systems involved extending Maron, Kuhns and Ray’s idea of using probability theory. <br>	Robertson defined the probability ranking principle [34], which determined how to optimally rank documents based on probabilistic measures with respect to defined evaluation measures. <br>	Robertson and Spärck Jones [35] along with a derivation of the probabilistic model in Van Rijsbergen’s book [27] stimulated much research on this form of modelling.<br>	==Question==:<br>	The basic probabilistic model assumed that words in a document occurred independently of each other, which is a somewhat unrealistic assumption. How to incorporating term dependency into ranked retrieval ?

### 1980s – mid 1990s

--> Variations of $tf \cdot idf$ weighting schemes were produced (Salton and Buckley [36] reviewed an extensive range), the vector space model and the formal models of retrieval were extended.<br>	The original probabilistic model did not include $tf$ weights and a number of researchers worked to incorporate them in an effective and principled way. Amongst other achievements, this work ultimately led to the ranking function BM25 (Robertson et al, 199?).<br>	The most well-known vector space model is Latent Semantic Indexing (LSI) [37].<br>	Others explored computational linguistics approaches considering the syntax of words, their semantics; addressing anaphora, ambiguity, and named entities. A great deal of this work led to little or no improvement in the effectiveness of retrieval systems. One technique that was found to produce a level of improvement was stemming, the process of matching words to their lexical variants. Although stemming algorithms date back to the 1960s, Porter in the late 1970s developed a compact set of English language stemming rules; his Porter stemmer [38] continues to influence stemming design today.

--> Learning to rank<br>	Up to this point, the ranking functions used in search engines were manually devised and tuned by hand through experimentation.<br>	Fuhr [40] described work where the retrieval function was learned based on relevant documents identified for an existing set of queries. Fuhr’s idea was to tune the ranking function for all queries for a particular document collection.

--> TREC - Donna Harman and colleagues formed TREC (Text REtrieval Conference) [39].<br>	Working with these new data sets showed that the existing weighting and ranking functions were not ideally suited for these different collections, and different collections required different ranking and weighting approaches.

### Mid 1990s – present

The arrival of the web initiated the study of new problems in IR.

--> Web search<br>	==Question==:<br>	How to combat the various types of spam and also identify the best pages on the web? <br>	Two important developments to achieving these goals were link analysis and searching of anchor text – i.e. searching both the content of a web page and the text of links pointing (anchoring) to that page.

--> Exploiting query logs<br>	query processing - examining users’ queries, click patterns, and reformulations of queries enabled researchers to develop more effective query processing techniques based on understanding the user’s “intent”, such as automated spell correction [49]; automated query expansion [50], and more accurate stemming [51].<br>	learning to rank - Joachims [46] found the solutions for extracting valuable information from the very noisy log data, and use of logs to train a rank function.



--> The retrieval models that are the basis of the core ranking function of IR systems continued to be developed in this period.<br>	The introduction of a probabilistic approach using **language models**, described by Ponte and Croft [54] and by Hiemstra [55]. By taking a new view of the matching process between documents and queries, the language model approach provided new understanding of a wide range of IR processes, such as relevance feedback, forming clusters of documents, and term dependence.



--> Others<br>	IR systems should be able to serve such diverse needs, by finding “differently relevant” documents to rank.



--> New areas of search<br>	web IR to mobile IR or social IR: The rapid growth of mobile devices and social media introduce new areas of search. Such as user tagging, conversation retrieval, filtering and recommendation, and collaborative search is starting to provide effective new tools for managing personal and social information.<br>	Short query of web IR to Long query of QA IR: The supporting users who issue longer, more natural questions. Such as the question answering task in TREC [58], that dealt with finding simple answers in text to a limited range of questions (such as the “wh” questions “who” and “when”).



### Further reading



### Conclusions and future directions

