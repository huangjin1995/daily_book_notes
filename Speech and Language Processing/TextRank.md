### pagerank

motivation: rank the web pages

key idea: let the web pages vote for each other

we can use the links information (These web pages contain links pointing to one another).

goal: calculate a score for each web pages

This score is called PageRank score, which is the probability of a user visiting that page.

intuition:<br>???
$$
PR(p_i) = \frac{1-\alpha}{N} + \alpha \sum_{p_j \in M_{p_i}} \frac{PR(p_j)}{L(p_j)}
$$




Algorithm:

step1: Define a matrix, where each element of this matrix denotes the probability of a user transitioning from one web page to another.

step2: Initialization matrix

step3: iteration 





#### code

```python
matrix = ...

import networkx as nx

nx_graph = nx.from_numpy_array(matrix)
scores = nx.pagerank(nx_graph)
```



#### question

+ why the pagerank will converge?





### textrank



#### code

keyword extraction [jieba](https://github.com/fxsjy/jieba) - create Undirect Weighted Graph and hard code

summarization [textrank](https://github.com/DerwenAI/pytextrank) - use networkx library

#### application

+ keyword extraction

  - In place of web pages, we use n-grams words
  - co-occurrence between any two words in n-grams window is used as an equivalent to the web page transition probability

  

+ summarization

  - In place of web pages, we use sentences
  - Similarity between any two sentences is used as an equivalent to the web page transition probability

