天气：晴<br>阅读时间：早<br>记录时间：2019-01-22~

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
&=& \sum_{c=1}^{k}\sum_{c'=1}^{k} p(c,c') \log \frac{p(c,c')}{p(c)p(c')} + G
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





Second algorithm:





### papers

Brown, P. F., Pietra, V. J. D., deSouza, P. V., Lai, J. C., and Mercer, R. L. (1992). Class-based n-gram models of natural language. Computational Linguistics, 18(4):467–479.

Miller, S., Guinness, J., and Zamanian, A. (2004). Name tagging with word clusters and discriminative training. In HLT-NAACL, pages 337–342.

