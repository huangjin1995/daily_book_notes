天气：晴<br>阅读时间：早<br>记录时间：2019-01-24~25

# chapter 5

### Challenges in machine translation

Lexical Ambiguity

Differing Word Orders

Syntactic Structure is not Preserved Across Translations

Syntactic Ambiguity Causes Problems

Pronoun Resolution

### Classical machine translation 

#### Rule-based approachs

Drawbacks:

1. translation word by word

2. very little analysis of the source text

   difficult or impossible to capture long-range reorderings

   words are translated without disambiguation of their syntactic role

3. after the words are translated, simple reordering rules are applied

4. relies on a large bilingual directionary. For each word in the source language, the dictionary specifies a set of rules for translating that word

#### Transfer-based approachs

Three phrases in translation:

$\blacktriangleright$ Analysis: Analyze the source language sentence

$\blacktriangleright$ Transfer: Convert the source-language parse tree to a target-language parse tree

$\blacktriangleright$ Generation: Convert the target-language parse tree to an output sentence

#### Interlingua-based approachs

$\blacktriangleright$ Analysis: Analyze the source language sentence into a (language-independent) representation of its meaning

$\blacktriangleright$ Generation: Convert the meaning representation into an output sentence

Advantage: if we want to build a translation system that translates between $n$ languages, we need to develop $n$ analysis and generation systems. With a transfer based system, we'd need to develop $O(n^2)$ sets of translation rules.

Disadvantage: What would a language-independent representation look like?

​			How to represent different concepts in an interlingua? Different languages break down concepts in quite different ways. 

### Statistical machine translation

#### The Noisy Channel Model

Goal: translation system from French to English

Have a model $p(e|f)$ which estimates conditional probability of any English sentence $e$ given the French sentence $f$. Use the training corpus to set the parameters.

Giving:
$$
p(e|f)= \frac{p(e,f)}{p(f)} = \frac{p(e)p(f|e)}{\sum_{e}p(e)p(f|e)}
$$
and 
$$
\arg \max_e p(e|f) = \arg \max_e p(e) p(f|e)
$$
A Noisy Channel Model has two components:

$p(e)$  the language model - could be a trigram model, estimated from any data.

$p(f|e)$ the translation model - is trained from a parallel corpus of French/English pairs.

Note:

The language model can make up for deficiencies of the translation model.



How to build $p(f|e)$?

How to decode and find $\arg \max_e p(e)p(f|e)$?



#### IBM Model  1

Alignments

English sentence $e$ has $l$ words $e_1, \dots, e_l$, French sentence $f$ has $m$ words $f_1,\dots,f_m$ 

An alignment $a$ is {$a_1,\dots,a_m$}, where each $a_j \in \{0 \dots l\}$, it identifies which English word each French word orginated from.
$$
p(f|e,m) = \sum_{a \in \cal{A}} p(f,a|e,m) = \sum_{a \in \cal{A}} p(a|e,m)p(f|a,e,m)
$$
where $\cal{A}$ is the set of all possible alignments.

We can also calculate 
$$
p(a|f,e,m) = \frac{p(f,a|e,m)}{\sum_{a \in \cal{A}} p(f,a|e,m)}
$$
for any alignment $a$.

For a given $f,e$ pair, we can also compute the most likely alignment,
$$
a^* = \arg \max_a p(a|f,e,m)
$$
We'll define models for $p(a|e,m)$and $p(f|a,e,m)$:
$$
p(a|e,m) = \frac{1}{(l+1)^m} \tag{1.1}
$$
​		This is a major simplifying assumptions, but it gets thing started...
$$
p(f|a,e,m) = \prod_{j=1}^{m} t(f_j|e_{a_j}) \tag{1.2}
$$


The Generative Process

To generate a French string $f$ from an English string $e$:

Step 1: Pick an alignment $a$ with probability $\frac{1}{(l+1)^m}$

Step 2: Pick the French words with probability $\prod\limits_{j=1}^{m} t(f_j|e_{a_j})$

The final result:

$p(f,a|e,m) = p(a|e,m) \times p(f|a,e,m) = \frac{1}{(l+1)^m}\prod\limits_{j=1}^{m} t(f_j|e_{a_j}) $

#### IBM Model 2

Only difference: we now introduce alignment or distortion paramters

$q(i|j,l,m)=$ Probability that $j$'s French word is connected to $i$'s English word, given sentence lengths of $e$ and $f$ are $l$ and $m$ respectively

Define the model $p(a|e,m)$: 
$$
p(a|e,m) = \prod_{j=1}^{m} q(a_j|j,l,m)
$$
where $a = \{a_1 \dots a_m\}$. 



The Generative Process

To generate a French string $f$ from an English string $e$:

Step 1: Pick an alignment $a$ with probability $\prod\limits_{j=1}^{m} q(a_j|j,l,m)$

Step 2: Pick the French words with probability $\prod\limits_{j=1}^{m} t(f_j|e_{a_j})$

The final result:

$p(f,a|e,m) = p(a|e,m) \times p(f|a,e,m) = \prod\limits_{j=1}^{m} q(a_j|j,l,m) t(f_j|e_{a_j}) $



if we have parameters $q$ and $t$, we can easily recover the most likely alignment for any sentence pair.

Given a sentence pair $e_1, e_2,\dots,e_l$, $f_1,f_2,\dots,f_m$, define 
$$
a_j = \arg \max_{a \in \{0 \dots l\}} q(a|j,l,m) \times t(f_j|e_a)
$$
for $j = 1 \dots m$.



#### EM traning of Models 1 and 2

The parameter estimation problem:

Input: $(e^{(k)},f^{(k)})$ for $k=1 \dots n$. Each $e^{(k)}$ is an English sentence, each $f^{(k)}$ is a French sentence.

Output: parameters $t(f|e)$ and $q(j|i,l,m)$ 

A key challenge: we do not have alignments on our traning examples. 



If the alignments are observed, traning data is $(e^{(k)},f^{(k)}, a^{(k)})$, each $a^{(k)}$ is an alignment, then just using maximum-likelihood parameter estimates:
$$
t_{ML}(f|e) = \frac{Count(e,f)}{Count(e)} \quad q_{ML}(j|i,l,m) = \frac{Count(j|i,l,m)}{Count(i,l,m)} 
$$


![mle](https://github.com/bifeng/daily_book_notes/raw/master/resource/mle_with_alignments_translation.png)



If the aligments are not observed, the algorithm is related to algorithm when alignments are observed, but two key differences:

1. The algorithm is iterative. We start with some initial (e.g., random) choice for the $q$ and $t$ parameters. At each iteration we compute some "counts" based on the data together with our current parameter estimates. We then re-estimate our parameters with these counts, and iterate.

2. We use the following definition for $\sigma(k,i,j)$ at each iteration:
   $$
   \sigma(k,i,j) = \frac{q(j|i,l_k,m_k)t(f_{i}^{(k)}|e_{j}^{(k)})}{\sum\limits_{j=0}^{l_k} q(j|i,l_k,m_k)t(f_{i}^{(k)}|e_{j}^{(k)})}
   $$



![em](https://github.com/bifeng/daily_book_notes/raw/master/resource/em_without_alignments_translation.png)



The maximum-likelihood estimates are
$$
\arg \max_{t,q} L(t,q)
$$
$L(t,q)=\sum\limits_{k=1}^{n} \log p(f^{(k)}|e^{(k)})= \sum\limits_{k=1}^{n} \log \sum\limits_{a} p(f^{(k)},a|e^{(k)})$

The EM algorithm will converge to a local maximum of the log-likelihood function.

#### Summary

+ Key ideas in the IBM translation models:

  Alignment variables

  Translation parameters, e.g., $t(chien|dog)$

  Distortion parameters, e.g., $q(2|1,6,7)$

+ The EM algorithm: an iterative algorithm for training the $q$ and $t$ parameters 

+ Once the parameters are trained, we can recover the most likely alignments on our training examples





