### head rule

#### Simplistic head-finding rule 

Used in Collins (1999)[[1]](Michael John Collins. 1999. Head-Driven Statistical Models for Natural Language Parsing. Ph.D. thesis, University of Pennsylvania.), Yamada & Matsumoto (2003)[[2]]( Yamada, Hiroyasu, and Yuji Matsumoto. "Statistical dependency analysis with support vector machines." In Proceedings of IWPT, vol. 3, pp. 195-206. 2003.), Zhang & Clark (2008)[[3]](Zhang, Y., & Clark, S. (2008). A Tale of Two Parsers : investigating and combining graph-based and transition-based dependency parsing using beam-search, (October), 562–571.), etc. This procedure is summarized in Johansson & Nugues (2007)[[4]](Johansson, R., & Nugues, P. (2007). Extended Constituent-to-dependency Conversion for English. In Proceedings of NODALIDA 2007 (pp. 105–112). Tartu, Estonia.):

> ... based on the idea of assigning each constituent in the parse tree a unique head selected amongst the constituent’s children (Magerman, 1994). For example, the toy grammar below would select the noun as the head of an NP, the verb as the head of a VP, and VP as the head of an S consisting of a noun phrase and a verb phrase:
>
> NP --> DT NN* 
> VP --> VBD* NP 
> S --> NP VP*
>
> By following the child-parent links from the token level up to the root of the tree, we can label every constituent with a head token. The heads can then be used to create dependency trees: to determine the parent of a token in the dependency tree, we locate the highest constituent that it is the head of and select the head of its parent constituent.

#### Extended head-finding rule

Proposed in Johansson & Nugues (2007)[[4]](Johansson, R., & Nugues, P. (2007). Extended Constituent-to-dependency Conversion for English. In Proceedings of NODALIDA 2007 (pp. 105–112). Tartu, Estonia.), the procedure "makes better use of the existing information in the Treebank". It introduces more labels, denotes more linguistic phenomenon, among other things. The authors reported a drop in dependency parsing accuracy but improvement in semantic role labeling with dependency as input.

#### English head rules



#### Chinese head rules

https://nlp.stanford.edu/nlp/javadoc/javanlp/edu/stanford/nlp/trees/international/pennchinese/package-summary.html

https://mailman.stanford.edu/pipermail/parser-user/2013-December/002701.html

https://github.com/AlexPoint/OpenNlp/blob/master/Resources/Models/Parser/head_rules

https://stackoverflow.com/questions/10297345/head-finding-rules-for-noun-phrases



