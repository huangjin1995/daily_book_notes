#### 1.3.3 Learning-to-Rank Framework



# Part V Practical Issues in Learning to Rank

## Chapter 13 Data Preprocessing for Learning to Rank

### 13.2 Ground Truth Mining from Logs
#### 13.2.1 User Click Models

Clicks are known to be biased and noisy. Therefore, it is necessary to develop some models to remove the bias and noises in order to obtain reliable relevance labels.
Classical click models include the position models and the cascade model.

the position models - assumption and drawbacks:



the cascade model - assumption and drawbacks:



In recent years, several new click models have been proposed in order to solve the aforementioned problems.

#### 13.2.2 Click Data Enhancement

The various click models can be effective, however, they also have certain limitations. 

First, the click information is not the only information source - such as the content information
about the query and the clicked documents. 

Second, the mined labels from clickthrough logs are highly sparse. There may be three reasons: (i) the click-through logs from a search engine company may not cover all the users’ behaviors due to its limited market share; (ii) since the search results provided by existing search engines are far from perfect, it is highly possible that no document is relevant with respect to some queries and therefore there will be no clicks for such queries; (iii) users may issue new queries constantly, and therefore historical click-through logs cannot cover newly issued queries.



To tackle the aforementioned problem, ...



### 13.3 Training Data Selection

#### 13.3.1 Document and Query Selection for Labeling

First, if we can only label a fixed total number of documents, how should we distribute them (more queries and fewer documents per query vs. fewer queries and more documents per query)? 

Second, if we can only label a fixed total number of documents, which of the documents in the corpus should we present to the annotators?

##### 13.3.1.1 Deep Versus Shallow Judgments

Given some number of judged documents per query, judging more documents for this query does not really add much information to the training set. However, including a new query is much more informative since the new query may have quite different properties than the queries that are already in the training set.

##### 13.3.1.2 Actively Learning for Labeling

The idea of active learning is to control what is presented to the annotators (or users in the case of click-through log mining).



...

#### 13.3.2 Document and Query Selection for Training

If we do not use all the data but only a proportion of it, how should we select the documents in order to maximize the effectiveness of the ranking model learned from the data? This is a meaningful question in the following sense.
• Sometimes one suffers from the scalability of the learning algorithms. When the algorithms cannot make use of the large amount of training data (e.g., out of memory), the most straightforward way is to down sample the training set.
• Sometimes the training data may contain noise or outliers. In this case, if using the entire training data, the learning process might not converge and/or the effectiveness of the learned model may be affected.

...

#### 13.3.3 Feature Selection for Training

Similar to document selection, the selection of features may also influence the effectiveness
and efficiency of the learning-to-rank algorithms.
• A large number of features will influence the efficiency of the learning-to-rank algorithms. When this becomes an issue, the most straightforward solution is to remove some less effective features.
• Some features are not very useful and sometimes are even harmful to learning to rank algorithms. In this case, if using the entire feature set, the effectiveness of the learned model may be affected.

...

### Question

+ Can we pre-define the distribution of the labeled data before labeling (e.g., the number of queries versus the number of documents)? 

+ Shall we label the data independent of the training process, or only ask human annotators to label those documents that have the biggest contribution to the training process?

  Some assumptions in the mining or labeling process might not be considered when collecting the data. This will make the ground-truth labels obtained from these data less effective for training a ranking model.

  So, if the labeling and training process is separated, it will hurt the model training (whose goal is to learn as much information about relevance as possible from the training data), but the model will be more generalize (?).

+ 











