天气：晴  
阅读时间：早班车<br>记录时间：2018-11-05

#### Keyphrases

+ sentence probability decide by the frequency of sentence in the **corpus**.
+ sentence probability -> word probability will generalize to new sentence.

### chapter 1

#### Motivation

Language models were originally developed for the problem of speech recognition, which is very useful as a good 'prior' distribution over which sentences are or aren't probable in language.  

The estimation techniques developed for this problem will be VERY useful for other problems in NLP.

#### Trigram language model

$$
p(x_1,...,x_n) = q(x_1) \prod_{i=2}^n q(x_i|x_1,...,x_{i-1})\\
= \prod_{i=1}^n q(x_i|x_{i-2},x_{i-1})
$$

For convenience we assume $x_0 = x_{-1} = *$, where $*$ is a special '"start" symbol, $x_n = STOP$ where $STOP$ is a special symbol.

##### maximum-likelihood estimates

Sparse Data Problems: Say our vocabulary size is $N = |V|$, then there are $V^3$ parameters in the model.

+  solution to data sparsity (smoothed estimation methods):  
  The key idea will be to rely on lower-order statistical estimates (using estimates based on bigram or unigram counts to smooth the estimates based on trigrams).  

    1. linear interpolation  

    $$q(w|u,v)=\lambda_1 \times q_{ML}(w|u,v) + \lambda_2 \times q_{ML}(w|v) + \lambda_3 \times q_{ML}(w)$$

    extension:  
    Add an additional degree of freedom, by allowing the values of parameters to vary depending on the bigram that is being conditioned on.  
    (Intuition, if the q(w|u,v) is more confident, then give more weights to it!)  
    a). linear interpolation with bucketing(page17)  
    define **the bucket function(like histogram)** for the bigrams count, for each bucket using its own set of smoothing paramters.  
    b). simpler method  
    $$\lambda_1 = \frac{c(u,v)}{c(u,v)+\gamma}$$

    $$\lambda_2=(1-\lambda_1) \times \frac{c(v)}{c(v)+\gamma}$$

    $$\lambda_3=1-\lambda_1-\lambda_2$$

    The only parameter is the $\gamma$.  

    2. discounting methods  

      It reflects the intuition that if we take counts from the training corpus, we will systematically over-estimate the probability of bigrams seen in the corpus (and under-estimate bigrams not seen in the corpus).  
      For the bigrams count larger than zero part, we discount the bigrams count, and it leads to the missing probability mass.  
      For the bigrams count identical to zero part, we using the missing probability mass as weight average of the probability of unigrams.  
      The only parameter is the discounting value.  

> question:  
> why the parameters of linear interpolation should be estimated by development data, rather than training data?  

#### Evaluation


+ perplexity  
  under a uniform probability model, the perplexity is equal to the vocabulary size.  







