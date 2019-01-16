天气：晴  
阅读时间：早班车\晨<br>记录时间：2018-11-05\2019-01-07~09

### chapter 1

#### The language modeling problem

We need to learn a probability distribution $p$ that satisfies
$$
\sum_{x \in V'} p(x) = 1, \quad  p(x) \ge 0 \ for\ all \ x \in V'
$$
$x$ is the sentence.

#### Motivation

Language models were originally developed for the problem of speech recognition, which is very useful as a good 'prior' distribution over which sentences are or aren't probable in language.  

The estimation techniques developed for this problem will be VERY useful for other problems in NLP.

#### Trigram language model

$$
\begin{align*}
p(x_1,...,x_n) 
& = q(x_1) \cdot q(x_2|x_1) \cdot q(x_3|x_2,x_1) \cdots \\ 
& = q(x_1) \prod_{i=2}^n q(x_i|x_1,...,x_{i-1})\\
& = \prod_{i=1}^n q(x_i|x_{i-2},x_{i-1})
\end{align*}
$$

For convenience we assume $x_0 = x_{-1} = *$, where $*$ is a special '"start" symbol, $x_n = STOP$ where $STOP$ is a special symbol.

##### maximum-likelihood estimates

Sparse Data Problems: Say our vocabulary size is $N = |V|$, then there are $V^3$ parameters in the model.

###### Solution to data sparsity (smoothed estimation methods)

The key idea will be to rely on lower-order statistical estimates (using estimates based on bigram or unigram counts to smooth the estimates based on trigrams).  

1. linear interpolation  

   $$q(w|u,v)=\lambda_1 \times q_{ML}(w|u,v) + \lambda_2 \times q_{ML}(w|v) + \lambda_3 \times q_{ML}(w)$$

   How to estimate the $\lambda$ values? 

   Hold out part of training set as "validation" data, and choose $\lambda_1,\lambda_2,\lambda_3$ to maximize:

$$
L(\lambda_1,\lambda_2,\lambda_3)=\sum_{w,u,v} \acute{c}(w,u,v) \log q(w|u,v)
$$
​	$\acute{c}(w,u,v)$ is the number of times the trigram in validation set.



  ​	Add an additional degree of freedom, by allowing the values of parameters to vary depending on the bigram that is being conditioned on.  
  ​	**Intuition**: if the $q(w|u,v)$ is more confident, then give more weights to it!

   	a). linear interpolation with bucketing (page17)  
​    	define **the bucket function(like histogram)** for the bigrams count, for each bucket using its own set of smoothing paramters.  
​    	b). simpler method  
​    	$$\lambda_1 = \frac{c(u,v)}{c(u,v)+\gamma}$$

  ​	$$\lambda_2=(1-\lambda_1) \times \frac{c(v)}{c(v)+\gamma}$$

   	$$\lambda_3=1-\lambda_1-\lambda_2$$

​	The only parameter is the $\gamma$.  

2. discounting methods  

   **Intuition**: It reflects the intuition that if we take counts from the training corpus, we will systematically over-estimate the probability of bigrams seen in the corpus (and under-estimate bigrams not seen in the corpus). (The maximum-likelihood estimates are high (particularly for low count items)) 
   For the bigrams count larger than zero part, we discount the bigrams count, and it leads to the missing probability mass.  
   For the bigrams count identical to zero part, we using **the missing probability mass** as weight average of the probability of unigrams.  
   The only parameter is the discounting value.  



   The missing probability mass:
$$
\alpha(w_{i-1})=1- \sum_{w} \frac{Count^*(w_{i-1},w)}{Count(w_{i-1})}
$$
   $Count^*(x) = Count(x) - \lambda$, $Count^*(x)$ is the discounted counts, $\lambda$ is the discounting value. 



   Katz Back-Off Models (Bigrams)

For a bigram model, define two sets
$$
A(w_{i-1}) = \{w: Count(w_{i-1},w) > 0 \} \\
B(w_{i-1}) = \{w: Count(w_{i-1},w) = 0 \}
$$
A bigram model
$$
q_{BO}(w_i|w_{i-1}) = 
\begin{cases} 
		\frac{Count^*(w_{i-1},w_i)}{Count(w_{i-1})}, & if \ w_i \in A(w_{i-1})\\ 
		\alpha(w_{i-1}) \frac{q(w_i)}{\sum_{w \in B(w_{i-1})} q(w)}, & if \ w_i \in B(w_{i-1}) 
\end{cases}
$$
where
$$
\alpha(w_{i-1})=1- \sum_{w \in A(w_{i-1})} \frac{Count^*(w_{i-1},w)}{Count(w_{i-1})}
$$


   Katz Back-Off Models (Trigrams)



##### other methods

other methods to improve language models:

+ "Topic" or "long-range" features
+ Syntactic models

#### Evaluation


+ perplexity  

  Under a uniform probability model, the perplexity is equal to the vocabulary size.  

  Perplexity is a measure of effective “branching factor”.

$$
Perplexity = 2^{-l} \quad where \quad l = \frac{1}{M} \sum_{i=1}^{m} \log p(s_i)
$$

and $m$ is the number of sentences, $M$ is the total number of words in test data.

#### notes

- sentence probability decide by the frequency of sentence in the **corpus**.
- sentence probability generalize poorly to new sentence -> word probability will generalize to new sentence.

#### QA

+ what makes a language model valid?

+ Let’s return to a smaller version of our corpus.
  • the book STOP
  • his house STOP
  This time we compute a bigram language model using Katz back-off with

  $c^*(v,w) = c(v,w) - 0.5$

  What is the value of $q_{BO}( book | his )$ estimated from this corpus?







