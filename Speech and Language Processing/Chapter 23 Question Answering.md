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

#### semantic parsers

Systems for mapping from a text string to any logical form are called semantic
parsers. Semantic parsers for question answering usually map either to some
version of **predicate calculus** or **a query language** like SQL or SPARQL.

##### rule-based 

For relations that are very frequent, it may be worthwhile to write hand-written rules
to extract relations from the question.

##### supervised-based

Most supervised algorithms for learning to answer these simple questions about
relations first parse the questions and then align the parse trees to the logical form.
Generally these systems bootstrap by having **a small set of rules** for building this
mapping, and an initial lexicon as well. (For complex questions that are not just about single relations, use the complex rules to break each training example down into smaller tuples that can then be recombined to parse new sentences.)

Disadvantage: Supervised datasets can’t cover the wide variety of forms that even simple factoid questions can take.

##### semi-supervised-based/unsupervised-based

###### web

Most methods make some use of web text, either via semi-supervised methods like **distant supervision** or unsupervised methods like **open information extraction**.

Example: the REVERB open information extractor

It extracts billions of (subject, relation, object) triples of strings from the web, such as (“Ada Lovelace”,“was born in”, “1815”).

align a triple with a canonical knowledge source:

+ align the arguments (subject, object) - linking a string like “Ada Lovelace” with a Wikipedia page is called entity linking.

+ align the predicate (relation) - Given the Freebase relation people.person.birthdate(ada lovelace,1815) and the string ‘Ada Lovelace was born in 1815’, we learn the mapping between the string ‘was born in’ and the relation people.person.birthdate. In the simplest case, this can be done by aligning the relation with the string of words in between the arguments; more complex alignment algorithms like IBM Model 1 can be used. Then if a phrase aligns with a predicate across many entities, it can be extracted into a **lexicon** for <u>mapping questions to relations</u>. 

By aligning these strings with a canonical knowledge source like Wikipedia, we create new relations that can be queried while simultaneously learning to <u>map between the words in question and canonical relations</u>.

###### paraphrase databases

Example: wikianswers.com

It contains millions of pairs of questions that users have tagged as having the same meaning.

Pairs of question paraphrases can be aligned to each other using MT alignment approaches to create an MT-style phrase table for translating from question phrases to synonymous phrases. These can be used by question answering algorithms to generate all paraphrases of a question as part of the process of finding an answer.

#### Question

将查询拆分为两部-question选择、question解析，然后进入图谱查询？



### Application

#### DeepQA

The DeepQA system in IBM’s Watson are often hybrids, using both text datasets and structured knowledge bases to answer questions. DeepQA finds many candidate answers in both knowledge bases and in textual sources, and then scores each candidate answer using knowledge sources like geospatial databases, taxonomical classification, or other textual sources.

![DeepQA Architecture](https://github.com/bifeng/daily_book_notes/raw/master/resource/DeepQA_architecture.png)

+ Step 1 - question processing

  first, parsing, named entity tagging, relation extraction

  second, extract the focus, the answer type (also called the lexical answer type or LAT), and performs question classification and question sectioning. 

  + The focus

    The focus is the part of the question that co-refers with the answer, used for example <u>to align with a supporting passage</u>.

    The focus is extracted by hand-written rules.

  + The lexical answer type

    The lexical answer type is a word or words which tell us something about the semantic type of the answer.

    The lexical answer types are again extracted by rules: the default rule is to
    choose the syntactic headword of the focus. Other rules improve this default choice. In addition to using the rules directly as a classifier, they can instead be used as features in a logistic regression classifier that can return a probability as well as a lexical answer type.

  + Question classification

    The question is classified by type (definition question, multiple-choice,
    puzzle, fill-in-the-blank). This is generally done by writing pattern-matching regular expressions over <u>words</u> or <u>parse trees</u>.

+ Step 2 - candidate answer generation

  The candidate answers can either be extracted from text documents or from structured knowledge bases.

  + text documents

    The method for extracting answers from text depends on the type of text documents.

    + normal text documents

      first, generate a query from the question by eliminating stop words, and
      then up-weighting any terms which occur in any relation with the focus.

      second, passage search (extracting passages from the retrieved document or directly return the Wikipedia document titles of the highly ranked retrieved documents as the possible answers)

      third, extract candidate answers. Two common approaches are to extract all anchor texts in the document (anchor text is the text between <a> and <\a> used to point to a URL in an HTML page), or to extract all noun phrases in the passage that are Wikipedia document titles.

  + knowledge bases

+ Step 3 - candidate answer scoring

  This stage uses many sources of evidence to score the candidates.

  + the lexical answer type

    DeepQA includes a system that takes a candidate answer and a lexical answer type and returns a score indicating whether the candidate answer can be interpreted as a subclass or instance of the answer type.

  + 

+ Step 4






### spoken question answering

- QASR: Spoken Question Answering Using Semantic Role Labeling, [paper](http://www.cs.columbia.edu/~sstoyanchev/papers/Stenchikova_Tur_QASR_ASRU05-demo.pdf)



### TREC

Question Answering Track<br>https://trec.nist.gov/data/qamain.html

Factoid QA has been extensively studied in the framework of the TREC conferences
(TREC).



### Tutorials

+  Phrase-Indexed Question Answering: A New Challenge for Scalable Document Comprehension, EMNLP 2018, [arxiv](https://arxiv.org/abs/1804.07726) | [code](https://github.com/uwnlp/piqa)
+ 



