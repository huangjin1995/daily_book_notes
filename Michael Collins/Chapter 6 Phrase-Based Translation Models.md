天气：晴<br>阅读时间：早<br>记录时间：2019-01-26~

# chapter 6

### Phrase-based models (1990s)

#### learning phrases from alignments

**First stage in training a phrase-based model is extraction of a phrase-based (PB)  lexicon.**

(How to get around of these problems-a) alignments are often "noisy" b) many-to-one)

<u>Finding alignment matrices:</u>

Step 1: train IBM model 2 for $p(f|e)$, and come up with most likely alignment for each $(e,f)$ pair.

Step 2: train IBM model 2 for $p(e|f)$, and come up with most likely alignment for each $(e,f)$ pair.

we now have two alignments: take intersection of the two alignments as a starting point.

<u>Heuristics for growing alignments:</u>

Only explore alignment in union of $p(f|e)$ and $p(e|f)$ alignments

Add one alignment point at a time

Only add alignment points which align a word that currently has no alignment

At first, restrict ourselves to alignment points that are "neighbors" (adjacent or diagonal) of current alignment points

Later, consider other alignment points

<u>The final alignment, created by taking the intersection of the two alignments, then adding new points using the growing heuristics.</u>

Note that the alignment is no longer many-to-one.

<u>Extacting phrase pairs form the alignment matrix:</u>

A phrase-pair $(e,f)$ is consistent if: 1) there is at least one word in $e$ aligned to a word in $f$;<br>							 2) there are no words in $f$ aligned to words outside $e$;<br>							 3) there are no words in $e$ aligned to words outside $f$.

We extract all consistent phrase pairs from the training example, and for each pair, we can calculate:
$$
t(f|e) = \frac{Count(f,e)}{Count(e)}
$$


#### A phrase-based model


$$
Score = \underbrace{\log q(e)}_{Language \ model} + \underbrace{\log t(f|e)}_{Phrase \ model} + \underbrace{\eta \times \theta}_{Distortion \ model}
$$
where $\theta$ is the number of skip words.

A phrase-based model consists of:

1. A trigram language model, with parameters $q(w|u,v)$.

   <u>Intuition</u> -> how likely the translation as a target-language sentence 

2. A phrase-based lexicon, consisting of entries $(f,e)$, and each lexical entry has a score $g(f,e)$, e.g.

$$
g(f,e) = \log \frac{Count(f,e)}{Count(e)}
$$

​	<u>Intuition</u> -> how well the target-language phrases match the source-language phrases

3. A "distortion parameter" $\eta$ (typically negative)

   <u>Intuition</u> -> penalize the phrases moving long-distance in translation

   Advantage and disadvantage of distortion:

   Advantage - 1) reduce the search space of possible translations; 2) imporve translation performance

   Disadvantage - using hard limit without flexibility.



#### Decoding in phrase-based model

##### Definition of the Decoding Problem

<u>Definitions</u><br>For a particular input (source-language) sentence $x_1 \dots x_n$, a phrase is a tuple $(s,t,e)$, signify that the subsequence $x_s \dots x_t$ in the <u>source-language</u> sentence can be translated as the <u>target-language</u> string $e$, using an entry from the phrase-based lexicon.<br>$\cal{P}$ is the set of all phrases for a sentence.<br>For any phrase $p$, $s(p), t(p)$, and $e(p)$ are its three components. $g(p)$ is the score for a phrase.

A <u>derivation</u> $y$ is a finite sequnce of phrases, $p_1, p_2,\dots,p_L$, where each $p_j$ for $j \in \{1 \dots L\}$ is a menber of $\cal{P}$.<br>The length $L$ can be any positive integer value.<br>For any derivation $y$ we use $e(y)$ to refer to the underlying translation defined by $y$.

<u>Valid Derivations</u><br>For an input sentence $x=x_1 \dots x_n$, we use $\cal{Y(x)}$ to refer to the set of <u>valid derivations</u> for $x$.<br>$\cal{Y(x)}$ is the set of all finite length sequences of phrases $p_1p_2 \dots p_L$ such that:<br>	Each $p_k$ for $k \in \{1 \dots L\}$ is a member of the set of phrases $\cal{P}$ for $x_1 \dots x_n$.<br>	Each word in $x$ is translated exactly once.<br>	For all $k \in \{1 \dots (L-1)\}$, $|t(p_k) + 1 - s(p_{k+1})| \le d$ where $d \ge 0$ is a parameter of the model. In addition, we 		must have $|1-s(p_1)| \le d$.

<u>Scoring Derivations</u><br>The optimal translation under the model for a source-language sentence $x$ will be
$$
\arg \max_{y \in \cal{Y(x)}} f(y)
$$
In phrase-base system, the score for any derivation $y$ is calculated as follows:
$$
f(y) = h(e(y)) + \sum_{k=1}^{L} g(p_k) + \sum_{k=0}^{L-1} \eta \times |t(p_k)+1-s(p_{k+1})|
$$
where $h(e(y))$ is the trigram languaga model score,  $g(p_k)$ is the phrase-based score for $p_k$, the parameter $\eta$ is the distortion penalty (typically negative). (We define $t(p_0)=0$).



Example:

we must also take this criticism seriously  $\leftarrow$ target-languge

wir m$\ddot{u}$ssen auch diese kritik ernst nehmen $\leftarrow$ source-language 

$p$ = (1,2,we must)  $\rightarrow$  $s(p)$ = 1, $t(p)$ = 2, $e(p)$ = we must.

$y$ = (1,3,we must also), (7,7,take), (4,5,this criticism), (6,6,seriously)  $\rightarrow$  $e(y)$ = we must also take this criticism seriously



##### The Decoding Algorithm

<u>Definitions</u><br>A state is a tuple
$$
q = (e_1,e_2,b,r,\alpha)
$$
where $e_1,e_2$ are English words, $b$ is a bit-string of length $n$, $r$ is an integer specifying the end-point of the last phrase in the state, and $\alpha$ is the score for the state.

The initial state is 
$$
q_0 = (*,*,0^n,0,0)
$$
where $0^n$ is bit-string of length $n$, with $n$ zeroes.

<u>Transitions</u><br>We have $ph(q)$ for any state $q$, for a phrase $p$ to be a member of $ph(q)$, it must satisfy the following conditions:<br>	$p$ must not overlap with the bit-string $b$.<br>	The distortion limit must not be violated. More formally, we must have $|r+1-s(p)| \le d$ where $d$ is the distortion limit. 

In addition, we define $next(q,p)$ to be the state formed by combining state $q$ with phrase $p$.

<u>The $next$ function</u><br>Formally, if $q=(e_1,e_2,b,r,\alpha)$, and $p=(s,t,\epsilon_1 \dots \epsilon_M)$, then $next(q,p)$ is the state $q^\prime = (e_{1}^{\prime},e_{2}^{\prime},b^\prime,r^\prime,\alpha^\prime)$ defined as follows:<br>First, for convenience, define $\epsilon_{-1}=e_1$, and $\epsilon_0=e_2$.<br>Define $e_{1}^{\prime} = \epsilon_{M-1},e_{2}^{\prime} = \epsilon_M$.<br>Define $b_{i}^{\prime} = 1$ for $i \in \{s \dots t\}$. Define $b_{i}^{\prime} = b_i$ for $i \notin \{s \dots t\}$.<br>Define $r^{\prime} = t$<br>Define
$$
\alpha^{\prime} = \alpha + g(p) + \sum_{i=1}^{M} \log q(\epsilon_i|\epsilon_{i-2}, \epsilon_{i-1}) + \eta \times |r+1-s|
$$
<u>The Equality function</u><br>The function
$$
eq(q,q^\prime)
$$
returns true of false.<br>Assuming $q=(e_1,e_2,b,r,\alpha)$, and $q^\prime = (e_{1}^{\prime},e_{2}^{\prime},b^\prime,r^\prime,\alpha^\prime)$, $eq(q,q^\prime)$ is true if and only if $e_{1}^{\prime}=e_{1}$, $e_{2}^{\prime}=e_{2}$, $b^\prime=b$, $r^\prime=r$.

<u>The Decoding Algorithm</u><br>Inputs: sentence $x_1 \dots x_n$. Phrase-based model $(\cal{L},h,d,\eta)$ $\rightarrow$ $\cal{L}$ is phrase pair of lexicon, $h$ is language model, $d$ is distortion limit, $\eta$ is distortion parameter. The phrase-based model defines the functions $ph(q)$ and $next(q,p)$.<br>Initialization: set $Q_0 = \{q_0\}$, $Q_i=\emptyset$ for $i=1 \dots n$.<br>For $i=0 \dots n-1$<br>	For each state $q \in beam(Q_i)$, for each phrase $p \in ph(q)$:<br>	(1) $q^\prime = next(q,p)$<br>	(2) Add$(Q_i, q^\prime, q, p)$ where $i=len(q^\prime)$<br>Return: highest scoring state in $Q_n$. Backpointers can be used to find the underlying sequence of phrases (and the translation).

<u>The Add$(Q, q^\prime, q, p)$ function</u><br>If there is some $q^{\prime \prime} \in Q$ such that $eq(q^{\prime \prime},q^{\prime})=$ True:<br>	If $\alpha(q^\prime) > \alpha(q^{\prime \prime}) $<br>		$Q = \{q^\prime\} \cup Q \setminus \{q^{\prime \prime}\}$<br>		set $bp(q^\prime) = (q,p)$<br>	Else return<br>Else<br>	$Q = Q \ \cup \{q^{\prime}\}$<br>	set $bp(q^\prime) = (q,p)$ 

<u>The $beam(Q)​$ function</u></u><br>Define 
$$
\alpha^* = \max_{q \in Q} \alpha(q)
$$
i.e., $\alpha^*$ is the highest score for any state in $Q$.<br>Define $\beta \ge 0$ to be the beam-width parameter
$$
beam(Q) = \{q \in Q: \alpha(q) \ge \alpha^* - \beta\}
$$




























