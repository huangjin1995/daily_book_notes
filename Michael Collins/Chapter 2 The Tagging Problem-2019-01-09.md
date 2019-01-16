天气：晴  
阅读时间：5日-晚班车\晨<br>记录时间：2018-11-06\2019-01-15


# chapter 2
## The Tagging Problem

### POS Tagging  

1. Challenges of POS  
a). ambiguity  
b). words rare(data sparsity)  

2. **Two Sources of Information** for POS  
a). "Local": individual words have statistical preferences for their pos  
b). "Contextual": the context has an important effect on the pos for a word  
c). Sometimes these two sources of evidence are in conflict.

### Named-Entity Recognition  



## modeling steps

First, how to model (define a model) ?

Second, how to estimate(estimate model)?

Third, how to predict (decoding a model)?

+ **generative models**

  interpretations - 

  $p(x,y)=p(y)p(x|y)$


+ **conditional models**

​	interpretations - 

​	$p(y|x)$

+ difference and common

$$
\begin{align*}
f(x) 
& = \mathop{\arg \max}_{y} p(y|x) \\
& = \mathop{\arg \max}_{y} \frac{p(y)p(x|y)}{p(x)} \\
& = \mathop{\arg \max}_{y} p(y)p(x|y)
\end{align*}
$$



> question: how to choose between generative model and conditional model?

## noisy channel model

who find its connection between noisy channel model with sequence tagging problem?



## markov model

who find its connection between markov model with noisy channel model?



Problem: for an input $x_1,\cdots,x_n$, find
$$
\arg \max_{y_1\cdots y_n} p(x_1,\cdots,x_n,y_1,\cdots,y_{n+1})
$$
where the $\arg \max$ is taken over all sequences $y_1,\cdots,y_{n+1}$ such that $y_i \in S$ for $i=1 \cdots n$, and $y_{n+1} = STOP$. 
$$
p(x_1,\cdots,x_n,y_1,\cdots,y_{n+1}) = \prod_{i=1}^{n+1}q(y_i|y_{i-2},y_{i-1}) \prod_{i=1}^{n}e(x_i|y_i)
$$
where $y_{0} = y_{-1} = *$, and $y_{n+1} = STOP$.



Solutions:

1. Probability methods - directly calculate the probability, but will encounter the data sparsity problem.
2. Search methods - viterbi algorithm



> question: For each sentence, the longer sentence modeling is better than the shorter sentence?
>
> How to include the context information in paragraph?

### stochastic process

stochastic process is very interesting!



## viterbi algorithm

who use the viterbi algorithm for markov model with noisy channel model?

1. The basic algorithm

   Define $n$ to be the length of the sentence

   Define $S_k$ for $k=-1 \dots n$ to be the set of possible tags at position k:
   $$
   S_{-1} = S_{0} = \{*\} \\
   S_k = S \quad for \quad k \in \{1 \dots n\}
   $$



   Define a dynamic programming table
$$
   \pi(k,u,v) = max_{<y_{-1},y_0,y_1,\cdots,y_k>:y_{k-1}=u,y_k=v} r(y_{-1},y_0,y_1,\cdots,y_k)
$$
   For any $k \in {1\dots n}$, for any $u \in S_{k-1}$ and $v \in S_{k}$:
$$
   \pi(k,u,v) = max_{w \in S_{k-2}} (\pi(k-1,w,u) * q(v|w,u) * e(x_k|v))
$$
   In particular, note that
$$
   p(x_1 \dots x_n,y_1 \dots y_{n+1}) = r(y_{-1},y_0,y_1,\dots,y_n) * q(STOP|y_{n-1},y_n)
$$
   So
$$
   max_{y_1 \dots y_{n+1}} p(x_1 \dots x_n,y_1 \dots y_{n+1}) = max_{u \in K_{n-1},v \in K_n} (\pi(n,u,v) * q(STOP|u,v)
$$

2. The Viterbi Algorithm with Backpointers

![viterbi](https://github.com/bifeng/daily_book_notes/raw/master/resource/viterbi_backpointers.png)

the complexity/running time of viterbi algorithm is $O(n|S|^3)$ ($S$ is the number of tags) .



## Dealing with Unknown words (data sparsity)

Unknown words will lead to the estimates for the emission probabilities in the HMM be equal to 0, then every tag sequence will have the same, maximum score, of 0.

Solution for POS:

1. Mapping low-frequency words to pseudo-words (**word class** depending on prefixes, suffixes etc).

A drawback of the approach is that some care is needed in defining the mapping to pseudo-words: this mapping may vary depending on the task being considered.

2. Using the ideas of log-linear models.

​	==notes==: Each general algorithm should consider the specific solution for the specific problem!





