天气：晴  
阅读时间：5日-晚班车\晨<br>记录时间：2018-11-06\2019-01-09


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



> notes: language model is modeling the label, not the observation data!

## markov model

who find its connection between markov model with noisy channel model?





> question: For each sentence, the longer sentence modeling is better than the shorter sentence?
>
> How to include the context information in paragraph?

### stochastic process

stochastic process is very interesting!



## viterbi algorithm

who use the viterbi algorithm for markov model with noisy channel model?

1. The basic algorithm
2. The Viterbi Algorithm with Backpointers



> question: why the running time of viterbi algorithm is $O(n|\kappa|^3)$? ($\kappa$ is the number of tags) 



## Dealing with Unknown words (data sparsity)

Unknown words will lead to the estimates for the emission probabilities in the HMM be equal to 0, then every tag sequence will have the same, maximum score, of 0.

Solution for POS:

1. Mapping low-frequency words to pseudo-words.

A drawback of the approach is ...

2. Using the ideas of log-linear models.

:question:

​	==notes==: Each general algorithm should consider the specific solution for the specific problem!





