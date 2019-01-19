天气：晴  
阅读时间：早班车<br>记录时间：2018-11-08\2019-01-19

# chapter 4

## Lexicalized Probabilistic Context-Free Grammars

### Weaknesses of PCFGs

#### lack of sensitivity to lexical information

the independence assumption of each lexical item in the rule $\alpha \to \beta $ where $\beta \in \Sigma$ (only depends on the POS)

the independence assumption of any lexical information in the rule $\alpha \to \beta $ where $\beta \in N $



Prepositional phrase attachment  ambiguity, attachment decision is completely independent of the words, such as If q(NP $\rightarrow$ NP PP) > q(VP $\rightarrow$ VP PP) then the NP is more probable, else VP is more probable.

Example: workers dumped sacks <u>into a bin</u>

Coordination ambiguity, the parses have identical rules, and therefore have identical probability under any assignment of PCFG rule probabilities.

Example: dogs in houses and cats

#### lack of sensitivity to structural preferences

lexical information may of course help again, in this case. Another useful source of information may be basic statistic about structural preferences (preferences that ignore lexical items).



Close Attachment, the parses have the same rules, therefore receive same probability under a PCFG.

Example: 

president of a company <u>in Africa</u>

John was believed to have been shot <u>by Bill</u>



### Features of LPCFGs

1. More accurate, but with more parameter, it mean need more data to estimate! It will face with data sparsity problem (how handle it :question:)


### How to identify heads?

Researchers have generally used a simple set of rules to automatically identify the head of each context-free rule. This rules are fairly heuristic, but rely on some linguistic guidance on what the head of a rule should be: in spite of their simplicity they work quite well in practice!





### QA

+ The lexicalized PCFGs how to consider​ the​ structural​ preferences:question:
+ 























