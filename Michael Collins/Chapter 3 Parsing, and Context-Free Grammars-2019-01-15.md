天气：晴  
阅读时间：早班车<br>记录时间：2018-11-07\2019-01-15~19

# chapter 3

### Context-Free Grammars

A context free grammar $G=(N,\Sigma,R,S)$ where:

​	$N$ is a finite set of non-terminal symbols.<br>	$\Sigma$ is a finite set of terminal symbols.<br>	$R$ is a finite set of rules of the form $X \to Y_1Y_2...Y_n$, where $X \in N$, $n \geq 0$, and $Y_i \in (N  \cup \Sigma)$ for $i=1...n$.<br>	$S \in N$ is a distinguished start symbol.

A <u>left-most derivation</u> is a sequence of string s $s_1 \dots s_n$, where 

​	$s_1=S$, the start symbol<br>	$s_n \in \sum^*$, i.e. $s_n$ is made up of terminal symbols only<br>	Each $s_i$ for $i=2 \dots n$ is derived from $s_{i-1}$ by picking the left-most non-terminal $X$ in $s_{i-1}$ and replacing it by some $\beta$ where $X \rightarrow \beta$ is a rule in $R$.

### A Simple Grammar for English

The grammar completely fails to capture.<br>We've only scratched the surface:

+ Agreement

  The dogs laugh vs. The dog laughs

+ Wh-movement

  The dog that the cat liked ...

+ Active vs. passiv

  The dog saw the cat vs.
  The cat was seen by the dog

Sources of Ambiguity:

Part-of-Speech ambiguity

Prepositional phrase attachment

Noun premodifier



### Chomsky Normal Form

A context free grammar $G=(N,\Sigma,R,S)$ in Chomsky Normal Form is as follows:

​	$N$ is a set of non-terminal symbols.<br>	$\Sigma$ is a set of terminal symbols.<br>	$R$ is a set of rules which take one of two forms:<br>		$X \to Y_1Y_2$ for $X \in N$, and $Y_1,Y_2 \in N$<br>		$X \rightarrow Y$ for $X \in N$, and $Y \in \Sigma$<br>​	$S \in N$ is a distinguished start symbol.

### Probabilistic Context-Free Grammars(PCFGs)

Probabilistic Context-Free Grammars(PCFGs), also known as the Stochastic Context-Free Grammars(SCFGs), first proposed by Booth(1969).

Probability of a tree $t$ with rules
$$
\alpha_1 \rightarrow \beta_1,\alpha_2 \rightarrow \beta_2, \cdots, \alpha_n \rightarrow \beta_n
$$
is $p(t)=\prod_{i-1}^{n}{q(\alpha_i \rightarrow \beta_i)}$ where $q(\alpha \rightarrow \beta) $ is the probability for rule $\alpha \rightarrow \beta$.

Say we have a sentence $s$, set of derivations for that sentence is $T(s)$. Then a PCFG assigns a probability $p(t)$ to each menber of $T(s)$. i.e., we now have a ranking in order of probability.

The most likely parse tree for a sentence $s$ is
$$
\arg \max_{t \in T(s)}p(t)
$$
how do we find it?

Solutions:

1. Probability methods - directly calculate the probability, but will encounter the data sparsity problem.
2. Search methods - The CKY algorithm

#### paramters estimation

$$
q_{ML}(\alpha \rightarrow \beta) = \frac{Count(\alpha \rightarrow \beta)}{Count(\alpha)}
$$

where the counts are taken from a training set of example trees.

An example parameter in a PCFGs:
$$
q(S \to NP \ VP)
$$


### The CKY algorithm

The CKY (Cocke-Kasami (1965)-Younger (1967)) algorithm is a dynamic-programming algorithm.

Define:

​	$n$ is the number of words in the sentence

​	$w_i$ is the $i'$th word in the sentence

​	$N$ is the set of non-terminals in the grammar

​	$S$ is the start symbol in the grammar

Define a dynamic programming table: maximum probability of a constituent with non-terminal $X$ spanning words $i \dots j$ inclusive. for all $i=1 \dots (n-1)$, $j=(i+1) \dots n$, $X \in N$,

$\pi[i,j,X] = max_{X \rightarrow Y Z \in R, s \in \{i \dots (j-1)\}} (q(X \rightarrow Y Z) \times \pi(i,s,Y) \times \pi(s+1,j,Z)) \tag{1}$

Our goal is to calculate $\pi[1,n,S] = \arg max_{t \in T(s)}p(t)$.

The formula (1) is recursive. How to justify it? If the highest scoring tree rooted in non-terminal $X$, and spanning words $x_i \dots x_j$, uses rule $X \rightarrow Y Z$ and split point $s$, then its two subtrees must be: 1) the highest scoring tree rooted in $Y$ that spans words $x_i \dots x_s$; 2) the highest scoring tree rooted in $Z$ that spans words $x_{s+1} \dots x_j$.

![CKY](https://github.com/bifeng/daily_book_notes/raw/master/resource/cky_algorithm.png)

the complexity/running time of the CKY algorithm is $O(n^3 \times |N|^3)​$ .

#### The probabilistic CKY algorithm

The probabilistic CKY algorithm first described by Ney (1991).

Where do PCFG rule probabilities come from? <br>There are two ways to learn probabilities for the rules of a grammar. <br>The simplest way is to use a treebank, a corpus of already parsed sentences.<br>The second way is to parsing a corpus of sentences with a (non-probabilities) parser, if sentences were unambiguous...but....The intuition for solving this  chicken-and-egg problem is to incrementally improve our estimates by beginning with a parser with equal rule probabilities, then parser the sentence...re-estimate the rule probabilities, and so on, until our probabilities converge. This solution is called the inside-outside algorithm, it was proposed by Baker (1979) as a generalization of **the forward-backward algorithm for HMMs**. It is **a special case of the Expectation Maximization (EM) algorithm**.

### Structure Ambiguity (Lexical)

It is not uncommon for a moderate-length sentence (say 20 or 30 words in length) to have hundreds, thousands, or even tens of thousands of possible parses. <br>**Structural ambiguity**, which arises from many commonly used rules in phrase-structure grammars. Structural ambiguity comes in many forms.Two common kinds of ambiguity are **attachment ambiguity** (such as, PP-attachment), **coordination ambiguity** (besides, noun-phrase bracketing ambiguity), **sub-categorization ambiguity**.<br>But CFGs don't model syntactic facts about specific words.

### Structure Dependencies

PCFGs can be applied both to disambiguation in syntactic parsing and to word prediction in language modeling (Special useful in long distance dependencies).<br>But CFGs impose an independence assumption on probabilities, resulting in poor modeling of structural dependencies across the parser tree.

### Summary

+ PCFGs augments CFGs by including a probability for each rule in the grammar.
+ The probability for a parse tree is the product of probabilities for the rules in the tree
+ To build a PCFG-parsed parser:
  1. Learn a PCFG from a treebank
  2. Given a test data sentence, use the CKY algorithm to compute the highest probability tree for the sentence under the PCFG











