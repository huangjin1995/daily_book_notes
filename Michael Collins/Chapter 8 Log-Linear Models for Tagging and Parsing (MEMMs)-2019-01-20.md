天气：晴  
阅读时间：8、9号-晚班车<br>记录时间：2018-11-11 \ 2019-01-20~23

# chapter 8

## Log-Linear Models for Tagging (MEMMs)

### What's MEMMs?

Log-linear tagging models are sometimes referred to as "maximum entropy Markov models (MEMMs)"[^1].

The name MEMM was first introduced by McCallum et al, (2000).

### Definition

We have an input sentence $w_{[1:n]} = w_1,w_2,\dots,w_n$, a tag sequence $t_{[1:n]} = t_1,t_2,\dots,t_n$, we'll use an log-linear model to define
$$
\begin{eqnarray*}
p(t_{[1:n]}|w_{[1:n]}) 
&=& \prod_{j=1}^{n} p(t_j|w_1 \dots w_n,t_1 \dots t_{j-1}) \\
&=& \prod_{j=1}^{n} p(t_j|w_1 \dots w_n,t_{j-2}, t_{j-1}) \\
&=& \prod_{j=1}^{n} p(t_j|w_{[1:n]},t_{j-2}, t_{j-1})
\end{eqnarray*}
$$
**Using log-linear models to estimate.**

We have some input domain $\cal{X}$, and a finite label set $\cal{Y}$. Aim is to provide a conditional probability $p(y|x)$ for any $x \in \cal{X}$ and $y \in \cal{Y}$.<br>A feature is a function $f: \cal{X} \times \cal{Y} \rightarrow \mathbb{R}$ (often binary features or indicator functions)<br>Say we have $m$ features $f_k$ for $k=1 \dots m$  $\Rightarrow$ A feature vector $f(x,y) \in \mathbb{R}^m$ for any $x \in \cal{X}$ and $y \in \cal{Y}$.<br>We also have a parameter vector $v \in \mathbb{R}^m$.<br>We define
$$
p(y|x;v) =\frac{e^{v \cdot f(x,y)}}{\sum_{y' \in \cal{Y}}{e^{v \cdot f(x, y')}}}
$$
$\rightarrow$ $\cal{X}$ is the set of all possible histories of form $<t_{-2},t_{-1}, w_{[1:n]},i>$.

​	$t_{-2},t_{-1}$ are the previous two tags

​	$w_{[1:n]}$ are the $n$ words in the input sentence

​	$i$ is the index of the word being tagged

$\rightarrow$ $\cal{Y}$ $ = \{NN, NNS, V_t, V_i, IN, DT, \dots\}$.



### The viterbi algorithm

Problem: for an input $w_1 \dots w_n$, find
$$
\arg \max_{t_{[1:n]}} p(t_{[1:n]}|w_{[1:n]}) 
$$
We assume that $p$ takes the form
$$
p(t_{[1:n]}|w_{[1:n]}) 
= \prod_{i=1}^{n} q(t_i|t_{i-2}, t_{i-1},w_{[1:n]},i)
$$


Define $n$ to be the length of the sentence

Define 
$$
r(t_{1} \cdots t_k) = \prod_{i=1}^{k}q(t_i|t_{i-2},t_{i-1},w_{[1:n]},i)
$$
Define a dynamic programming table: maximum probability of a tag sequence ending in tags $u,v$ at position $k$.
$$
\pi(k,u,v) = max_{<t_1,\cdots,t_{k-2},t_{k-1},t_k>:t_{k-1}=u,t_k=v} r(t_1,\cdots,t_{k-2},u,v)
$$
 For any $k \in {1\dots n}$, for any $u \in S_{k-1}$ and $v \in S_{k}$:
$$
\pi(k,u,v) = max_{t \in S_{k-2}} (\pi(k-1,t,u) * q(v|t,u,w_{[1:n]},k) \tag{1}
$$
base case, $\pi(0, *,*) = 1​$.



![viterbi](https://github.com/bifeng/daily_book_notes/raw/master/resource/viterbi_backpointers_memms.png)



### Ratnaparkhi's POS tagger (1996)



### Advantage

Key advantage over HMM taggers:  flexibility in the features they can use



## Log-Linear Models for History-Based Parsing



### Definition

How do we dene $p(T|S)$ if $T$ is a parse tree (or another structure)?(We use the notation $S = w_{[1:n]}$)

Represent a tree as a sequnce of decisions $d_1 \dots d_m$, then $T=<d_1,d_2,\dots,d_m>$, $m$ is not necessarily the length of the sentence. The probability of a tree is
$$
p(T|S) 
= \prod_{i=1}^{m} p(d_i|d_1 \dots d_{i-1},S) \\
$$
**Using log-linear models to estimate.**

We define
$$
p(y|x;v) =\frac{e^{v \cdot f(x,y)}}{\sum_{y' \in \cal{Y}}{e^{v \cdot f(x, y')}}}
$$
$\rightarrow$ $\cal{X}$ is the set of all possible histories of form $<d_1 \dots d_{i-1},S>$.

$\rightarrow$ $\cal{Y}$ is set of possible actions.

How do we define $f$?

### The beam or heuristic search

Problem: for an input $S$, find
$$
\arg \max_T p(T|S)
$$
Now: Decision $d_i$ could depend on arbitrary decisions in the "past" $\Rightarrow$ no chance for dynamic programming.
Instead, Ratnaparkhi uses a beam search method

### Ratnaparkhi's Parser

Tree layers of structure:

1. Part of speech tags

   First $n$ decisions are tagging decisions $\rightarrow$  $<d_1,d_2,\dots,d_n> = <DT,NN,Vt,\dots>$ 

2. Chunks

   Chunks are dened as any phrase where all children are part-of-speech tags.

   Next n decisions are chunk tagging decisions $\rightarrow$ $<d_{n+1},d_{n+2},\dots,d_{2n}> = <Start(NP),Join(NP),Other,\dots>$ 

3. Remaining structure

   Alternate Between Two Classes of Actions:
   $\blacktriangleright$ Join(X) or Start(X), where X is a label (NP, S, VP etc.)
   $\blacktriangleright$ Check=YES or Check=NO
   Meaning of these actions:
   $\blacktriangleright$ Start(X) starts a new constituent with label X
   (always acts on leftmost constituent with no start or join label above it)
   $\blacktriangleright$ Join(X) continues a constituent with label X
   (always acts on leftmost constituent with no start or join label above it)
   $\blacktriangleright$ Check=NO does nothing
   $\blacktriangleright$ Check=YES takes previous Join or Start action, and converts it into a completed constituent

   Remaning decisions are high level structure decisions $\rightarrow$

   $<d_{2n+1},d_{2n+2},\dots,d_{m}> = <Start(S),Check=NO,Start(VP),Check=NO,\dots>$ 

Finally, we represent a tree as a sequnce of decisions $d_1 \dots d_m$, then $T=<d_1,d_2,\dots,d_m>$,



Ratnaparkhi's method denes $f$ differently depending on whether next decision is:
$\blacktriangleright$ A tagging decision
(same features as before for POS tagging!)
$\blacktriangleright$ A chunking decision
$\blacktriangleright$ A start/join decision after chunking
$\blacktriangleright$ A check=no/check=yes decision



## Log-Linear Models, MEMMs, and CRFs

### how to define the global feature vector about CRFs?



## papers

Ratnaparkhi, A. A maximum entropy model for part-of-speech tagging. In Proceedings of the Conference on Empirical Methods in Natural Language Processing EMNLP-96, (1996). [paper](http://acl.ldc.upenn.edu/W/W96/W96-0213.pdf) | [introduction](http://curtis.ml.cmu.edu/w/courses/index.php/Ratnaparkhi_EMNLP_1996)

Adwait Ratnaparkhi. (1997). A Linear Observed Time Statistical Parser Based on Maximum Entropy Models. In Proceedings of the Second Conference on Empirical Methods in Natural Language Processing (EMNLP). Brown University, Providence, Rhode Island. [paper](http://www.aclweb.org/anthology/W/W97/W97-0301.pdf) 

https://sites.google.com/site/adwaitratnaparkhi/publications

## Question

### What's maximum entropy models :question: 

For the models which maximum the entropy, that will be lots of models!



### What's the difference between CRF and MEMMs :question:



### what's the process of training data to  algorithm estimation and finally sentence prediction :question:



### CRF/MEMMs​ is the combination of generation model and condition model:question:

It combines the advantages of these two kinds of models :question:

The advantages of generation model (such as, HMMs) is assumption (such as, Markov assumption) or decoding algorithm :question:





[^1]: 1) log-linear models are also referred to as maximum entropy models, as it can be shown in the un-regularized case that the maximum likelihood-estimates maximize an entropic measure subject to certain linear constraints;    2) MEMMs make a Markov assumption.

