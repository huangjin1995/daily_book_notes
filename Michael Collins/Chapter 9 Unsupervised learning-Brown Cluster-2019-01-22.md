天气：晴<br>阅读时间：早<br>记录时间：2019-01-22~24

# chapter 8

## The Brown  Clustering Algorithm

Input: a (large) corpus of words
Output 1: a partition of words into word clusters
Output 2 (generalization of 1): a hierarchichal word clustering

### Definition

The Intuition<br>Similar words appear in similar contexts
More precisely: similar words have similar distributions of words to their immediate left and right

$\cal{V}$ is the set of all words seen in the corpus $w_1,w_2,\dots,w_n$, $C:\cal{V} \rightarrow \{1,2,\dots,k\}$ is a partition of the vocabulary into $k$ classes.

The model:
$$
\begin{eqnarray*}
p(w_1,w_2,\dots,w_n) 
&=& \prod_{i=1}^{n} e(w_i|C(w_i))q(C(w_i)|C(w_{i-1}))
\end{eqnarray*}
$$
$C(w_0)$ is a special start state.



How do we measure the quality of a partition $C$?
$$
\begin{eqnarray*}
Quality(C) 
&=& \sum_{i=1}^{n} \log e(w_i|C(w_i))q(C(w_i)|C(w_{i-1})) \\
&=& \sum_{c=1}^{k}\sum_{c'=1}^{k} p(c,c') \log \frac{p(c,c')}{p(c)p(c')} + G \tag{1}
\end{eqnarray*}
$$
where $G$ is a constant.

Here 
$$
p(c,c')= \frac{n(c,c')}{\sum_{c,c'}n(c,c')} \quad p(c) = \frac{n(c)}{\sum_{c}n(c)}
$$
where $n(c)$ is the number of times class $c$ occurs in the corpus, $n(c,c')$ is the number of times $c'$ is seen following $c$, under the function $C$.



### Algorithm

First algorithm:

We start with $\cal{V}$ clusters: each word gets its own cluster
Our aim is to find $k$ final clusters
We run $\cal{V}-k$ merge steps:
​	At each merge step we pick two clusters $c_i$ and $c_j$ , and merge them into a singlec luster
​	We greedily pick merges such that $Quality(C)$ for the clustering $C$ after the merge step is maximized at each stage
Cost? Naive = $O(|\cal{V}|^5)$. Improved algorithm gives $O(|\cal{V}|^3)$: still two slow for realistic values of $|V|$.



Second algorithm:

Parameter of the approach is $m$ (e.g., $m = 1000$)
Take the top $m$ most frequent words, put each into its own cluster, $c1, c2, \dots c_m$
For $i = (m + 1) \dots |V|$
​	Create a new cluster, $c_{m+1}$, for the $i$'th most frequent word. We now have $m+1$ clusters
​	Choose two clusters from $c_1 \dots c_{m+1}$ to be merged: pick the merge that gives a maximum value for $Quality(C)$. We're now back to $m$ clusters
Carry out $(m - 1)$ final merges, to create a full hierarchy
Running time: $O(|\cal{V}|m^2 + n)$ where $n$ is corpus length.



### papers

Brown, P. F., Pietra, V. J. D., deSouza, P. V., Lai, J. C., and Mercer, R. L. (1992). Class-based n-gram models of natural language. Computational Linguistics, 18(4):467–479.

Miller, S., Guinness, J., and Zamanian, A. (2004). Name tagging with word clusters and discriminative training. In HLT-NAACL, pages 337–342.

The Brown et al. Word Clustering Algorithm, Michael Collins 讲义

semi-supervised learning for natural language, percy liang 硕士论文

Brown et al. 1992 Clustering [slides](http://simonsuster.github.io/talks/Brown_RUG.pdf) 

### Question

+ why using language model to do word cluster? it's incredible!
+ how to find the quality measure fomula of (1)?
+ 