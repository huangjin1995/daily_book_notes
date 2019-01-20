天气：晴  
阅读时间：早班车<br>记录时间：2018-11-08\2019-01-19

# chapter 4

## Lexicalized Probabilistic Context-Free Grammars

### Weaknesses of PCFGs

#### lack of sensitivity to lexical information

the independence assumption of each lexical item in the rule $\alpha \to \beta $ where $\beta \in \Sigma$ (only depends on the POS)

the independence assumption of any lexical information in the rule $\alpha \to \beta $ where $\beta \in N $



Prepositional phrase attachment  ambiguity, attachment decision is completely independent of the words, such as If q(NP $\rightarrow$ NP PP) > q(VP $\rightarrow$ VP PP) then the NP is more probable, else VP is more probable.

Example: 

Ted saw Jill <u>in town</u>

workers dumped sacks <u>into a bin</u>

Coordination ambiguity, the parses have identical rules, and therefore have identical probability under any assignment of PCFG rule probabilities.

Example: dogs in houses and cats

#### lack of sensitivity to structural preferences

lexical information may of course help again, in this case. Another useful source of information may be basic statistic about structural preferences (preferences that ignore lexical items).



Close Attachment, the parses have the same rules, therefore receive same probability under a PCFG.

Example: 

president of a company <u>in Africa</u>

John was believed to have been shot <u>by Bill</u>



### LPCFGs

#### heads in context-free rules

Researchers have generally used a simple set of rules to automatically identify the head of each context-free rule. This rules are fairly heuristic, but rely on some linguistic guidance on what the head of a rule should be: in spite of their simplicity they work quite well in practice!

A core idea in syntax (e.g., see X-bar Theory, Head-Driven Phrase Structure Grammar)

Some intuitions:
The central sub-constituent of each rule.
The semantic predicate in each rule.

#### Chomsky Normal Form

A lexicalized context free grammar $G=(N,\Sigma,R,S)$ in Chomsky Normal Form is as follows:

​	$N$ is a set of non-terminal symbols.<br>	$\Sigma$ is a set of terminal symbols.<br>	$R$ is a set of rules which take one of three forms:<br>		$X(h) \to_{1} Y_1(h) Y_2(w)$ for $X \in N$, and $Y_1,Y_2 \in N$, and $h,w \in \Sigma$<br>		$X(h) \to_{2} Y_1(w) Y_2(h)$ for $X \in N$, and $Y_1,Y_2 \in N$, and $h,w \in \Sigma$<br>		$X(h) \rightarrow h $ for $X \in N$, and $h \in \Sigma$<br>	$S \in N$ is a distinguished start symbol.

#### paramters estimation

An example parameter in a Lexicalized PCFGs:
$$
q(S(saw) \to_{2} NP(man) \ VP(saw))
$$
A Model from Charniak (1997):<br>First step: decompose this parameter into a product of two parameters
$$
q(S(saw) \to_2 NP(man)\ VP(saw))
= q(S \to_2 NP\ VP|S, saw) \times q(man|S \to_2 NP\ VP, saw)
$$
Second step: use smoothed estimation for the two parameter estimates
$$
\begin{eqnarray*}
q(S \to_2 NP\ VP|S, saw) 
&=& \lambda_1 \times q_{ML}(S \to_2 NP\ VP|S, saw) + \lambda_2 \times q_{ML}(S \to_2 NP\ VP|S) \\
q(man|S \to_2 NP\ VP, saw) 
&=& \lambda_3 \times q_{ML}(man|S \to_2 NP\ VP, saw) + \lambda_4 \times q_{ML}(man|S \to_2 NP\ VP) + \lambda_5 \times q_{ML}(man|NP)
\end{eqnarray*}
$$


Need to deal with rules with more than two children, e.g.,
$$VP(told) \to V(told) \ NP(him) \ PP(on) \ SBAR(that)$$

Need to incorporate parts of speech (useful in smoothing)
$$VP_{V}(told) \to V(told) \ NP_{PRP}(him) \ PP_{IN}(on) \ SBAR_{COMP}(that)$$

Need to encode preferences for close attachment
John was believed to have been shot by Bill

Further reading:
Michael Collins. 2003. Head-Driven Statistical Models for Natural Language Parsing. In Computational
Linguistics.

#### parsing with Lexicalized CFGs

the complexity/running time of the CKY algorithm is $O(n^3 \times n^2|N|^3)$.

#### Features of LPCFGs

1. More accurate, but with more parameter, it mean need more data to estimate! It will face with data sparsity problem (how handle it :question:)

#### Evaluation

##### representing trees as constituents

![constituents](https://github.com/bifeng/daily_book_notes/raw/master/resource/constituents.png)

results:

Training data: 40,000 sentences from the Penn Wall Street Journal treebank. Testing: around 2,400 sentences from the Penn Wall Street Journal treebank.
Results for a PCFG: 70.6% Recall, 74.8% Precision
Results for a lexicalized PCFG: 88.1% recall, 88.3% precision (from Collins (1997, 2003))
More recent results: <br>90.7% Recall/91.4% Precision (Carreras et al., 2008); 91.2% Recall, 91.8% Precision (Charniak and Johnson, 2005) - discriminative estimation (log linear models and conditional random fields)<br> 91.7% Recall, 92.0% Precision (Petrov 2010) - latent-variable PCFGs

##### representing trees as dependency

![dependency](https://github.com/bifeng/daily_book_notes/raw/master/resource/dependency.png)

<h, w, rule>

1. All parses for a sentence with n words have n dependencies.
   So, report a single figure, dependency accuracy (recall=precision)
2. Can calculate precision/recall on particular dependency types

Results from Collins, 2003: 88.3% dependency accuracy<br>Subject-verb pairs: over 95% recall and precision
Object-verb pairs: over 92% recall and precision
Other arguments to verbs: $\approx$ 93% recall and precision
Non-recursive NP boundaries: $\approx$ 93% recall and precision
PP attachments: $\approx$ 82% recall and precision
Coordination ambiguities: $\approx$ 61% recall and precision

### Summary

Lexicalized PCFGs:

1. Lexicalize a treebank using head rules
2. Estimate the parameters of a lexicalized PCFG using smoothed estimation

### QA

+ The lexicalized PCFGs how to consider​ the​ structural​ preferences:question:
+ 























