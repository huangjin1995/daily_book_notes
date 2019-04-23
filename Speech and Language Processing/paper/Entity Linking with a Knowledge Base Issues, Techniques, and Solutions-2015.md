Entity linking is also called Named Entity Disambiguation (NED) in the NLP community.

## challenge

name variations and entity ambiguity. 

A named entity may have multiple surface forms, such as its full name, partial names, aliases, abbreviations, and alternate spellings.

On the other hand, an entity mention could possibly denote different named entities.

## related tasks

entity coreference resolution

word sense disambiguation

record linkage

## architecture 

Generally speaking, a typical entity linking system consists of the following three modules:

+ Candidate Entity Generation

+ Candidate Entity Ranking

+ Unlinkable Mention Prediction

  

### Candidate Entity Generation





### Candidate Entity Ranking

We can broadly divide these candidate entity ranking methods into two categories:

+ Supervised ranking methods. These approaches rely on annotated training data to “learn” how to rank the candidate entities in Em. These approaches include binary classification methods, learning to rank methods, probabilistic methods, and graph based approaches.
+ Unsupervised ranking methods. These approaches are based on unlabeled corpus and do not require any manually annotated corpus to train the model. These approaches include Vector Space Model (VSM) based methods and information retrieval based methods.

In addition, we could also categorize the candidate entity ranking methods into another three categories:

+ Independent ranking methods. These approaches consider that entity mentions which need to be linked in a document are independent, and <u>do not leverage the relations between the entity mentions in one document</u> to
  help candidate entity ranking. In order to rank the candidate entities, they <u>mainly leverage the context similarity</u> between the text around the entity mention and the document associated with the candidate entity.
+ Collective ranking methods. These methods assume that <u>a document largely refers to coherent entities from one or a few related topics, and entity assignments for entity mentions in one document are interdependent with each other</u>. Thus, in these methods, entity mentions in one document are collectively linked by exploiting this “topical coherence”.
+ Collaborative ranking methods. For an entity mention that needs to be linked, these approaches identify other entity mentions having similar surface forms and similar textual contexts in the other documents. They <u>leverage this cross-document extended context information obtained from the other similar entity mentions and the context information of the entity mention itself to rank candidate entities for the entity mention</u>.

#### Features

##### context-independent features

+ Name String Comparison

+ **Entity Popularity**

+ **Entity Type**

##### context-dependent features

+ Textual Context

  Bag of words

  Concept vector

Based on these different formulations of representations, each text around the entity mention or associated
with the candidate entity could be converted to a vector.

To calculate the similarity between vectors, different methods have been utilized, including dot-product, cosine similarity, Dice coefficient, word overlap, KL divergence, n-gram based measure, and Jaccard similarity.

+ Coherence Between Mapping Entities

  

##### Summary

when designing features for entity linking systems, the decision needs to be made regarding many aspects, such as the tradeoff between accuracy and efficiency, and the characteristics of the applied data set.



#### Supervised Ranking Methods

##### Binary Classification Methods

For one entity mention, if there are two or more candidate entities that are labeled positive, some techniques are employed to select the most likely one, such as confidence based methods [63,69,104], VSM based methods [65],
and SVM ranking models [66].

For the binary classifier, most systems employ Support Vector Machines (SVM) .

The drawbacks of binary classification approach:<br>Firstly, the training data is very unbalanced since the vast majority of candidate entities are negative examples.
Moreover, when multiple candidate entities for an entity mention are classified as positive by the binary classifier, they have to utilize other techniques to select the most likely one.

##### Learning to Rank Methods

Most entity linking systems that leverage the learning to rank framework utilize the ranking SVM framework to learn the ranking model.

##### Probabilistic Methods



##### Graph Based Approaches



##### Model Combination



##### Training Data Generation

One problem with the supervised ranking methods is the requirement of many annotated training examples to train the classifier.

Method: Zhang et al. leveraged the unambiguous entity mention (i.e., the entity mention associated with only one entity in the knowledge base) in the document collection, and replaced it with its ambiguous name variations to create more training data. (<u>Leverage the cross of unambiguous entity mention name and ambiguous name variations</u>)

However, the distribution of the automatically generated annotation data is not consistent with the real entity linking data set.

Zhang et al. used an instance selection strategy (similar to active learning) to select a more balanced and informative subset from the generated instances.

W. Zhang, J. Su, C. L. Tan, and W. T. Wang, “Entity linking leveraging automatically generated annotation,” in COLING,
2010.<br>W. Zhang, Y. C. Sim, J. Su, and C. L. Tan, “Entity linking with effective acronym expansion, instance selection and topic
modeling,” in IJCAI, 2011, pp. 1909–1914.

#### Unsupervised Ranking Methods

##### VSM Based Methods

##### Information Retrieval Based Methods



### Unlinkable Mention Prediction











