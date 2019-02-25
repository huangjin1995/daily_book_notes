https://en.wikipedia.org/wiki/PageRank

https://en.wikipedia.org/wiki/Markov_chain

refer:

[Why does PageRank converge?](https://www.quora.com/Why-does-PageRank-converge) 

### pagerank

motivation: rank the web pages

key idea: let the web pages vote for each other

we can use the links information (These web pages contain links pointing to one another).

goal: calculate a score for each web pages

This score is called PageRank score, which is the probability of a user visiting that page.

intuition:<br>the more and higher rank pages that link to the page, the more important of this page.<br>如果一个网页被很多其他网页所链接，那么它的排名就高；<br>如果一个网页被排名很高的网页链接，那么它的排名也高。
$$
PR(p_i) = \frac{1-d}{N} + d \sum_{p_j \in M(p_i)} \frac{PR(p_j)}{L(p_j)}
$$
where $p_1,p_2, \ldots, p_N$ are the pages under consideration, $M(p_i)$ is the set of pages that link to $p_i$, $L(p_j)$ is the number of outbound links on page $p_j$, $N$ is the total number of pages, $d​$ is the smooth factor.

Question: 计算搜索结果的网页排名过程中需要用到网页本身的排名？（先有鸡还是先有蛋）



Algorithm:

step1: Define a matrix, where each element of this matrix denotes the probability of a user transitioning from one web page to another.

step2: Initialization matrix

step3: iteration 



#### contribution

网页排名算法的高明之处在于它把整个互联网当做一个整体来对待。这无意中符合了系统论的观点。

+ Change the view from local to global perspective

  How to measure the importance of page?

  For this problem, most people think every page it's independent, so each page's importance is just determine by its content. 

  But from a general perspective, every page in the Internet is connected and the probability of arriving at that page will be converge to an stable number.

#### theory (markov chain)

The formula uses a model of a random surfer who gets bored after several clicks and switches to a random page. The PageRank value of a page reflects the chance that the random surfer will land on that page by clicking on a link. It can be understood as <u>a Markov chain</u> in which the states are pages, and the transitions, which are all equally probable, are the links between pages.

As a result of Markov theory, it can be shown that the PageRank of a page is the probability of arriving at that page after a large number of clicks. This happens to equal $t^{-1}$ where $t$ is the expectation of the number of clicks (or random jumps) required to get from the page back to itself.

There is a theorem in Markov chain theory that says the following.

> The <u>probability</u> (before the surfer starts surfing) that he is at a particular page *X* in *k* steps **tends to a fixed number** and this number is **independent of the starting point** as *k* grows large.

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

