天气：晴  
阅读时间：2019-1-2-晨<br>

Question Answering - slp2 - chapter 23.2/ slp3 - chapter 23

Most question answering systems focus on **factoid questions**, questions that can be answered with simple facts expressed in short texts. The answers to the questions below can expressed by a personal name, temporal expression, or location.

By the early 1960s, systems used the two major paradigms of question answering: information retrieval-based and knowledge-based.

### Retrieval-based

Information-retrieval or IR-based question answering relies on the vast quantities of textual information on the web or in collections like PubMed. Given a user question, information retrieval techniques first find relevant documents and passages. Then systems (feature-based, neural, or both) use **reading comprehension algorithms** to read these retrieved documents or passages and draw an answer directly from spans of text.

![IR-based](https://github.com/bifeng/daily_book_notes/raw/master/resource/IR-based_factoid_question_answering.png)

#### Question Processing

##### query formulation (查询构建)

query expansion methods can add query terms in hopes of matching the particular form of the answer as it appears, like adding morphological variants of the content words in the question, or synonyms from a thesaurus.

query reformulation rules rephrase the question to make it look like a substring of possible declarative answers.

##### answer type detection

#### Document and Passage Retrieval

#### Answer Extraction

##### Neural Answer Extraction

###### Reading Comprehension Algorithm

The architecture of the Document Reader component of the DrQA system of Chen et al. (2017).

![reading comprehension algorithm](https://github.com/bifeng/daily_book_notes/raw/master/resource/reading_comprehension_algorithm_chen_2017.png)

Like most such systems, DrQA builds an embedding for the question, builds an embedding for each token in the passage, computes **a similarity function** between the question and each passage word in context, and then uses the question-passage similarity scores to decide where the answer span starts and ends.

paper: Chen, D., Fisch, A., Weston, J., and Bordes, A. (2017). Reading wikipedia to answer open-domain questions. In ACL 2017.

### Knowledge-based

knowledge-based question answering, a system instead builds a semantic representation of the query, mapping What states border Texas? to the logical representation: $\lambda$x.state(x) $\wedge$ borders(x, texas), or When was Ada Lovelace born? to the gapped relation: birth-year (Ada Lovelace, ?x). These meaning representations are then used to query databases of facts.

#### Question

如何选择合适的question进入图谱查询？

如何解析question？



### Application

#### DeepQA

the DeepQA system in IBM’s Watson are
often hybrids, using both text datasets and structured knowledge bases to answer
questions. DeepQA finds many candidate answers in both knowledge bases and in
textual sources, and then scores each candidate answer using knowledge sources like
geospatial databases, taxonomical classification, or other textual sources.



### spoken question answering

- QASR: Spoken Question Answering Using Semantic Role Labeling, [paper](http://www.cs.columbia.edu/~sstoyanchev/papers/Stenchikova_Tur_QASR_ASRU05-demo.pdf)



### TREC

Question Answering Track<br>https://trec.nist.gov/data/qamain.html

Factoid QA has been extensively studied in the framework of the TREC conferences
(TREC).



### Tutorials

+  Phrase-Indexed Question Answering: A New Challenge for Scalable Document Comprehension, EMNLP 2018, [arxiv](https://arxiv.org/abs/1804.07726) | [code](https://github.com/uwnlp/piqa)
+ 



