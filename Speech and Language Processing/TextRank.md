refer:

[Why does PageRank converge?](https://www.quora.com/Why-does-PageRank-converge) 

https://en.wikipedia.org/wiki/PageRank

### pagerank

motivation: rank the web pages

key idea: let the web pages vote for each other

we can use the links information (These web pages contain links pointing to one another).

goal: calculate a score for each web pages

This score is called PageRank score, which is the probability of a user visiting that page.

intuition:<br>the more and higher rank pages that link to the page, the more important of this page.<br>
$$
PR(p_i) = \frac{1-d}{N} + d \sum_{p_j \in M(p_i)} \frac{PR(p_j)}{L(p_j)}
$$
where $p_1,p_2, \ldots, p_N$ are the pages under consideration, $M(p_i)$ is the set of pages that link to $p_i$, $L(p_j)$ is the number of outbound links on page $p_j$, $N$ is the total number of pages.



Algorithm:

step1: Define a matrix, where each element of this matrix denotes the probability of a user transitioning from one web page to another.

step2: Initialization matrix

step3: iteration 



#### contribution

+ Change the view from local to global perspective

  How to measure the importance of page?

  For this problem, most people think every page it's independent, so each page's importance is just determine by its content. 

  But from a general perspective, the visitor of this page will be converge to an stable number.

#### theory

There is a theorem in Markov chain theory that says the following.

> The probability (before the surfer starts surfing) that he is at a particular page *X* in *k* steps **tends to a fixed number** and this number is **independent of the starting point** as *k* grows large.

**This magic probability is defined to be the PageRank of a page. It is the probability that a random surfer would end up there after a "long time" of surfing.** 

#### advantage/disadvantage

disadvantage:<br>For search engine, one main disadvantage of PageRank is that it favors older pages. A new page, even a very good one, will not have many links unless it is part of an existing site (a site being a densely connected set of pages, such as [Wikipedia](https://en.wikipedia.org/wiki/Wikipedia)).

#### code

```python
matrix = ...

import networkx as nx

nx_graph = nx.from_numpy_array(matrix)
scores = nx.pagerank(nx_graph)
```



#### question

+ why the pagerank will converge and independent of the starting point?

Why should the probability converge? 

**Intuitively,** imagine a billion surfers who all start at the same point. Think about the system a thousand steps later. After this point, there will have been a bunch of teleportations and a bunch of random decisions. I think it's clear that it would take a "weird" circumstance for the mass of surfers at, say, this page on the web (the one you're looking at) to depend sensitively on whether it is time period 1000 or 1001. The various sequences of events that might lead me to this page at time 1000 are about as likely as those that would bring me here one period later, because there is a lot of inherent randomness in the system. So the number of surfers there at the two times should be about the same.

You can think of the random surfers as analogous to molecules of air in a room. It is conceivable that all the molecules would randomly go to the left side of the room (leaving a vacuum on the right side), then go back to the right side of the room one second later, and keep doing this kind of thing, but this would take a very special "transportation" process with a lot of "nonrandomness" in it.

Why should the eventual distribution of surfers be independent of the starting point? 

Well, because if you have a bunch of randomness each surfer will eventually "forget where he started". After enough random turns, it is those turns that have determined where he is, not the arbitrary selection of his initial spot in the network (unless the process is very nonrandom -- e.g. unless the network is a perfect directed cycle and there is no teleportation). 

In this particular context, the teleportation is a way of getting the surfer's next-period position to be independent of his current-period position, and since teleportation eventually happens to everyone, eventually the system forgets the state in which it started. This is a particularly simple mechanism for forgetting starting point, but even without teleportation, the forgetfulness property still holds for "most" networks.  



### textrank



#### code

https://en.wikipedia.org/wiki/PageRank#Python

keyword extraction [jieba](https://github.com/fxsjy/jieba) - create Undirect Weighted Graph and hard code

summarization [textrank](https://github.com/DerwenAI/pytextrank) - use networkx library

#### application

+ keyword extraction

  - In place of web pages, we use n-grams words
  - co-occurrence between any two words in n-grams window is used as an equivalent to the web page transition probability

  

+ summarization

  - In place of web pages, we use sentences
  - Similarity between any two sentences is used as an equivalent to the web page transition probability

